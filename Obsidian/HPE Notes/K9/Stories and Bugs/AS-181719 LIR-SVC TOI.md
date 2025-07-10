**Acceptance Criteria**
1. TOI content is created for how to report the current status of LIR-SVC and determine whether it is healthy or unhealthy.
2. TOI content describing LIR-SVC's purpose, role, and common workflows is created.
3. TOI content describing troubleshooting problems with LIR-SVC is created.
4. TOI content for interpreting LIR-SVC log files is created.
5. TOI content is presented to the support team.
6. Updates are made to the TOI collateral following feedback from the support team.

Local Image Repository Service (lir-svc) Transfer of Information

**Intro**
Value proposition
- The local image repository is the Kubernetes service inside the on-prem HF cluster which is responsible for storing and serving all required software images used by the cluster
	- Container images
	- OS images
	- Drive firmware
	- Raider service packs
- The local image repository is a vital component to installing, updating or removing cluster software. It is made up of two central pieces, lir-svc, and lir-data.
- lir-data is made up of five separate containers. These are the docker registry and the nginx file for data service, a docker registry authenication container for security, an rsync daemon for data replication, and an rsync grpc server to service requests for replication.
- lir-svc can either add a new release using a squashfs url or remove a previously added release using it's version. These are the most common workflows. There is also an additional API provided to get information about stored releases and their progress. The three API names are AddRelease, RemoveRelease, and GetStatus.
- lir-svc only has a single replica across the cluster which starts on the first control plane node.

Theory of operation
- lir-svc is the client of software update service and all operations are automatically triggered by the swus controller
- lir-svc uses a task runner to process task asynchronously. Multiple grpc requests can be made almost instantly however the lir-svc task runner only processes a single task at a time. After the task completes, then it consumes a new task off the queue. 
- Adding, Removing, or Getting info about a release can be manually triggered using these grpcurl command examples:
```
grpcurl -d '{"release_id":"<url>", "release_version":"<version>"}' -plaintext `kubectl -n cm get svc/lir-svc -o=jsonpath='{.spec.clusterIP}':80` lir.Service/AddRelease

grpcurl -d '{"release_version":"<version>"}' -plaintext `kubectl -n cm get svc/lir-svc -o=jsonpath='{.spec.clusterIP}':80` lir.Service/RemoveRelease

grpcurl -plaintext `kubectl -n cm get svc/lir-svc -o=jsonpath='{.spec.clusterIP}':80` lir.Service/GetStatus

grpcurl -d '{"release_version":"<version>"}' -plaintext `kubectl -n cm get svc/lir-svc -o=jsonpath='{.spec.clusterIP}':80` lir.Service.GetStatus
```
- These commands use a nested kubectl command to extract the kubernetes service cluster IP. This IP should always be used to access lir-svc from the node.
- Use a GetStatus query with a specific release version to check it's current progress as well as to see it's error message should anything go wrong

- Add Release steps
	- Initiate scaling
	- Download file
	- Verify code signing
	- Unsquashfs
	- Layout checking
	- Sync files to the lir-data file server
	- Push containers to the lir-data docker registry
	- Replicate data to all lir-data replicas across the nodes

- Remove Release steps:
	- Initiate scaling
	- Delete container images from the lir-data docker registry
	- Remove files from the lir-data file server
	- Garbage collection on docker registry
	- Replicate data to all lir-data replicas across the nodes

- Statuses:
	- 

**Known limitations or requirements**
**Expected behaviour**
- Perhaps show expected logs and highlight each step
**Troubleshooting**
Deciphering Add Release logs 
- lir-svc startup and receiving add release request
```
Beginning lir-svc startup script
Requesting systems info from NCS - Attempt 1
Proxy not found in systems info. Launching lir-svc without proxy
[INFO] lir-svc.go:55] ===================================
[INFO] cluster.go:358] Current lir-data replicas: 1, Expected lir-data replicas: 1
[INFO] lir-svc.go:62] Completed initial lir-data replica check
[INFO] lir-svc.go:69] Completed initial configmap setup
2024/05/01 22:43:20 Starting task runner
[INFO] lir-svc.go:47] Starting server...
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
[INFO] server.go:279] Release version not found: 9999.0.0.0-1052647
[INFO] server.go:96] Received AddRelease Request - ReleaseVersion: '9999.0.0.0-1052647'
[INFO] server.go:332] Successful save to lir-svc-releases configmap on attempt 1
2024/05/01 22:45:43 Starting Task 0.
```
- Initiate scaling
```
2024/05/01 22:45:43 Task 0 received status AddRelease: Initializing replica pods.
2024/05/01 22:45:43 Task 0 running for 0s.
[INFO] add_release.go:111] Waiting for 3 lir-data replicas to start...
[INFO] wait.go:91] waiting for Deployment "lir-data" to be ready
[INFO] wait.go:107] polling Deployment "lir-data" until condition is met
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
...
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
[INFO] add_release.go:118] Successfully scaled up to 3 lir-data replicas
2024/05/01 22:45:56 Task 0 received status AddRelease: Initialized.
2024/05/01 22:45:56 Task 0 running for 13s.
```
- Download File
```
[INFO] add_release.go:136] Created working directory /tmp/tmp.fos.1232999799 successfully
[INFO] add_release.go:151] Started downloading https://artifactory.eng.nimblestorage.com/artifactory/fleetos-local/prj-fleetos/release/1052647/fleetos-1052647~gite6f344f80917b8-opt.squashfs
2024/05/01 22:45:56 Task 0 received status AddRelease: Downloading.
2024/05/01 22:45:56 Task 0 running for 13s.
[INFO] add_release.go:318] Sending GET with bytes=0-
[INFO] server.go:332] Successful save to lir-svc-releases configmap on attempt 1
[INFO] add_release.go:367] release total size: 3959596032
2024/05/01 22:45:56 Task 0 received status AddRelease: Downloading (1%).
2024/05/01 22:45:56 Task 0 running for 13s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:45:57 Task 0 received status AddRelease: Downloading (2%).
2024/05/01 22:45:57 Task 0 running for 13s.
2024/05/01 22:45:57 Task 0 received status AddRelease: Downloading (3%).
2024/05/01 22:45:57 Task 0 running for 13s.
2024/05/01 22:45:57 Task 0 received status AddRelease: Downloading (4%).
2024/05/01 22:45:57 Task 0 running for 14s.
2024/05/01 22:45:57 Task 0 received status AddRelease: Downloading (5%).
2024/05/01 22:45:57 Task 0 running for 14s.
2024/05/01 22:45:57 Task 0 received status AddRelease: Downloading (6%).
2024/05/01 22:45:57 Task 0 running for 14s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:45:58 Task 0 received status AddRelease: Downloading (7%).
2024/05/01 22:45:58 Task 0 running for 14s.
2024/05/01 22:45:58 Task 0 received status AddRelease: Downloading (8%).
2024/05/01 22:45:58 Task 0 running for 14s.
2024/05/01 22:45:58 Task 0 received status AddRelease: Downloading (9%).
2024/05/01 22:45:58 Task 0 running for 15s.
2024/05/01 22:45:58 Task 0 received status AddRelease: Downloading (10%).
2024/05/01 22:45:58 Task 0 running for 15s.
2024/05/01 22:45:58 Task 0 received status AddRelease: Downloading (11%).
2024/05/01 22:45:58 Task 0 running for 15s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:45:59 Task 0 received status AddRelease: Downloading (12%).
2024/05/01 22:45:59 Task 0 running for 15s.
2024/05/01 22:45:59 Task 0 received status AddRelease: Downloading (13%).
2024/05/01 22:45:59 Task 0 running for 15s.
2024/05/01 22:45:59 Task 0 received status AddRelease: Downloading (14%).
2024/05/01 22:45:59 Task 0 running for 16s.
2024/05/01 22:45:59 Task 0 received status AddRelease: Downloading (15%).
2024/05/01 22:45:59 Task 0 running for 16s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:00 Task 0 received status AddRelease: Downloading (16%).
2024/05/01 22:46:00 Task 0 running for 16s.
2024/05/01 22:46:00 Task 0 received status AddRelease: Downloading (17%).
2024/05/01 22:46:00 Task 0 running for 16s.
2024/05/01 22:46:00 Task 0 received status AddRelease: Downloading (18%).
2024/05/01 22:46:00 Task 0 running for 17s.
2024/05/01 22:46:00 Task 0 received status AddRelease: Downloading (19%).
2024/05/01 22:46:00 Task 0 running for 17s.
2024/05/01 22:46:00 Task 0 received status AddRelease: Downloading (20%).
2024/05/01 22:46:00 Task 0 running for 17s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:01 Task 0 received status AddRelease: Downloading (21%).
2024/05/01 22:46:01 Task 0 running for 17s.
2024/05/01 22:46:01 Task 0 received status AddRelease: Downloading (22%).
2024/05/01 22:46:01 Task 0 running for 17s.
2024/05/01 22:46:01 Task 0 received status AddRelease: Downloading (23%).
2024/05/01 22:46:01 Task 0 running for 18s.
2024/05/01 22:46:01 Task 0 received status AddRelease: Downloading (24%).
2024/05/01 22:46:01 Task 0 running for 18s.
2024/05/01 22:46:01 Task 0 received status AddRelease: Downloading (25%).
2024/05/01 22:46:01 Task 0 running for 18s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:02 Task 0 received status AddRelease: Downloading (26%).
2024/05/01 22:46:02 Task 0 running for 18s.
2024/05/01 22:46:02 Task 0 received status AddRelease: Downloading (27%).
2024/05/01 22:46:02 Task 0 running for 18s.
2024/05/01 22:46:02 Task 0 received status AddRelease: Downloading (28%).
2024/05/01 22:46:02 Task 0 running for 19s.
2024/05/01 22:46:02 Task 0 received status AddRelease: Downloading (29%).
2024/05/01 22:46:02 Task 0 running for 19s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:02 Task 0 received status AddRelease: Downloading (30%).
2024/05/01 22:46:02 Task 0 running for 19s.
2024/05/01 22:46:03 Task 0 received status AddRelease: Downloading (31%).
2024/05/01 22:46:03 Task 0 running for 19s.
2024/05/01 22:46:03 Task 0 received status AddRelease: Downloading (32%).
2024/05/01 22:46:03 Task 0 running for 20s.
2024/05/01 22:46:03 Task 0 received status AddRelease: Downloading (33%).
2024/05/01 22:46:03 Task 0 running for 20s.
2024/05/01 22:46:03 Task 0 received status AddRelease: Downloading (34%).
2024/05/01 22:46:03 Task 0 running for 20s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:04 Task 0 received status AddRelease: Downloading (35%).
2024/05/01 22:46:04 Task 0 running for 20s.
2024/05/01 22:46:04 Task 0 received status AddRelease: Downloading (36%).
2024/05/01 22:46:04 Task 0 running for 20s.
2024/05/01 22:46:04 Task 0 received status AddRelease: Downloading (37%).
2024/05/01 22:46:04 Task 0 running for 21s.
2024/05/01 22:46:04 Task 0 received status AddRelease: Downloading (38%).
2024/05/01 22:46:04 Task 0 running for 21s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:05 Task 0 received status AddRelease: Downloading (39%).
2024/05/01 22:46:05 Task 0 running for 21s.
2024/05/01 22:46:05 Task 0 received status AddRelease: Downloading (40%).
2024/05/01 22:46:05 Task 0 running for 21s.
2024/05/01 22:46:05 Task 0 received status AddRelease: Downloading (41%).
2024/05/01 22:46:05 Task 0 running for 22s.
2024/05/01 22:46:05 Task 0 received status AddRelease: Downloading (42%).
2024/05/01 22:46:05 Task 0 running for 22s.
2024/05/01 22:46:05 Task 0 received status AddRelease: Downloading (43%).
2024/05/01 22:46:05 Task 0 running for 22s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:06 Task 0 received status AddRelease: Downloading (44%).
2024/05/01 22:46:06 Task 0 running for 22s.
2024/05/01 22:46:06 Task 0 received status AddRelease: Downloading (45%).
2024/05/01 22:46:06 Task 0 running for 22s.
2024/05/01 22:46:06 Task 0 received status AddRelease: Downloading (46%).
2024/05/01 22:46:06 Task 0 running for 23s.
2024/05/01 22:46:06 Task 0 received status AddRelease: Downloading (47%).
2024/05/01 22:46:06 Task 0 running for 23s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:07 Task 0 received status AddRelease: Downloading (48%).
2024/05/01 22:46:07 Task 0 running for 23s.
2024/05/01 22:46:07 Task 0 received status AddRelease: Downloading (49%).
2024/05/01 22:46:07 Task 0 running for 23s.
2024/05/01 22:46:07 Task 0 received status AddRelease: Downloading (50%).
2024/05/01 22:46:07 Task 0 running for 23s.
2024/05/01 22:46:07 Task 0 received status AddRelease: Downloading (51%).
2024/05/01 22:46:07 Task 0 running for 24s.
2024/05/01 22:46:07 Task 0 received status AddRelease: Downloading (52%).
2024/05/01 22:46:07 Task 0 running for 24s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:08 Task 0 received status AddRelease: Downloading (53%).
2024/05/01 22:46:08 Task 0 running for 24s.
2024/05/01 22:46:08 Task 0 received status AddRelease: Downloading (54%).
2024/05/01 22:46:08 Task 0 running for 24s.
2024/05/01 22:46:08 Task 0 received status AddRelease: Downloading (55%).
2024/05/01 22:46:08 Task 0 running for 25s.
2024/05/01 22:46:08 Task 0 received status AddRelease: Downloading (56%).
2024/05/01 22:46:08 Task 0 running for 25s.
2024/05/01 22:46:08 Task 0 received status AddRelease: Downloading (57%).
2024/05/01 22:46:08 Task 0 running for 25s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:09 Task 0 received status AddRelease: Downloading (58%).
2024/05/01 22:46:09 Task 0 running for 25s.
2024/05/01 22:46:09 Task 0 received status AddRelease: Downloading (59%).
2024/05/01 22:46:09 Task 0 running for 25s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:09 Task 0 received status AddRelease: Downloading (60%).
2024/05/01 22:46:09 Task 0 running for 26s.
2024/05/01 22:46:10 Task 0 received status AddRelease: Downloading (61%).
2024/05/01 22:46:10 Task 0 running for 26s.
2024/05/01 22:46:10 Task 0 received status AddRelease: Downloading (62%).
2024/05/01 22:46:10 Task 0 running for 26s.
2024/05/01 22:46:10 Task 0 received status AddRelease: Downloading (63%).
2024/05/01 22:46:10 Task 0 running for 27s.
2024/05/01 22:46:10 Task 0 received status AddRelease: Downloading (64%).
2024/05/01 22:46:10 Task 0 running for 27s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:11 Task 0 received status AddRelease: Downloading (65%).
2024/05/01 22:46:11 Task 0 running for 27s.
2024/05/01 22:46:11 Task 0 received status AddRelease: Downloading (66%).
2024/05/01 22:46:11 Task 0 running for 27s.
2024/05/01 22:46:11 Task 0 received status AddRelease: Downloading (67%).
2024/05/01 22:46:11 Task 0 running for 28s.
2024/05/01 22:46:11 Task 0 received status AddRelease: Downloading (68%).
2024/05/01 22:46:11 Task 0 running for 28s.
2024/05/01 22:46:11 Task 0 received status AddRelease: Downloading (69%).
2024/05/01 22:46:11 Task 0 running for 28s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:12 Task 0 received status AddRelease: Downloading (70%).
2024/05/01 22:46:12 Task 0 running for 28s.
2024/05/01 22:46:12 Task 0 received status AddRelease: Downloading (71%).
2024/05/01 22:46:12 Task 0 running for 28s.
2024/05/01 22:46:12 Task 0 received status AddRelease: Downloading (72%).
2024/05/01 22:46:12 Task 0 running for 29s.
2024/05/01 22:46:12 Task 0 received status AddRelease: Downloading (73%).
2024/05/01 22:46:12 Task 0 running for 29s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:12 Task 0 received status AddRelease: Downloading (74%).
2024/05/01 22:46:12 Task 0 running for 29s.
2024/05/01 22:46:13 Task 0 received status AddRelease: Downloading (75%).
2024/05/01 22:46:13 Task 0 running for 29s.
2024/05/01 22:46:13 Task 0 received status AddRelease: Downloading (76%).
2024/05/01 22:46:13 Task 0 running for 29s.
2024/05/01 22:46:13 Task 0 received status AddRelease: Downloading (77%).
2024/05/01 22:46:13 Task 0 running for 30s.
2024/05/01 22:46:13 Task 0 received status AddRelease: Downloading (78%).
2024/05/01 22:46:13 Task 0 running for 30s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:14 Task 0 received status AddRelease: Downloading (79%).
2024/05/01 22:46:14 Task 0 running for 30s.
2024/05/01 22:46:14 Task 0 received status AddRelease: Downloading (80%).
2024/05/01 22:46:14 Task 0 running for 30s.
2024/05/01 22:46:14 Task 0 received status AddRelease: Downloading (81%).
2024/05/01 22:46:14 Task 0 running for 30s.
2024/05/01 22:46:14 Task 0 received status AddRelease: Downloading (82%).
2024/05/01 22:46:14 Task 0 running for 31s.
2024/05/01 22:46:14 Task 0 received status AddRelease: Downloading (83%).
2024/05/01 22:46:14 Task 0 running for 31s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:15 Task 0 received status AddRelease: Downloading (84%).
2024/05/01 22:46:15 Task 0 running for 31s.
2024/05/01 22:46:15 Task 0 received status AddRelease: Downloading (85%).
2024/05/01 22:46:15 Task 0 running for 31s.
2024/05/01 22:46:15 Task 0 received status AddRelease: Downloading (86%).
2024/05/01 22:46:15 Task 0 running for 32s.
2024/05/01 22:46:15 Task 0 received status AddRelease: Downloading (87%).
2024/05/01 22:46:15 Task 0 running for 32s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:16 Task 0 received status AddRelease: Downloading (88%).
2024/05/01 22:46:16 Task 0 running for 32s.
2024/05/01 22:46:16 Task 0 received status AddRelease: Downloading (89%).
2024/05/01 22:46:16 Task 0 running for 32s.
2024/05/01 22:46:16 Task 0 received status AddRelease: Downloading (90%).
2024/05/01 22:46:16 Task 0 running for 33s.
2024/05/01 22:46:16 Task 0 received status AddRelease: Downloading (91%).
2024/05/01 22:46:16 Task 0 running for 33s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:16 Task 0 received status AddRelease: Downloading (92%).
2024/05/01 22:46:16 Task 0 running for 33s.
2024/05/01 22:46:17 Task 0 received status AddRelease: Downloading (93%).
2024/05/01 22:46:17 Task 0 running for 33s.
2024/05/01 22:46:17 Task 0 received status AddRelease: Downloading (94%).
2024/05/01 22:46:17 Task 0 running for 33s.
2024/05/01 22:46:17 Task 0 received status AddRelease: Downloading (95%).
2024/05/01 22:46:17 Task 0 running for 34s.
2024/05/01 22:46:17 Task 0 received status AddRelease: Downloading (96%).
2024/05/01 22:46:17 Task 0 running for 34s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
2024/05/01 22:46:18 Task 0 received status AddRelease: Downloading (97%).
2024/05/01 22:46:18 Task 0 running for 34s.
2024/05/01 22:46:18 Task 0 received status AddRelease: Downloading (98%).
2024/05/01 22:46:18 Task 0 running for 34s.
2024/05/01 22:46:18 Task 0 received status AddRelease: Downloading (99%).
2024/05/01 22:46:18 Task 0 running for 35s.
[INFO] add_release.go:383] download complete, final startingOffset 0, final bytesWritten 3959596032, totalBytes (start+written) 3959596032
[INFO] add_release.go:433] Body checksum "rC0Dqz4iD4jYrEmcHPltvHdFzl4/XYdIkYokN8sSupc=" matches digest header "rC0Dqz4iD4jYrEmcHPltvHdFzl4/XYdIkYokN8sSupc="
[INFO] add_release.go:161] Downloaded fleetos-1052647~gite6f344f80917b8-opt.squashfs successfully
```
- Verify code signing
```
2024/05/01 22:46:18 Task 0 received status AddRelease: Processing.
2024/05/01 22:46:18 Task 0 running for 35s.
Verifying Release
[INFO] server.go:332] Successful save to lir-svc-releases configmap on attempt 1
Verifying Internal Build
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
...
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
Verified OK
[INFO] add_release.go:186] Code Signing verification successful
```
- Unsquashfs
```
[INFO] add_release.go:454] UnsquashFS to /tmp/tmp.fos.1232999799/fleetos-1052647~gite6f344f80917b8-opt.squashfs.release
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
...
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
[INFO] add_release.go:196] UnsquashFS to /tmp/tmp.fos.1232999799/fleetos-1052647~gite6f344f80917b8-opt.squashfs.release successfully
```
- Extract lir-data IPs and verify expected lir-data replica count is equal to number of IPs returned
```
[INFO] replication.go:30] Retrieving IPs of all lir-data replicas
[INFO] add_release.go:218] Found lir-data replica IPs: [172.26.121.130 172.26.122.2 172.26.58.12]
[INFO] add_release.go:235] - Primary lir-data registry server: 172-26-121-130.lir-data.cm.svc.cluster.local.:5000
[INFO] add_release.go:236] - Primary lir-data rsyncd server: 172-26-121-130.lir-data-sync.cm.svc.cluster.local.:8873
[INFO] add_release.go:237] - Primary lir-data grpc server: 172-26-121-130.lir-data-sync.cm.svc.cluster.local.:1111
```
- Sync files to the lir-data file server
```
[INFO] add_release.go:529] Running rsync operation: 'rsync -av /tmp/tmp.fos.1232999799/fleetos-1052647~gite6f344f80917b8-opt.squashfs.release/FleetOS-files/ rsync://lir@172-26-121-130.lir-data-sync.cm.svc.cluster.local.:8873/lir-data/lir-f/9999.0.0.0-1052647'
2024/05/01 22:46:40 Task 0 received status Running rsync operation: 'rsync -av /tmp/tmp.fos.1232999799/fleetos-1052647~gite6f344f80917b8-opt.squashfs.release/FleetOS-files/ rsync://lir@172-26-121-130.lir-data-sync.cm.svc.cluster.local.:8873/lir-data/lir-f/9999.0.0.0-1052647'.
2024/05/01 22:46:40 Task 0 running for 57s.
sending incremental file list
created directory lir-f/9999.0.0.0-1052647
./
FleetOS-charts.tar.gz
install-control.yaml
manifest.txt
software-recipe.yaml
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'

sent 407,966 bytes  received 150 bytes  816,232.00 bytes/sec
total size is 407,519  speedup is 1.00
[INFO] add_release.go:249] All files rsynced to LIR-F on primary LIR-DATA successfully
```
- Push containers to the lir-data docker registry
```
[INFO] add_release.go:601] Loading calico/apiserver:v3.26.1
[INFO] add_release.go:606] Pushing calico/apiserver:v3.26.1 to 172-26-121-130.lir-data.cm.svc.cluster.local.:5000
2024/05/01 22:46:41 Task 0 received status Loading calico/apiserver:v3.26.1.
2024/05/01 22:46:41 Task 0 running for 57s.
2024/05/01 22:46:41 Task 0 received status Pushing calico/apiserver:v3.26.1 to 172-26-121-130.lir-data.cm.svc.cluster.local.:5000.
2024/05/01 22:46:41 Task 0 running for 57s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
[INFO] add_release.go:638] Tagging image 172-26-121-130.lir-data.cm.svc.cluster.local.:5000/calico/apiserver:v3.26.1 with tag 9999.0.0.0-1052647-v3.26.1
2024/05/01 22:46:42 Task 0 received status Tagging image 172-26-121-130.lir-data.cm.svc.cluster.local.:5000/calico/apiserver:v3.26.1 with tag 9999.0.0.0-1052647-v3.26.1.
2024/05/01 22:46:42 Task 0 running for 58s.
[INFO] add_release.go:652] Tagged image 172-26-121-130.lir-data.cm.svc.cluster.local.:5000/calico/apiserver:v3.26.1, with tag 9999.0.0.0-1052647-v3.26.1
[INFO] add_release.go:601] Loading calico/cni:v3.26.1
[INFO] add_release.go:606] Pushing calico/cni:v3.26.1 to 172-26-121-130.lir-data.cm.svc.cluster.local.:5000
2024/05/01 22:46:42 Task 0 received status Loading calico/cni:v3.26.1.
2024/05/01 22:46:42 Task 0 running for 58s.
2024/05/01 22:46:42 Task 0 received status Pushing calico/cni:v3.26.1 to 172-26-121-130.lir-data.cm.svc.cluster.local.:5000.
2024/05/01 22:46:42 Task 0 running for 58s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
[INFO] add_release.go:638] Tagging image 172-26-121-130.lir-data.cm.svc.cluster.local.:5000/calico/cni:v3.26.1 with tag 9999.0.0.0-1052647-v3.26.1
2024/05/01 22:46:44 Task 0 received status Tagging image 172-26-121-130.lir-data.cm.svc.cluster.local.:5000/calico/cni:v3.26.1 with tag 9999.0.0.0-1052647-v3.26.1.
2024/05/01 22:46:44 Task 0 running for 1m0s.
[INFO] add_release.go:652] Tagged image 172-26-121-130.lir-data.cm.svc.cluster.local.:5000/calico/cni:v3.26.1, with tag 9999.0.0.0-1052647-v3.26.1
[INFO] add_release.go:601] Loading hexos/container-base-2.0:2.0.0-10
[INFO] add_release.go:606] Pushing hexos/container-base-2.0:2.0.0-10 to 172-26-121-130.lir-data.cm.svc.cluster.local.:5000
2024/05/01 22:46:44 Task 0 received status Loading hexos/container-base-2.0:2.0.0-10.
2024/05/01 22:46:44 Task 0 running for 1m0s.
2024/05/01 22:46:44 Task 0 received status Pushing hexos/container-base-2.0:2.0.0-10 to 172-26-121-130.lir-data.cm.svc.cluster.local.:5000.
2024/05/01 22:46:44 Task 0 running for 1m0s.
[INFO] add_release.go:638] Tagging image 172-26-121-130.lir-data.cm.svc.cluster.local.:5000/hexos/container-base-2.0:2.0.0-10 with tag 9999.0.0.0-1052647-2.0.0-10
2024/05/01 22:46:44 Task 0 received status Tagging image 172-26-121-130.lir-data.cm.svc.cluster.local.:5000/hexos/container-base-2.0:2.0.0-10 with tag 9999.0.0.0-1052647-2.0.0-10.
2024/05/01 22:46:44 Task 0 running for 1m1s.
[INFO] add_release.go:652] Tagged image 172-26-121-130.lir-data.cm.svc.cluster.local.:5000/hexos/container-base-2.0:2.0.0-10, with tag 9999.0.0.0-1052647-2.0.0-10
...
[INFO] add_release.go:263] All images pushed to LIR-DR on primary LIR-DATA successfully
```
- Replicate data to all lir-data replicas across the nodes
```
[INFO] replication.go:99] Starting lir-data replication - attempt 1
[INFO] replication.go:103] Extracted lir-data primary IP: 172.26.121.130
[INFO] replication.go:30] Retrieving IPs of all lir-data replicas
[INFO] replication.go:143] Replicating release from primary: 172-26-121-130.lir-data-sync.cm.svc.cluster.local.:1111 to nodes: [172.26.121.130 172.26.122.2 172.26.58.12]
2024/05/01 22:47:34 Task 0 received status AddRelease: Replicating.
2024/05/01 22:47:34 Task 0 running for 1m51s.
[INFO] replication.go:169] Created gRPC client for lir-data grpc server '172-26-121-130.lir-data-sync.cm.svc.cluster.local.:1111'
[INFO] replication.go:183] Replicating to '172-26-121-130.lir-data-sync.cm.svc.cluster.local.' (lir-data 1 of 3)
[INFO] server.go:332] Successful save to lir-svc-releases configmap on attempt 1
2024/05/01 22:47:34 Task 0 received status AddRelease: Replicating to '172-26-121-130.lir-data-sync.cm.svc.cluster.local.' (lir-data 1 of 3).
2024/05/01 22:47:34 Task 0 running for 1m51s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
[INFO] replication.go:211]  -> Rsync request succeeded with status message 'Rsync pushed /var/opt/hpe/containers/lir/ to 172-26-121-130.lir-data-sync.cm.svc.cluster.local. successfully'
[INFO] replication.go:183] Replicating to '172-26-122-2.lir-data-sync.cm.svc.cluster.local.' (lir-data 2 of 3)
2024/05/01 22:47:34 Task 0 received status AddRelease: Replicating to '172-26-122-2.lir-data-sync.cm.svc.cluster.local.' (lir-data 2 of 3).
2024/05/01 22:47:34 Task 0 running for 1m51s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
...
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
[INFO] replication.go:211]  -> Rsync request succeeded with status message 'Rsync pushed /var/opt/hpe/containers/lir/ to 172-26-122-2.lir-data-sync.cm.svc.cluster.local. successfully'
[INFO] replication.go:183] Replicating to '172-26-58-12.lir-data-sync.cm.svc.cluster.local.' (lir-data 3 of 3)
2024/05/01 22:47:49 Task 0 received status AddRelease: Replicating to '172-26-58-12.lir-data-sync.cm.svc.cluster.local.' (lir-data 3 of 3).
2024/05/01 22:47:49 Task 0 running for 2m5s.
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
...
[INFO] server.go:259] Received GetStatus Request - ReleaseVersion: '9999.0.0.0-1052647'
[INFO] replication.go:211]  -> Rsync request succeeded with status message 'Rsync pushed /var/opt/hpe/containers/lir/ to 172-26-58-12.lir-data-sync.cm.svc.cluster.local. successfully'
[INFO] replication.go:218] Replication completed on attempt 1
[INFO] add_release.go:275] Replication of release successful
```
- Scale back and clean up
```
[INFO] add_release.go:143] Cleaned up successfully
[INFO] add_release.go:97] Reducing lir-data replica count...
[INFO] add_release.go:103] Waiting for reduction to 2 lir-data replicas...
[INFO] wait.go:91] waiting for Deployment "lir-data" to be ready
[INFO] wait.go:107] polling Deployment "lir-data" until condition is met
2024/05/01 22:48:03 Task 0 received status AddRelease: Ready.
2024/05/01 22:48:03 Task 0 running for 2m19s.
[INFO] add_release.go:108] Successfully scaled back to 2 lir-data replicas
[INFO] add_release.go:78] Sending final add release status over the channel: 'AddRelease: Ready'
[INFO] server.go:332] Successful save to lir-svc-releases configmap on attempt 1
```
**Gotchas**
- Perhaps discuss lir-svc restart scenarios
- lir-svc can be accessed using pod IPs but the Kubernetes service cluster IP should be used
**Comparisons**
**Additional Information**
- Add configuration details about the deployment
