Services expose TKE in clusters based on the layer-4 network. Exposed service types, such as ClusterIP, NodePort, or LoadBalancer are all based on the access entry of layer-4 network services. They lack Layer-7 network capabilities, such as load balancing, SSL, and name-based virtual hosts. An ingress exposes HTTP and HTTPS services in the layer-7 network and provides common layer-7 network capabilities.



## Basic Ingress Concepts
An ingress is a collection of rules that allows access to services within a cluster. You can configure forwarding rules to allow different URLs to access different services within the cluster. To ensure proper ingress operation, a cluster needs to run `Ingress Controller`. By default, a TKE cluster enables CLB-based `TKE Ingress Controller`.

## Ingress Lifecycle Management
The external service capability of an ingress depends on resources provided by the CLB. Service resource management is one of the important function of an ingress. The following table describes the labels that an ingress will use for resource lifecycle management.

<table>
<tr>
<th>Label</th><th>Description</th>
</tr>
<tr>
<td><code>tke-createdBy-flag = yes</code></td>
<td><ul class="params">
<li>Indicates that the resource was created by TKE. When an ingress with this label is deleted, the corresponding resources are also deleted.</li>
<li>When an ingress without this label is destroyed, only the CLB listener is deleted and the CLB will not be deleted.</li>
</td></td>
</tr>
<td><code>tke-clusterId = &lt;clusterId&gt;</code></td>
<td><ul class="params">
<li>Identifies the cluster that uses the resource.</li>
<li>When the ingress is deleted, the corresponding label (with correct ClusterId) will be deleted.</li>
</td></td>
</tr>
<td><code>tke-lb-ingress-uuid = &lt;Ingress UUID&gt;</code></td>
<td><ul class="params">
<li>Identifies the ingress that uses the resource.</li>
<li>Currently, an ingress cannot reuse a CLB with other ingresses. If you specify that an ingress use an existing CLB but the label value is incorrect, the request will be rejected.</li>
<li>When the ingress is deleted, the corresponding label (with correct ingress UUID) will also be deleted.</li>
</td></td>
</tr>
</table>



## Ingress Controller Usage Method
In addition to `TKE Ingress Controller` provided by Tencent Cloud, the Kubernetes community has various third-party `Ingress Controllers`. These ingress controllers expose services in the layer-7 network. The Kubernetes community allows you to use the `kubernetes.io/ingress.class` annotation to distinguish different ingress controllers and determine the controller that processes an ingress. `TKE Ingress Controller` also supports this annotation. The detailed rules and use suggestions are as follows:
- When an ingress does not have the `kubernetes.io/ingress.class` annotation, `TKE Ingress Controller` will manage the ingress.
- When an ingress has the `kubernetes.io/ingress.class` annotation and its value is `qcloud`, `TKE Ingress Controller` will manage the ingress.
- When an ingress modifies the `kubernetes.io/ingress.class` annotation content, `TKE Ingress Controller` will add the ingress to or remove it from its management scope based on the annotation content. This operation will create or release an ingress.
- When `TKE Ingress Controller` is not required, you can change the number of `Deployment` (`kube-system:l7-lb-controller`) replicas in the cluster to 0 to disable the `TKE Ingress Controller` feature.
>? Before disabling the `TKE Ingress Controller` feature, ensure that no ingress is managed by `TKE Ingress Controller` to prevent CLB release failures.
>


## Ingress Operations
For more information about ingress-related operations and features, see the following documents:
- [Ingress Management](https://intl.cloud.tencent.com/document/product/457/30673)
- [Using an Existing CLB for Direct Pod Connection](https://intl.cloud.tencent.com/document/product/457/37014)
- [Using TkeServiceConfig to Configure the CLB](https://intl.cloud.tencent.com/document/product/457/37015)
- [Ingress Certificate Management](https://intl.cloud.tencent.com/document/product/457/37016)

<style>
.params{margin:0px !important}
</style>
