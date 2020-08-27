
## Basic Service Concepts

You can deploy various containers in a Kubernetes cluster. Some containers use HTTP or HTTPS to provide external Layer-7 network services, and the others use TCP or UDP to provide Layer-4 network services. Kubernetes defines service resources to manage Layer-4 network service access in a cluster.

Kubernetes `ServiceTypes` allows you to specify what kind of service you want. The default type is `ClusterIP`. `ServiceTypes` values and their behaviors are as follows:
* **ClusterIP**: exposes the service on a cluster-internal IP address. Choosing this value makes the service only reachable from within the cluster. This is the default `ServiceType`.
* **NodePort**: exposes the service on each node's IP address at a static port (NodePort). A `ClusterIP` service, to which the `NodePort` service routes, is automatically created. You can access the `NodePort` service from outside the cluster by requesting <NodeIP>:<NodePort>. Except in test and non-production environments, we do not recommend that cluster nodes provide external or even public network services. Typically, cluster nodes are dynamic and scalable. When this service type is used, cluster nodes are exposed and can be attacked easily, and the address and cluster node used to provide external services are coupled.
* **LoadBalancer**: the CLB provided by Tencent Cloud is used to expose the service to the Internet or a VPC. The CLB can be routed to the `NodePort` service or directly forwarded to a pod in a VPC-CNI network.

Services of the `ClusterIP` and `NodePort` types typically behave in the same way in clusters provided by different cloud providers or off-premises clusters. Services of the `LoadBalancer` type are exposed using the cloud provider's CLB and the service provider provides extra features related to the CLB, for example, controlling the CLB network type and adjusting weights of bound backend nodes. For more information, please see documents related to service management.



## Service Access

The following table describes four service access modes that TKE provides based on `ServiceTypes` definition.

<table>
<thead>
<tr>
<th style="
    width: 5%;
">Access Method</th>
<th style="
    width: 15%;
">Service Type</th>
<th style="
    "width": "80%",
">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Via Internet</td>
<td>LoadBalancer</td>
<td><ul class="params"><li>A service of the Loadbalancer type is used, and public IP addresses can access backend pods. This access method applies to web frontend services.</li><li>After a service of this type is created, you can use <strong>CLB domain name or IP address + Service port</strong> to access the service from outside the cluster and use <strong>Service name + Service port</strong> to access the service from inside the cluster.</li></ul></td>
</tr>
<tr>
<td>Via VPC<br></td>
<td>LoadBalancer</td>
<td><ul class="params"><li>A service of the Loadbalancer type is used. With the <code>service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxxxx</code> annotation, you can use a VPC IP address to access backend pods.</li><li>After a service of this type is created, you can use <strong>CLB domain name or IP address + Service port</strong> to access the service from outside the cluster and use <strong>Service name + Service port</strong> to access the service from inside the cluster.</li></ul></td>
</tr>
<tr>
<td>Node Port Access</td>
<td>NodePort</td>
<td><ul class="params"><li>This access method maps node ports to pods and supports TCP and UDP. A service can customize the upper-layer CLB to access pods through these node ports.</li><li>After a service of this type is created, you can use <strong>CVM IP address + Node port</strong> to access the service.</li></ul></td>
</tr>
<tr>
<td>Intra-cluster</td>
<td>ClusterIP</td>
<td><ul class="params"><li>A service of the ClusterIP type is used, and IP addresses in the service IP range are automatically assigned for intra-cluster access. You can select this access method for database services, such as MySQL, to isolate service networks.</li><li>After a service of this type is created, you can use <strong>Service name + Service port</strong> to access the service.</li></ul></td>
</tr>
</tbody></table>


## CLB-related Concepts

### Service principles
The `Service Controller` component in a TKE cluster synchronizes users' service resources when a service is created, modified, or deleted, a cluster node or service endpoint is changed, or a pod is shifted or restarted.

`Service Controller` will create CLB resources and configure listeners and backend nodes based on the service resource description. When you delete cluster service resources, `Service Controller` will reclaim the corresponding CLB resources.

### Service lifecycle management
The external service capabilities of a service depend on resources provided by the CLB. Service resource management is one of the important tasks of a service. A service will use the following labels in resource lifecycle management:

* `tke-createdBy-flag = yes`: identifies that the resource was created by TKE.
 * With this label, the resource is deleted when the service is destroyed.
 * Without this label, only listener resources in the CLB will be deleted and the CLB will not be deleted when the service is destroyed.
* `tke-clusterId = <ClusterId>`: identifies the cluster that uses the resource.
 * If ClusterId is correct, the corresponding label will be deleted when the service is destroyed.

> If you use an existing CLB for a service, the service will only use the CLB and will not delete the CLB.
>

When a service of the `LoadBalancer` type is created, the corresponding CLB lifecycle starts. The CLB lifecycle ends only when the service is deleted or the CLB is rebuilt. In the CLB lifecycle, the CLB is synchronized based on the service description. **When you change the service access mode, for example, from Via Internet to Via VPC or from Via VPC to Via Internet or VPC subnet switching or change to use an existing CLB for the service, the CLB will be rebuilt or destroyed.**
The following figure shows the working principles of a service of the `LoadBalancer` type.
![image.png](https://main.qcloudimg.com/raw/de1a453250a111505a7dccdfd3dade85.png)


### High-risk service operations

1. Use a traditional CLB (no recommended)
2. Modify or delete a CLB label added by TKE, and then purchase a new CLB to restore the CLB label.
3. Modify the name of a CLB listener managed by TKE in the CLB console.

### Service features
The following lists service-related operations and features. For more information, see the corresponding documents.
* Basic features
* CLB configuration
* Using existing CLBs
* Backend selection

## Reference
For more information about services, see [Kubernetes Service](https://kubernetes.io/en/docs/concepts/services-networking/service/). 

<style>
.params{margin:0px !important}
</style>
