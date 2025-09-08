**Week of 8/22/25**

To Do:
- Update nvim config and push to repo
- Make story for updating the kubectl dsp plugin.


ActPodRefactor: Probably need a story for this work soon
- DSP name is the name of the deployment
- Pod name is the per instance name of the pod 

perhaps pod type is part of config
when you create a config at the highest level you provide the type
We can actually use the existing act pod type for identification i believe

Need to update comments that mention dsp and osd
consts within the k8s client become part of config

Env var differences
```
DSP_NAME -> ACT_NAME
DSP_ID -> ACT_ID
DSP_TYPE -> ACT_TYPE
OSD_GRPC_HOST -> ACTIVATOR_HOST
OSD_GRPC_PORT -> ACTIVATOR_PORT
OSD_NAMESPACE -> ACTIVATOR_NAMESPACE
OSD_APP_NAME -> ACTIVATOR_APP_NAME
DSP_NAME_SPACE -> ACT_NAME_SPACE
```

```
root@c0n2:~# kubectl logs -n ds-dsp dsp-14962-7d5ccd4698-5xmjs -f
[INFO] 2025-08-27,19:51:25.767034Z dsp.go:156] ===================================
[INFO] 2025-08-27,19:51:25.769098Z dsp.go:40] dsp-14962 Starting ...
[INFO] 2025-08-27,19:51:25.76914Z dsp.go:41]     With ID: 1f0ded75-8b7f-40f2-92f1-bc2215b3ab71:14962
[INFO] 2025-08-27,19:51:25.769179Z dsp.go:42] Using configuration: env={ActName:dsp-14962 ActType:data LongId:1f0ded75-8b7f-40f2-92f1-bc2215b3ab71 ShortId:14962 PodName:dsp-14962-7d5ccd4698-5xmjs EtcdServiceName:etcd-cluster-client EtcdNamespace:cm EtcdComponentName:dsp.hfetcdconnectivity EtcdActToNodePath:/dsp-mgmt/ EtcdNodeToActPath:/dsp-node-mgmt/ EtcdActivatorHealthCheckPrefix:/dsp-mgmt/health-check/ EtcdWatchdogDisabledKey:/dsp-mgmt/watchdog/disabled ActivatorHost:172.19.12.22 ActivatorPort:32801 ActivatorNameSpace:ds ActivatorAppName:osd ActNameSpace:ds-dsp NodeName:c0n1 PodIP:172.26.122.37 PodUUID:71105fc3-0422-4257-8da9-ec2593161380 LivenessPort:50051 PlatformType:hfsim ConfigFile:/hf/data/config/config.yaml} file={HealthPollingInterval:10s MaxStateTransitionDuration:1m30s GrpcTimeout:40s GrpcShortwaitDuration:2s GrpcLongwaitDuration:5s GrpcConnCheckInterval:1s ActivatorHealthcheckFailThreshold:45 MaxNodeLeaseWaitTime:30s NodeLeaseRetryInterval:2s DisableActMetrics:false ActMetricsScrapeIntervalInSec:15 GrpcMaxStateChangeWaitDuration:1m40s} nodeUUID=1e2a33e9a1a44533a18c7d0a50a0dd30
[INFO] 2025-08-27,19:51:25.76921Z etcdclient.go:162] Connecting to etcd, using configuration {Endpoints:[etcd-cluster-client.cm.svc.cluster.local.:2379] AutoSyncInterval:0s DialTimeout:100ms DialKeepAliveTime:10s DialKeepAliveTimeout:100ms MaxCallSendMsgSize:0 MaxCallRecvMsgSize:0 TLS:<nil> Username: Password: RejectOldCluster:false DialOptions:[0xc000324010 0xc000324018] Context:<nil> Logger:<nil> LogConfig:<nil> PermitWithoutStream:false MaxUnaryRetries:0 BackoffWaitBetween:0s BackoffJitterFraction:0}
[INFO] 2025-08-27,19:51:25.805944Z etcdclient.go:176] etcd client created successfully
[DEBUG] 2025-08-27,19:51:25.805994Z etcdclient.go:186] clientv3.New() took 36.77098ms
[INFO] 2025-08-27,19:51:25.806652Z health.go:88] Register component dsp.hfetcdconnectivity with health module
[INFO] 2025-08-27,19:51:25.80728Z healthservice.go:76] Adding service dsp.hfetcdconnectivity with status SERVING
[INFO] 2025-08-27,19:51:25.807309Z health.go:88] Register component dsp.k8sconnectivity with health module
[INFO] 2025-08-27,19:51:25.817433Z healthservice.go:76] Adding service dsp.k8sconnectivity with status SERVING
[INFO] 2025-08-27,19:51:25.817469Z health.go:88] Register component dsp.statemachine with health module
[INFO] 2025-08-27,19:51:25.817481Z healthservice.go:76] Adding service dsp.statemachine with status SERVING
[INFO] 2025-08-27,19:51:25.817684Z health.go:129] Starting gRPC health service probe at 172.26.122.37:50051....
[INFO] 2025-08-27,19:51:25.817914Z nvgrid.go:66] Initiating connection to the Metrics server using config {172.26.122.37 15 etcd-cluster-client.cm.svc.cluster.local.:2379 c0n1 71105fc3-0422-4257-8da9-ec2593161380}
2025-08-27,19:51:25.818013Z [INFO] retryOp:metrics.go:302 Executing operation: Create etcd client. Address: etcd-cluster-client.cm.svc.cluster.local.:2379, dial timeout: 5s
[INFO] 2025-08-27,19:51:25.820216Z dsp.go:142] Started the DSP Pod state machine
[INFO] 2025-08-27,19:51:25.820268Z dsp.go:145] Current state: ClaimingOwnership
[DEBUG] 2025-08-27,19:51:25.820283Z statemachine.go:202] Calling onStep() of state ClaimingOwnership
[INFO] 2025-08-27,19:51:25.820295Z leader.go:39] Claiming ownership over pod
2025-08-27T19:51:25Z    INFO    leader  Trying to become the leader.
2025-08-27T19:51:25Z    DEBUG   leader  Found podname   {"Pod.Name": "dsp-14962-7d5ccd4698-5xmjs"}
2025-08-27,19:51:25.835031Z [INFO] connectToEtcd:metrics.go:336 Successfully created client for etcd server running at: etcd-cluster-client.cm.svc.cluster.local.:2379
2025-08-27,19:51:25.835074Z [INFO] getEnv:metrics.go:160 For environment variable with key: NVG_METRICS_GO_PORT, could not find a value, returning default: 47007
2025-08-27,19:51:25.835087Z [INFO] getPortFromEnv:metrics.go:183 Got port from ENV variable [ NVG_METRICS_GO_PORT ]: 47007
2025-08-27,19:51:25.835143Z [INFO] startHttpServer:metrics.go:262 Adding metrics handler for the path: /metrics
2025-08-27,19:51:25.835205Z [INFO] startHttpServer:metrics.go:265 Adding health check handler for the path: /nvg-health
2025-08-27,19:51:25.83522Z [INFO] NvgMetricsInit:metrics.go:867 The metrics exporter is running at: 172.26.122.37:47007, scrape interval: 15
2025-08-27,19:51:25.835233Z [INFO] addBucketRegistry:metrics.go:971 Added new bucket registry for scrape interval: 15
2025-08-27,19:51:25.835244Z [INFO] updateMetricsTargetInEtcd:metrics.go:474 Assigned target id: [2000] to key: 172.26.122.37:47007:/metrics
2025-08-27,19:51:25.835342Z [INFO] retryOp:metrics.go:302 Executing operation: Insert key nvgrid::metrics::c0n1:71105fc3-0422-4257-8da9-ec2593161380:dsp:2000 into etcd server running at: etcd-cluster-client.cm.svc.cluster.local.:2379
2025-08-27T19:51:25Z    DEBUG   leader  Found Pod       {"Pod.Namespace": "ds-dsp", "Pod.Name": "dsp-14962-7d5ccd4698-5xmjs"}
2025-08-27T19:51:25Z    INFO    leader  Found existing lock     {"LockOwner": "dsp-14962-56f6c5c4f8-gxk47"}
2025-08-27,19:51:25.863477Z [INFO] insertMetricsTargetIntoEtcd:metrics.go:427 Successfully inserted key: nvgrid::metrics::c0n1:71105fc3-0422-4257-8da9-ec2593161380:dsp:2000 into etcd server running at: etcd-cluster-client.cm.svc.cluster.local.:2379
2025-08-27,19:51:25.863521Z [INFO] updateMetricsTargetInEtcd:metrics.go:492 Insert/update metrics target with key nvgrid::metrics::c0n1:71105fc3-0422-4257-8da9-ec2593161380:dsp:2000 and interval(s) [15] into etcd server running at: etcd-cluster-client.cm.svc.cluster.local.:2379 succeeded
2025-08-27,19:51:25.86354Z [INFO] NvgMetricsInit:metrics.go:892 NVGMetrics intitialized successfully with config: Hostname: 172.26.122.37, scrape interval: 15, ETCD address: etcd-cluster-client.cm.svc.cluster.local.:2379, node name: c0n1, pod UUID: 71105fc3-0422-4257-8da9-ec2593161380 selectedPort: 47007
[INFO] 2025-08-27,19:51:25.863553Z nvgrid.go:97] Metrics server execution started...
2025-08-27,19:51:25.863579Z [INFO] getEnv:metrics.go:160 For environment variable with key: NVG_REREGISTER_FREQUENCY, could not find a value, returning default:
2025-08-27,19:51:25.86359Z [INFO] func1:metrics.go:793 Started thread to reregister dropped targets, frequency: 3m0s
2025-08-27T19:51:25Z    INFO    leader  Not the leader. Waiting.
2025-08-27T19:51:27Z    INFO    leader  Not the leader. Waiting.
2025-08-27T19:51:29Z    INFO    leader  Not the leader. Waiting.
2025-08-27T19:51:34Z    INFO    leader  Became the leader.
[INFO] 2025-08-27,19:51:34.176695Z leader.go:51] Pod dsp-14962 is leader for life
[INFO] 2025-08-27,19:51:34.176738Z statemachine.go:283] Setting state from ClaimingOwnership to CheckingCurrentNodeHealth
[DEBUG] 2025-08-27,19:51:34.176765Z statemachine.go:410] Time spent in previous state ClaimingOwnership, {Instance count: 1, Current elapsed: 8.356466292s, Average elapsed: 8.356466292s}
[INFO] 2025-08-27,19:51:34.176776Z dsp.go:145] Current state: CheckingCurrentNodeHealth
[DEBUG] 2025-08-27,19:51:34.176785Z statemachine.go:202] Calling onStep() of state CheckingCurrentNodeHealth
[INFO] 2025-08-27,19:51:34.185904Z statemachine.go:283] Setting state from CheckingCurrentNodeHealth to CheckingPreviousDspLocation
[DEBUG] 2025-08-27,19:51:34.185945Z statemachine.go:410] Time spent in previous state CheckingCurrentNodeHealth, {Instance count: 2, Current elapsed: 9.141362ms, Average elapsed: 4.182803827s}
[INFO] 2025-08-27,19:51:34.185957Z dsp.go:145] Current state: CheckingPreviousDspLocation
[DEBUG] 2025-08-27,19:51:34.185968Z statemachine.go:202] Calling onStep() of state CheckingPreviousDspLocation
[INFO] 2025-08-27,19:51:34.185985Z etcdclient.go:139] THF ActToNodeKey: /dsp-mgmt/1f0ded75-8b7f-40f2-92f1-bc2215b3ab71
[INFO] 2025-08-27,19:51:34.191326Z checkingpreviousdsplocationstate.go:47] DSP to node mapping key value 0ac485cc0f984961a28fcbd2be08d812 is not the current node 1e2a33e9a1a44533a18c7d0a50a0dd30
[INFO] 2025-08-27,19:51:34.191365Z statemachine.go:283] Setting state from CheckingPreviousDspLocation to CheckingPreviousNodeHealth
[DEBUG] 2025-08-27,19:51:34.19139Z statemachine.go:410] Time spent in previous state CheckingPreviousDspLocation, {Instance count: 3, Current elapsed: 5.401546ms, Average elapsed: 2.7903364s}
[INFO] 2025-08-27,19:51:34.191402Z dsp.go:145] Current state: CheckingPreviousNodeHealth
[DEBUG] 2025-08-27,19:51:34.191412Z statemachine.go:202] Calling onStep() of state CheckingPreviousNodeHealth
[INFO] 2025-08-27,19:51:34.191421Z checkingpreviousnodehealthstate.go:34] Watchdog is disabled by default on HFSim. Checking previous node's lease to avoid split-brain.
[INFO] 2025-08-27,19:51:34.193786Z checkingpreviousnodehealthstate.go:58] Node Lease found, deactivating DSP on node: 0ac485cc0f984961a28fcbd2be08d812
[INFO] 2025-08-27,19:51:34.193833Z statemachine.go:283] Setting state from CheckingPreviousNodeHealth to DeactivatingDspOnPreviousNode
[DEBUG] 2025-08-27,19:51:34.193851Z statemachine.go:410] Time spent in previous state CheckingPreviousNodeHealth, {Instance count: 4, Current elapsed: 2.425246ms, Average elapsed: 2.093358611s}
[INFO] 2025-08-27,19:51:34.193861Z dsp.go:145] Current state: DeactivatingDspOnPreviousNode
[DEBUG] 2025-08-27,19:51:34.19387Z statemachine.go:202] Calling onStep() of state DeactivatingDspOnPreviousNode
[INFO] 2025-08-27,19:51:34.2206Z deactivatingdsponpreviousnodestate.go:36] Found IP address of previous node: 172.19.12.21
[INFO] 2025-08-27,19:51:34.221327Z common.go:56] Successfully dialed gRPC server 172.19.12.21:32801
[DEBUG] 2025-08-27,19:51:34.221368Z remoteosdclient.go:44] Dialing remote OSD on 172.19.12.21 took 715.052µs
[DEBUG] 2025-08-27,19:51:34.221384Z remoteosdclient.go:63] Going to deactivate.
[INFO] 2025-08-27,19:51:34.228504Z error.go:85] Successfully made StopDSP request for long ID 1f0ded75-8b7f-40f2-92f1-bc2215b3ab71, short ID 14962
[INFO] 2025-08-27,19:51:34.228546Z statemachine.go:283] Setting state from DeactivatingDspOnPreviousNode to NotifyingDspDeactivation
[DEBUG] 2025-08-27,19:51:34.228564Z statemachine.go:410] Time spent in previous state DeactivatingDspOnPreviousNode, {Instance count: 5, Current elapsed: 34.67846ms, Average elapsed: 1.681622581s}
[INFO] 2025-08-27,19:51:34.228575Z dsp.go:145] Current state: NotifyingDspDeactivation
[DEBUG] 2025-08-27,19:51:34.228589Z statemachine.go:202] Calling onStep() of state NotifyingDspDeactivation
[INFO] 2025-08-27,19:51:34.228766Z etcdclient.go:146] THF NodeToActKey: /dsp-node-mgmt/0ac485cc0f984961a28fcbd2be08d812/1f0ded75-8b7f-40f2-92f1-bc2215b3ab71
[INFO] 2025-08-27,19:51:34.228783Z etcdclient.go:139] THF ActToNodeKey: /dsp-mgmt/1f0ded75-8b7f-40f2-92f1-bc2215b3ab71
[DEBUG] 2025-08-27,19:51:34.236209Z metrics.go:243] Updating metric dsp_metrics_service_state with label values [0ac485cc0f984961a28fcbd2be08d812, dsp-14962, GRPC] to 0
[INFO] 2025-08-27,19:51:34.236267Z statemachine.go:283] Setting state from NotifyingDspDeactivation to RegisteringCurrentNode
[DEBUG] 2025-08-27,19:51:34.236283Z statemachine.go:410] Time spent in previous state NotifyingDspDeactivation, {Instance count: 6, Current elapsed: 7.681737ms, Average elapsed: 1.40263244s}
[INFO] 2025-08-27,19:51:34.236306Z dsp.go:145] Current state: RegisteringCurrentNode
[DEBUG] 2025-08-27,19:51:34.236315Z statemachine.go:202] Calling onStep() of state RegisteringCurrentNode
[INFO] 2025-08-27,19:51:34.236326Z etcdclient.go:139] THF ActToNodeKey: /dsp-mgmt/1f0ded75-8b7f-40f2-92f1-bc2215b3ab71
[INFO] 2025-08-27,19:51:34.240476Z statemachine.go:283] Setting state from RegisteringCurrentNode to CheckingDspVersion
[DEBUG] 2025-08-27,19:51:34.240523Z statemachine.go:410] Time spent in previous state RegisteringCurrentNode, {Instance count: 7, Current elapsed: 4.194128ms, Average elapsed: 1.202855538s}
[INFO] 2025-08-27,19:51:34.24054Z dsp.go:145] Current state: CheckingDspVersion
[DEBUG] 2025-08-27,19:51:34.240549Z statemachine.go:202] Calling onStep() of state CheckingDspVersion
[INFO] 2025-08-27,19:51:34.254008Z k8sclient.go:251] Activator Pod is running: osd-359aab3a-grh8s
[INFO] 2025-08-27,19:51:34.254053Z checkingdspversionstate.go:25] DSP version: 359aab3a matches latest version in OSD Pod: 359aab3a
[INFO] 2025-08-27,19:51:34.254081Z statemachine.go:283] Setting state from CheckingDspVersion to ActivatingDspOnCurrentNode
[DEBUG] 2025-08-27,19:51:34.254096Z statemachine.go:410] Time spent in previous state CheckingDspVersion, {Instance count: 8, Current elapsed: 13.527671ms, Average elapsed: 1.054189555s}
[INFO] 2025-08-27,19:51:34.254106Z dsp.go:145] Current state: ActivatingDspOnCurrentNode
[DEBUG] 2025-08-27,19:51:34.25412Z statemachine.go:202] Calling onStep() of state ActivatingDspOnCurrentNode
[INFO] 2025-08-27,19:51:34.254271Z common.go:56] Successfully dialed gRPC server 172.19.12.22:32801
[DEBUG] 2025-08-27,19:51:34.254287Z localosdclient.go:70] Dialing local OSD took 156.13µs
[DEBUG] 2025-08-27,19:51:34.254299Z localosdclient.go:212] Going to activate. Type=false
[DEBUG] 2025-08-27,19:51:34.254327Z localosdclient.go:166] Going to wait for connection state CONNECTING to change (timeout 1m40s)
[DEBUG] 2025-08-27,19:51:34.256047Z localosdclient.go:181] Connection state changed to READY
[INFO] 2025-08-27,19:51:55.349603Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = keepalive ping failed to receive ACK within timeout
[INFO] 2025-08-27,19:51:55.349656Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:51:55.97272Z localosdclient.go:129] detected disconnection from OSD gRPC endpoint, connection state IDLE
[DEBUG] 2025-08-27,19:51:57.353408Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:06.734141Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "error reading server preface: read tcp 172.26.122.37:39774->172.19.12.22:32801: read: connection reset by peer"
[INFO] 2025-08-27,19:52:06.734198Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:08.734409Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:08.734536Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:52:08.734555Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:10.735416Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:10.73554Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:52:10.735558Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:12.749274Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:12.749378Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:52:12.749396Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:14.750017Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:14.750097Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:52:14.750113Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:16.758701Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:27.771951Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = keepalive ping failed to receive ACK within timeout
[INFO] 2025-08-27,19:52:27.771995Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:29.953176Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:32.159429Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "error reading server preface: read tcp 172.26.122.37:58726->172.19.12.22:32801: read: connection reset by peer"
[INFO] 2025-08-27,19:52:32.159465Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:34.160031Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:34.160134Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:52:34.160153Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:36.194061Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:36.267869Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:52:36.267907Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:38.365601Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:38.36569Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:52:38.365712Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:40.366298Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:40.366384Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:52:40.366398Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:42.48868Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:42.488815Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:52:42.48885Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:44.48949Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:44.489575Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:52:44.489593Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:46.490498Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:46.490589Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:52:46.490606Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:48.491441Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:48.491524Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:52:48.491539Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:50.492291Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:50.492382Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:52:50.492397Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:52.492997Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:52.493071Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:52:52.493099Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:54.493502Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:54.493584Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "error reading server preface: read tcp 172.26.122.37:39834->172.19.12.22:32801: use of closed network connection"
[INFO] 2025-08-27,19:52:54.4936Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:56.494374Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:52:56.494477Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "error reading server preface: read tcp 172.26.122.37:39834->172.19.12.22:32801: use of closed network connection"
[INFO] 2025-08-27,19:52:56.494497Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:52:58.556475Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:53:09.590521Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = keepalive ping failed to receive ACK within timeout
[INFO] 2025-08-27,19:53:09.590561Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:53:11.602668Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:53:11.603015Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:53:11.603048Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:53:13.603357Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:53:13.603464Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:53:13.60348Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:53:15.604418Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:53:26.609597Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = keepalive ping failed to receive ACK within timeout
[INFO] 2025-08-27,19:53:26.609635Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:53:28.756087Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:53:28.756997Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:53:28.757022Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:53:30.951505Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:53:30.951611Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:53:30.951627Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:53:32.951846Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:53:43.955313Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = keepalive ping failed to receive ACK within timeout
[INFO] 2025-08-27,19:53:43.955361Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:53:45.957656Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:53:45.957947Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:53:45.957968Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:53:47.9595Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:53:47.959575Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:53:47.959589Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:53:49.960432Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:53:58.981937Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = error reading from server: EOF
[INFO] 2025-08-27,19:53:58.981988Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:54:00.985364Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:54:00.985659Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:54:00.985685Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:54:02.988575Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:54:14.159273Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = keepalive ping failed to receive ACK within timeout
[INFO] 2025-08-27,19:54:14.159315Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:54:16.164656Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:54:16.165025Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:54:16.16505Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:54:18.166757Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:54:29.361221Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = keepalive ping failed to receive ACK within timeout
[INFO] 2025-08-27,19:54:29.361266Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:54:31.561448Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:54:31.789708Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "error reading server preface: read tcp 172.26.122.37:52726->172.19.12.22:32801: read: connection reset by peer"
[INFO] 2025-08-27,19:54:31.789746Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:54:33.790442Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:54:33.790528Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:54:33.790546Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:54:35.964555Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:54:47.371355Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = keepalive ping failed to receive ACK within timeout
[INFO] 2025-08-27,19:54:47.3714Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:54:49.567817Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:54:49.585302Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "error reading server preface: read tcp 172.26.122.37:51996->172.19.12.22:32801: read: connection reset by peer"
[INFO] 2025-08-27,19:54:49.585335Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:54:51.586498Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:54:51.586569Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:54:51.586583Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:54:53.772592Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:55:01.998645Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = error reading from server: EOF
[INFO] 2025-08-27,19:55:01.99868Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:55:03.999434Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:55:03.999747Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp 172.19.12.22:32801: connect: connection refused"
[INFO] 2025-08-27,19:55:03.999773Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:55:06.000338Z localosdclient.go:212] Going to activate. Type=false
[INFO] 2025-08-27,19:55:17.003664Z error.go:45] Encountered OSD unreachable error while making StartDSP gRPC request: rpc error: code = Unavailable desc = keepalive ping failed to receive ACK within timeout
[INFO] 2025-08-27,19:55:17.003701Z localosdclient.go:221] Retrying activate DSP request after 2s
[DEBUG] 2025-08-27,19:55:19.579431Z localosdclient.go:212] Going to activate. Type=false
{"level":"warn","ts":"2025-08-27T19:55:27.581028Z","logger":"etcd-client","caller":"v3@v3.6.4/retry_interceptor.go:65","msg":"retrying of unary invoker failed","target":"etcd-endpoints://0xc0005530e0/etcd-cluster-client.cm.svc.cluster.local.:2379","method":"/grpc.health.v1.Health/Check","attempt":0,"error":"rpc error: code = Unavailable desc = keepalive ping failed to receive ACK within timeout"}
[DEBUG] 2025-08-27,19:55:27.581122Z etcdclient.go:370] failed to probe etcd server endpoint, rpc error: code = Unavailable desc = keepalive ping failed to receive ACK within timeout
[ERROR] 2025-08-27,19:55:27.581155Z health.go:177] health check failed for component dsp.hfetcdconnectivity, {HealthStatus:1 Reason:failed to probe etcd server endpoint, rpc error: code = Unavailable desc = keepalive ping failed to receive ACK within timeout}
[INFO] 2025-08-27,19:55:27.581176Z healthservice.go:74] Updating service dsp.hfetcdconnectivity status from SERVING to NOT_SERVING
```