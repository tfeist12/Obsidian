## Build:

#### Local Options:

Build hfcluster
```bash
nb build hfcluster -v dbg
```
Build release squashfs
```bash
nb dist release -v dbg
```
Build release squashfs and iso
```bash
nb dist fleetos -v dbg
```
If you receive "Nothing to do, build skipped."
```bash
nb dist fleetos -v dbg --force-full 
```
#### Remote Options:

Cluster build of release squashfs and iso
```bash
nb dist release -v opt --cluster
```
## Get Commit:
#### Latest:
```shell
nb artifacts search -A fleetos-local -stg fleetos "*.iso" -br prj-fleetos-next -nw -ip --json | jq -r '.[0].rootdir_commit'
```
#### QA-Accept:
```shell
nb artifacts search -A fleetos-local -stg fleetos "*.iso" -br prj-fleetos-next -st qa-accept -nw -ip --json | jq -r '.[0].rootdir_commit'
```

## ISO Download:
#### Latest:
```bash
nb artifacts download -A fleetos-local -stg fleetos "*.iso" -br prj-fleetos-next -nw -ip -dt ~/tf-ws/fos-iso/latest/
```
#### QA-Accept:
```bash
nb artifacts download -A fleetos-local -stg fleetos "*.iso" -br prj-fleetos-next -b $(nb artifacts search -A fleetos-local -stg fleetos "*.iso" -br prj-fleetos -st qa-accept -nw -ip --json | jq -r '.[0].build_id') -nw -ip -dt ~/tf-ws/fos-iso/qa-accept/
```
## Full Install:
#### Local Build:

Start hfsim using latest locally built iso:
```bash
~/tf-ws/bin/hf-dev-tools/hf_setup_hfsim latest
```
Install latest locally built release:
```bash
~/tf-ws/bin/hf-dev-tools/hf_install --create latest && hf_config_hfsim_nodes
```

#### QA Accept Build:

Start hfsim using latest qa-accept iso:
```bash
~/tf-ws/bin/hf-dev-tools/hf_setup_hfsim prj-fleetos-next
```
You may need to set some environment variables:
```bash
source .hfsim
```
Install latest qa-accept build
```bash
~/tf-ws/bin/hf-dev-tools/hf_install --create prj-fleetos-next && hf_config_hfsim_nodes
```
#### Remote Build:

##### Using Manual Steps:
Start hfsim:
```bash
/usr/local/bin/hfcsh create --setup-module fleetos_setup_modules.virtual_rack --nodes 3 --jbof 1 --build $(nb artifacts search -A fleetos-local -stg fleetos -br $(git rev-parse --abbrev-ref HEAD) "*.iso" --json | jq -r '.[0].build')
```
Download latest cluster create script:
```bash
rm -rf ~/tf-ws/cluster-create/* && nb artifacts download -A fleetos-local -stg fleetos "homefleet_cluster_setup-*.py" -br $(git rev-parse --abbrev-ref HEAD) -nw -dt ~/tf-ws/cluster-create
```
Install latest qa-accept release :
```bash
source ~/python3.9/bin/activate && python3 ~/tf-ws/cluster-create/homefleet_cluster_setup-*.py --create-cluster --nodes 172.19.0.100,172.19.0.101,172.19.0.102 --release qa-accept
```
Or choose fos.squashfs artifact to install
```bash
source ~/python3.9/bin/activate && python3 ~/tf-ws/cluster-create/homefleet_cluster_setup-*.py --create-cluster --nodes 172.19.0.100,172.19.0.101,172.19.0.102 --release $(nb artifacts search -br $(git rev-parse --abbrev-ref HEAD) "fleetos*squashfs" --json | jq -r '.[0].url')
```
##### Using Dev Tools
Start hfsim:
```
~/tf-ws/bin/hf-dev-tools/hf_setup_hfsim $(nb artifacts search -A fleetos-local -stg fleetos -br $(git rev-parse --abbrev-ref HEAD) "*.iso" --json | jq -r '.[0].build')
```
Install:
```bash
~/tf-ws/bin/hf-dev-tools/hf_install --create $(nb artifacts search -A fleetos-local -stg release -br $(git rev-parse --abbrev-ref HEAD) "*.squashfs" --json | jq -r '.[0].build') && hf_config_hfsim_nodes
```

## Update Cluster:
#### Download latest cluster setup script
```bash
rm ~/tf-ws/cluster-create/custom/* && nb artifacts download -A fleetos-local -stg fleetos "*.py" -br $(git rev-parse --abbrev-ref HEAD) -nw -dt ~/tf-ws/cluster-create/custom/
```
#### Update hfsim cluster
```bash
python3 ~/tf-ws/cluster-create/custom/homefleet_cluster_setup-*.py --update-cluster --cluster hfsim-rd-cluster.hfsim.nimblestorage.com --release <url> --softwareVersion <version>
```

## Update Individual Pod:
#### K9 Pods:
```bash
./build.sh -i THF-test
```
```bash
kubectl edit deployment -n cm lir-svc
```
#### Non K9 Pods:
```bash
nb build hfcluster -v dbg
```
```bash
docker build -f hfcluster/src/homefleet-cluster/deployment/Dockerfile --build-arg=http_proxy=$http_proxy  -t localhost:31320/homefleet/homefleet-cluster-thf:v0.0.1  hfcluster/build-dbg/services/homefleet-cluster
```
```bash
/auto/share.cxo/andersda/add-container-to-lir-skopeo --local 172.19.0.100 localhost:31320/homefleet/homefleet-cluster-thf:v0.0.1 homefleet/homefleet-cluster-thf:v0.0.1
```
```bash
kubectl edit pod -n homefleet-cluster  hpe-hfc-manager-operator-<uuid>
```

## Node Connect:
#### HFSim:
```
~/tf-ws/bin/hf-dev-tools/ssh-hfsim-node 0
```
or
```bash
ssh-keygen -R 172.19.0.100 && sshpass -p admin ssh root@172.19.0.100 -o StrictHostKeyChecking=no -t "export KUBECONFIG=/etc/kubernetes/admin.conf; bash"
```
#### Raider:
```bash
ssh root@cxo-array409-c1.lab.nimblestorage.com
```
#### Disable Auto-Logout:
```
sed -i.bak '/TMOUT=600/d' /etc/profile.d/fleetos-core-profile.sh
```

## Testing:
#### Local Go Unit Tests:

Build Test Binary:
```bash
go test -gcflags=all=-l -o <binary-name> <package-directory>
```

Serial Runs:
```bash
go test ./... -gcflags=all=-l -v
```
	or
```bash
go test ./... -gcflags=all=-l -coverprofile cover.out
```
	or
```bash
go test ./... -gcflags=all=-l -v -run <test-name> -count <x>
```

Parallel Runs:
```bash
lotsofTestRunsParallel 1000 ./ bin 2>&1 | tee test_log.txt
```
```bash
tail -f test_log.txt | grep "Failure on run"
```
```bash
truncate -s 0 test_log.txt
```

Build coverage html file and copy it to local machine for viewing:
```bash
go tool cover -html cover.out -o /tmp/coverage.html
```
```bash
scp vdt:/tmp/coverage.html . && explorer.exe coverage.html
```

#### Rodeo Test from VDT:
```bash
nb build -v dbg hfcluster -S fleetos.yml
```
```bash
nb rodeo hfcluster -S fleetos.yml -d -v dbg -- -o python_files=test_lir-svc.py -sv --log-level INFO
```
```bash
nb rodeo hfcluster -S fleetos.yml -d -v dbg -- lir-svc/test_lir-svc.py
```
```bash
nb rodeo hfcluster -S fleetos.yml -d -v dbg -- lir-svc/test_lir-svc.py::test_lirsvc_release
```

#### Rodeo Test from NB Container:
Build latest changes
```bash
nb build -v dbg hfcluster -S fleetos.yml
```
Enter the container and go to the test binary directory
```bash
nb container
```
```bash
cd hfcluster/build-all/tests
```
Run individual test or use lotsOftestRuns bash script
```bash
./lir-svc/lir-svc_release_test
```
	or
```bash
./lotsOfTestRuns 1000 ./lir-svc/lir-svc_release_test
```

#### GRPC Command Examples:
```bash
 ssh-keygen -R 172.19.0.102 && sshpass -p admin scp -o StrictHostKeyChecking=no /auto/share/bin/grpcurl root@172.19.0.102:/tmp/grpcurl
```
```bash
grpcurl -plaintext `kubectl -n cm get svc/lir-svc -o=jsonpath='{.spec.clusterIP}':80` list lir.Service
```
```bash
grpcurl -plaintext `kubectl -n cm get svc/lir-svc -o=jsonpath='{.spec.clusterIP}':80` lir.Service/GetStatus
```
```bash
grpcurl -d '{"release_version":"THF-Test-0"}' -plaintext `kubectl -n cm get svc/lir-svc -o=jsonpath='{.spec.clusterIP}':80` lir.Service.GetStatus
```
```bash
grpcurl -d '{"release_id":"'"$REL"'", "release_version":"THF-Test-0"}' -plaintext `kubectl -n cm get svc/lir-svc -o=jsonpath='{.spec.clusterIP}':80` lir.Service/AddRelease
```
```bash
grpcurl -d '{"release_version":"THF-Test-0"}' -plaintext `kubectl -n cm get svc/lir-svc -o=jsonpath='{.spec.clusterIP}':80` lir.Service/RemoveRelease
```
```bash
grpcurl -d '{"dst_pod_hostname":"<dst-lir-data-pod-ip(replace dots with dashes)>.lir-data.cm.svc"}' -plaintext <sending-lir-data-pod-ip>:1111 lir.RsyncService.Rsync
grpcurl -d '{"dst_pod_hostname":"172-26-122-52.lir-data.cm.svc"}' -plaintext 172.26.121.172:1111 lir.RsyncService.Rsync
```

#### Switch Util
```bash
kubectl exec svc/nvg-switchd-svc -- /opt/switchd/bin/nvg_switchd_util show switch
```

#### Trigger Switch Controller Rescan
From Node:
```bash
curl -X POST http://"$(kubectl -ncm get pods -owide | grep hpe-hfc-manager-operator | awk '{print $6}')":8090/rescanNeeded/switch/*
```
From Switchd P
```bash
curl -m 5 --silent --output /dev/null -X POST ${NVG_SWITCHD_CTRL_ENDPOINT}*
```

#### Get Zeus Build Number - Local Branch
ISO:
```bash
nb artifacts search -A fleetos-local -stg fleetos -br $(git rev-parse --abbrev-ref HEAD) "*.iso" --json | jq -r '.[0].name' | sed 's/.iso$//'
```
```
nb artifacts search -A fleetos-local -stg fleetos -br $(git rev-parse --abbrev-ref HEAD) "*.iso" --json | jq -r '.[0].name' | sed -e 's/^fleetos-//' -e 's/~git[0-9a-f]*//' -e 's/.iso$//'
```
Release:
```bash
nb artifacts search -A fleetos-local -stg release -br $(git rev-parse --abbrev-ref HEAD) "*.squashfs" --json | jq -r '.[0].name' | sed 's/.squashfs$//'
```
#### Get Zeus Build Number - QA Accept
```bash
nb artifacts search -A fleetos-local -stg fleetos "*.iso" -br prj-fleetos -st qa-accept -nw -ip --json | jq -r '.[0].name' | sed 's/.iso$//'
```
#### Host Release in NGINX Container
```bash
~/tf-ws/bin/hf/install/serve-local-release --start
```
## Debug:
#### Install Issues:
Check cluster status:
```bash
grpcurl -plaintext localhost:30030 cms.CmsService/GetClusterStatus
```
#### Get log times of a list of files:
```
find . | grep foo | while read line; do ~/tf-ws/bin/debug/logtimes $line; done
```

#### Helm Chart:
Manual Application
```bash
kubectl apply -f /var/opt/hpe/cms/lir-data.yaml --validate=false
```
## Clean Up:
#### Clean up docker containers and previous build artifacts
```bash
~/tf-ws/bin/hf-dev-tools/hf_make_space
```
#### Remove untracked git files
```bash
sudo git clean -fdx
```