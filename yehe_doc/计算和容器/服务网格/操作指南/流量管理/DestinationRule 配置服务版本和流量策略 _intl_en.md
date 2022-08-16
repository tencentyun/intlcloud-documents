DestinationRule defines versions of a service and traffic policies for the service after routing has occurred. These rules include load balancing, connection pool size, and health check (to detect and evict unhealthy hosts from the load balancing backend).

## Description of Major DestinationRule Fields

Major DestinationRule fields are described as follows.

| Name | Type | Description |
| ----- | ---- | ----- |
| `spec.host` | `string` | Name of a service associated with DestinationRule configurations. The service can be a service automatically discovered (for example, a Kubernetes service) or a host declared by ServiceEntry. Rules defined in the DestinationRule for the service that does not exist in the preceding source will be ignored. |
| `spec.subsets` | `Subset[]` | Versions (subnets) of a service. Versions can be matched against endpoints of the service by label key-value pairs. Traffic policies can be overridden at subset level. |
| `spec.trafficPolicy` | `trafficPolicy` | Traffic policies (load balancing, connection pools, health check, and TLS policy). |
| `spec.trafficPolicy.loadBalancer` | - | Load balancer algorithms. The following algorithms are available: simple load balancer algorithms (such as round robin, least conn, and random), consistent hashing (session persistence, and hashing based on header name, cookie, IP, and query parameters), and locality load balancing |
| `spec.trafficPolicy.connectionPool` | - | Volume of connections to an upstream service. A TCP or HTTP connection pool can be set. |
| `spec.trafficPolicy.outlierDetection` | - | Eviction of unhealthy hosts from the load balancing pool. |
| `spec.trafficPolicy.tls` | - | TLS-related configurations for the client connected to the upstream service. These configurations are used together with PeerAuthentication policies (TLS mode configurations for the server). |
| `spec.trafficPolicy.portLevelSettings` | - | Port-level traffic policies. Note that port-level policies will override the service-level or subset-level traffic policies. |

## Defining Service Versions (Subsets)

DestinationRule can define versions (subsets) of a service, and a subset is the smallest traffic management unit of Tencent Cloud Mesh. For example, you can configure traffic to be routed to a specified subset of a specified service. The following is a configuration example of using DestinationRule to define two subsets of the product service.

<dx-tabs>
::: YAML Configuration Example
```
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
        version: v1 # Subset v1 is matched against an endpoint of the service by using label version:v1.
    - name: v2
      labels:
        version: v2 # Subset v2 is matched against an endpoint of the service by using label version:v2.
```
:::
::: Console Configuration Example
DestinationRules and services are in a one-to-one binding relationship. To configure a DestinationRule of the product service, you need to enter the product service details page from the service list page, and configure the DestinationRule on the **Basic information** tab page. The steps to configure two versions of the product service on the console are as follows:

1. On the service list page, click **product** to enter the product service details page.
![](https://qcloudimg.tencent-cloud.cn/raw/7f2a1ab3660bc0c74f531d16d8c19823.png)
2. In the third card area **DestinationRule** on the **Basic information** tab page of the service details page, click **Create DestinationRule** to enter the creation pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/4ffbb73c3148fd796d7b49d2d69f0601.png)
3. In the pop-up window, add two versions for the product service and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/270ff0a5b2fa2694548b94d9351f0e36.png)
4. Version configuration of the product service is complete.
![](https://qcloudimg.tencent-cloud.cn/raw/e863b77671d659deb338b5253fd7b04f.png)

:::
</dx-tabs>



## Configuring Consistent Hash-based Load Balancing

The following is a configuration example of using DestinationRule to configure the cart service to perform consistent hash-based load balancing based on the HTTP header name.

<dx-tabs>
::: YAML Configuration Example
```
kind: DestinationRule
metadata:
  name: cart
  namespace: base
spec:
  host: cart
  trafficPolicy:
    loadBalancer:
      consistentHash:
        httpHeaderName: UserID # Configure hash-based load balancing to be performed on the cart service access traffic based on UserID in the header.
```
:::
::: Console Configuration Example
![](https://qcloudimg.tencent-cloud.cn/raw/47e42ee5d503450127bb7063aff4150d.png)
:::
</dx-tabs>

