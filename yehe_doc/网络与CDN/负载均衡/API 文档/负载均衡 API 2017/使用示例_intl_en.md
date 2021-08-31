An example is given here to help you get started with CLB APIs. Before using the APIs, deploy TCP service on two CVMs and listen on port 80. If the service returns the “hello world” string, the deployment is successful. By creating a CLB instance, you can access CVM services through the CLB VIP.
## Purchasing a Public Network CLB Instance
To use CLB services, you need to purchase a public network CLB instance (with static IP). For more information on CLB instance purchase, use the [CreateLoadBalancer](https://intl.cloud.tencent.com/document/product/214/1254) API.

This example shows you how to create a public network CLB instance (with static IP). The `Action` field in the common request parameters of this API is `CreateLoadBalancer`. The list below contains the API request parameters.

| Parameter |  Description | Value |
|---------|---------|---------|
| loadBalancerType | CLB instance type. | **2**: public network CLB instance, the service of which is accessed via a public network. |


By combining common request parameters and API request parameters, you can get the final request as follows:

```
https://lb.api.qcloud.com/v2/index.php?Action=CreateLoadBalancer
&Region=ap-guangzhou
&Timestamp=1465750149
&Nonce=46364
&SecretId=AKIDxxxxugEY
&Signature=5umi9gUWpTTyk18V2g%2FYi56hqls%3D
&loadBalancerType=2
```
Response of the request is as follows:

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "requestId": 3901941,
    "dealIds": [
        "3901941"
    ],
    "unLoadBalancerIds": {
        "3901941": [
            "lb-cjcymkw5"
        ]
    }
}
```
Where, `lb-cjcymkw5` is the unique ID of the CLB instance you just purchased. Next, use the [DescribeLoadBalancers](https://intl.cloud.tencent.com/document/product/214/1261) API to query whether the instance has been successfully created.

## Creating a CLB Listener
This example shows you how to create a CLB listener with the unique ID of the CLB instance. For more information on the CLB listener creation, use the [CreateLoadBalancerListeners](https://intl.cloud.tencent.com/document/product/214/1255) API.

In this example, the table below lists the API request parameters.

| Parameter |  Description | Value |
|---------|---------|---------|
| loadBalancerId | Unique ID of the CLB instance | This example uses the unique ID of the instance you’ve just created, i.e. `lb-cjcymkw5` |
| listeners.0.loadBalancerPort | Listening port of the CLB listener. | 80 |
| listeners.0.instancePort | Listening port on real server of the CLB instance. | 80 |
| listeners.0.protocol | Protocol listened by the CLB listener. 1: HTTP; 2: TCP; 3: UDP; 4: HTTPS | This example uses `2: TCP` |
| listeners.0.healthSwitch | Whether to enable the health check for the CLB listener. 1: enable; 0: disable. The health check is enabled by default. | This example uses `1: enable` |
| listeners.0.listenerName | Name of the CLB listener. This field is optional. Default value will be used if it is left empty. |This example uses `listenerTest` |


By combining common request parameters and API request parameters, you can get the final request as follows:

```
https://lb.api.qcloud.com/v2/index.php?Action=CreateLoadBalancerListeners
&Region=ap-guangzhou
&Timestamp=1465750149
&Nonce=46364
&SecretId=AKIDxxxxugEY
&Signature=5umi9gUWpTTyk18V2g%2FYi56hqls%3D
&loadBalancerId=lb-cjcymkw5
&listeners.0.loadBalancerPort=80
&listeners.0.instancePort=80
&listeners.0.protocol=2
&listeners.0.healthSwitch=1
&listeners.0.listenerName=listenerTest
  
```
Response of the request is as follows:
```
{
  "code" : 0,
  "message" : "",
  "codeDesc": "Success",
  "requestId" : 12354
}
```
To query the execution result of the task with the request ID, use the asynchronous [DescribeLoadBalancersTaskResult](https://intl.cloud.tencent.com/document/api/214/4007) API.

## Binding Real Server to the CLB Instance
You need to bind CVM to the CLB instance after creating the listener. For more information on the binding method, use the [RegisterInstancesWithLoadBalancer](https://intl.cloud.tencent.com/document/product/214/1265) API.

This example shows you how to bind two CVMs (with the unique ID of `ins-5678test` and `ins-1234test` respectively) on the CLB instance. The `Action` field in the common request parameters of this API is `RegisterInstancesWithLoadBalancer`. The list below contains the API request parameters.

| Parameter | Description | Value |
|---------|---------|---------|
| loadBalancerId | Unique ID of the CLB instance. | This example uses the unique ID of the instance you’ve just created: `lb-abcdefgh` |
| backends.0.instanceId | Unique ID of the CVM bound to the CLB instance. | This example uses the unique ID of the first CVM:`ins-5678test` |
| backends.0.weight | Weight of the CVM bound to the CLB instance. | This example uses the default value `10` |
| backends.1.instanceId | Unique ID of the CVM bound to the load balancer instance | This example uses the unique ID of the second CVM: `ins-1234test` |
| backends.1.weight | Weight of the CVM bound to the CLB instance. | This example uses the default value `10` |


By combining common request parameters and API request parameters, you can get the final request as follows:
```
https://lb.api.qcloud.com/v2/index.php?Action=RegisterInstancesWithLoadBalancer
&Region=ap-guangzhou
&Timestamp=1465750149
&Nonce=46364
&SecretId=AKIDxxxxugEY
&Signature=5umi9gUWpTTyk18V2g%2FYi56hqls%3D
&loadBalancerId=lb-cjcymkw5
&backends.0.instanceId=ins-5678test
&backends.0.weight=10
&backends.1.instanceId=ins-1234test
&backends.1.weight=10
```
Response of the request is as follows:
```
{
  "code" : 0,
  "message" : "",
  "codeDesc": "Success",
  "requestId" : 1234
}
```
To query the execution result of the task with the request ID, use the asynchronous [DescribeLoadBalancersTaskResult](https://intl.cloud.tencent.com/document/api/214/4007) API.

## Querying and Using the CLB Instance
This example shows you how to query the VIP or domain name of the CLB instance. For more information on the query method, use the [DescribeLoadBalancers](https://intl.cloud.tencent.com/document/product/214/1261) API.

The `Action` field in the common request parameters of the API is `DescribeLoadBalancers`. The list below contains the API request parameters.

| Parameter | Description | Value |
|---------|---------|---------|
| loadBalancerIds.0 | Unique ID of the CLB instance. | This example uses the unique ID of the instance you’ve just created: `lb-cjcymkw5` |

By combining common request parameters and API request parameters, you can get the final request as follows:
```
https://lb.api.qcloud.com/v2/index.php?Action=DescribeLoadBalancers
&Region=ap-guangzhou
&Timestamp=1465750149
&Nonce=46364
&SecretId=AKIDxxxxugEY
&Signature=5umi9gUWpTTyk18V2g%2FYi56hqls%3D
&loadBalancerIds.0=lb-cjcymkw5
```

Response

```
{
	"code": 0,
	"message": "",
	"codeDesc": "Success",
	"loadBalancerSet": [{
		"loadBalancerId": "lb-cjcymkw5",
		"unLoadBalancerId": "lb-cjcymkw5",
		"loadBalancerName": "59b25ffb-0",
		"loadBalancerType": 2,
		"domain": "20de02-0.gz.1251000011.clb.myqcloud.com",
		"loadBalancerVips": [
			"119.28.168.196"
		],
		"status": 1,
		"createTime": "2017-09-08 17:16:42",
		"statusTime": "2017-09-20 13:37:55",
		"vpcId": 0,
		"uniqVpcId": "",
		"subnetId": 0,
		"projectId": 1005621,
		"forward": 0,
		"snat": false,
		"openBgp": 0,
		"isolation": 0,
		"log": ""
	}],
	"totalCount": 1
}
```

As the query results suggest, you can use the VIP `119.28.168.196` or domain name `20de02-0.gz.1251000011.clb.myqcloud.com` of the CLB instance to forward the request to the associated backend CVMs according to the rule of CLB listener, thereby balancing the load.
 
