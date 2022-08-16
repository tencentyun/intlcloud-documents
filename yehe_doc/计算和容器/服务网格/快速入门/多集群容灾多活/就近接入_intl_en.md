
 ## Overview
 As the ecommerce website business expands, businesses need to be quickly deployed to and accessed from a cluster in another region/AZ. Instead of deploying a complete set of businesses, you only need to deploy an edge gateway in the meshed cluster and configure the listener rule. Nearby access is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/32fecc8594a7c31cecbbea0aeee6c1d4.png)

## Directions
Apply the following configuration to the primary cluster. Configure the listener rule of the edge gateway in cluster 2 (sub-cluster), open port 80, and configure the HTTP protocol and `VirtualService` to route the traffic from the edge gateway to the frontend service.

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: frontend-gw-2
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
    app: istio-ingressgateway-1
    istio: ingressgateway

---
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: frontend-vs
  namespace: base
spec:
  hosts:
    - '*'
  gateways:
    - base/frontend-gw
    - base/frontend-gw-2
  http:
    - route:
        - destination:
            host: frontend.base.svc.cluster.local
```

After the configuration, the ecommerce website can be accessed through the IP address of the edge gateway in cluster 2 (sub-cluster), as traffic is routed to the service in the primary cluster, even when no ecommerce website services are configured in the Shanghai cluster.
Requests from the secondary cluster are routed to the nearby service in the primary cluster as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/2ad2142f1f6b8a1e4719e613ef38d58b.png)