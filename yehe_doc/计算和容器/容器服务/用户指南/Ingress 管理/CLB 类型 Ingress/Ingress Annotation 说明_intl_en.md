You can use the following annotations to configure Ingress to enrich CLB capabilities.

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
**Sample:**
`kubernetes.io/ingress.class: "qcloud"`
:::
::: kubernetes.io/ingress.qcloud-loadbalance-id
**Note:**
This is a read-only annotation that provides the LoadBalanceId referenced by the current Ingress.
**Sample:**
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
<b>Use case</b><br>
<code>kubernetes.io/ingress.internetChargeType: "TRAFFIC_POSTPAID_BY_HOUR"</code>
:::
::: kubernetes.io/ingress.internetMaxBandwidthOut
**Note:**
This annotation is used to specify the maximum outbound bandwidth of the CLB when a CLB is created, which applies only to public network CLB instances. Please use it with `kubernetes.io/ingress.internetChargeType` annotation.

**Valid values:**
Value range: 0-2,048 Mbps

**Sample:**
`kubernetes.io/ingress.internetMaxBandwidthOut: "2048"`
:::
::: kubernetes.io/ingress.extensiveParameters
**Note:**
You can add custom parameters for creating a CLB instance as instructed in [CreateLoadBalancer](https://intl.cloud.tencent.com/document/product/214/33841).
**Sample:**

- Creating an NAT64 IPv6 instance
  `kubernetes.io/ingress.extensiveParameters: '{"AddressIPVersion":"IPV6"}'`
- Creating an IPv6 instance
  `kubernetes.io/ingress.extensiveParameters: '{"AddressIPVersion":"IPv6FullChain"}'`
- Purchasing a China Telecom CLB instance
  `kubernetes.io/ingress.extensiveParameters: '{"VipIsp":"CTCC"}'`
- Specifying an AZ for creation
  `kubernetes.io/ingress.extensiveParameters: '{"ZoneId":"ap-guangzhou-1"}'`
:::
::: kubernetes.io/ingress.subnetId
**Note:**
This annotation is used to specify the creation of a private network CLB, and specify the subnet where the CLB locates.
**Sample:**
`kubernetes.io/ingress.subnetId: "subnet-3swgntkk"`
:::
::: kubernetes.io/ingress.existLbId
**Note:**
This annotation is used to specify the use of the existing CLB as the entry resource of the access layer.
<dx-alert infotype="notice" title="">
When using an existing CLB, you need to ensure that it does not include other listeners.
</dx-alert>

**Sample:**
`kubernetes.io/ingress.existLbId: "lb-342wppll"`
:::
::: ingress.cloud.tencent.com/direct-access
**Note:**
You can use this annotation to achieve CLB-to-Pod direct access in layer 7. Pay attention to the service dependency of directly access under different networks.
**Sample:**
For more information on how to use it, please see [Using Services with CLB-to-Pod Direct Access Mode](https://intl.cloud.tencent.com/document/product/457/36837).
:::
::: ingress.cloud.tencent.com/tke-service-config
**Note:**
This annotation is used to set the CLB related configurations through tke-service-config, including listeners, forwarding rules, etc.
**Sample:**
`ingress.cloud.tencent.com/tke-service-config: "nginx-config"`. For more information, please see [Using TKEServiceConfig to Configure CLBs](https://intl.cloud.tencent.com/document/product/457/37015).
:::
::: ingress.cloud.tencent.com/tke-service-config-auto
**Note:**
You can use this annotation to automatically create the TkeServiceConfig resource and provide a configuration template for user to configure as needed.
**Sample:**
`ingress.cloud.tencent.com/tke-service-config-auto: "true"`. For more information, please see [Using TKEServiceConfig to Configure CLBs](https://intl.cloud.tencent.com/document/product/457/37015)
:::
::: ingress.cloud.tencent.com/rewrite-support
**Note:**
<li>This annotation is used to achieve manual redirection together with <code>kubernetes.io/ingress.http-rules</code> and <code>kubernetes.io/ingress.https-rules</code>.</li>
<li>This annotation is used to achieve automatic redirection together with <code>ingress.cloud.tencent.com/auto-rewrite</code>.</li>
<b>Use case</b><br>
<code>ingress.cloud.tencent.com/rewrite-support: "true"</code>
:::
::: ingress.cloud.tencent.com/auto-rewrite
**Note:**
This annotation is used to provide automatic redirection for the HTTP port. All forwarding rules declared on the HTTPS port will create corresponding redirection rules. It is used together with the `ingress.cloud.tencent.com/rewrite-support` annotation to enable redirection management capabilities.
**Sample:**
`ingress.cloud.tencent.com/auto-rewrite: "true"`
:::
::: ingress.cloud.tencent.com/cross-region-id
**Note:**
This annotation is used for Ingress cross-region binding, and is used to specify which region to access. It is used together with `kubernetes.io/ingress.existLbId` or `ingress.cloud.tencent.com/cross-vpc-id`.
**Sample:**

- Creating a CLB for remote access
  `ingress.cloud.tencent.com/cross-region-id: "ap-guangzhou"`
  `ingress.cloud.tencent.com/cross-vpc-id: "vpc-646vhcjj"`
- Selecting an existing CLB for remote access
  `ingress.cloud.tencent.com/cross-region-id: "ap-guangzhou"`
  `kubernetes.io/ingress.existLbId: "lb-342wppll"`
:::
::: ingress.cloud.tencent.com/cross-vpc-id
**Note:**
This annotation is used for Ingress cross-region binding, and is used to specify which VPC to access. It can be used together with `ingress.cloud.tencent.com/cross-region-id` annotation to specify the VPC of other region.
>! This annotation applies to the CLB created and managed by TKE. It is invalid for scenarios that use the existing CLB.
>
**Sample:**
Creating CLB for remote access:
`ingress.cloud.tencent.com/cross-region-id: "ap-guangzhou"`
`ingress.cloud.tencent.com/cross-vpc-id: "vpc-646vhcjj"`
:::
::: ingress.cloud.tencent.com/enable-grace-shutdown
**Note:**
This annotation is used to shut down CLB gracefully in direct access mode.
**Sample:**
It is only supported in direct access mode and needs to be used together with `ingress.cloud.tencent.com/direct-access`. For more information on how to use it, please see [Graceful Ingress Shutdown](https://intl.cloud.tencent.com/document/product/457/42069).
:::
</dx-accordion>

