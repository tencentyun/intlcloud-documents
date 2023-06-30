

After the sample environment is created, all the website services are deployed in the Guangzhou cluster (the product and order services only have v1 deployed). The envoy sidecar is automatically injected to take over service traffic, `istio-ingressgateway` is created, but no listener or routing rules are configured to connect the frontend service to the public network.


#### 1. Creating a gateway and configuring the listener rule
Create a gateway resource, configure the `istio-ingressgateway` listener rule, and set the port to 80 and protocol to HTTP. You only need to configure the gateway rule, and the Tencent Cloud Mesh backend will automatically sync the configurations of Pod, service, and associated CLB of `istio-ingressgateway`.


<dx-tabs>
::: Via the console
1. Log in to the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/mesh?rid=4).
2. Click the target service mesh ID to enter the management page of created service meshes.
3. In **Gateway**, click **Create**.
4. In **Create Gateway**, set the gateway parameters as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/48112c47fcc6998ea57f4c68de90dc7c.png)
5. Click **Save**.
:::
::: Via kubectl 
Submit the following YAML file to the **primary cluster** via kubectl:

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

:::
</dx-tabs>


#### 2. Configuring the routing rule
After configuring the listener rule, configure the routing rule through the `VirtualService` resource to route the traffic from `istio-ingressgateway` to the frontend service.
<dx-tabs>
::: Via the console
1. Log in to the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/mesh?rid=4).
2. Click the target service mesh ID to enter the management page of created service meshes.
3. In **Virtual Service**, click **Create**.
4. In **Create Virtual Service**, set the parameters as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/45c6f95d6c2b9e991356f0848836568f.png)
5. Click **Save**.
:::
::: Via kubectl 
Submit the following YAML file to the **primary cluster** via kubectl:

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
    - base/frontend-gw
  http:
    - route:
        - destination:
            host: frontend.base.svc.cluster.local
```
:::
</dx-tabs>

After the configuration, the demo website can be accessed through the public network IP address of `istio-ingressgateway`. The currently deployed website is as structured below:
![](https://qcloudimg.tencent-cloud.cn/raw/417e68c014e01654255383c22e326c3c.png)


Click the website link to log in (with accounts 1–5, including member accounts 1–3 and non-member accounts 4 and 5), add an item to the cart, and place an order to generate requests to call all the deployed services. The bottom-left floating window of the page displays the name, region, version, and Pod name of the service called by the frontend service, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/cef6cc7cc4daf7caab56515cc56ee6ba.png)

After traffic data is generated, click the **Network Topology** tab to view the network traffic topology in the mesh. Click the **Service** tab to enter the service details page, where you can view the call linkage of the request as well as the full linkage and details at each layer when the stock service is called.

As the business accommodates more services, nearly each frontend request will have a complex call linkage. This calls for fast fault locating and analysis to determine the impact, organizing service call dependencies to determine their reasonableness, or analyzing performance parameters of the linkage, such as request duration, to optimize the call logic with serial/parallel analysis.

The full-linkage tracking system describes the traffic characteristics of the entire network to help you analyze the linkage.
- The network topology is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/7a4a9443d3723e5a8e6280d530b904cc.png)

- Linkage tracking is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/c2625219482dd1f92615f8b0fd86b961.png)

