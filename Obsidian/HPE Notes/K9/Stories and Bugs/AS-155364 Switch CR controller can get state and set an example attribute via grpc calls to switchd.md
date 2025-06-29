**Notes/Questions:**
- is reconcile called on an individual switch object?
- Does switchd even need to be a service as we are querying etcd for the service address and the service handle? -> use etcd for now, perhaps change later.
- Should we be copying the proto api files for switchd and it's rpc wrapper from the nvgrid repo each time? -> no
- Should I cherry pick my updated crd commit?
- If I cherry pick a bunch of commits from the future what happens when I pull them in? Merge conflict?

**To Do:**
- Test service handle 0 with grpc dial using switchd svc address
- grpcurl testing

**People:**
- QA: Building python client: [arunkumar.arkali-suryaprakash@hpe.com](mailto:arunkumar.arkali-suryaprakash@hpe.com)
- NVGrid: Jeong Lee, Forrest Kerslager

**Protoc:**
```
export LD_LIBRARY_PATH=/auto/share/toolroots/latest-prj-fleetos/lib64
```
```
/auto/share/toolroots/latest-prj-fleetos/bin/protoc --go_out=. --go_opt=paths=source_relative --go-grpc_out=. --go-grpc_opt=paths=source_relative ./*.proto
```

**Local Build:**
```
cd hfcluster/src/release/
```
```
./build_all -t <identifier>
```
```
./hf_setup_k8scluster_pl2 --local --release <identifier>
```

**Switchd gRPC call Examples:
```
grpcurl -plaintext 172.19.0.103:34000 svcrpc.SvcRpcHandler.RpcCall
```
```
grpcurl -d '{"name":"Switchd", "service_handle":"1469626139541505"}' -plaintext 10.97.180.104:80 svcrpc.SvcRpcHandler.ListFunctions
```
```
grpcurl -d '{"client_req_handle":"1", "service_handle":"1469626139541505", "function_index":"1", "function_name":"ListSwitches", "ser_params":"", "service_name":"Switchd"}' -plaintext 10.97.180.104:80 svcrpc.SvcRpcHandler/RpcCall

```
**Update only the operator manager pod**
```
nb build hfcluster -S fleetos.yml -v dbg
```
```
docker build -f hfcluster/src/homefleet-cluster/deployment/Dockerfile --build-arg=http_proxy=$http_proxy -t localhost:31320/homefleet/homefleet-cluster-thf:v0.0.1 hfcluster/build-dbg/services/homefleet-cluster
```
```
/auto/share/k9/add-container-to-lir --local 172.19.0.101 localhost:31320/homefleet/homefleet-cluster-thf:v0.0.1
```
```
kubectl edit pod -n homefleet-cluster  hpe-hfc-manager-operator-<uuid>
```

**If nginx fails to serve release file to install:**
```
hfcluster/src/release/build_release_tgz -v dbg --start-nginx
```
```
docker rm <hash>
```
