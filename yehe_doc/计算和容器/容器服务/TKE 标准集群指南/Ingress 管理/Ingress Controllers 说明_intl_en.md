## Ingress Controllers

### Application CLB

Application CLB is a TKE Ingress Controller based on the Tencent Cloud Load Balancer (CLB), which can implement the access of different services in the cluster with different URLs. CLB directly forwards the traffic to the Pod through the NodePort (the traffic is forwarded to Pod in the CLB-to-Pod direct access mode). One Ingress configuration is bound to one CLB instance (IP), which is suitable for scenarios that only require simple routing management and are insensitive to IP address convergence. For more information, see [CLB Type Ingress](https://intl.cloud.tencent.com/document/product/457/37013).

### Istio Ingress Gateway

Istio Ingress Gateway is an Ingress Controller based on Tencent Cloud CLB and Istio Ingress Gateway (provided by Tencent Cloud TCM). The control plane and related supporting components are maintained by Tencent Cloud. You only need to deploy the containerized data plane that performs traffic forwarding in the cluster. You can use native Kubernetes Ingress or [Istio API](https://istio.io/latest/docs/concepts/traffic-management/) that provides more refined traffic management capabilities. A layer of proxy (envoy) is added after CLB, which is suitable for scenarios where there are more requirements for access layer routing management, IP address convergence, and entrance traffic management of cross-cluster and heterogeneous deployment service.

### Dedicated API Gateway

Dedicated API Gateway is a TKE Ingress Controller based on dedicated Tencent Cloud API Gateway instance. It is suitable for scenarios where multiple TKE clusters require a unified access layer or the access layer requires authentication and traffic throttling. It has the following strengths:
- API Gateway is directly connected to the Pods of the TKE cluster without any intermediate nodes.
- An API Gateway TKE tunnel can connect multiple TKE services at the same time, among which the traffic is distributed according to the weighted round robin algorithm.
- Advanced extended capabilities provided by API Gateway can be used, such as authentication, traffic throttling, grayscale traffic distribution, caching, and downgrade upon circuit breaking.
- Supported by the dedicated API Gateway instance, the underlying physical resources are exclusive to one user, with a stable performance and high SLA delivered.


### Nginx Ingress Controller

Nginx Ingress Controller is an Ingress controller based on Tencent Cloud CLB and Nginx reverse proxy (containerized deployment in cluster). It extends the features of native Kubernetes Ingress through [Annotations](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/), and adds a layer of proxy (nginx) after CLB, which is suitable for scenarios where there are more requirements for access layer routing management and IP address convergence. For more information, see [Nginx Type Ingress](https://intl.cloud.tencent.com/document/product/457/38980).

## Ingress Controllers Comparison

<table>
<thead>
<tr>
<th>Module</th>
<th>Feature</th>
<th>Application CLB</th>
<th>Istio Ingress Gateway (provided by Tencent Cloud TCM)</th>
<th>Dedicated API Gateway</th>
<th>Nginx Ingress Controller</th>
</tr>
</thead>
<tbody><tr>
<th rowspan=5>Traffic management</th>
<td>Supported protocol</td>
<td>http, https</td>
<td>http, https, http2, grpc, tcp, tcp+tls</td>
<td>http, https, http2, grpc</td>
<td>http, https, http2, grpc, tcp, udp</td>
</tr>
<tr>
<td>IP management</td>
<td>One Ingress rule corresponds to one IP (CLB)</td>
<td>Multiple Ingress rules correspond to one IP (CLB). IP address convergence is supported.</td>
<td>Multiple Ingress rules correspond to one IP (dedicated API Gateway). IP address convergence is supported.</td>
<td>Multiple Ingress rules correspond to one IP (CLB). IP address convergence is supported.</td>
</tr>
<tr>
<td>Attribute route</td>
<td>host, URL</td>
<td>More attributes are supported: header, method, query, parameter, etc.</td>
<td>More attributes are supported: header, method, query, parameter, etc.</td>
<td>More attributes are supported: header, cookie, etc.</td>
</tr>
<tr>
<td>Traffic behavior</td>
<td>Not supported</td>
<td>Rewrite, redirection, etc. are supported.</td>
<td>Redirection, custom request, custom response, etc. are supported.</td>
<td>Rewrite, redirection, etc. are supported.</td>
</tr>
<tr>
<td>Region-aware load balancing</td>
<td>Not supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<th>Application access addressing</th>
<td>Service discovery</td>
<td>Single Kubernetes cluster</td>
<td>Multiple Kubernetes clusters + heterogeneous service</td>
<td>Multiple Kubernetes clusters</td>
<td>Single Kubernetes cluster</td>
</tr>
<tr>
<th rowspan=2>Security</th>
<td>SSL configuration</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Authentication authorization</td>
<td>Not supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<th rowspan=3>Observability</th>
<td>Monitoring metrics</td>
<td>Supported. View in CLB.</td>
<td>Supported. (Cloud native monitoring or Cloud Monitor)</td>
<td>Supported. View in API Gateway.</td>
<td>Supported. (Cloud native monitoring)</td>
</tr>
<tr>
<td>Call tracking</td>
<td>Not supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<td>Add-on OPS</td>
<td>The associated CLB has been managed. You only need to run TKE Ingress Controller in the cluster.</td>
<td>The control plane has been managed. You only need to run the data plane Ingress Gateway.</td>
<td>You don't need to run the control plane in the Kubernetes cluster; instead, simply enable the private network access feature in the cluster.</td>
<td>You need to run Nginx Ingress Controller in the cluster (control plane + data plane).</td>
</tr>
</tbody></table>
