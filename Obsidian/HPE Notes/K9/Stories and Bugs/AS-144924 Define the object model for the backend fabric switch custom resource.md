To Do:
Get in touch with Maria about switch configuration

Ongoing Questions:
- Where do we get the initial config if we want to call update config. Do we store and make changes
- Do switchloginfo and switchstats count toward readable elements as they are a part of the collect telemetry response?
- How was it decided which switch settings have getters and setters (Shantanu?)

Story Notes:
- Determine default values for the spec keys
- Unsure if I need to include requests and response in the yaml
	- these functions will be implemented in the protobuf and in the switchd client
- Should we update mock switchd as well as the operator controller/client? 
- GRPC calls made to switchd based on what the spec and status show needs to be done
- Check what the architecture currently is and use that to determine readable attributes
- Repeated in the proto file means that that field can be repeated any number of times including zero

Top Down Architecture:
1. GLCP: Greenlake Cloud platform
2. Switchdoperator <-> Local image repository
3. Switchd
	1. mcall, grpc, rest
	- grpc is external request to switchd?
	2. mcall is internal request for information?
	- rest to the switch itself?
4. Aruba switch

Teams:
- nvgrid = containerization of switchd
- switch_mgmt = switchd proper

Mcall Handler Functions
- show
- locate led
- enable port
- update firmware
- reboot switch
- collect
- insert fault
- set offline mode
- update config
- upload firmware
- set interface ip


Aruba Switch VM
```
curl   --noproxy 10.226.68.243  -k -X POST  -c /tmp/auth_cookie  -H 'Content-Type: multipart/form-data'   "https://10.226.68.243/rest/v1/login"  -F 'username=admin' -F 'password=admin'
```
```
curl --noproxy 10.226.68.243 -k GET -b /tmp/auth_cookie "https://10.226.68.243/rest/v1/system"
```