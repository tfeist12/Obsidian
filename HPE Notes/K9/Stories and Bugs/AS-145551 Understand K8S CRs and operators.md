
[https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)
[https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/](https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/)

Operator = Custom Resource Definition (CRD) + Custom Controller

Kubernetes is good at managing stateless apps. Operators are used when you need more complex configuration details for stateful apps such as a database.

- An operator can also automate software configuration and maintenance activities that are typically performed by human operators
- Stateful apps save data to persistent disk storage for use by the server, clients, and other apps
- Is switchd stateful?

Why does k8s need operators

- Kubernetes needs operators to automate tasks that are normally performed manually by IT operations personnel. A stateful workload is more difficult to manage than a stateless workload. The state in a workload changes how a workload:

1. Is installed
2. Upgrades to a new version
3. Recovers from failures
4. Needs to be monitored
5. Scales out and back in again

- The operator takes care of everything that's needed to make sure the service keeps running successfully. An operator makes its service more self-managing, enabling an application team to spend less effort managing the service so that it can spend more effort using the service.

Operator Components

- A custom resource definition defines a schema of settings available for configuring a workload
- A custom resource is the Kubernetes API extension created by the CRD. A custom resource instance sets specific values for the settings defined by the CRD to describe the configuration of the workload
- A controller is customized for the workload and configures the current state of the workload to match the desired state that’s represented by the values in CR. Current state is reconciled to match desired state

What Do Operators do:

- In Kubernetes, controllers in the control plane run in a control loop that repeatedly compares the desired state of the cluster to the actual state. If they don’t match the controller takes action to adjust current state to more closely match the desired state.
- Controllers are run in a loop by the control plane. Some controllers are built into Kubernetes and are a part of the control plane. These are optimized for stateless workloads. Some are part of operators and optimized for a stateful workload. Each stateful workload has its own operator with its own controller that knows how to manage this workload.

Built using kubebuilder

- Operators are implemented in go, ansible, or helm
- The levels of maturity are:

1. Basic install
2. Upgrades
3. Lifecycle (app/storage + backup/failure recovery)
4. Insights (deep logging + metrics + analysis)
5. Autopilot (auto config tuning  + horizonal/vertical scaling)

If you press y for Create Resource [y/n] and for Create Controller [y/n] then this will create the files api/v1/guestbook_types.go where the API is defined and the controllers/guestbook_controller.go where the reconciliation business logic is implemented for this Kind(CRD).