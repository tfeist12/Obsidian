**Week of 7/21/25**

In Progress:
- Update nvim config and push to repo
- Secure development training before taking off next week
- Check on goals
- Make story for updating the kubectl dsp plugin.
- Review has been posted for the switch controller webhook changes

Today:
- Reviewed Karisma's Partner CRD and controller after their recent update
- Discussion about the code organization for the activation pod. Mostly Britt and Matt
- Discussion about how to quickly recover the switch for qa firmware update testing
- Continued looking into this lir-data scaling bug
- Once I've figured out next steps for this bug I will move on. Sounds like there will be a few switch firmware update stories I should prioritize before I complete the one in my backlog
- Taking off a wee bit early to go pick up the new vehicle this afternoon

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