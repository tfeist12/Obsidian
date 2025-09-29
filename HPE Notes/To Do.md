**Week of 9/24/25**

Yesterday:
- Radhika ran into an issue with her fw update automation. Need to look into this more
- DSP Refactor walkthrough
- v3.6.7 switchd added to base containers so I posted a review to use the new port name
	- Sounds like there needs a be a change from the QA side before check-in though
	- Both test_switch_get_attributes tests seem to be failing after this change
- Discussions with Eric Champagne about inactive firmware version reporting and fake firmware update
- Run dsp related tests before refactor check in

To Do:
- Make story for updating the kubectl dsp plugin.
- Clean up Raj's checkin:
	- Naming - clienthfTLSConfig -> clientHfTLSConfig
	- Formatting - `go fmt`
		- hfcluster/src/ippodd/client/grpc_client.go
		- hfcluster/src/ippodd/ippodd/internal/rpc/server_test.go
- Randomize number in range for each sleep in fake firmware update


```
I feel like I need to clarify the difference between fake and real here...
In an hfsim environment, it is impossible to make real changes, like a firmware update does, to a switch. This is because there is no real switch... Everything is simulated. That's why every hfsim switchd runs in a fake mode where two switches are shown and API calls update these two fake switches. Currently, the firmware update related API calls don't do anything in hfsim's fake mode. This change (https://github.hpe.com/StorageGBU/nvgrid/pull/4245) is what makes the API calls work in hfsim fake mode. This is also why we previously were doing all the fake firmware update handling within the switch controller. This switchd version update allows the switch controller to be platform agnostic. We would be making the same API calls no matter the platform, and every firmware update is treated as a real one from the perspective of the switch controller.
```