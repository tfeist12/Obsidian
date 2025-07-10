Setup kubectl to control hfsim cluster from VDT:
- sudo vim /etc/hosts >add line> 172.19.0.100    kind-control-plane
- export no_proxy="kind-control-plane,$no_proxy"
- scp root@172.19.0.100:/etc/kubernetes/admin.conf ~/.kube
- mv ~/.kube/admin.conf ~/.kube/config
- export KUBECONFIG=~/.kube/config

Build and push mockswitchd image: (Likely to change later when Daniel updates dockerfile of mockswitchd) (Also not necessary if you just want to test running the image)
- git clone git@github.hpe.com:daniel-anderson/mockswitchd.git
- cd mockswitchd
- docker login -u feist docker.artifactory.eng.nimblestorage.com
- docker build -t docker.artifactory.eng.nimblestorage.com/k9/mockswitchd .
- docker push docker.artifactory.eng.nimblestorage.com/k9/mockswitchd

Run mockswitchd on control plane:
	VDT8:
	- scp mockswitchd/deployments/switchd.yaml root@kind-control-plane:/root/
	HFSim control plane:
	- Update controllers section of the yaml:
		image: docker.artifactory.eng.nimblestorage.com/k9/mockswitchd
		imagePullPolicy: IfNotPresent
	- kubectl apply -f /root/switchd.yaml

Install CRD, make switchdoperator image, and run it:
	On VDT8:
	- git clone git@github.hpe.com:tyler-feist/switchdoperator.git
	- cd switchdoperator
	- make install
	- kubectl apply -f config/samples/
	- make docker-build docker-push IMG=docker.artifactory.eng.nimblestorage.com/feist/switchdoperator:latest
	- make deploy IMG=docker.artifactory.eng.nimblestorage.com/feist/switchdoperator:latest

Setup test
	On VDT8 copy over crd yaml:
	- cd switchdoperator
	- scp config/samples/k8sim_v1alpha1_switchd.yaml root@kind-control-plane:/root/
	HFSim Control Plane:
	- kubectl describe switchd
	- Change desired spec of the yaml
		Switchledcolour: red
	- kubectl apply -f /root/k8sim_v1alpha1_switchd.yaml
	- Kubectl logs <podname> --namespace
	- kubectl describe switchd