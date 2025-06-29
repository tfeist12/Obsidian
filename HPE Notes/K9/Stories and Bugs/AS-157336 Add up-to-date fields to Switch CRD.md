**HFSim:**
scp root@172.19.0.101:/etc/kubernetes/admin.conf ~/.kube/config.hfsim
rm ~/.kube/config && ln -s ~/.kube/config.hfsim ~/.kube/config
export no_proxy="172.19.0.101,$no_proxy"

**Minikube:**
rm ~/.kube/config
ln -s ~/.kube/config.minikube ~/.kube/config
export no_proxy=$no_proxy,192.168.59.0/24,192.168.49.0/24,192.168.39.0/24
make
make install
make deploy

**Testing:**
kubectl apply -f deployment/sample_Switch_led_on.yaml
kubectl get switch -ojson
kubectl get switch switch-sample -ojsonpath='{.spec}'
cp config/crd/bases/sc.hpe.com_switches.yaml ../helm/homefleet-cluster/crds/homefleetswitches-crd.yaml

**FOS Install:**
scp root@172.19.0.100:/etc/kubernetes/admin.conf ~/.kube/config.hfsim &&
rm ~/.kube/config && ln -s ~/.kube/config.hfsim ~/.kube/config &&
export no_proxy="172.19.0.100,$no_proxy"