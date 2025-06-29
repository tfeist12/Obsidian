Currently working on a story to add a NOT_FOUND status to lir. this status is returned when we attempt a getstatus with a release version that doesn't exist or we attempt to remove a release with a version that doesn't exist

https://nimblejira.nimblestorage.com/browse/AS-180864 is also impacted as I added a CODE_SIGN_FAILURE status which will be used in the future

```
[INFO] job_queue.go:74] mode is idle
[INFO] job_queue.go:221] found version 0.0.4870.0-187322975088809 pending install
[INFO] job_queue.go:385] starting install to version 0.0.4870.0-187322975088809
[INFO] status.go:234] received event job_queue_start_install with context {CR:0.0.4870.0-187322975088809 Deleted:false Paused:false Message:}
[INFO] status.go:250] not transitioning state from event job_queue_start_install at pending
[INFO] status.go:257] transitioning mode from event job_queue_start_install at idle to updating
[INFO] status.go:481] starting update to version 0.0.4870.0-187322975088809
[INFO] job_queue.go:60] already processing job, waiting...
[INFO] status.go:866] starting update heartbeat
[INFO] statemachine.go:43] enter stageGetConfig
[INFO] cluster_config.go:149] GenerateConfigMapYaml: /tmp/swus/swupdate-cluster-config.yaml
[ERROR] cluster_config.go:212] filter key does not exists in config: numSharedCoresPerNode
[ERROR] cluster_config.go:212] filter key does not exists in config: minNodeCoreCount
[INFO] statemachine.go:60] exit stageGetConfig
[INFO] statemachine.go:43] enter stageDownload
[INFO] status.go:234] received event staging_start with context {CR:0.0.4870.0-187322975088809 Deleted:false Paused:false Message:}
[INFO] status.go:241] transitioning state from event staging_start at pending to staging
[INFO] status.go:266] not transitioning mode from event staging_start at updating
[INFO] k8sserver.go:178] Notifying clients that resource cluster-software's state is now UPDATE_STAGING_STARTING...
[INFO] k8sserver.go:221] Resource cluster-software's state is now set to UPDATE_STAGING_STARTING. Waiting for acknowledgements.
[INFO] k8sserver.go:261] All acknowledgements have been received for state UPDATE_STAGING_STARTING and resource cluster-software
[INFO] statemachine.go:43] enter checkDownloadProgress
[INFO] stage_download.go:118] stageDownload - download already in progress for release version "0.0.4870.0-187322975088809", waiting for completion
[INFO] statemachine.go:60] exit checkDownloadProgress
[INFO] statemachine.go:43] enter waitForDownloadCompletion
2024-03-25T18:09:47Z    DEBUG   controller-runtime.webhook.webhooks     received request        {"webhook": "/validate-sc-hpe-com-v1-clustersoftware", "UID": "4f70951b-d54d-4610-91fd-daacf289d09d", "kind": "sc.hpe.com/v1, Kind=ClusterSoftware", "resource": {"group":"sc.hpe.com","version":"v1","resource":"clustersoftware"}}
2024-03-25T18:09:47Z    DEBUG   controller-runtime.webhook.webhooks     wrote response  {"webhook": "/validate-sc-hpe-com-v1-clustersoftware", "code": 200, "reason": "", "UID": "4f70951b-d54d-4610-91fd-daacf289d09d", "allowed": true}
```

```
kubectl patch clustersoftware cluster-software -n cm --type merge -p '{"spec":{"version":{"id":"https://artifactory.eng.nimblestorage.com/artifactory/fleetos-local/private/feist-AS179080-lirStatusNotFound/release/1710993182719895/fleetos-1710993182719895~gitc5fead530b8ebf-opt.squashfs","version": "THF-TEST-0"}}}'
```
