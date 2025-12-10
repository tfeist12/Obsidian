**To Do:**
- Make story for updating the kubectl dsp plugin.
- Make story to refactor lir-svc configmap code to use k8scommon configmap functions
- Use Claude within nvim
	- Potentially send all open buffers to the tool
	- Plugin Options:
		- https://github.com/olimorris/codecompanion.nvim
		- https://github.com/yetone/avante.nvim
- When is HPE switching to WiPro?
	- How long are we going to tolerate the mediocrity of these contractors?

```
time="2025-12-10T07:37:40Z" level=error msg="Failed to perform lir data rsync operation: rpc error: code = Unknown desc = Rsync operation failed with the following error: GRPC_ERR, ''"  
root@c0n0:/var/opt/hpe/containers# k get pods -n cm -o wide -w | grep lir-data  
lir-data-58b487f578-9v8z2                         0/5     Pending    0             7m51s   <none>           <none>   <none>           <none>  
lir-data-5d47589964-hrg9r                         0/5     Init:1/2   2 (33s ago)   8m54s   172.26.121.173   c0n0     <none>           <none>  
lir-data-6bcc58f9f4-sszjx                         5/5     Running    0             16m     172.26.122.2     c0n1     <none>           <none>  
lir-data-f7bbbdd78-9s47k                          5/5     Running    0             14m     172.26.58.7      c0n2     <none>           <none>
```