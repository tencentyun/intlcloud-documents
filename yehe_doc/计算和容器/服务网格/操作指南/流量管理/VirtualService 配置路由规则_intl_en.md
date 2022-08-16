VirtualService defines a set of routing rules and traffic operations (such as weighted routing and fault injection) for a specified host. Each routing rule defines a matching rule for traffic of a specified protocol. If the traffic is matched, it is routed to a specified service or a version of the service. VirtualService configurations mainly include the following parts:

- **hosts**: defines hosts associated with routing rules. The value can be a DNS name with a wildcard or an IP address.
- **gateways**: defines the source of traffic to which routing rules are to be applied. The source can be:
	- One or more gateways
	- Sidecars in a mesh
- **Routing rules**: defines detailed routing rules, including routing rules for three protocol types HTTP, TLS/HTTPS, and TCP.
	- http: defines an ordered list of routing rules for HTTP traffic.
	- tcp: defines an ordered list of routing rules for TCP traffic.
	- tls: defines an ordered list of routing rules for non-terminated TLS or HTTPS traffic.

## Description of Major VirtualService Fields

Major VirtualService fields are described as follows.

| Name | Type | Description |
| ----- | ---- | ----- |
| `spec.hosts` | `string[]`| A group of hosts associated with routing rules. The value can be a DNS name with a wildcard or an IP address (IP addresses are allowed only for traffic that comes from a gateway.). The hosts field applies to both HTTP and TCP traffic. In a Kubernetes environment, service short names can be used. If a short name is used, Istio will interpret the short name based on the namespace where the VirtualService locates. For example, a rule in the default namespace containing a host `reviews` will be interpreted as `reviews.default.svc.cluster.local`. To avoid misconfigurations, it is recommended to use the full name of the host. |
| `spec.gateways ` | `string[]` | Source of traffic to which routing rules are to be applied. The source can be one or multiple gateways, or sidecars in a mesh. The value is specified by `<gateway namespace>/<gateway name>`. The reserved word `mesh` is used to indicate all sidecars in the mesh. When this field is absent, it is set to `mesh` by default, indicating that the routing rules are applied to all sidecars in the mesh. |
| `spec.http` | `HTTPRoute[]` | An ordered list of routing rules for HTTP traffic (The first routing rule matching traffic is used.). HTTP routing rules will be applied to traffic over mesh service ports named `http-`, `http2-`, or `grpc-` and traffic over gateway ports using protocol `HTTP`, `HTTP2`, `GRPC`, or `TLS-Terminated-HTTPS`.  |
| `spec.http.match` | `HTTPMatchRequest[]` | A list of matching rules for a routing rule. All conditions in a single matching rule have AND semantics, while the matching rules in the list have OR semantics. |
| `spec.http.route` | `HTTPRouteDestination[]` | A list of forwarding destinations of a routing rule. An HTTP rule can either redirect or forward (default) traffic. The forwarding destination can be one or multiple services (service versions). Behaviors such as configuring weights or header operations are allowed. |
| `spec.http.redirect` | `HTTPRedirect` | Route redirection. An HTTP rule can either redirect or forward (default) traffic. If the `passthrough` option is specified in the rule, route and redirect will be ignored. The redirect primitive can be used to send an HTTP 301 redirect to a different URL or Authority. |
| `spec.http.rewrite` | `HTTPRewrite` | Rewrite HTTP URLs or Authority headers. Rewrite cannot be configured together with the redirect primitive. Rewrite will be performed before forwarding. |
| `spec.http.timeout` | [Duration](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#duration) | Timeout for HTTP requests. |
| `spec.http.retries` | `HTTPRetry` | Retry policy for HTTP requests. |
| `spec.http.fault` | `HTTPFaultInjection` | Fault injection policy to be applied on HTTP traffic. Note that the timeout or retry policy will not be enabled when fault injection is enabled. |
| `spec.http.mirror` | `Destination` | Mirror HTTP traffic to a another specified destination. Mirrored traffic is on a "best effort" basis where the sidecar or gateway will not wait for a response to traffic mirroring before returning the response from the original destination. Statistics will be generated for the mirrored destination. |
| `spec.http.mirrorPercent` | `uint32 ` | Percentage of the traffic to be mirrored. If this field is absent, all the traffic (100%) will be mirrored. The maximum value is 100. |
| `spec.http.corsPolicy` | `CorsPolicy` | Cross-Origin Resource Sharing (CORS) policy. For more details about CORS, see [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS). For description about Istio CORS policy configuration syntax, see [CorsPolicy](https://istio.io/latest/docs/reference/config/networking/virtual-service/#CorsPolicy). |
| `spec.http.headers` | `Headers` | Header operation rules, including updating, adding, and deleting request and response headers. |
| `spec.tcp` | `TCPRoute[]` | An ordered list of routing rules for TCP traffic (The first routing rule matching traffic is used.). TCP rules will be applied to any port that is not an HTTP or TLS port. |
| `spec.tcp.match` | `L4MatchAttributes[]` | A list of matching rules for a TCP routing rule. All conditions in a single matching rule have AND semantics, while the matching rules in the list have OR semantics. |
| `spec.tcp.route` | `RouteDestination[]`| Destination to which the TCP connection is forwarded to. |
| `spec.tls` | `TLSRoute[]` | An ordered list of routing rules for non-terminated TLS or HTTPS traffic (The first routing rule matching traffic is used.). TLS rules will be applied to traffic over mesh service ports named `https-` or `tls-`, traffic over unterminated gateway ports using `HTTPS` or `TLS`, and service entry ports using `HTTPS` or `TLS`. Note that traffic over `https-` or `tls-` ports without associated VirtualService will be treated as TCP traffic. |
| `spec.tls.match` | `TLSMatchAttributes[]` | A list of matching rules for a TLS routing rule. All conditions in a single matching rule have AND semantics, while the matching rules in the list have OR semantics. |
| `spec.tls.route` | `RouteDestination[]` | Destination to which the connection is forwarded to. |

## Configuring Routing Rules for Traffic (South-North) from a Gateway

VirtualServices can be configured by using the console UI or YAML editing. The following shows VirtualService configurations for routing traffic from a gateway to the service frontend. The relevant gateway configurations are as follows:

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: frontend-gw
  namespace: base
spec:
  servers:
    - port:
        number: 80
        name: http
        protocol: HTTP
      hosts:
        - '*'
  selector:
    app: istio-ingressgateway
    istio: ingressgateway
```

<dx-tabs>
::: YAML Configuration Example
```yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: frontend-vs
  namespace: base
spec:
  hosts:
    - '*'
  gateways:
    - base/frontend-gw # Enter the gateway mounted to the VirtualService in the format of {namespace}/{Gateway name}.
  http:
    - route:
        - destination:
            host: frontend.base.svc.cluster.local # Set the routing destination to the full name of the host of the frontend service.
```
:::
::: Console Configuration Example
![](https://qcloudimg.tencent-cloud.cn/raw/b40d686ee940f4185d8edf99dcb4ffde.png)
:::
</dx-tabs>



## Configuring Routing Rules for Traffic (East-West) from a Mesh

The following shows VirtualService configurations about routing rules for internal mesh traffic of accessing the product service host: `product.base.svc.cluster.local`: 50% of the traffic is routed to v1 and 50% of the traffic is routed to v2 (a canary release). The service versions of product are defined by the following DestinationRule:

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: product
  namespace: base
spec:
  host: product
  subsets:
    - name: v1
      labels:
        version: v1
    - name: v2
      labels:
        version: v2
```

<dx-tabs>
::: YAML Configuration Example
```
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: product-vs
  namespace: base
spec: # Default gateway parameters, indicating that the routing configurations are applied to traffic from sidecars in the mesh.
  hosts:
    - "product.base.svc.cluster.local" # The traffic of accessing the host is matched.
  http:
    - match:
        - uri:
            exact: /product
      route:
        - destination: # Configure the destination and weight.
            host: product.base.svc.cluster.local
            subset: v1
            port:
              number: 7000
          weight: 50
        - destination:
            host: product.base.svc.cluster.local
            subset: v2
            port:
              number: 7000
          weight: 50
```

:::
::: Console Configuration Example
![](https://qcloudimg.tencent-cloud.cn/raw/c9a117dec8811dd26c054fac5bf3e91c.png)
:::
</dx-tabs>

