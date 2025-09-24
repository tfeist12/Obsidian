**Week of 9/24/25**

Yesterday:
- DSP Refactor walkthrough
- v3.6.7 switchd added to base containers so I posted a review to use the new port name
	- SOu

To Do:
- Make story for updating the kubectl dsp plugin.
- Clean up Raj's checkin:
	- Naming - clienthfTLSConfig -> clientHfTLSConfig
	- Formatting - `go fmt`
		- hfcluster/src/ippodd/client/grpc_client.go
		- hfcluster/src/ippodd/ippodd/internal/rpc/server_test.go
- Randomize number in range for each sleep in fake firmware update