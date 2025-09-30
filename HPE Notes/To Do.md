### Week of 9/29/25

**To Do:**
- Make story for updating the kubectl dsp plugin.
- Clean up Raj's checkin - stashed as "rajFix"
	- Naming - clienthfTLSConfig -> clientHfTLSConfig
	- Formatting - `go fmt`
		- hfcluster/src/ippodd/client/grpc_client.go
		- hfcluster/src/ippodd/ippodd/internal/rpc/server_test.go
- Self Evaluation

**Yesterday:**
- Code reviews, Raj and Eric
- Caught up on training
- Checked in the new port name usage


role 
list get patch for pods 
may not need get

check for ready state in pod list

Create a new review 

new function updatepodannotation -> takes ip
use merge patch

ippodd/iptools/networkinterface/networkinterface.go 
- ipaddr show -j deserialize
- needs to address instead of mac