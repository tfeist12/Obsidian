**Week of 6/30/25:**

In Progress:
- Make story for updating the kubectl dsp plugin.
- More editing for my switch controller webhook changes
	- Currently only validating firmware version
	- Other validations are part of another story that matt defined
	- Need to test
	- Will put out a review once one of my other two switch controller stories gets checked in
- Need to test webhook changes on top of changes currently out for review so need to get those checked in
- Move firmware validation code into the webhook 
- Once this is complete I can start putting it all together

Complete:
- Checked in the cli user rbac permissions for oncs P0 bug fix
- Renewed Virtual Digital Badge
- Finished writing webhook unit tests
- Check in with DSCC folks about switch port name field change
	- Need to provide the build number of this R3 change
- Pushed switch port name change
- Pushed switch firmware crd update and fake reconcile loop

[AS-197203](https://jira.storage.hpecorp.net/browse/AS-197203)
	Required switchd
	Switch Firmware update steps:
		1. Set Offline request api -> OFF
		2. Upload firmware request api
		3. Reboot switch request api
		4. Set Offline request api -> ON
	Switchd GRPC client updates will be required

Update notes:
	Potentially use a mutating webhook that runs on create and update to populate spec fields
	This could render the creation reconciliation operation obsolete 