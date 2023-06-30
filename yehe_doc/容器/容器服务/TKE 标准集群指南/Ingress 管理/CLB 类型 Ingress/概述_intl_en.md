Services expose TKE in clusters based on the layer-4 network. Exposed service types, such as ClusterIP, NodePort, and LoadBalancer, are all based on the access entry of layer-4 network services. They lack layer-7 network capabilities, such as load balancing, SSL, and name-based virtual hosts. An Ingress exposes HTTP and HTTPS services in the layer-7 network and provides common layer-7 network capabilities.



## Basic Ingress Concepts
An Ingress is a collection of rules that allow access to services of a cluster. You can configure different forwarding rules to allow different URLs to access different services. To properly run Ingress resources, the cluster must run an Ingress controller. TKE enables the CLB-based TKE Ingress Controller by default in the cluster.

## Ingress Lifecycle Management
The external service capability of an Ingress depends on resources provided by the CLB. Service resource management is one of the important feature of an Ingress. The following table describes the labels that an Ingress will use for resource lifecycle management.

<table>
<tr>
<th>Label</th><th>Description</th>
</tr>
<tr>
<td><code>tke-createdBy-flag = yes</code></td>
<td><ul class="params">
<li>Indicates that the resource was created by TKE. When an Ingress with this label is deleted, the corresponding resources are also deleted.</li>
<li>When an Ingress without this label is destroyed, only the CLB listener is deleted and the CLB will not be deleted.</li>
</td></td>
</tr>
<td><code>tke-clusterId = &lt;clusterId&gt;</code></td>
<td><ul class="params">
<li>Identifies the cluster that uses the resource.</li>
<li>When the Ingress is deleted, the corresponding label (with correct ClusterId) will be deleted.</li>
</td></td>
</tr>
<td><code>tke-lb-ingress-uuid = &lt;Ingress UUID&gt;</code></td>
<td><ul class="params">
<li>Identifies the Ingress that uses the resource.</li>
<li>Currently, an Ingress cannot reuse a CLB with other Ingresses. If you specify that an Ingress use an existing CLB but the label value is incorrect, the request will be rejected.</li>
<li>When the Ingress is deleted, the corresponding label (with correct Ingress UUID) will be deleted.</li>
</td></td>
</tr>
</table>



## Ingress Controller Usage Method
In addition to TKE Ingress Controller provided by Tencent Cloud, the Kubernetes community has various third-party Ingress controllers. These Ingress controllers expose services in the layer-7 network. The Kubernetes community allows you to use the `kubernetes.io/ingress.class` annotation to distinguish different Ingress controllers and determine the controller that processes an ingress. TKE Ingress Controller also supports this annotation. The detailed rules and use suggestions are as follows:
- When an Ingress does not have the `kubernetes.io/ingress.class` annotation, TKE Ingress Controller will manage the Ingress.
- When an Ingress has the `kubernetes.io/ingress.class` annotation and its value is `qcloud`, TKE Ingress Controller will manage the Ingress.
- When an Ingress modifies the `kubernetes.io/ingress.class` annotation content, TKE Ingress Controller will add the Ingress to or remove it from its management scope based on the annotation content. This operation will create or release an Ingress.
- When TKE Ingress Controller is not required, you can change the number of `Deployment` (`kube-system:l7-lb-controller`) replicas in the cluster to 0 to disable the TKE Ingress Controller feature.
>? 
>- Before disabling the TKE Ingress Controller feature, ensure that no Ingress is managed by TKE Ingress Controller to prevent CLB release failures.
>- If **Deletion Protection** is enabled or a **private connection** is used for the CLB, the CLB will not be deleted when services are deleted.
>


## Ingress Operations
For more information about Ingress-related operations and features, see the following documents:
- [Basic Ingress Features](https://intl.cloud.tencent.com/document/product/457/30673)
- [Using an Existing CLB for Direct Pod Connection](https://intl.cloud.tencent.com/document/product/457/37014)
- [Using TKEServiceConfig to Configure CLBs](https://intl.cloud.tencent.com/document/product/457/37015)
- [Mixed Use of HTTP and HTTPS Protocols through Ingress](https://intl.cloud.tencent.com/document/product/457/43504) 
- [Ingress Certificate Configuration](https://intl.cloud.tencent.com/document/product/457/37016)

<style>
.params{margin:0px !important}
</style>



