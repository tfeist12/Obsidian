**Setup LIR-DR:**
cd lir-data
./setup-lir-data 172.19.0.100-104
export TOKEN=`curl -u admin:badmin --silent  https://localhost:31321/auth\?service="local.image.repository"\&scope="registry:catalog:*" | jq -r .access_token`
curl --oauth2-bearer $TOKEN  https://localhost:31320/v2/_catalog

**Setup LIR-EXP:**
cd ../lir-exp/deployment/
./build.sh pl2-0.1
../../tools/add-container-tarball-to-lir build/lir-exp.tar 172.19.0.100
scp lir-exp.yaml root@172.19.0.100:
kubectl apply -f lir-exp.yaml

**Testing LIR-EXP:**
hfctl exec lir-exp -it -- bash
skopeo  inspect --cert-dir /certs docker://lir-dr:5000/lir/lir-exp:pl2-0.1 --debug
export TOKEN=`curl -u admin:badmin --silent  https://lir-dr:5001/auth\?service="local.image.repository"\&scope="repository:lir/lir-exp:*" -k  | cut -c 18- | awk -F, '{print $1}' | sed -e s/\"//g`
skopeo  inspect --cert-dir /certs docker://lir-dr:5000/lir/lir-exp:pl2-0.1 --debug --registry-token $TOKEN
mkdir ~/foo/; skopeo --src-cert-dir /certs --src-registry-token $TOKEN --debug copy docker://lir-dr:5000/lir/lir-exp:pl2-0.1 dir:///root/foo/
skopeo list-tags --cert-dir /certs docker://lir-dr:5000/hexos-base --registry-token $TOKEN

**Debug:**
kubectl describe pod lir-exp
kubectl logs lir-exp -c lir-exp-dr-auth

**Login:**
skopeo login --cert-dir /certs lir-dr:5000 --username admin --password badmin

Only able to inspect and not copy without a valid token.
When doing copy but not specifying "--src-registry-token $TOKEN", copy appears to work fine


**To run the process_release go program:**
build process_release.go:
	go build process_release.go
copy binary to node: 
	scp process_release root@172.19.0.100:/root
copy binary to lir-exp: 
	kubectl cp root/process_release lir-exp:/root -c lir-exp
Open lir-exp pod:
	hfctl exec lir-exp -c lir-exp -it -- bash
set env var:
	export SSL_CERT_DIR="/certs"
run binary:
	./root/process_release -d test -u https://artifactory.eng.nimblestorage.com/artifactory/testrepo/home-fleet/pl2/FleetOS.pl2-0.1.4586f64c93d.1670879040.tar.gz
Check repos in lir-dr: 
	export TOKEN=`curl -k -u admin:badmin --silent  https://localhost:31321/auth\?service="local.image.repository"\&scope="registry:catalog:*" | jq -r .access_token`
	curl --silent -k --oauth2-bearer $TOKEN https://lir-data:5000/v2/_catalog | jq -S .

Goal: Essentially need to proxy from 32321 to lir-dr 5001
Option 3: setup a lir-dr-auth inside the lir-svc container listening on port 32321

registry and auth need to use same port number
disable autoredirect if setting up in lir-svc

deploy lir auth in lir-exp 32381

auth conf vol
certs vol
