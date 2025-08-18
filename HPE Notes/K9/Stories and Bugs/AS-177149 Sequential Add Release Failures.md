Initial Timing:
- 2024-01-11T17:32:58.775406864Z [INFO] add_release.go:91] Waiting for 3 lir-data replicas to start…
- 2024-01-11T17:33:08.683371156Z [INFO] add_release.go:97] Successfully scaled up to 3 lir-data replicas
- 2024-01-11T17:34:02.616452969Z [INFO] replication.go:36] Retrieving IPs of all lir-data replicas
- 2024-01-11T17:34:02.693771470Z [INFO] add_release.go:175] Found lir-data replica IPs: [172.26.122.30 172.26.121.156 172.26.58.50]

~54s between scale up and query

Sequential Timing
- 2024-01-11T17:34:13.128932230Z [INFO] add_release.go:91] Waiting for 3 lir-data replicas to start...
- 2024-01-11T17:34:13.140889160Z [INFO] add_release.go:97] Successfully scaled up to 3 lir-data replicas  
  
The deferred scale down of lir-data replicas from the initial add is happening during the download step of the subsequent add:
- 2024-01-11T17:34:12.948384542Z 2024/01/11 17:34:12 Starting Task 1.
- 2024-01-11T17:34:12.956014089Z 2024/01/11 17:34:12 Task 1 received status AddRelease: Initializing replica pods.
- 2024-01-11T17:34:12.956038430Z 2024/01/11 17:34:12 Task 1 running for 0s.
- 2024-01-11T17:34:13.128932230Z [INFO] add_release.go:91] Waiting for 3 lir-data replicas to start...
- 2024-01-11T17:34:13.128959346Z [INFO] wait.go:69] waiting for Deployment "lir-data" to be ready
- 2024-01-11T17:34:13.128963024Z [INFO] wait.go:85] polling Deployment "lir-data" until condition is met
- 2024-01-11T17:34:13.140889160Z [INFO] add_release.go:97] Successfully scaled up to 3 lir-data replicas
- 2024-01-11T17:34:13.140904899Z [INFO] add_release.go:114] Created working directory /tmp/tmp.fos.1788768366 sucessfully
- 2024-01-11T17:34:13.140908462Z [INFO] add_release.go:129] Started downloading [http://172.19.0.1/fleetos-36765482776232~gituncommitted-opt.squashfs](http://172.19.0.1/fleetos-36765482776232~gituncommitted-opt.squashfs)
- 2024-01-11T17:34:13.140922226Z 2024/01/11 17:34:13 Task 1 received status AddRelease: Initialized.
- 2024-01-11T17:34:13.140932838Z 2024/01/11 17:34:13 Task 1 running for 0s.
- 2024-01-11T17:34:13.140935770Z 2024/01/11 17:34:13 Task 1 received status AddRelease: Downloading.
- 2024-01-11T17:34:13.140938548Z 2024/01/11 17:34:13 Task 1 running for 0s.
- 2024-01-11T17:34:13.142373397Z 2024/01/11 17:34:13 Successfully wrote 'lir-svc/THF-Test-2:DOWNLOADING' into hf-etcd at: etcd-cluster-client.cm.svc.cluster.local.:2379
- 2024-01-11T17:34:13.482629721Z 2024/01/11 17:34:13 Task 1 received status AddRelease: Downloading (1%).
- 2024-01-11T17:34:13.482639849Z 2024/01/11 17:34:13 Task 1 running for 1s.
- 2024-01-11T17:34:13.686915823Z 2024/01/11 17:34:13 Task 1 received status AddRelease: Downloading (2%).
- 2024-01-11T17:34:13.686947386Z 2024/01/11 17:34:13 Task 1 running for 1s.
- 2024-01-11T17:34:13.783696570Z [INFO] add_release.go:121] Cleaned up successfully
- 2024-01-11T17:34:13.783719284Z [INFO] add_release.go:81] Reducing lir-data replica count...
- 2024-01-11T17:34:13.860173331Z [INFO] add_release.go:88] Successfully scaled back to 2 lir-data replicas