**To Do:**
- Update fleetOS release on artifactory
- Old URL
	- [https://artifactory.eng.nimblestorage.com/artifactory/testrepo/home-fleet/pl2/FleetOS.pl2-0.1.4586f64c93d.1670879040.tar.gz](https://artifactory.eng.nimblestorage.com/artifactory/testrepo/home-fleet/pl2/FleetOS.pl2-0.1.4586f64c93d.1670879040.tar.gz)
- New URL
	- [https://artifactory.eng.nimblestorage.com:443/artifactory/testrepo/home-fleet/pl2/FleetOS.pl2-0.1.57461128493.1673990034.tar.gz](https://artifactory.eng.nimblestorage.com:443/artifactory/testrepo/home-fleet/pl2/FleetOS.pl2-0.1.57461128493.1673990034.tar.gz)

**Questions**:
- Where will addRelease be called from at a top level?
- Remove lir-exp after lir-svc complete?

lir/lir-svc/internal/rpc/server.go

process release will act as the backbone of lir-svc APIs

will need to start the async process of downloading and processing the release.

must be in a thread
goroutines for this

Channels provide a convenient, typed way to send and receive messages with the operator <-. Its usage is

Use for passing the status back without exiting

Automated tests:
- lir-dr Push test
- lir-f copy test
- add release validate input - daniel
- get status test -daniel

./build -t thf
docker save docker.artifactory.eng.nimblestorage.com/fleetos/lir/lir-svc:thf > lir-svc.tar
update lir-svc.yaml to use new container image lir-svc:thf
../../tools/add-container-to-lir 172.19.0.101 lir-svc.tar lir/lir-svc:thf
on hfsim node kubctl apply -f lir-svc.yaml

on lir-svc pod:

tar -xvf /root/grpcurl_1.8.7_linux_x86_64.tar.gz -C /usr/local/bin/

grpcurl -d '{"release_id":"https://artifactory.eng.nimblestorage.com:443/artifactory/testrepo/home-fleet/pl2/FleetOS.pl2-0.1.57461128493.1673990034.tar.gz", "release_version":"pl2-0.1"}' -plaintext lir-svc.default.svc.cluster.local:80 lir.Service/AddRelease

grpcurl -plaintext lir-svc.default.svc.cluster.local:80 lir.Service/GetStatus

update lir install to use recent build

can also build an lir-svc image then use docker push to push it. then uncomment image in lir-svc.yaml

downloaded successfully even though failed

change lir-svc build script
vim build
REGISTRY="docker.artifactory.eng.nimblestorage.com/private/feist/"
./build -t thf

push new container image to location in docker artifactory that can be modified
docker push docker.artifactory.eng.nimblestorage.com/private/feist/lir/lir-svc:thf

update preload container commands in hf_setup_k8scluster_pl2
vim hf_setup_k8scluster_pl2
"/usr/local/bin/ctr -n k8s.io i pull docker.artifactory.eng.nimblestorage.com/private/feist/lir/lir-svc:thf && /usr/local/bin/ctr -n k8s.io i convert docker.artifactory.eng.nimblestorage.com/private/feist/lir/lir-svc:thf localhost:31320/lir/lir-svc:pl2-0.2 & "