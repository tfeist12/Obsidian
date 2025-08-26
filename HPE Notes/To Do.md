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