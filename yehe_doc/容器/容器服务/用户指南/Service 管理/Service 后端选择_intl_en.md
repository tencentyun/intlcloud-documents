
## Default Backend Selection

By default, a Service configures the CLB backends to cluster node NodePorts, such as the TKE access-layer component in the figure below. This solution offers a very high level of fault tolerance. After traffic from the CLB reaches a NodePort, the NodePort will randomly select a pod to which the traffic will then be forwarded. This is also the most basic network access layer solution officially proposed by Kubernetes. See the figure below:
![A.png](https://main.qcloudimg.com/raw/de1a453250a111505a7dccdfd3dade85.png)

By default, `TKE Service Controller` will not set the following nodes as the CLB backend:
- Master nodes (master nodes are not allowed to participate in network access layer loads)
- Nodes in the status of NotReady or Unschedulable



## Specifying the Access-Layer Backend
For some clusters of a very large scale, the NodePorts of almost all cluster nodes are mounted on the Service-managed CLB as backends. In this scenario, there are the following issues:
- There is a quantity limit to the number of CLB backends.
- The CLB performs health checks on each NodePort, and all health check requests are routed to the backend workloads.

These issues can be resolved by using the following method:
For some large-scale clusters, you can use the annotation `service.kubernetes.io/qcloud-loadbalancer-backends-label` to specify some nodes for binding. The content of `service.kubernetes.io/qcloud-loadbalancer-backends-label` is a label selector. You can attach labels to cluster nodes. Then, the label selector described in the annotation is used in the Service to select matching nodes for binding. This synchronization will take place continuously. When a node changes and is selected or deselected, Service Controller will add or delete the corresponding backend on the CLB. For more information, see [Kubernetes Labels and Selector](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/).

### Precautions
- When the selector of `service.kubernetes.io/qcloud-loadbalancer-backends-label` fails to select any node, the service backend will be drained, leading to service interruption. When using this feature, you need to manage the labels of cluster nodes.
- Adding nodes that meet requirements or changing existing nodes will also trigger controller updates.

### Use cases
#### Application testing on a large–scale cluster
On a large-scale cluster, deploy a test application that contains only one or two pods. During service opening via a Service, the CLB will carry out health checks on all backend NodePorts, and the number of such health check requests has a huge impact on the test application. To avoid this, you can use labels to specify a small portion of nodes in the cluster as the backends to relieve the pressure of the health checks. For more information, see [Notes on High-Frequency Health Checks](https://intl.cloud.tencent.com/ko/document/product/214/38451).

## Sample
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
This sample includes the following configurations:
- It describes service opening by a public network CLB.
- The annotation `service.kubernetes.io/qcloud-loadbalancer-backends-label` specifies the backend selector. Only cluster nodes with the `group=access-layer` Label can be the backend of this CLB.




## Service Local Mode
Kubernetes provides the Service feature `ExternalTrafficPolicy`. When `ExternalTrafficPolicy` is set to Local, it can prevent traffic forwarding between nodes via NAT, thus reducing NAT operations and retaining source IP addresses. NodePort will forward traffic only to the pods of the current node. The features of Local mode are as follows:
* Advantages:
 1. It prevents the performance loss caused by NAT and inter-node forwarding.
  2. It retains the source IP addresses of requests for the server.
* Disadvantages:
  - NodePort cannot provide services to nodes without workloads.

### Precautions
CLB synchronization takes time. When the number of service workloads of the Local type is very small, the speed of workload drift or rolling update is very fast. Therefore, if the backend is not synchronized in time, backend services may become unavailable.


#### Sample: a Service enables Local forwarding (externalTrafficPolicy: Local)
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


### Default backend selection in Local mode
By default, when a Service enables Local mode, it will still adopt the default approach of mounting the NodePorts of almost all nodes as the backends. Based on health check results, the CLB will prevent traffic from entering backend nodes without workloads. To prevent backends without workloads from being bound, you can use the annotation `service.kubernetes.io/local-svc-only-bind-node-with-pod: "true"` to specify nodes bound with workloads as the backends in Local mode. For more information, see [Kubernetes Service Local](https://kubernetes.io/zh/docs/tutorials/services/source-ip/).

#### Sample: a Service enables Local forwarding and Local binding
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

In Local mode, request traffic will not be forwarded between nodes after entering a node. Therefore, when nodes have different quantities of workloads, the same backend weight will cause uneven loads on each node. You can use `service.cloud.tencent.com/local-svc-weighted-balance: "true"` to configure weighted balance. With this annotation, the NodePort backend weight will be determined by the number of workloads on the specific node. This prevents the issue of uneven loads caused by different quantities of workloads on different nodes. Note that **Local weighted balance and Local binding must be used at the same time**. A sample is as follows:

#### Sample: a Service enables Local forwarding, Local binding, and Local weighted balance
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


