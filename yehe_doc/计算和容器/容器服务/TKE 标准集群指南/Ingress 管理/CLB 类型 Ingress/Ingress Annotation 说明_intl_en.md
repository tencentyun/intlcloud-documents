You can use the following annotations to configure Ingress to enrich CLB capabilities.

## Annotation Usage

```yaml
apiVersion: 
kind: Ingress
metadata:
    annotations:  
      kubernetes.io/ingress.class: "qcloud"
    name: test
........
```

## Annotation Collection



### kubernetes.io/ingress.class

   
**Note:**
This annotation is used to configure the Ingress type for the component management that is not configured with the annotation or the Ingress resource whose annotation content is qcloud.  		 

**Use case:**
`kubernetes.io/ingress.class: "qcloud"`
 
--- 
### kubernetes.io/ingress.qcloud-loadbalance-id
   
**Note:**
This is a read-only annotation that provides the LoadBalanceId referenced by the current Ingress.
  
   
**Use case:**
`kubernetes.io/ingress.qcloud-loadbalance-id: "lb-3imskkfe"`
 
--- 
### ingress.cloud.tencent.com/loadbalance-nat-ipv6
   
**Note:**
This is a read-only annotation that provides IPv6 address when the user configures or applies for NAT IPv6 CLB.
 
--- 
### ingress.cloud.tencent.com/loadbalance-ipv6
   
**Note:**
This is a read-only annotation that provides IPv6 address when the user configures or applies for FullStack IPv6 CLB.
 
--- 
### kubernetes.io/ingress.internetChargeType
   
**Note:**
The billing type of CLB can only be configured at the time of creation, and cannot be modified after the creation.
This annotation is used to specify the CLB payment mode when a CLB instance is created. You need to use it with `kubernetes.io/ingress.internetMaxBandwidthOut` annotation.     

**Valid values:**
- TRAFFIC_POSTPAID_BY_HOUR: Postpaid by traffic on an hourly basis.  
- BANDWIDTH_POSTPAID_BY_HOUR: Postpaid by bandwidth on an hourly basis.       
   
**Use case:**
`kubernetes.io/ingress.internetChargeType: "TRAFFIC_POSTPAID_BY_HOUR"`
 
--- 
### kubernetes.io/ingress.internetMaxBandwidthOut

   
**Note:**
CLB bandwidth can only be configured at the time of creation, and cannot be modified after the creation.
This annotation is used to specify the maximum outbound bandwidth of the CLB instance when a CLB instance is created, which applies only to public network CLB instances. You need to use it with `kubernetes.io/ingress.internetChargeType` annotation.

**Valid values:**
Value range: 1-2,048 Mbps


   
**Use case:**
`kubernetes.io/ingress.internetMaxBandwidthOut: "2048"`
 
--- 
### kubernetes.io/ingress.extensiveParameters
   
**Note:**
This annotation uses the parameters configured when the CLB was created. It can only be configured at the time of creation and cannot be modified after the creation.
Refer to [Creating a CLB Instance](https://intl.cloud.tencent.com/document/product/214/33841) to add custom parameters for the created CLB instance.  		 

**Use case:**
- Creating a NAT64 IPv6 instance:
  `kubernetes.io/ingress.extensiveParameters: '{"AddressIPVersion":"IPV6"}'`
- Creating an IPv6 Instance
  `kubernetes.io/ingress.extensiveParameters: '{"AddressIPVersion":"IPv6FullChain"}'`
- Purchasing a CTCC CLB:
  `kubernetes.io/ingress.extensiveParameters: '{"VipIsp":"CTCC"}'`
- Specifying a availability zone to create
  `kubernetes.io/ingress.extensiveParameters: '{"ZoneId":"ap-guangzhou-1"}'`
 
--- 
### kubernetes.io/ingress.subnetId
   
**Note:**
This annotation is used to specify the creation of a private network CLB, and specify the subnet where the CLB locates.  		 

**Use case:**
`kubernetes.io/ingress.subnetId: "subnet-3swgntkk"`
 
--- 
### kubernetes.io/ingress.existLbId
   
**Note:**
This annotation is used to specify the use of the existing CLB as the entry resource of the access layer.
>! When using an existing CLB, you need to ensure that it does not include other listeners.



   
**Use case:**
`kubernetes.io/ingress.existLbId: "lb-342wppll"`
 
--- 
### kubernetes.io/ingress.rule-mix: 
### kubernetes.io/ingress.http-rules: 
### kubernetes.io/ingress.https-rules:
   
**Note:**
The first annotation is used to configure hybrid protocols. The second and third annotations are used to configure the forwarding rules, which support forwarding via both http and https protocols. These annotations can be used to configure manual redirection.  	

**Use case:**
For more information on usage, see [Mixed Use of HTTP and HTTPS Protocols through Ingress](https://intl.cloud.tencent.com/document/product/457/43504).
 
--- 
### ingress.cloud.tencent.com/direct-access
   
**Note:**
You can use this annotation to achieve CLB-to-Pod direct access in layer 7. Pay attention to the service dependency of directly access under different networks.  		 

**Use case:**
For details, see [Using Services with CLB-to-Pod Direct Access Mode](https://intl.cloud.tencent.com/document/product/457/36837).
 
--- 
### ingress.cloud.tencent.com/tke-service-config
   
**Note:**
This annotation is used to set the CLB related configurations through tke-service-config, including listeners, forwarding rules, etc.  		 

**Use case:**
`ingress.cloud.tencent.com/tke-service-config: "nginx-config"`. For more information, see [Using TkeServiceConfig to Configure CLBs](https://intl.cloud.tencent.com/document/product/457/37015).
 
--- 
### ingress.cloud.tencent.com/tke-service-config-auto
   
**Note:**
You can use this annotation to automatically create the TkeServiceConfig resource and provide a configuration template for user to configure as needed.  		

**Use case:**
`ingress.cloud.tencent.com/tke-service-config-auto: "true"`. For more information, see [Using TKEServiceConfig to Configure CLBs](https://intl.cloud.tencent.com/document/product/457/37015).
 
--- 
### ingress.cloud.tencent.com/rewrite-support
   
**Note:**
- This annotation can be used to configure manual redirection together with `kubernetes.io/ingress.http-rules` and `kubernetes.io/ingress.https-rules`.
- This annotation can be used to configure automatic redirection together with `ingress.cloud.tencent.com/auto-rewrite`.
   
**Use case:**
`ingress.cloud.tencent.com/rewrite-support: "true"`
 
--- 
### ingress.cloud.tencent.com/auto-rewrite
   
**Note:**
This annotation is used to provide automatic redirection for the HTTP port. All forwarding rules declared on the HTTPS port will create corresponding redirection rules. It is used together with the `ingress.cloud.tencent.com/rewrite-support` annotation to enable redirection management capabilities.  		 

**Use case:**
`ingress.cloud.tencent.com/auto-rewrite: "true"`
 
--- 
### ingress.cloud.tencent.com/cross-region-id
   
**Note:**
This annotation is used for Ingress cross-region binding, and is used to specify which region to access. It is used together with `kubernetes.io/ingress.existLbId` or `ingress.cloud.tencent.com/cross-vpc-id`.  		 

**Use case:**
- Creating a CLB for remote access
  `ingress.cloud.tencent.com/cross-region-id: "ap-guangzhou"`
  `ingress.cloud.tencent.com/cross-vpc-id: "vpc-646vhcjj"`
- Selecting an existing CLB for remote access
  `ingress.cloud.tencent.com/cross-region-id: "ap-guangzhou"`
  `kubernetes.io/ingress.existLbId: "lb-342wppll"`
 
--- 
### ingress.cloud.tencent.com/cross-vpc-id
   
**Note:**
This annotation is used for Ingress cross-region binding, and is used to specify which VPC to access. It can be used together with `ingress.cloud.tencent.com/cross-region-id` annotation to specify the VPC of other region.
>! This annotation applies to the CLB created and managed by TKE. It is invalid for scenarios that use the existing CLB.
>

   
**Use case:**
Creating CLB for remote access:
`ingress.cloud.tencent.com/cross-region-id: "ap-guangzhou"`
`ingress.cloud.tencent.com/cross-vpc-id: "vpc-646vhcjj"`
 
--- 
### ingress.cloud.tencent.com/enable-grace-shutdown
   
**Note:**
This annotation is used to shut down CLB instances gracefully in direct access mode. If a deleted Pod contains `DeletionTimestamp` and is in **Terminating** status, the weight of the Pod on the CLB backend is adjusted to `0`. 

**Use case:**
It is only supported in direct access mode and needs to be used together with `ingress.cloud.tencent.com/direct-access`. For more information on how to use it, see [Graceful Ingress Shutdown](https://intl.cloud.tencent.com/document/product/457/42069).

---
### ingress.cloud.tencent.com/enable-grace-shutdown-tkex
**Note:**
This annotation is used to shut down CLB instances gracefully in direct access mode. If the endpoints in the Endpoint object are `not-ready`, the weights on the CLB backend are adjusted to `0`.

**Use case:**
It is only supported in direct access mode and needs to be used together with `ingress.cloud.tencent.com/direct-access`. For detailed directions, see [Graceful Ingress Shutdown](https://intl.cloud.tencent.com/document/product/457/42069).

---
### ingress.cloud.tencent.com/security-groups

**Note:**
This annotation is used to bind security groups to CLB-type Ingresses. Up to five security groups can be bound to a CLB.

**Notes:**
- For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/214/14733) of CLB security groups.
- Usually, the "Allow Traffic by Default" feature must be enabled, with which the traffic forwarding between CLB and CVM is allowed by default. Traffic coming from the CLB only needs to be verified by the security group bound to the CLB. The annotation is `ingress.cloud.tencent.com/pass-to-target`.

**Use case:**
`ingress.cloud.tencent.com/security-groups: "sg-xxxxxx,sg-xxxxxx"`

---

### ingress.cloud.tencent.com/pass-to-target 

**Note:**
This annotation is used to configure the "Allow Traffic by Default" feature for the CLB-type Ingress. The traffic forwarding between CLB and CVM is allowed by default. Traffic coming from the CLB only needs to be verified by the security group bound to the CLB.

**Notes:**

- For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/214/14733) of CLB security groups.
- Usually, the feature of binding a security group is required. The annotation is `ingress.cloud.tencent.com/security-groups`.

**Use case:**
`ingress.cloud.tencent.com/pass-to-target: "true"`
