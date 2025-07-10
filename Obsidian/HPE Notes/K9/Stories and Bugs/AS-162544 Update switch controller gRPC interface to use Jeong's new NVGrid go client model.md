Switchd gRPC call Examples:
- grpcurl -plaintext 172.19.0.103:34000 list
- grpcurl -plaintext 172.19.0.103:34000 svcrpc.SvcRpcHandler.RpcCall
- grpcurl -d '{"name":"Switchd", "service_handle":"1469626139541505"}' -plaintext 10.97.180.104:80 svcrpc.SvcRpcHandler.ListFunctions
- grpcurl -d '{"client_req_handle":"1", "service_handle":"0", "function_index":"1", "function_name":"ListSwitches", "ser_params":"", "service_name":"Switchd"}' -plaintext 10.97.180.104:80 svcrpc.SvcRpcHandler/RpcCall

2023/07/31 21:35:55 Found a matching service: service_name=Switchd, node_uuid=7866139d-5978-453a-b532-4a9b8ec34a0f

2023/07/31 21:35:55 Server found. IP:Port=172.19.0.101:34000, service_handle=70695161692161

So Matt and I did some digging in svc_server_v2.cc to try and figure out where the IP the switchd service is being hosted at comes from. It appears that the address it uses comes from an interface specified by a local config file /tmp/nvgrid_config_local.txt. There is a function that gets the IP from the interface and then uses it to start up the grpc server. This is why we see the node IP hosting the grpc service and etcd contains this address. 

Can we make an interface that points to service IP and put it in config map/file (/tmp/nvgrid_config_local.txt)?

Service is hosting on node ip instead of pod ip

Kubernetes service is virtual so it's not pingable

Determined that DNS resolution is working (nvg-switchd-svc.default.svc.cluster.local -> IP addr) from within a pod but not from the node which is expected.

User "system:serviceaccount:homefleet-cluster:hpe-hfc-manager"