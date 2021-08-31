You can use the following annotations to configure Services so as to enrich CLB capabilities.

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

#### service.kubernetes.io/loadbalance-id
**Note:**
This is a read-only annotation that provides the LoadBalanceId referenced by the current Service.
#### service.kubernetes.io/qcloud-loadbalancer-internal-subnetid
**Note:**
This annotation is used to specify the creation of a private-network CLB, and its value indicates the subnet ID.
**Use case:**
`service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxxxx`
#### service.kubernetes.io/tke-existed-lbid
**Note:**
When you use an existing CLB, note that different ways of use have different impacts on Tencent Cloud labels.
**Use case:**
For usage details, see [Service Using an Existing CLB](https://intl.cloud.tencent.com/document/product/457/36835).

#### service.kubernetes.io/local-svc-only-bind-node-with-pod
**Note:**
In Service Local mode, only nodes with pods are bound.
**Use case:**
For usage details, see [Service Local Mode](https://intl.cloud.tencent.com/document/product/457/36836#service-local-.E6.A8.A1.E5.BC.8F).

#### service.cloud.tencent.com/local-svc-weighted-balance
**Note:**

- This is used together with the annotation `service.kubernetes.io/local-svc-only-bind-node-with-pod`.
- The CLB backend weight is determined by the number of workloads on nodes.

**Use case:**
For usage details, see [Service Local Mode](https://intl.cloud.tencent.com/document/product/457/36836#service-local-.E6.A8.A1.E5.BC.8F).

#### service.kubernetes.io/qcloud-loadbalancer-backends-label
**Note:**
This annotation is used to specify a label for setting the nodes to be bound with the CLB backend.
**Use case:**
For usage details, see [Specifying the Access-Layer Backend](https://intl.cloud.tencent.com/document/product/457/36836#.E6.8C.87.E5.AE.9A.E6.8E.A5.E5.85.A5.E5.B1.82.E5.90.8E.E7.AB.AF).
#### service.cloud.tencent.com/direct-access
**Note:**
Adopt direct connection between the CLB and pods.
**Use case:**
For usage details, see [Using Services with LoadBalancer Directly Connected to Pods](https://intl.cloud.tencent.com/document/product/457/36837).

#### service.cloud.tencent.com/tke-service-config
**Note:**
Configure the CLB through tke-service-config.
**Use case:**
For usage details, see [Service CLB Configuration](https://intl.cloud.tencent.com/document/product/457/36834).

#### service.cloud.tencent.com/tke-service-config-auto
**Note:**
This annotation can be used to automatically create TkeServiceConfig.
**Use case:**
For usage details, see [Associated Actions Between Service and TkeServiceConfig](https://intl.cloud.tencent.com/document/product/457/36834#service-.E4.B8.8E-tkeserviceconfig-.E5.85.B3.E8.81.94.E8.A1.8C.E4.B8.BA).

#### service.kubernetes.io/loadbalance-nat-ipv6
**Note:**
This is a read-only annotation. During the creation of a NAT64 IPv6 CLB, the CLB IPv6 address will be displayed in the annotation.
**Use case:**
`service.kubernetes.io/loadbalance-nat-ipv6: "2402:4e00:1402:7200:0:9223:5842:2a44"`
#### service.kubernetes.io/loadbalance-type (to be deprecated soon)
**Note:**

- This annotation controls the type of automatically created CLBs: Classic CLB or CLB.
- Values: yunapi_clb (Classic CLB), classic (Classic CLB), yunapiv3_forward_clb (CLB)
- Default value: yunapiv3_forward_clb (CLB)
>! Except in special circumstances, we do not recommend using Classic CLBs because they are no longer upgrades, will soon be discontinued, and lack many features.

#### service.cloud.tencent.com/specify-protocol
**Note:**
You can use this annotation to configure TCP, UDP, TCP SSL, HTTP, or HTTPS for the specified listening port.
**Use case:**
For usage details, see [Service Extension Protocol](https://intl.cloud.tencent.com/document/product/457/39141).

#### service.kubernetes.io/service.extensiveParameters
**Note:**
Refer to [Creating a CLB Instance](https://intl.cloud.tencent.com/document/product/214/33841) to add custom parameters for creating a CLB instance.
**Use case:**
- Creating a NAT64 IPv6 instance: service.kubernetes.io/service.extensiveParameters: '{"AddressIPVersion":"IPV6"}' 
- Purchasing a CTCC CLB: service.kubernetes.io/service.extensiveParameters: '{"VipIsp":"CTCC"}'

