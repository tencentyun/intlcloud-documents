## Multiple Containers in One Pod
### Advantages
**Resource sharing and communication**: a pod facilitates data sharing and communication between internal containers. Containers in the same pod use the same network namespace, IP address, and port range. They can discover and communicate with one another through the localhost. In a non-hierarchical shared network, each pod has an IP address that is used in its communications with other physical hosts and containers while the host name is the name of the pod in the communications between containers. Containers running in the same pod share the storage volume and space. Data stored in the volume will not be lost when a container restarts, and the data can be read by other containers in the same pod.

**Management**: compared with native container APIs, pods simplify the deployment and management of applications by providing abstraction at a higher level. A pod is a unit for management and horizontal deployment. It can automatically handle hosting, resource sharing, replication coordination, and dependency management.


### Common application scenarios
A pod can be used to construct a vertically integrated application stack. However, its main purpose is to centrally manage certain auxiliary programs, such as:
- Content management, processes for loading files and data, and processes for managing the local cache
- Log compression, rotation, backup, and snapshots
- Monitor and log data changes, monitor adapters, and event distribution
- Proxies, bridges, and adapters
- Control, management, configuration, and program upgrades

For more information, see the [application scenarios of pods](https://kubernetes.io/docs/concepts/workloads/pods/pod/).
