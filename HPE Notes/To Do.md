### Week of 10/21/25

**To Do:**
- Make story for updating the kubectl dsp plugin.
- Review comments and test scenarios on ippodd osd add and remove ip address requests change

**Firmware update notes
- Webhook validators unable to do concurrent switch firmware updates. They must be done serially. 
- We also verify that a firmware image file exists in lir-data for the requested version before we begin the update
- Offline -> Upload -> Reboot -> Online
- State machine sets conditions on our switch custom resource for each state
- Offline and online mode are set almost instantly. upload takes about 5 minutes. reboot takes about 4
- Upload is skipped if the inactive partition is already running the requested version
- In its current state we perform a real firmware update with real API calls when our platform type is raider hardware. If it is hfsim we perform a mock firmware update managed by the switch controller. It follows the same steps with similar wait times but no API calls happen
- NVGrid has an update to handle a switch firmware update in switchd fake mode (hfsim). Planning to work on this and improving firmware update unit tests in the coming sprint