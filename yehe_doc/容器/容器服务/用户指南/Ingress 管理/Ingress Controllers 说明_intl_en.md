
## Ingress Controllers

### Application CLB
Application CLB is a TKE Ingress Controller based on the Tencent Cloud Load Balancer (CLB), which can implement the access of different services in the cluster with different URLs. CLB directly forwards the traffic to the Pod through the NodePort (the traffic is forwarded to Pod in the CLB-to-Pod direct access mode). One Ingress configuration is bound to one CLB instance (IP), which is suitable for scenarios that only require simple routing management and are insensitive to IP address convergence. For more information, see [CLB Type Ingress](https://intl.cloud.tencent.com/document/product/457/37013).

### Nginx Ingress Controller
Nginx Ingress Controller is an Ingress controller based on Tencent Cloud CLB and Nginx reverse proxy (containerized deployment in cluster). It extends the features of native Kubernetes Ingress through [Annotations](https://kubernetes.github.io/ingress-nginx/user-guide /nginx-configuration/annotations/), and adds a layer of proxy (nginx) after CLB, which is suitable for scenarios where there are more requirements for access layer routing management and IP address convergence. For more information, see [Nginx Type Ingress](https://intl.cloud.tencent.com/document/product/457/38980).



## Ingress Controllers Comparison



<table>
<thead>
<tr>
<th>Module</th>
<th>Feature</th>
<th>Application CLB</th>
<th>Nginx Ingress Controller</th>
</tr>
</thead>
<tbody><tr>
<th rowspan=5>Traffic management</th>
<td>Supported protocol</td>
<td>http, https</td>
<td>http, https, http2, grpc, tcp, udp</td>
</tr>
<tr>
<td>IP management</td>
<td>One Ingress rule corresponds to one IP (CLB)</td>
<td>Multiple Ingress rules correspond to one IP (CLB). IP address convergence is supported.</td>
</tr>
<tr>
<td>Attribute route</td>
<td>host, URL</td>
<td>More attributes are supported such as header, cookie.</td>
</tr>
<tr>
<td>Traffic behavior</td>
<td>Unsupported</td>
<td>Rewrite, redirection, etc. are supported.</td>
</tr>
<tr>
<td>Region-aware load balancing</td>
<td>Unsupported</td>
<td>Unsupported</td>
</tr>
<tr>
<th>Application access addressing</th>
<td>Service discovery</td>
<td>Single Kubernetes cluster</td>
<td>Single Kubernetes cluster</td>
</tr>
<tr>
<th rowspan=2>Security</th>
<td>SSL configuration</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Authentication authorization</td>
<td>Unsupported</td>
<td>Supported</td>
</tr>
<tr>
<th rowspan=3>Observability</th>
<td>Monitoring metrics</td>
<td>Supported. View in CLB.</td>
<td>Supported. View in cloud native monitoring.</td>
</tr>
<tr>
<td>Call tracking</td>
<td>Unsupported</td>
<td>Unsupported</td></tr>
<tr>
<td>Add-on OPS</td>
<td>The associated CLB has been managed. You only need to run TKE Ingress Controller in the cluster.</td>
<td>You need to run Nginx Ingress Controller in the cluster (control plane + data plane).</td>
</tr>
</tbody></table>
