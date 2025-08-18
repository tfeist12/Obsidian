**A ListSwitches call includes the following data:**
- ID
- Model
- Serial
- Firmware Version
- Status
- Usage
- LED State
- Ps0 State
- Ps1 State
- Fan State
- Temp State
- IP Address
- MAC Address
- VSX Status
- List of Fan Info
- List of Port Info
- List of DHCP SVC Info
- List of VLAN Info

**The PL3 switch CRD includes the following fields:**
- Switch Object
	- clusterId
	- clusterRef
	- modelNumber
	- numberOfPorts
	- partNumber
	- serialNumber
	- spec
		- locatorLEDState
	- status
		- commonResourceStatusAttributes
			- lastModifiedTime
			- observedGeneration
			- ready
		- lastModifedTime
		- locatorLED
		- SwitchFans

**Story Captain Steps:**
1. Determine reconcile functionality and frequency for calling ListSwitches
2. ListSwitches Grpc call to switchd
3. Parse response
4. Fill PL3 fields
5. kubectl describe switch pretty print
	1. fleetos-node is a good example of this