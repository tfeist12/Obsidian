**Week of 7/21/25**

To Do:
- Update nvim config and push to repo
- Check on goals
- Make story for updating the kubectl dsp plugin.

Today:
- Talked to Greg about the lir-data scaling bug
	- Sounds similar to a one he had been working on but it's at a different point in the lifecycle
	- Hoping for a repro of the other bug with containerd set to log at debug level
- Talked to Matt a bit about the Ring3 dsp spread failure
	- Dsps are balanced but the test is hitting exceptions, perhaps unable to query the cluster for dsp info
- Start working on the switch conditions story we made last week

[AS-197203](https://jira.storage.hpecorp.net/browse/AS-197203)
	Switch Firmware update steps:
		1. Set Offline request api -> OFF
		2. Upload firmware request api
		3. Reboot switch request api
		4. Set Offline request api -> ON
	Requirements:
	- Switchd to report if firmware version has been uploaded to the inactive partition ([AS-189429](https://jira.storage.hpecorp.net/browse/AS-189429 "Provide FW version for the secondary partition in ListSwitches/\"show switch\"")) or use a fixed wait time after which we assume the upload is complete.
	- Switchd GRPC client updates
	- State machine
	- Unit test updates

762
593