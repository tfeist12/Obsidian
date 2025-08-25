**Week of 8/22/25**

To Do:
- Update nvim config and push to repo
- Check on goals
- Make story for updating the kubectl dsp plugin.


ActPodRefactor: Probably need a story for this work soon
- dsp name is the name of the deployment
- pod name is the per instance name of the pod 

perhaps pod type is part of config
when you create a config at the highest level you provide the type
We can actually use the existing act pod type for identification i believe

Need to update comments that mention dsp and osd
consts within the etcd client and k8s client become part of config

currently build and unit tests pass but I need to test install 