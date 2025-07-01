**Week of 6/30/25:**

Work:
- Make story for updating the kubectl dsp plugin.
- Checked in the cli user rbac permissions for oncs P0 bug fix
- Reached out to one of the DSCC folks because I never heard from them after the integration meeting on tuesday. Hoping to check if I can check in the switch port name addition to the CRD.
- More editing for my switch controller webhook changes
	- Currently only validating firmware version
	- Other validations are part of another story that matt defined
	- Need to test
	- Will put out a review once one of my other two switch controller stories gets checked in
- Need to test webhook changes on top of changes currently out for review so need to get those checked in
- Webhook Validation Logic: 
	if nil -> something don't validate
	if something -> something validate
- Move firmware validation code into the webhook 
- Started writing webhook unit tests
- Once this is complete I can start putting it all together
	Switch Firmware update steps:
	1. Set Offline request api -> OFF
	2. Upload firmware request api
	3. Reboot switch request api
	4. Set Offline request api -> ON
- Renewed Virtual Digital Badge

push switch port name change to R3 - rebase change
provide build # to dscc folks