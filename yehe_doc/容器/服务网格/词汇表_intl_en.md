### Mesh
A service mesh is a layer of infrastructure that is uncoupled from the service logic, and its core responsibility is to provide additional capabilities such as traffic management, observability enhancement, and security hardening for services in the mesh in a non-intrusive manner. In cloud-native scenarios, service applications in the service mesh are usually deployed in a containerized form.

### Istio

Istio is an open-source service mesh implementation project. Tencent Cloud Mesh is a service mesh product developed based on the Istio project.

### Envoy

Envoy is an open-source layer-7 proxy project. The Istio data plane is implemented on the basis of Envoy. For details about Envoy, see [Envoy](https://www.envoyproxy.io/docs/envoy/latest/intro/what_is_envoy).

### Sidecar

A sidecar adds control features for applications in a non-intrusive manner. In Istio, Envoy is deployed in a service pod as a sidecar container.

### Virtual Service
A virtual service defines a routing policy based on which traffic is forwarded. Each virtual service contains a set of routing rules. For example, traffic is forwarded to services of different versions based on different headers.

### Destination Rule

Similar to a virtual service, a destination rule is also a major part of Istio traffic management. The destination rule defines a processing policy after a service receives traffic.

### Gateway

In Istio, a gateway is an entry through which traffic flows into or out of a mesh. Gateways are classified into ingress gateways and egress gateways. With gateway policies, inbound and outbound traffic of the mesh can be controlled.

### Gateway

A gateway is a physical device of the gateway from which traffic flows into or out. Gateway rules are finally executed on the gateway. In Tencent Cloud Mesh, Tencent Cloud CLB functions as a gateway.

