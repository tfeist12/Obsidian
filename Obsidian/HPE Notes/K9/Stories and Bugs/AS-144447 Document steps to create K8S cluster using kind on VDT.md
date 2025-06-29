Kind Installation:
- sudo su -
- cd /usr/local/bin (should we try /auto/share/bin?)
- curl -Lo ./kind [https://kind.sigs.k8s.io/dl/v0.13.0/kind-linux-amd64](https://kind.sigs.k8s.io/dl/v0.13.0/kind-linux-amd64)
- chmod +x ./kind
- exit

Build custom debian base image:
- cd /data/workspace
- git clone [https://github.com/kubernetes-sigs/kind.git](https://github.com/kubernetes-sigs/kind.git)
- git clone [https://github.com/kubernetes/kubernetes.git](https://github.com/kubernetes/kubernetes.git)
- mkdir -p $HOME/go/src/[k8s.io](http://k8s.io/)
- ln -s /data/workspace/kubernetes $HOME/go/src/[k8s.io/kubernetes](http://k8s.io/kubernetes)
- cd /data/workspace/kubernetes
- build/run.sh make
- patch -p1 < hf-kind.diff
- cd /data/workspace/kind/images/base
- DOCKER_BUILDKIT=1 docker build --build-arg HTTP_PROXY=http_proxy --build-arg HTTPS_PROXY=http_proxy --build-arg NO_PROXY="no_proxy" --build-arg http_proxy=http_proxy --build-arg https_proxy=http_proxy --build-arg no_proxy="no_proxy" -t luan-kind/base -f Dockerfile .

Create Kind Cluster (only control plane):
- kind create cluster --image [docker.artifactory.eng.nimblestorage.com/luan/kind/node:deb1.0](http://docker.artifactory.eng.nimblestorage.com/luan/kind/node:deb1.0)

Create Kind Cluster with multinode config:
-  vim cluster config

```
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
- role: worker
```
- kind create cluster --image [docker.artifactory.eng.nimblestorage.com/luan/kind/node:deb1.0](http://docker.artifactory.eng.nimblestorage.com/luan/kind/node:deb1.0)

Nginx Deployment:
- docker exec -it kind-control-plane bash
- kubectl create deployment nginx --image=nginx
- kubectl create service nodeport nginx --tcp=80:80
- kubectl get nodes -> get port of nodeport node
- curl kind-worker:30991