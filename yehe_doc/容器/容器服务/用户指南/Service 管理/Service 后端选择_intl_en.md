
## Default Backend Selection

By default, a service will configure NodePorts of cluster nodes to serve as the CLB backend, as shown by the TKE access layer components in the following figure. This solution ensures high fault tolerance. When traffic is transmitted from the CLB to any NodePort, the NodePort selects a pod at random to which to forward the traffic. This solution is also the basic network access layer solution provided by Kubernetes.
![A.png](https://main.qcloudimg.com/raw/de1a453250a111505a7dccdfd3dade85.png)

By default, `TKE Service Controller` will not use the following nodes as the CLB backend:
- Master nodes (Master nodes are not allowed to participate in load balancing at the network access layer.)
- Nodes whose state is NotReady or nodes that are set to Unschedulable (unhealthy or unschedulable)



## Specifying the Backend for the Access Layer
In a large-scale cluster, a CLB managed by a service will mount NodePorts of almost all cluster nodes to use for the backend. This results in the following issues:
- The CLB backend quantity is limited.
- The CLB will check the health status of each NodePort, and all health check requests will be sent to backend workloads.

These issues can be solved using the following methods:
In large-scale clusters, you can use the `service.kubernetes.io/qcloud-loadbalancer-backends-label` annotation to specify some nodes to bind. `service.kubernetes.io/qcloud-loadbalancer-backends-label` specifies a label selector. You can label cluster nodes and use the label selector described by the annotation to select matching nodes to bind. When a node is selected or deselected due to changes, `Service Controller` will add or delete the corresponding CLB backend. For more information, see [Kubernetes Label and Label Selector](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).

### Note
- When the label selector specified by `service.kubernetes.io/qcloud-loadbalancer-backends-label` does not select any node, the service backend will be empty, causing a service interruption. To use this feature, you must manage cluster node labels.
- When you add nodes that meet requirements or change existing nodes, `Service Controller` will update the CLB backend.

### Use cases
#### Test application in a large-scale cluster
In a large-scale cluster, deploy a test application that contains only one or two pods. When a CLB is created using the service template, the CLB will check the health status of all backend NodePorts. The health check request quantity has a major impact on the test application. You can label a small number of cluster nodes for the backend to mitigate the health check pressure. For more information, please see [Notes on high-frequency health checks](https://intl.cloud.tencent.com/document/product/214/6097).

### Samples
```
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.kubernetes.io/qcloud-loadbalancer-backends-label: "group=access-layer"
  name: nginx-service
spec:
  ports:
    - name: 80-80-no
      port: 80
      protocol: TCP
      targetPort: 80
  selector:
    app: nginx
  type: LoadBalancer
```
This example contains the following configurations:
- It describes the service exposure of a public CLB.
- The `service.kubernetes.io/qcloud-loadbalancer-backends-label` annotation declares the backend selector. Only cluster nodes with the `group=access-layer` label will be used for the CLB backend.




## Service Local Mode
Kubernetes provides the service feature `ExternalTrafficPolicy`. When `ExternalTrafficPolicy` is set to Local, traffic will not be forwarded between nodes using NAT, which reduces NAT operations and retains the source IP addresses of requests. A NodePort will forward traffic only to pods of the current node. Local mode has the following advantages and disadvantages:
* Advantages:
 - Prevents performance loss due to traffic forwarding between nodes using NAT.
  2. Retains the source IP addresses of requests for servers.
* Disadvantages:
  - NodePorts cannot provide services to nodes without workloads.

### Note
The CLB requires time for synchronization. When a local service has few workloads, workload shifts or rolling updates are quick. If the backend fails to synchronize the update within the specified time, the backend service may become unavailable.


#### Example: enabling local forwarding (externalTrafficPolicy: Local) for a service
```
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  externalTrafficPolicy: Local
  ports:
    - name: 80-80-no
      port: 80
      protocol: TCP
      targetPort: 80
  selector:
    app: nginx
  type: LoadBalancer
```


### Default backend selection in local mode
When local mode is enabled for a service, the CLB will still mount NodePorts of almost all nodes to serve as the backend by default. The CLB will prevent traffic from being forwarded to backend nodes without workloads based on their health check results. To prevent backend nodes without workloads from being bound, you can use the `service.kubernetes.io/local-svc-only-bind-node-with-pod: "true"` annotation to bind nodes with workloads to serve as the backend in local mode. For more information, see [Kubernetes Service Local](https://kubernetes.io/docs/tutorials/services/source-ip/).

#### Example: enabling local forwarding and local binding for a service
```
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.kubernetes.io/local-svc-only-bind-node-with-pod: "true"
  name: nginx-service
spec:
  externalTrafficPolicy: Local
  ports:
    - name: 80-80-no
      port: 80
      protocol: TCP
      targetPort: 80
  selector:
    app: nginx
  type: LoadBalancer
```

In local mode, request traffic sent to nodes will not be forwarded between nodes. When nodes have different numbers of workloads, nodes with the same backend weight may have uneven loads. You can use the `service.cloud.tencent.com/local-svc-weighted-balance: "true"` annotation to adjust the weights of nodes. With this annotation, the NodePort backend weight is determined by the number of workloads on the node. This prevents uneven loads due to nodes with different numbers of workloads. **Local weight adjustment must be used with local binding.**
> If you need to use the local weight adjustment feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1).


#### Example: enabling local forwarding, local binding, and local weight adjustment for a service
```
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.kubernetes.io/local-svc-only-bind-node-with-pod: "true"
    service.cloud.tencent.com/local-svc-weighted-balance: "true"
  name: nginx-service
spec:
  externalTrafficPolicy: Local
  ports:
    - name: 80-80-no
      port: 80
      protocol: TCP
      targetPort: 80
  selector:
    app: nginx
  type: LoadBalancer
```


