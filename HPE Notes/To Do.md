**Week of 7/21/25**

In Progress:
- Update nvim config and push to repo
- Secure development training before taking off next week
- Check on goals
- Make story for updating the kubectl dsp plugin.
- Review has been posted for the switch controller webhook changes
- Once this is complete I can start putting it all together
- Starting to dig more into the lir-data scaling bug
	- where is the lir-data init pod stored?
	- I see that the container was not initalized causing the pod to fail

Complete:

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