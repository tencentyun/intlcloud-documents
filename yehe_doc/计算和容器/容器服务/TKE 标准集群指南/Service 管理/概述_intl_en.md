
## Basic Concepts of the Service 

You can deploy various containers in Kubernetes. Some of them provide layer-7 network services externally over HTTP or HTTPS, and others provide layer-4 network services over TCP or UDP. Service resources defined in Kubernetes are used to manage access to layer-4 network services in a cluster.

You can specify the Service type with Kubernetes `ServiceType`, which defaults to `ClusterIP`. `ServiceType` values and their behaviors are:
* **ClusterIP**: Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster. This is the default value of `ServiceType`.
* **NodePort**: Exposes the Service on each Node's IP at a static port (the `NodePort`). The `NodePort` Service will be routed to the `ClusterIP` Service that will be created automatically. It can be accessed from outside the cluster through the &lt;NodeIP&gt;:&lt;NodePort&gt; request. We recommend you not provide external and even public network services directly through cluster nodes in the production environment, as using `NodePort` will expose cluster nodes directly to attacks. Generally, cluster nodes are dynamic and can be added or removed, and using `NodePort` will couple them with addresses providing external services.
* **LoadBalancer**: Exposes the Service externally or privately by using a CLB instance. `LoadBalancer` can be routed to `NodePort` or directly forwarded to containers in the VPC-CNI network.

`ClusterIP` and `NodePort` Services usually behave in the same way in external clusters or those provided by cloud vendors. `LoadBalancer` Services are exposed by using a cloud vendor's load balancer and will have additional load balancer capabilities provided by the cloud vendor, for example, control of the network type of the load balancer and adjustment of weights of bound real servers. For more information, see [Service Management](https://www.tencentcloud.com/document/product/457/36831).



## Service Access Methods

You can use the following service access methods provided by TKE based on the above definition of `ServiceTypes`:

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
    width: 80%;
">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Public network</td>
<td>LoadBalancer</td>
<td><ul class="params"><li>In `Loadbalance` mode of the Service, public IPs can directly access backend Pods. This method is applicable to web frontend Services.</li><li>A created Service can be accessed from outside the cluster with the <strong>CLB instance domain name or IP + Service port</strong> or from within the cluster with the <strong>Service name + Service port</strong>.</li></ul></td>
</tr>
<tr>
<td>VPC<br></td>
<td>LoadBalancer</td>
<td><ul class="params"><li>In `Loadbalance` mode of the Service, private IPs can directly access backend Pods by specifying the <code>service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxxxx</code> annotation.</li><li>A created Service can be accessed from outside the cluster with the <strong>CLB instance domain name or IP + Service port</strong> or from within the cluster with the <strong>Service name + Service port</strong>.</li></ul></td>
</tr>
<tr>
<td>Access through the node port</td>
<td>NodePort</td>
<td><ul class="params"><li>This access method maps node ports to containers and is supported for TCP, UDP, and Ingress. It can be used for customizing upper-layer load balancer forwarding to nodes.</li><li>A created Service can be accessed with the <strong>CVM instance IP + node port</strong>.</li></ul></td>
</tr>
<tr>
<td>Access from within the cluster only</td>
<td>ClusterIP</td>
<td><ul class="params"><li>In `ClusterIP` mode of the Service, Service IPs are automatically assigned for access from within the cluster. This method can be used for database services such as MySQL, so as to ensure service network isolation.</li><li>A created Service can be accessed with the <strong>Service name + Service port</strong>.</li></ul></td>
</tr>
</tbody></table>


## CLB Concepts

### How a Service works
In a Tencent Cloud container cluster, the `Service Controller` add-on syncs your Service resources when you create, modify, or delete Service resources, cluster nodes or service endpoints change, or add-on containers drift or restart.

The `Service Controller` add-on will create CLB resources and configure listeners and real servers based on the description of the Service resource. When you delete the Service resource, it will repossess the CLB resources.

### Service lifecycle management
The external service capabilities of a Service rely on the resources provided by the CLB instance. Service resource management matters to a Service, which will use the following labels during the resource lifecycle management:

* `tke-createdBy-flag = yes`: Indicates that the resource is created by TKE.
 * If this label exists, the corresponding resource will be deleted when the Service is terminated.
 * If this label does not exist, only the listener resources in the CLB instance but not the CLB instance itself will be deleted when the Service is terminated.
* `tke-clusterId = <ClusterId>`: Identifies the cluster that uses the resource.
 * If the `ClusterId` is correct, the corresponding label will be deleted when the Service is terminated.

>?
>- If you use an existing CLB instance, the Service will only use but not delete the instance.
>- If you have enabled deletion protection for the CLB instance or use private connections, the instance will not be deleted when the Service is deleted.
>

When a Service of the `LoadBalancer` type is created, the lifecycle of the corresponding CLB instance starts; when the Service is deleted or the CLB instance is recreated, the lifecycle ends. During the lifecycle, the CLB instance will be continuously synced based on the description of the Service. **The CLB instance will be recreated or terminated if you switch the network for accessing the Service (public network > VPC, VPC > public network, or between VPC subnets) or replace the CLB instance**.
A Service of the `LoadBalancer` type works as follows:
![](https://main.qcloudimg.com/raw/de1a453250a111505a7dccdfd3dade85.png)


### High-risk operations on a Service

- Use a traditional CLB instance (not recommended).
-  Modify or delete a CLB instance label added by TKE, purchase a new CLB instance, and recover the label.
-  Rename a CLB listener managed by TKE in the CLB console.

### Service features
For more information on Service operations and features, see the following documents:
* [Basic Features](https://intl.cloud.tencent.com/document/product/457/36833)
* [Service CLB Configuration](https://intl.cloud.tencent.com/document/product/457/36834)
* [Using Existing CLBs](https://intl.cloud.tencent.com/document/product/457/36835)
* [Service Backend Selection](https://intl.cloud.tencent.com/document/product/457/36836)

## References
For more information, see [Service](https://kubernetes.io/zh/docs/concepts/services-networking/service/) on the Kubernetes website.  

<style>
.params{margin:0px !important}
</style>
