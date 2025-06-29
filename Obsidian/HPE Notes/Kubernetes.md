Pods
- Smallest unit of K8s and
- They are a layer of abstraction above containers
- One app per pod
- Each gets its own ip and gets reassigned if the pod dies and is recreated

Service
- Permanent ip
- Lifecyle of pods and services aren't connected
- Need external service to be accessible from the web (http//ip:port)
	- Need to use ingress to get secure protocol (https) with domain name

Volumes
- Normally if a pod goes down all data it stores goes with it
- Volumes are storage which is outside of the cluster

Stateful set
- Avoid data inconsistencies but can be a bit tedious
- Deployment for statless apps, statefulset for stateful apps/databases
- Databases are typically hosted outside of a cluster

ConfigMap
- External configuration of your application

Deployment Config:
- Kind in type of config being created (deployment, secret or configmap)
- Labels are additional identifiers to names
	- Not unique so multiple pods in a deployment can be identified using one label
	- Required for pods
- Selector/matchlabels are used to outline which pods are a part of a deployment
- Template is configuration of pod within the configuration of the deployment
	- Has own metadata and spec
	- Includes contains which can be used to decide image and listening  port
- Replicas are used to specified desired number of pods in a deployment

Service Config:
- Kept in same file as deployment
- Protocol can be configured, port is service port and targetport is same as the container port in the deployment config
- Selector is used to select pods to forward requests to
- Can specify nodePort as spec/type tpo create external service
- Can also add spec/nodePort which exposes the service on each Node's IP at a static port
	- Must be between 30000 and 32767