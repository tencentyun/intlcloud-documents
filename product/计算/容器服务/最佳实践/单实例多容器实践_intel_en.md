## One Pod with Multiple Containers

### Advantages of Using One Pod with Multiple Containers

**Resource sharing and communication**: Place containers in the same pod can implement easier data sharing and communication. Containers in the same Pod use the same network namespace, IP address, and port range. They can discover and communicate with each other through localhost. In a non-hierarchical shared network, each Pod has an IP address used for communicating with other physical nodes and containers. The name of the Pod is used as the host name when the container communicates. Containers running in the same Pod share the same storage volume. The data stored in the volume will not be lost when the container is restarted, and it can be read by other containers in the same Pod.

**Management**: In comparison to native container APIs, Pods simplify the deployment and management of applications by providing a higher level of abstraction. Pods are like a unit for management and horizontal deployment and management. Hosting, resource sharing, replication coordination, and dependency management can all be handled automatically.

### Common Application Scenarios for Single Pod with Multiple Containers

Pods can be used to construct a vertically-integrated application stack. However, their main purpose is to manage certain supportive programs in a centralized manner, such as:

- Content management, processes for loading files and data, processes for managing local cache, etc.
- Log compression, rotation, backup, snapshot, etc.
- Data change listening, log and monitor adapters, event distribution, etc.
- Proxies, network bridges, adapters, etc.
- Program control, management, configuration, upgrade, etc.

For more information, see [Uses of Pods](https://kubernetes.io/docs/concepts/workloads/pods/pod/)
