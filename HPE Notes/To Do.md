**Week of 8/22/25**

To Do:
- Update nvim config and push to repo
- Check on goals
- Make story for updating the kubectl dsp plugin.


ActPodRefactor: Probably need a story for this work soon
- DSP name is the name of the deployment
- Pod name is the per instance name of the pod 

perhaps pod type is part of config
when you create a config at the highest level you provide the type
We can actually use the existing act pod type for identification i believe

Need to update comments that mention dsp and osd
consts within the etcd client and k8s client become part of config

currently build and unit tests pass but I need to test install 

```
const (
	DspNameEnv       = "DSP_NAME"
	DspIdEnv         = "DSP_ID" // {UUID}.{2-byte ID}
	DspTypeEnv       = "DSP_TYPE"
	PodNameEnv       = "POD_NAME"
	PodIPEnv         = "POD_IP"
	PodUUIDEnv       = "POD_UUID"
	EtcdServiceEnv   = "HF_ETCD_SERVICE"
	EtcdNamespaceEnv = "HF_ETCD_NAMESPACE"
	OsdHostEnv       = "OSD_GRPC_HOST"  // for now, DSP process expects the IPv4 address of the node
	OsdPortEnv       = "OSD_GRPC_PORT"  // port of OSD gRPC service
	OsdNameSpaceEnv  = "OSD_NAMESPACE"  // K8s namespace for OSD Pods
	OsdAppNameEnv    = "OSD_APP_NAME"   // K8s app name associated with the OSD Pod. Current value = osd (app.kubernetes.io/name=osd)
	DspNameSpaceEnv  = "DSP_NAME_SPACE" // K8s namespace DSP Pods are deployed in
	NodeNameEnv      = "NODE_NAME"      // Name of the node the Pod is running on
	LivenessPortEnv  = "LIVENESS_PORT"
	PlatformTypeEnv  = "PLATFORM_TYPE"
	ConfigFileEnv    = "CONFIG_FILE"
)
```