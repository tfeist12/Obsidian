I spent some more time digging into  this bug and have a working theory about what's going on and how to fix it.

For the 2/06 instance, the event logs show that at 21:25:53 lir-svc is assigned to cxo-array122-c2 then at 21:33:20 lir-svc is assigned to cxo-array107-c2. Unfortunately the common operator logs begin at 21:34:08. They state "Notifying clients that resource cxo-array122-c2's state is now MAINTENANCE_FLOATING_PODS_DRAIN_ENTERING...". I would wager that we enter maintenance mode sometime before 21:33:20 as that is when lir-svc is reassigned. In his testing for [AS-176729](https://nimblejira.nimblestorage.com/browse/AS-176729), Mattd found that when a node is put into maintenance mode and pod eviction happens, lir-svc successfully respawns on a new node as expected but the client's connection stopped working and started giving "context deadline exceeded" errors, which last a long time. Since this bug follows that exact same sequence of events, I'm led to believe these two bugs have a similar root cause.

Matt also created a gRPC client for lir-svc which would regularly perform getStatus requests. He then triggered maintenance mode on the node which lir-svc is running on. This causes lir-svc to be a evicted as well as a context deadline exceeded error on the requests. The interesting thing to note here is that after  about 15 min of context deadline exceeded errors (far more than it takes to error out on cluster creation) the connection seems to recover automatically.

After Matt reached out to Team Ironfist and Muthu, we learned that this could be because of the way TCP is handling recovery if the connection is still alive but RTO retransmissions remain unacknowledged. When sending using an established connection, the default is to retransmit with exponential increase. The number of times is set by net.ipv4.[tcp_retries2](https://man7.org/linux/man-pages/man7/tcp.7.html) (linux default of 15 used in swus). This translates to a duration of approximately between 13 to 30 minutes, depending on the retransmission timeout, before a new connection is established. This lines up pretty well with what Matt experienced.

As far as fixes go we have a few options here:
- Perform a redial within swus to manually recover the connection.
- Reduce swus net.ipv4.tcp_retries2 to reduce the number of retries before error (probably not the best idea as not entirely sure how this will impact other connections)
- Set the TCP_USER_TIMEOUT socket option. This will cause writes to fail if data remains unacknowledged for longer than the specified time. This setting overrides tcp keepalives (enabled by default in go) to determine when the connection should be closed. This can be done when creating a grpc client in golang by doing the following:  

```
var kacp = keepalive.ClientParameters{
	// send pings every 10 seconds if there is no activity 
	Time:                10 * time.Second,
	// wait 1 second for ping ack before considering the connection dead
	Timeout:             time.Second,
	// send pings even without active streams 
	PermitWithoutStream: true,             
}

conn, err := grpc.Dial(addr, grpc.WithTransportCredentials(insecure.NewCredentials()), grpc.WithKeepaliveParams(kacp))
if err != nil {
	log.Fatalf("did not connect: %v", err)
}
defer conn.Close()
```

I tested the last option out with Mattd using his grpc test client/reproduction method and the connection can back up very quickly.

**Some useful resources I found while researching today:**
Great article on this subject: [https://www.evanjones.ca/tcp-connection-timeouts.html](https://www.evanjones.ca/tcp-connection-timeouts.html)
GRPC tpc_user_timeout proposal: [https://github.com/grpc/proposal/blob/master/A18-tcp-user-timeout.md](https://github.com/grpc/proposal/blob/master/A18-tcp-user-timeout.md)
GRPC keepalive client example: [https://github.com/grpc/grpc-go/blob/5ccf176a08ab/examples/features/keepalive/client/main.go](https://github.com/grpc/grpc-go/blob/5ccf176a08ab/examples/features/keepalive/client/main.go)