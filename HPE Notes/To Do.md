**Week of 7/21/25**

To Do:
- Update nvim config and push to repo
- Check on goals
- Make story for updating the kubectl dsp plugin.

Today:
- Work with Asha for manual verification of fake fw update
- Intern Project fair
- Initial switch conditions code change is done, need to test it and write some unit tests
- Take a look at AS-207587

[AS-197203](https://jira.storage.hpecorp.net/browse/AS-197203)
	Switch Firmware update steps:
		1. Set Offline request api -> OFF
		2. Upload firmware request api
		3. Reboot switch request api
		4. Set Offline request api -> ON
	Requirements:
	- Switchd GRPC client updates
	- State machine
	- Unit test updates