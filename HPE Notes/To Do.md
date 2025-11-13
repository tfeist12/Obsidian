### Week of 10/21/25

**To Do:**
- Make story for updating the kubectl dsp plugin.
- Review comments and test scenarios on ippodd osd add and remove ip address requests change

**Firmware update notes
- offline -> upload -> reboot -> online
- state machine sets conditions on our switch custom resource for each state
- offline and online mode are set almost instantly. upload takes about 5 minutes

- In its current state we perform a real firmware update with real API calls when our platform type is raider hardware. If it is hfsim we perform a mock firmware update managed by the switch controller. It follows the same steps with similar wait times but no API calls happen