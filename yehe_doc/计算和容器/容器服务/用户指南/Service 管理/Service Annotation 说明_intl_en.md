You can use the following annotations to configure Services to enrich CLB capabilities.

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
This is a read-only annotation that provides the `LoadBalanceId` imported by the current Service. You can go to Tencent Cloud CLB console to view the IDs of the CLB instances in the same VPC with the cluster.
:::
::: service.kubernetes.io/qcloud-loadbalancer-internal-subnetid
**Note:**
This annotation is used to specify the creation of a private network CLB instance. Its value is the subnet ID.
**Use case:**
`service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxxxx`
:::
::: service.kubernetes.io/tke-existed-lbid
**Note:**
When you use an existing CLB instance, you should note that different usages have different impacts on Tencent Cloud tags.
**Use case:**
For the detailed usage, see [Using Existing CLBs](https://intl.cloud.tencent.com/document/product/457/36835).
:::
::: service.kubernetes.io/local-svc-only-bind-node-with-pod
**Note:**
In Service Local mode, only nodes with Pods are bound.
**Use case:**
For the detailed usage, see [Service Local Mode](https://intl.cloud.tencent.com/document/product/457/36836).
:::
::: service.cloud.tencent.com/local-svc-weighted-balance
**Note:**
- It is used with the annotation `service.kubernetes.io/local-svc-only-bind-node-with-pod`.
- The weight of the CLB backend is determined by the number of workloads on the nodes.

**Use case:**
For the detailed usage, see [Service Local Mode](https://intl.cloud.tencent.com/document/product/457/36836).
:::
::: service.kubernetes.io/qcloud-loadbalancer-backends-label
**Note:**
This annotation is used to specify a tag for setting the nodes to be bound to the CLB backend.
**Use case:**
For the detailed usage, see [Specifying the Access-Layer Backend](https://intl.cloud.tencent.com/document/product/457/36836).
:::
::: service.cloud.tencent.com/direct-access
**Note:**
This annotation is used to connect a CLB instance directly to a Pod.
**Use case:**
For details, see [Using Services with CLB-to-Pod Direct Access Mode](https://intl.cloud.tencent.com/document/product/457/36837).
:::
::: service.cloud.tencent.com/tke-service-config
**Note:**
This annotation is used to configure CLB through `tke-service-config`.
**Use case:**
For the detailed usage, see [Service CLB Configuration](https://intl.cloud.tencent.com/document/product/457/36834).
:::
::: service.cloud.tencent.com/tke-service-config-auto
**Note:**
This annotation is used to automatically create a `TkeServiceConfig`.
**Use case:**
For more information on how to use it, please see [Service CLB Configuration](https://intl.cloud.tencent.com/document/product/457/36834#service-.E4.B8.8E-tkeserviceconfig-.E5.85.B3.E8.81.94.E8.A1.8C.E4.B8.BA).
:::
::: service.kubernetes.io/loadbalance-nat-ipv6
**Note:**
This is a read-only annotation. When you create an NAT64 IPv6 CLB instance, its IPv6 address will be displayed in the annotation.
**Use case:**
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
**Use case:**
For the detailed usage, see [Service Extension Protocol](https://intl.cloud.tencent.com/zh/document/product/457/39141).
:::
::: service.kubernetes.io/service.extensiveParameters
**Note:**
Refer to [Creating a CLB Instance](https://intl.cloud.tencent.com/document/product/214/33841) to add custom parameters for the created CLB instance.
**Use case:**
- Creating a NAT64 IPv6 instance:
 service.kubernetes.io/service.extensiveParameters: '{"AddressIPVersion":"IPV6"}' 
- Purchasing a CTCC CLB:
  service.kubernetes.io/service.extensiveParameters: '{"VipIsp":"CTCC"}'

:::
::: service.cloud.tencent.com/enable-grace-shutdown
**Note:**
This annotation is used to shut down CLB gracefully in direct access mode.
**Use case:**
It is only supported in direct access mode and needs to be used together with `service.cloud.tencent.com/direct-access`,For the detailed usage, see [Graceful Service Shutdown](https://intl.cloud.tencent.com/document/product/457/42070).
:::
::: kubernetes.io/service.internetChargeType
**Note:**
This annotation is used to specify the CLB payment mode when a CLB is created. Please use it with `kubernetes.io/service.internetMaxBandwidthOut` annotation.
**Valid values:**

TRAFFIC_POSTPAID_BY_HOUR：postpaid by traffic on an hourly basis.
BANDWIDTH_POSTPAID_BY_HOUR：postpaid by bandwidth on an hourly basis.
**Use case:**
`kubernetes.io/service.internetChargeType: "TRAFFIC_POSTPAID_BY_HOUR"`
:::
::: kubernetes.io/service.internetMaxBandwidthOut
**Note:**
This annotation is used to specify the maximum outbound bandwidth of the CLB when a CLB is created, which applies only to public network CLB instances. Please use it with `kubernetes.io/service.internetChargeType` annotation.

**Valid values:**
Value range: 1-2,048 Mbps

**Use case:**
`kubernetes.io/service.internetMaxBandwidthOut: "2048"`
:::
</dx-accordion>

