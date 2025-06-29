**Operator Setup Steps**
- Note: Had to setup proxy for docker host in order to get these steps to work
1. Setup golang on VDT8
	1. GOPATH is setup to be /data/workspace/feist/go
2. Install kubebuilder
	1. sudo su -
	2. cd /usr/local/bin
	3. curl -L -o kubebuilder [https://go.kubebuilder.io/dl/latest/$(go](https://go.kubebuilder.io/dl/latest/$(go) env GOOS)/$(go env GOARCH)
	4. chmod +x kubebuilder
3. Initialize go module and kubebuilder
	1. go mod init helloOperator
	2. kubebuilder init --domain docker.artifactory.eng.nimblestorage.com repo=helloOperator
4. Create API
	1. kubebuilder create api --group k8sim --version v1alpha1 --kind HelloOperator (kind must start with uppercase character)
		1. Press y to accept creation of controller and resource
	2. Make changes to api
	3. Make manifests
5. Test CRD
	1. Start local cluster
	2. Make install
	3. Make run (runs in foreground)
6. Install instances of custom resources
	1. kubectl apply -f config/samples/
6. Run on cluster
	1. make docker-build docker-push 
		1. IMG=docker.artifactory.eng.nimblestorage.com/hello-operator:latest
		2. Ensure docker host has env proxy settings
	2. Remove ./bin/kustomize
	3. make deploy IMG=docker.artifactory.eng.nimblestorage.com/hello-operator:latest

**The Stack:**
Management Cluster W CAPI
Worker Cluster with switchd Operator and switchd server
- Are these on the same cluster?
Aruba 8325 Switch

In a typical Kubernetes cluster, a controller manager runs controllers in a reconciliation loop in the control plane. Each controller is responsible for managing a specific part of the cluster's behavior. An operator can add multiple controllers to the control plane's reconciliation loop

Cluster manages switchd and switchd manages the switch itself

<service-name>.<namespace>.svc.cluster.local:<service-port>