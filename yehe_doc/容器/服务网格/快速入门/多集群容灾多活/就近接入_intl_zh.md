
 ## 操作场景
 随着电商网站业务规模的扩张，网站的业务需要快速部署至另一地域/可用区的集群，从另一集群的网关也能访问电商网站业务。此时无需在另一集群部署整套业务，只需在网格管理的另一个集群中部署边缘代理网关并配置好监听规则，即可以另一集群为入口访问电商网站业务。就近接入如下图所示：
![就近接入](https://qcloudimg.tencent-cloud.cn/raw/32fecc8594a7c31cecbbea0aeee6c1d4.png)

## 操作步骤
应用以下配置到主集群，gateway 配置集群 2（子集群）的边缘代理网关的监听器规则，放通 80 端口，http 协议，VirtualService 配置将来自边缘代理网关的流量路由至 frontend 服务。

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

配置完成后，通过集群 2（子集群）的边缘代理网关 IP 地址即可访问到电商网站，即使上海的集群中没有部署电商网站相关服务，因为流量被路由到了主集群的服务。
来自子集群的请求就近接入后访问部署在主集群的服务如下图所示：
![来自子集群的请求就近接入后访问部署在主集群的服务](https://qcloudimg.tencent-cloud.cn/raw/2ad2142f1f6b8a1e4719e613ef38d58b.png)