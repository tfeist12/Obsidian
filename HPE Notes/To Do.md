**Week of 9/24/25**

Yesterday:
- Radhika ran into an issue with her automation. Need to look into this more
- DSP Refactor walkthrough
- v3.6.7 switchd added to base containers so I posted a review to use the new port name
	- Sounds like there needs a be a change from the QA side before check-in though
	- Both test_switch_get_attributes tests seem to be failing after this change
- Discussions with Eric Champagne about inactive firmware version reporting and fake firmware update

To Do:
- Make story for updating the kubectl dsp plugin.
- Clean up Raj's checkin:
	- Naming - clienthfTLSConfig -> clientHfTLSConfig
	- Formatting - `go fmt`
		- hfcluster/src/ippodd/client/grpc_client.go
		- hfcluster/src/ippodd/ippodd/internal/rpc/server_test.go
- Randomize number in range for each sleep in fake firmware update