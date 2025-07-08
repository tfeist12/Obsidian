**Week of 6/30/25:**

In Progress:
- Make story for updating the kubectl dsp plugin.
- Need to reactivate my copilot account because I keep getting 30 day usage warning emails
- Currently working on switch controller webhook changes
	- Added a mutating webhook that should solve the update scenario we discussed
	- Submit a new build and test it
- Once this is complete I can start putting it all together
- Need to take a look at more bugs after this

Complete:
- Checked in the cli user rbac permissions for oncs P0 bug fix
- Renewed Virtual Digital Badge
- Finished writing webhook unit tests
- Check in with DSCC folks about switch port name field change
	- Need to provide the build number of this R3 change
- Pushed switch port name change
- Pushed switch firmware crd update and fake reconcile loop

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

Update notes:
- Potentially use a mutating webhook that runs on create and update to populate spec fields
- This could render the creation reconciliation operation obsolete 