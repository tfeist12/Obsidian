### Week of 10/6/25

**To Do:**
- Make story for updating the kubectl dsp plugin.
- Review Jonathan's Ippodd state monitoring change now that 
- Firmware update fix options:
	- If cluster is recoverable, watch firmware update and DNA collect for switch folks
	- Test manual firmware update to see if we get into a similar state

```
2025-10-17 16:37:21,030 379[454] I switchd_service.cc:488:UploadFirmware API UploadFirmware requested
2025-10-17 16:37:21,031 379[454] I switchd_service.cc:494:UploadFirmware UploadFirmwareRequest:
switch_id: 1
file_override: "/var/opt/switchd/firmware/ArubaOS-CX_8325_10_13_1110.swi"

Sent for switch 1 , partition: 0 file-override: /var/opt/switchd/firmware/ArubaOS-CX_8325_10_13_1110.swi
aruba_fw_upload: partition input: 0 active partition: primary updating: 1
aruba_fw_upload: FW file to upload: /var/opt/switchd/firmware/ArubaOS-CX_8325_10_13_1110.swi switchd idx 1
switch_err_inj_point: Injection ID 7 is for switch 1 target object -1 is not active. Skipping...
switchd_rest_fw_update called for switch_num 1 fw_file /var/opt/switchd/firmware/ArubaOS-CX_8325_10_13_1110.swi
   URL https://172.29.20.1/rest/v10.12/firmware?image=secondary
Upload cmd =/usr/bin/curl -v -k -b /var/tmp/switch_cookies/cookiesD_SW1_172.29.20.1.txt --write-out %{response_code} --silent --header 'Content-Type: multipart/form-data' --header 'Accept: */*' -F "fileupload=@/var/opt/switchd/firmware/ArubaOS-CX_8325_10_13_1110.swi" "https://172.29.20.1/rest/v10.12/firmware?image=secondary" 2>&1
line read  = *   Trying 172.29.20.1:443...

line read  = * Connected to 172.29.20.1 (172.29.20.1) port 443 (#0)

line read  = * ALPN: offers h2,http/1.1

line read  = } [5 bytes data]

line read  = * TLSv1.3 (OUT), TLS handshake, Client hello (1):

line read  = } [240 bytes data]

line read  = * TLSv1.3 (IN), TLS handshake, Server hello (2):

line read  = { [104 bytes data]

line read  = * TLSv1.2 (IN), TLS handshake, Certificate (11):

line read  = { [931 bytes data]

line read  = * TLSv1.2 (IN), TLS handshake, Server key exchange (12):

line read  = { [365 bytes data]

line read  = * TLSv1.2 (IN), TLS handshake, Server finished (14):

line read  = { [4 bytes data]

line read  = * TLSv1.2 (OUT), TLS handshake, Client key exchange (16):

line read  = } [102 bytes data]

line read  = * TLSv1.2 (OUT), TLS change cipher, Change cipher spec (1):

line read  = } [1 bytes data]

line read  = * TLSv1.2 (OUT), TLS handshake, Finished (20):

line read  = } [16 bytes data]

line read  = * TLSv1.2 (IN), TLS handshake, Finished (20):

line read  = { [16 bytes data]

line read  = * SSL connection using TLSv1.2 / ECDHE-RSA-AES256-GCM-SHA384

line read  = * ALPN: server accepted http/1.1

line read  = * Server certificate:

line read  = *  subject: CN=switch,SN=TW32KM304S; C=US; L=Roseville; ST=CA; O=HPE; OU=Aruba

line read  = *  start date: Mar  9 12:34:58 2018 GMT

line read  = *  expire date: Mar  1 12:34:58 2048 GMT

line read  = *  issuer: CN=switch,SN=TW32KM304S; C=US; L=Roseville; ST=CA; O=HPE; OU=Aruba

line read  = *  SSL certificate verify result: self-signed certificate (18), continuing anyway.

line read  = * using HTTP/1.1

line read  = } [5 bytes data]

line read  = > POST /rest/v10.12/firmware?image=secondary HTTP/1.1

line read  = > Host: 172.29.20.1

line read  = > User-Agent: curl/7.88.1

line read  = > Cookie: id=l2RL1Cn2nq7Ry7c26h8D3g==

line read  = > Accept: */*

line read  = > Content-Length: 389624804

line read  = > Content-Type: multipart/form-data; boundary=------------------------c897a2ddb94bc335

line read  = > Expect: 100-continue

line read  = >

line read  = { [5 bytes data]

line read  = < HTTP/1.1 100 Continue

line read  = } [5 bytes data]

switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
2025-10-17 16:37:31,032 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:37:31,244 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_hb_monitor: hb final status is 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:37:31,638 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
2025-10-17 16:37:47,937 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:37:48,136 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
2025-10-17 16:38:18,350 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_monitor_thread: starting switchd_monitor_thread
switchd_monitor_thread: Woke up! number of clients 1
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:38:19,557 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_hb_monitor: hb final status is 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:38:22,740 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:38:22,927 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:38:23,128 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:38:23,315 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
2025-10-17 16:38:52,740 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
callback_switch_events: case LWS_CALLBACK_CLIENT_WRITEABLE switch 2
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:38:54,948 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
2025-10-17 16:39:18,908 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:39:19,104 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:39:19,303 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_monitor_thread: Woke up! number of clients 1
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:39:20,504 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_hb_monitor: hb final status is 0
callback_switch_events: case LWS_CALLBACK_CLIENT_WRITEABLE switch 1
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:39:25,150 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:39:25,337 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
2025-10-17 16:39:55,540 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:39:55,732 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
2025-10-17 16:40:18,909 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:40:19,096 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:40:19,297 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:40:19,696 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
2025-10-17 16:40:25,931 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:40:27,391 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
2025-10-17 16:40:58,612 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:41:01,565 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
2025-10-17 16:41:18,907 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:41:20,791 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:41:21,417 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:41:21,610 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
2025-10-17 16:41:31,763 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_hb_monitor: hb final status is 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:41:33,554 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
callback_switch_events: case LWS_CALLBACK_CLIENT_WRITEABLE switch 2
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
2025-10-17 16:42:03,755 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:42:03,944 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_monitor_thread: starting switchd_monitor_thread
callback_switch_events: case LWS_CALLBACK_CLIENT_WRITEABLE switch 1
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
line read  = * We are completely uploaded and fine

2025-10-17 16:42:18,908 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:42:19,829 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:42:20,057 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:42:20,256 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
line read  = { [5 bytes data]

line read  = < HTTP/1.1 200 OK

line read  = < Server: nginx

line read  = < Date: Fri, 17 Oct 2025 16:42:26 GMT

line read  = < Content-Type: application/json; charset=utf-8

line read  = < Content-Length: 53

line read  = < Connection: keep-alive

line read  = < X-Frame-Options: SAMEORIGIN

line read  = < X-Content-Type-Options: nosniff

line read  = < X-XSS-Protection: 1; mode=block

line read  = < Strict-Transport-Security: max-age=31536000; includeSubdomains;

line read  = < Content-Security-Policy: script-src 'self' 'unsafe-inline'; object-src 'none'; font-src *; media-src 'none'; form-action 'self';

line read  = <

line read  = { [53 bytes data]

line read  = * Connection #0 to host 172.29.20.1 left intact

line read  = {"output":"Verifying and writing system firmware..."}200
switchd_rest_fw_update: Switch FW upload passed
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
2025-10-17 16:42:34,157 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:42:34,450 379[454] I switchd_service.cc:393:RebootSwitch API RebootSwitch requested
2025-10-17 16:42:34,450 379[454] I switchd_service.cc:399:RebootSwitch RebootSwitchRequest:
switch_id: 1

switchd_reboot called for switch id 1
aruba_reboot: partition input: 0 active partition: primary booting to: 1
SEC boot image =/rest/v10.12/boot?image=secondary
curler: switch_idx: 1 URL is https://172.29.20.1/rest/v10.12/boot?image=secondary, cpath: /var/tmp/switch_cookies/cookiesD_SW1_172.29.20.1.txt curlVer: 75801
UP: 0 of 0 DOWN: 0 of 0
*   Trying 172.29.20.1:443...
UP: 0 of 0 DOWN: 0 of 0
* Connected to 172.29.20.1 (172.29.20.1) port 443 (#0)
* ALPN: offers h2,http/1.1
UP: 0 of 0 DOWN: 0 of 0
UP: 0 of 0 DOWN: 0 of 0
* SSL connection using TLSv1.2 / ECDHE-RSA-AES256-GCM-SHA384
* ALPN: server accepted http/1.1
* Server certificate:
*  subject: CN=switch,SN=TW32KM304S; C=US; L=Roseville; ST=CA; O=HPE; OU=Aruba
*  start date: Mar  9 12:34:58 2018 GMT
*  expire date: Mar  1 12:34:58 2048 GMT
*  issuer: CN=switch,SN=TW32KM304S; C=US; L=Roseville; ST=CA; O=HPE; OU=Aruba
*  SSL certificate verify result: self-signed certificate (18), continuing anyway.
* using HTTP/1.1
UP: 0 of 0 DOWN: 0 of 0
UP: 0 of 0 DOWN: 0 of 0
> POST /rest/v10.12/boot?image=secondary HTTP/1.1
UP: 0 of 0 DOWN: 0 of 0
UP: 0 of 0 DOWN: 0 of 0
Host: 172.29.20.1
Transfer-Encoding: chunked
Cookie: id=l2RL1Cn2nq7Ry7c26h8D3g==
Accept: application/json
Content-Type: application/json
charset: utf-8

UP: 5 of 0 DOWN: 0 of 0
UP: 5 of 0 DOWN: 0 of 0
* Signaling end of chunked upload via terminating chunk.
< HTTP/1.1 202 Accepted
< Server: nginx
< Date: Fri, 17 Oct 2025 16:42:34 GMT
< Content-Length: 0
< Connection: keep-alive
< X-Frame-Options: SAMEORIGIN
< X-Content-Type-Options: nosniff
UP: 5 of 0 DOWN: 0 of 0
< X-XSS-Protection: 1; mode=block
UP: 5 of 0 DOWN: 0 of 0
UP: 5 of 0 DOWN: 0 of 0
UP: 5 of 0 DOWN: 0 of 0
< Strict-Transport-Security: max-age=31536000; includeSubdomains;
< Content-Security-Policy: script-src 'self' 'unsafe-inline'; object-src 'none'; font-src *; media-src 'none'; form-action 'self';
<
* Connection #0 to host 172.29.20.1 left intact
switch_err_inj_point: Injection ID 8 is for switch 1 target object -1 is not active. Skipping...
2025-10-17 16:42:34,503 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 1, overall_status: 0, ser_num: TW32KM304S
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
LWS_CALLBACK_CLIENT_CLOSED, subscription is 0 switch 1
Retry connection for switch 1
switchd_hb_monitor: hb final status is 0
LWS_CALLBACK_CLIENT_HTTP_BIND_PROTOCOL
switchd_monitor_thread: starting switchd_monitor_thread
curl_easy_perform() error with status: Timeout was reached
switchd_hb_monitor: heartbeat start for switch idx 1
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 1 conn idx 0 conn status 0
switch_installed: switch idx 1 conn idx 1 conn status 0
CLIENT_CONNECTION_ERROR: Unable to connect, Subscription is 0
Retry connection for switch 1
LWS_CALLBACK_CLIENT_HTTP_DROP_PROTOCOL_ERROR: __lws_close_free_wsi
Retry connection for switch 1
Go to clean for switch 1 on node 0
clean done for switch 1 on node 0
curl_easy_perform() retry status: Timeout was reached
curler: Error! Curl GET info failed: Timeout was reached IP: 172.29.20.1 conn idx 0 httpcode: 0 url: https://172.29.20.1/rest/v10.12/system/interfaces?attributes=admin_state&depth=2 cpath: /var/tmp/switch_cookies/cookiesD_SW1_172.29.20.1.txt switch_idx: 1
curler_verify: Error! All curler retries failed. switch_idx: 1 local_http_code 0 ret: 1 url_substr: /rest/v10.12/system/interfaces?attributes=admin_state&depth=2
switchd_rest_get_admin_state: Error! switch id: 1 failure in curler
switchd_monitor_thread: try 4 for switch 1
switchd_monitor_thread: starting switchd_monitor_thread
switchd_monitor_thread: starting switchd_monitor_thread

connection to IP failed after 0 tries: 172.29.20.1: 114 (Operation already in progress)
set_comm_degraded_state: switch idx 1, status SWITCH_COMM_DEGRADED
reset_curr_conn: switch idx 1 new curr connection idx 1, conn IP 16.1.8.250 old connection 0
switchd_hb_monitor: hb final status is 1
switchd_hb_monitor: heartbeat start for switch idx 2
2025-10-17 16:43:02,787 379[444] I switchd_event_agent_helper_c_wrapper.cc:786:EMIT_SW_PING_FAIL_EVENT Switch SW1 is offline, skipping event
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
2025-10-17 16:43:04,705 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:43:04,811 379[454] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:43:04,925 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_monitor_thread: Woke up! number of clients 1
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:43:05,050 379[454] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:43:05,904 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:43:06,087 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:43:06,349 379[454] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:43:06,769 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:43:07,511 379[454] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_monitor_thread: starting switchd_monitor_thread
2025-10-17 16:43:08,894 379[454] I switchd_service.cc:144:ListSwitches API ListSwitch requested
switchd_hb_monitor: heartbeat start for switch idx 1
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
Switch 1 is not healthy. Status 3 Skip.
2025-10-17 16:43:12,166 379[454] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
2025-10-17 16:43:17,395 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:43:18,908 379[454] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:43:19,011 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:43:19,106 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
2025-10-17 16:43:27,737 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 3 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
switch_installed: switch idx 1 conn idx 0 conn status 1
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens2f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens2f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens2f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens2f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens2f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
switch_installed: switch idx 1 conn idx 1 conn status 1
2025-10-17 16:43:59,521 379[444] I switchd_event_agent_helper_c_wrapper.cc:567:EMIT_SW_NOT_PRESENT_EVENT Switch SW1 is offline, skipping event
switchd_hb_monitor: out of hb, switch idx 1, status  SWITCH_NOT_PRESENT
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
2025-10-17 16:44:09,466 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 4 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
Switch 1 is not healthy. Status 4 Skip.
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
callback_switch_events: case LWS_CALLBACK_CLIENT_WRITEABLE switch 2
2025-10-17 16:44:18,908 379[454] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 4 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:44:19,012 379[454] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 4 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:44:19,107 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 4 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
switch_installed: switch idx 1 conn idx 0 conn status 1
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens2f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens2f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens2f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens2f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens2f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

2025-10-17 16:44:52,711 379[447] I k8_evtagent.cc:768:PrintMetrics Event Agent metrics: [queued: 315, processed: 315, duplicates: 0, recorded: 315, total record latency (us): 60010778, avg record latency (us): 190510, patched: 0, total patch latency (us): 0, avg patch latency (us): 0, check alarms: 0, total check alarm latency (us): 0, avg check alarm latency (us): 0]
switchd_monitor_thread: starting switchd_monitor_thread
switch_installed: switch idx 1 conn idx 1 conn status 1
switchd_hb_monitor: out of hb, switch idx 1, status  SWITCH_NOT_PRESENT
switchd_hb_monitor: heartbeat start for switch idx 2
2025-10-17 16:44:56,284 379[444] I switchd_event_agent_helper_c_wrapper.cc:567:EMIT_SW_NOT_PRESENT_EVENT Switch SW1 is offline, skipping event
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

Switch 1 is not healthy. Status 4 Skip.
switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

2025-10-17 16:45:18,909 379[454] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 4 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:45:19,015 379[453] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 4 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
2025-10-17 16:45:19,111 379[454] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 4 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
switchd_monitor_thread: starting switchd_monitor_thread
switch_installed: switch idx 1 conn idx 0 conn status 1
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens2f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
2025-10-17 16:45:31,635 379[454] I switchd_service.cc:144:ListSwitches API ListSwitch requested
Switch 1 is not healthy. Status 4 Skip.
switchd_show: Returned values Version: , switch_id: 1, overall_status: 3, ser_num:
, part_num: , ps0: , ps1: , fan_state:  led_state:  offline: 0
switchd_show: Returned values Version: GL.10.12.1000, switch_id: 2, overall_status: 0, ser_num: TW29KM3068
, part_num: JL636A, ps0: ok, ps1: ok, fan_state: ok led_state: off offline: 0
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens2f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens2f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens2f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens2f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------

switchd_monitor_thread: starting switchd_monitor_thread
switch_installed: switch idx 1 conn idx 1 conn status 1
2025-10-17 16:45:53,054 379[444] I switchd_event_agent_helper_c_wrapper.cc:567:EMIT_SW_NOT_PRESENT_EVENT Switch SW1 is offline, skipping event
switchd_hb_monitor: out of hb, switch idx 1, status  SWITCH_NOT_PRESENT
switchd_hb_monitor: heartbeat start for switch idx 2
switch_model_valid: Aruba_JL636A_GL.10.12.1000_ model is valid
switch_installed: switch idx 2 conn idx 0 conn status 0
switch_installed: switch idx 2 conn idx 1 conn status 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: hb final status is 0
switchd_monitor_thread: starting switchd_monitor_thread
switchd_hb_monitor: heartbeat start for switch idx 1
check_switch: Error! Failed to find switch 1 cmd [ -f /usr/sbin/lldpcli ] && /usr/sbin/lldpcli show neighbors ports ens1f0np0 details 2>&1 length: 176 lldp output:
 -------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------
```