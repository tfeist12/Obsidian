EnablePort List Format
[Port 1: On, Port 2: Off … ]
On, Off, Uninitialized/Unknown/Idfk

Questions:
- Does the aruba switch always have 32 ports
- How / where to trigger update?
- Use current state to set spec for all 'settables'?
- What happens if switchPort enabled state changes asynchronously?

Notes:
- We can assume that if mac and ip are populated then a port is enabled
- We cannot assume that if mac and ip are not populated then a port is disabled
- Going to break a lot of automated tests with these changes

First reconcile:
- All ports in spec.enablePort list should be set to uninitialized
- Enter handleCreateRequest function and if spec.enablePort list is nil or uninitialized then we need to populate it using the status so we should trigger a refresh to get status
- Set spec equal to status but only on create to move out of uninitialized state?
- This assumes that the status.SwitchPorts struct contains enabled (either from hack or API)

When we edit CR:
- After first reconcile the spec.EnablePort list should now contain an updated list
- Ideally want this to be key value pairs in the yaml for readability
- We want to take the spec.EnablePort list, iterate and check against status.switchPorts.Enabled
- If any differ then launch update handler and make grpc calls for each differing port
- Refresh will be triggered afterwards

![[Pasted image 20240314091423.png]]