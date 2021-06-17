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
**Use case:**
`kubernetes.io/ingress.class: "qcloud"`
:::
::: kubernetes.io/ingress.qcloud-loadbalance-id
**Note:**
This is a read-only annotation that provides the LoadBalanceId referenced by the current Ingress.
**Use case:**
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

**Use case:**
`kubernetes.io/ingress.internetMaxBandwidthOut: "2048"`
:::
::: kubernetes.io/ingress.extensiveParameters
**Note:**
Refer to [Creating a CLB Instance](https://intl.cloud.tencent.com/document/product/214/33841) to add custom parameters for the created a CLB instance.
**Use case:**

- Creating a NAT64 IPv6 instance
  `kubernetes.io/ingress.extensiveParameters: '{"AddressIPVersion":"IPV6"}'`
- Creating an IPv6 Instance
  `kubernetes.io/ingress.extensiveParameters: '{"AddressIPVersion":"IPv6FullChain"}'`
- Purchasing a CTCC CLB
  `kubernetes.io/ingress.extensiveParameters: '{"VipIsp":"CTCC"}'`
- Specifying a availability zone to create
  `kubernetes.io/ingress.extensiveParameters: '{"ZoneId":"ap-guangzhou-1"}'`
:::
::: kubernetes.io/ingress.subnetId
**Note:**
This annotation is used to specify the creation of a private network CLB, and specify the subnet where the CLB locates.
**Use case:**
`kubernetes.io/ingress.subnetId: "subnet-3swgntkk"`
:::
::: kubernetes.io/ingress.existLbId
**Note:**
This annotation is used to specify the use of the existing CLB as the entry resource of the access layer.

<blockquote class="doc-tip"><p class="doc-tip-tit"><i class="doc-icon-tip"></i>Note</p><p>When using an existing CLB, you need to ensure that it does not include other listeners.</a></p></blockquote>


**Use case:**
`kubernetes.io/ingress.existLbId: "lb-342wppll"`
:::
::: ingress.cloud.tencent.com/direct-access
**Note:**
You can use this annotation to achieve CLB-to-Pod direct access in layer 7. Pay attention to the service dependency of directly access under different networks.
**Use case:**
For details, see [Using Services with CLB-to-Pod Direct Access Mode](https://intl.cloud.tencent.com/document/product/457/36837).
:::
::: ingress.cloud.tencent.com/enable-grace-shutdown
**Note:**
You can use this annotation to gracefully shut down the workload in access layer. When the Pod is in the “Terminating” state, the workload will not be removed directly but the weight will become 0. It is used together with the PreStop feature of the workload to control the traffic when the workload is shut down.
**Use case:**
`ingress.cloud.tencent.com/enable-grace-shutdown: "true"`
:::
::: ingress.cloud.tencent.com/tke-service-config
**Note:**
This annotation is used to set the CLB related configurations through tke-service-config, including listeners, forwarding rules, etc.
**Use case:**
`ingress.cloud.tencent.com/tke-service-config: "nginx-config"`. For more information, see [Using TKEServiceConfig to Configure CLBs](https://intl.cloud.tencent.com/document/product/457/37015).
:::
::: ingress.cloud.tencent.com/tke-service-config-auto
**Note:**
You can use this annotation to automatically create the TkeServiceConfig resource and provide a configuration template for user to configure as needed.
**Use case:**
`ingress.cloud.tencent.com/tke-service-config-auto: "true"`. For more information, see [Using TKEServiceConfig to Configure CLBs](https://intl.cloud.tencent.com/document/product/457/37015)
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
**Use case:**
`ingress.cloud.tencent.com/auto-rewrite: "true"`
:::
::: ingress.cloud.tencent.com/cross-region-id
**Note:**
This annotation is used for Ingress cross-region binding, and is used to specify which region to access. It is used together with `kubernetes.io/ingress.existLbId` or `ingress.cloud.tencent.com/cross-vpc-id`.
**Use case:**
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
<blockquote class="doc-tip"><p class="doc-tip-tit"><i class="doc-icon-tip"></i>Note</p><p>This annotation applies to the CLB created and managed by TKE. It is invalid for scenarios that use the existing CLB.</a></p></blockquote>

**Use case:**
Creating CLB for remote access:
`ingress.cloud.tencent.com/cross-region-id: "ap-guangzhou"`
`ingress.cloud.tencent.com/cross-vpc-id: "vpc-646vhcjj"`
:::
</dx-accordion>

