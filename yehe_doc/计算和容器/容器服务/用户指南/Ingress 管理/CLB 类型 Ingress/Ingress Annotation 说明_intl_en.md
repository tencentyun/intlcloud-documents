You can use the following annotations to configure Ingress to implement more CLB capabilities.

### Annotation usage

```yaml
apiVersion: 
kind: Ingress
metadata:
    annotations:  
      kubernetes.io/ingress.class: "qcloud"
    name: test
........
```

### Annotation collection

<dx-accordion>
::: kubernetes.io/ingress.class
**Note:**
This annotation is used to configure the Ingress type for the component management that is not configured with the annotation or the Ingress resource whose annotation content is qcloud.
**Example:**
`kubernetes.io/ingress.class: "qcloud"`
:::
::: kubernetes.io/ingress.qcloud-loadbalance-id
**Note:**
This is a read-only annotation that provides the LoadBalanceId referenced by the current Ingress.
**Example:**
`kubernetes.io/ingress.qcloud-loadbalance-id: "lb-3imskkfe"`
:::
::: ingress.cloud.tencent.com/loadbalance-nat-ipv6
**Note:**
This is a read-only annotation that provides IPv6 address when the user configures or applies for NAT IPv6 CLB.
:::
::: ingress.cloud.tencent.com/loadbalance-ipv6
**Note:**
This is a read-only annotation that provides IPv6 address when the user configures or applies for FullStack IPv6 CLB.
:::
::: kubernetes.io/ingress.internetChargeType
**Note:**
This annotation is used to specify the CLB payment mode when a CLB is created. Please use it with `kubernetes.io/ingress.internetMaxBandwidthOut` annotation.    
**Valid values:**
<li>TRAFFIC_POSTPAID_BY_HOUR pay-as-you-go by traffic on an hourly billing cycle</li>
<li>BANDWIDTH_POSTPAID_BY_HOUR: pay-as-you-go by bandwidth on an hourly billing cycle</li>    
<b>Example:</b><br>
<code>kubernetes.io/ingress.internetChargeType: "TRAFFIC_POSTPAID_BY_HOUR"</code>
:::
::: kubernetes.io/ingress.internetMaxBandwidthOut
**Note:**
This annotation is used to specify the maximum outbound bandwidth of the CLB when a CLB is created, which applies only to public network CLB instances. Please use it with `kubernetes.io/ingress.internetChargeType` annotation.

**Valid values:**
Value range: 0-2,048 Mbps

**Example:**
`kubernetes.io/ingress.internetMaxBandwidthOut: "2048"`
:::
::: kubernetes.io/ingress.extensiveParameters
**Note:**
Refer to [Creating a CLB Instance](https://intl.cloud.tencent.com/document/product/214/33841) to add custom parameters for the created a CLB instance.
**Example:**

- Creating a NAT64 IPv6 instance
  `service.kubernetes.io/service.extensiveParameters: '{"AddressIPVersion":"IPV6"}'`
- Creating an IPv6 Instance
  `service.kubernetes.io/service.extensiveParameters: '{"AddressIPVersion":"IPv6FullChain"}'`
- Purchasing a CTCC CLB
  `service.kubernetes.io/service.extensiveParameters: '{"VipIsp":"CTCC"}'`
- Specifying a availability zone to create
  `service.kubernetes.io/service.extensiveParameters: '{"ZoneId":"ap-guangzhou-1"}'`
:::
::: kubernetes.io/ingress.subnetId
**Note:**
This annotation is used to specify the creation of a private network CLB, and specify the subnet where the CLB locates.
**Example:**
`kubernetes.io/ingress.subnetId: "subnet-3swgntkk"`
:::
::: kubernetes.io/ingress.existLbId
**Note:**
This annotation is used to specify the use of the existing CLB as the entry resource of the access layer.
<dx-alert infotype="notice" title="">
When using an existing CLB, you need to ensure that it does not include other listeners.
</dx-alert>

**Example:**
`kubernetes.io/ingress.existLbId: "lb-342wppll"`
:::
::: ingress.cloud.tencent.com/direct-access
**Note:**
You can use this annotation to achieve CLB-to-Pod direct access in layer 7. Pay attention to the service dependency of directly access under different networks.
**Example:**
For details, see [Using Services with CLB-to-Pod Direct Access Mode](https://intl.cloud.tencent.com/document/product/457/36837).
:::
::: ingress.cloud.tencent.com/enable-grace-shutdown
**Note:**
You can use this annotation to gracefully shut down the workload in access layer. When the Pod is in the “Terminating” state, the workload will not be removed directly but the weight will become 0. It is used together with the PreStop feature of the workload to control the traffic when the workload is shut down.
**Example:**
`ingress.cloud.tencent.com/enable-grace-shutdown: "true"`
:::
::: ingress.cloud.tencent.com/tke-service-config
**Note:**
This annotation is used to set the CLB related configurations through tke-service-config, including listeners, forwarding rules, etc.
**Example:**
`ingress.cloud.tencent.com/tke-service-config: "nginx-config"`. For more information, see [Using TKEServiceConfig to Configure CLBs](https://intl.cloud.tencent.com/document/product/457/37015).
:::
::: ingress.cloud.tencent.com/tke-service-config-auto
**Note:**
You can use this annotation to automatically create the TkeServiceConfig resource and provide a configuration template for user to configure as needed.
**Example:**
`ingress.cloud.tencent.com/tke-service-config-auto: "true"`. For more information, see [Using TKEServiceConfig to Configure CLBs](https://intl.cloud.tencent.com/document/product/457/37015)
:::
::: ingress.cloud.tencent.com/rewrite-support
**Note:**
<li>To implement manual redirection, use this annotation in combination with <code>kubernetes.io/ingress.http-rules</code> and <code>kubernetes.io/ingress.https-rules</code>.</li>
<li>To implement automatic redirection, use this annotation in combination with <code>ingress.cloud.tencent.com/auto-rewrite</code>.</li>
<b>Example:</b><br>
<code>ingress.cloud.tencent.com/rewrite-support: "true"</code>
:::
::: ingress.cloud.tencent.com/auto-rewrite
**Note:**
This annotation is used to provide automatic redirection for HTTP ports. For all forwarding rules declared on HTTPS ports, corresponding redirection rules are created. You need use it in combination with `ingress.cloud.tencent.com/rewrite-support` annotation to enable redirection management capabilities.
**Example:**
`ingress.cloud.tencent.com/auto-rewrite: "true"`
:::
::: ingress.cloud.tencent.com/cross-region-id
**Note:**
This annotation specifies the source region for Ingress cross-region binding. It should be used in combination with `kubernetes.io/ingress.existLbId` or `ingress.cloud.tencent.com/cross-vpc-id`.
**Example:**
- Creating a CLB for remote access
  `ingress.cloud.tencent.com/cross-region-id: "ap-guangzhou"`
  `ingress.cloud.tencent.com/cross-vpc-id: "vpc-646vhcjj"`
- Selecting an existing CLB for remote access
  `ingress.cloud.tencent.com/cross-region-id: "ap-guangzhou"`
  `kubernetes.io/ingress.existLbId: "lb-342wppll"`
:::
::: ingress.cloud.tencent.com/cross-vpc-id
**Note:**
This annotation specifies the VPC to access for Ingress cross-region binding. It can be used together with `ingress.cloud.tencent.com/cross-region-id` annotation to specify the VPC of other region.
>! This annotation applies to the CLB created and managed by TKE. It is invalid for scenarios that use the existing CLB.
>
**Example:**
Creating CLB for remote access:
`ingress.cloud.tencent.com/cross-region-id: "ap-guangzhou"`
`ingress.cloud.tencent.com/cross-vpc-id: "vpc-646vhcjj"`
:::
</dx-accordion>

