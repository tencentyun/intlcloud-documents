## General APIs
| API Name | Description |
|---------|---------|
| [DescribeLoadBalancersTaskResult](https://intl.cloud.tencent.com/document/product/214/4007) | Queries the result of executing an asynchronous CLB API. |
| [CreateLoadBalancer](https://intl.cloud.tencent.com/document/product/214/1254) | Purchases a CLB instance.|
| [InquiryLBPriceAll](https://intl.cloud.tencent.com/document/product/214/1328) | Queries the prices of CLB instances. |
| [DescribeLoadBalancers](https://intl.cloud.tencent.com/document/product/214/1261) | Queries the list of CLB instances. |
| [DeleteLoadBalancers](https://intl.cloud.tencent.com/document/product/214/1257) | Deletes a CLB instance. |
| [GetMonitorData](https://intl.cloud.tencent.com/document/product/214/8801) | Queries the monitoring data of the CLB instance. |
| [ReplaceCert](https://intl.cloud.tencent.com/document/product/214/6045)| Replaces the certificate of the CLB instance. |
| [GetCertListWithLoadBalancer](https://intl.cloud.tencent.com/document/product/214/6046) | Queries the information of the CLB instance associated with the certificate. |
| [DescribeLoadBalancerLog](https://intl.cloud.tencent.com/document/product/214/12235) | Queries the CLB Layer-7 log in COS.|
| [CloneLB](https://intl.cloud.tencent.com/document/product/214/37069) | Clones a CLB instance. |


## Classic CLB APIs

#### Instance APIs

| API Name | Description |
|---------| ---------|
| [ModifyLoadBalancerAttributes](https://intl.cloud.tencent.com/document/product/214/1263) | Modifies the attributes of the specified CLB instance, including the CLB instance name. |

### Listener APIs

| API Name | Description |
|---------| ---------|
| [CreateLoadBalancerListeners](https://intl.cloud.tencent.com/document/product/214/1255) | Creates a CLB listener for the specified CLB instance. A CLB listener provides the protocols for the requests to be forwarded, as well as ports and health check policies. |
| [DescribeLoadBalancerListeners](https://intl.cloud.tencent.com/document/product/214/1260) | Returns the list of listeners for the specified CLB instances, including unique ID, name, port health check policy and other information of listeners. |
| [DeleteLoadBalancerListeners](https://intl.cloud.tencent.com/document/product/214/1256) | Deletes a set of listeners for the specified CLB instance. |
| [ModifyLoadBalancerListener](https://intl.cloud.tencent.com/document/product/214/3601) | Modifies the attributes of the listener for the CLB instance, including the name, health check policy and other information of the listener. |

### Real server APIs

| API Name | Description |
| ---------| ---------|
| [RegisterInstancesWithLoadBalancer](https://intl.cloud.tencent.com/document/product/214/1265) | Binds a set of specified CVMs to the specified CLB instance. |
| [DescribeLoadBalancerBackends](https://intl.cloud.tencent.com/document/product/214/1259) | Obtains the list of CVMs bound to the CLB instance identified by *LoadBalanceId*. |
| [ModifyLoadBalancerBackends](https://intl.cloud.tencent.com/document/product/214/1264) | Modifies the weight of a set of CVMs bound to the CLB instance.|
| [DeregisterInstancesFromLoadBalancer](https://intl.cloud.tencent.com/document/product/214/1258) | Unbinds CVMs from the CLB instance. |

### Health check APIs

| API Name | Description |
|---------|---------|
| [DescribeLBHealthStatus](https://intl.cloud.tencent.com/document/product/214/1326) | Queries the health status of a CLB instance. |


## CLB APIs
>? The following CLB APIs have been updated to version 3.0, which is more standardized with significantly reduced access latency. The legacy APIs will be deprecated and is currently not displayed on the left sidebar. We recommend using [CLB API 3.0](https://intl.cloud.tencent.com/document/product/214/36412).

### CLB instance APIs

| API Name | Description |
|---------| ---------|
| [ModifyForwardLBName](https://intl.cloud.tencent.com/document/product/214/13295) | Modifies the name of a CLB instance. |


### Listener APIs

| API Name | Description |
|---------| ---------|
| [DescribeForwardLBListeners](https://intl.cloud.tencent.com/document/product/214/9005) | Queries the CLB listener. |
| [CreateForwardLBSeventhLayerListeners](https://intl.cloud.tencent.com/document/product/214/9000) | Creates a Layer-7 listener. |
| [CreateForwardLBFourthLayerListeners](https://intl.cloud.tencent.com/document/product/214/9001) | Creates a Layer-4 listener. |
| [ModifyForwardLBFourthListener](https://intl.cloud.tencent.com/document/product/214/8998) | Modifies the attributes of the CLB Layer-4 listener. |
| [ModifyForwardLBSeventhListener](https://intl.cloud.tencent.com/document/product/214/8997) | Modifies the attributes of the CLB Layer-7 listener. |
| DeleteForwardLBListener | Deletes a CLB listener.|

### Forwarding rule APIs

| API Name | Description |
|---------| ---------|
| [CreateForwardLBListenerRules](https://intl.cloud.tencent.com/document/product/214/9011) | Creates forwarding rules of the CLB Layer-7 listener. |
| [ModifyForwardLBRulesDomain](https://intl.cloud.tencent.com/document/product/214/9007) | Modifies the domain name under the CLB Layer-7 listener. |
| [ModifyLoadBalancerRulesProbe](https://intl.cloud.tencent.com/document/product/214/9008) | Modifies the health check and forwarding path for the forwarding rules of the CLB Layer-7 listener. |
| [DeleteForwardLBListenerRules](https://intl.cloud.tencent.com/document/product/214/9012) | Deletes the forwarding rules of the CLB Layer-7 listener. |

### CVM APIs

| API Name | Description |
|---------| ---------|
| DescribeForwardLBBackends | Queries the list of CVMs bound to the CLB instance. |
| [RegisterInstancesWithForwardLBFourthListener](https://intl.cloud.tencent.com/document/product/214/8989) | Binds a CVM to the forwarding rules of the CLB Layer-4 listener. |
| [RegisterInstancesWithForwardLBSeventhListener](https://intl.cloud.tencent.com/document/product/214/8988) | Binds a CVM to the forwarding rules of the CLB Layer-7 listener. |
| [ModifyForwardFourthBackendsWeight](https://intl.cloud.tencent.com/document/product/214/8981) | Modifies the weight of a CVM bound to the Layer-4 listener. |
| [ModifyForwardSeventhBackends](https://intl.cloud.tencent.com/document/product/214/8978) | Modifies the weight of a CVM bound to the Layer-7 listener. |
| [ModifyForwardFourthBackendsPort](https://intl.cloud.tencent.com/document/product/214/8984) | Modifies the port of a CVM bound to the Layer-4 listener. |
| [ModifyForwardSeventhBackendsPort](https://intl.cloud.tencent.com/document/product/214/8979) | Modifies the port of a CVM bound to the Layer-7 listener. |
| [DeregisterInstancesFromForwardLBFourthListener](https://intl.cloud.tencent.com/document/product/214/8992) | Unbinds a CVM from the CLB Layer-4 listener. |
| [DeregisterInstancesFromForwardLB](https://intl.cloud.tencent.com/document/product/214/8991) | Unbinds a CVM from the forwarding rules of the CLB Layer-7 listener. |

### Health check APIs

| API Name | Description |
|---------| ---------|
| [DescribeForwardLBHealthStatus] | Queries the health check of a CLB instance. |

### Redirection APIs

| API Name | Description |
|---------| ---------|
| [DescribeRewrite](https://intl.cloud.tencent.com/document/product/214/9016) | Queries the redirection relationship of the CLB instance. |
| [DeleteRewrite](https://intl.cloud.tencent.com/document/product/214/9014) | Deletes the redirection relationship of the CLB instance. |
| [ManualRewrite](https://intl.cloud.tencent.com/document/product/214/9015) | Adds the redirection relationship to a CLB instance manually. |
| [AutoRewrite](https://intl.cloud.tencent.com/document/product/214/9017) | Generates the redirection relationship for a CLB instance automatically. |




