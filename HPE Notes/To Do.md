**Week of 7/21/25**

Complete:

In Progress:
- Update nvim config and push to repo
- Secure development training before taking off next week
- Check on goals
- Make story for updating the kubectl dsp plugin.
- Review has been posted for the switch controller webhook changes
- Once this is complete I can start putting it all together
- Starting to dig more into the lir-data scaling bug
	- Where is the lir-data init pod stored and what does it do?
		- This is the container that returned an incomplete status
		- Is the full thing just the chown and mkdir commands stored in the lir-data deployment helm chart?
		- I don't believe the other containers are cleared to start if the init container fails

Today:
- Review Asha's FW update test plan
- Continue looking into this lir-data scaling bug
	- boot.log for containerd info
	- likely after schedule but check kubescheduler

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