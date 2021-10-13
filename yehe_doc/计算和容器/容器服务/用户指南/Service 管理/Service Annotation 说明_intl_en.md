You can use the following annotations to configure Services to implement more CLB capabilities.

### Annotation usage

```yaml
apiVersion: v1
kind: Service
metadata:
    annotations:  
      service.kubernetes.io/tke-existed-lbid: lb-6swtxxxx
    name: test
........
```

### Annotation collection

<dx-accordion>
::: service.kubernetes.io/loadbalance-id
**Note:**
This is a read-only annotation that provides the `LoadBalanceId` imported by the current Service.
:::
::: service.kubernetes.io/qcloud-loadbalancer-internal-subnetid
**Note:**
This annotation is used to specify the creation of a private network CLB instance. Its value is the subnet ID.
**Sample:**
`service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxxxx`
:::
::: service.kubernetes.io/tke-existed-lbid
**Note:**
When you use an existing CLB instance, you should note that different usages have different impacts on Tencent Cloud tags.
**Sample:**
For more information on how to use it, please see [Using Existing CLBs](https://intl.cloud.tencent.com/document/product/457/36835).
:::
::: service.kubernetes.io/local-svc-only-bind-node-with-pod
**Note:**
In Service Local mode, only nodes with Pods are bound.
**Sample:**
For more information on how to use it, please see [Service Backend Selection](https://intl.cloud.tencent.com/document/product/457/36836).
:::
::: service.cloud.tencent.com/local-svc-weighted-balance
**Note:**
- It is used with the annotation `service.kubernetes.io/local-svc-only-bind-node-with-pod`.
- The weight of the CLB backend is determined by the number of workloads on the nodes.

**Sample:**
For more information on how to use it, please see [Service Backend Selection](https://intl.cloud.tencent.com/document/product/457/36836).
:::
::: service.kubernetes.io/qcloud-loadbalancer-backends-label
**Note:**
This annotation is used to specify a tag for setting the nodes to be bound to the CLB backend.
**Sample:**
For more information on how to use it, please see [Service Backend Selection](https://intl.cloud.tencent.com/document/product/457/36836).
:::
::: service.cloud.tencent.com/direct-access
**Note:**
This annotation is used to connect a CLB instance directly to a Pod.
**Sample:**
For more information on how to use it, please see [Using Services with CLB-to-Pod Direct Access Mode](https://intl.cloud.tencent.com/document/product/457/36837).
:::
::: service.cloud.tencent.com/tke-service-config
**Note:**
This annotation is used to configure CLB through `tke-service-config`.
**Sample:**
For more information on how to use it, please see [Service CLB Configuration](https://intl.cloud.tencent.com/document/product/457/36834).
:::
::: service.cloud.tencent.com/tke-service-config-auto
**Note:**
This annotation is used to automatically create a `TkeServiceConfig`.
**Sample:**
For more information on how to use it, please see [Service CLB Configuration](https://intl.cloud.tencent.com/document/product/457/36834#service-.E4.B8.8E-tkeserviceconfig-.E5.85.B3.E8.81.94.E8.A1.8C.E4.B8.BA).
:::
::: service.kubernetes.io/loadbalance-nat-ipv6
**Note:**
This is a read-only annotation. When you create an NAT64 IPv6 CLB instance, its IPv6 address will be displayed in the annotation.
**Sample:**
`service.kubernetes.io/loadbalance-nat-ipv6: "2402:4e00:1402:7200:0:9223:5842:2a44"`
:::
::: service.kubernetes.io/loadbalance-type (it will be disused soon)
**Note:**
- This annotation is used to control the type of the automatically created CLB instance: classic CLB or CLB.
- Valid values: yunapi_clb (classic), classic (classic), yunapiv3_forward_clb (CLB)
- Default value: yunapiv3_forward_clb (CLB)
>! Without special needs, we don't recommend you use classic CLB, which has ceased to be iterated and lacks many features.
:::
::: service.cloud.tencent.com/specify-protocol
**Note:**
This annotation is used to configure TCP, UDP, TCP SSL, HTTP, or HTTPS for the specified listening port.
**Sample:**
For more information on how to use it, please see [Service Extension Protocol](https://intl.cloud.tencent.com/document/product/457/39141).
:::
::: service.kubernetes.io/service.extensiveParameters
**Note:**
You can add custom parameters for creating a CLB instance as instructed in [CreateLoadBalancer](https://intl.cloud.tencent.com/document/product/214/33841).
**Sample:**
- Create an NAT64 IPv6 instance: service.kubernetes.io/service.extensiveParameters: '{"AddressIPVersion":"IPV6"}' 
- Purchase a China Telecom CLB instance: service.kubernetes.io/service.extensiveParameters: '{"VipIsp":"CTCC"}'

:::
::: service.cloud.tencent.com/enable-grace-shutdown
**Note:**
This annotation is used to shut down CLB gracefully in direct access mode.
**Sample:**
It is only supported in direct access mode and needs to be used together with `service.cloud.tencent.com/direct-access`. For more information on how to use it, please see [Graceful Service Shutdown](https://intl.cloud.tencent.com/document/product/457/42070).
:::
</dx-accordion>

