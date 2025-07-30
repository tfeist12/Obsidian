DSP Balance
- dspmapper logs
- descheduler logs
- node problem detector logs

Containerd
- boot.log
	- "Inserted module 'nvmet'" indicates a reboot

**Notes**
- There is only a single scheduler and descheduler on the cluster at a time
- Check the cluster confirm directory for txt files that show pod and node data
- If the kube-scheduler is showing a failure to acquire a lease this indicates it's not the leader