## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (ModifyLoadBalancers) is used to modify the load balancer of an auto scaling group.

* This API can specify a new load balancer configuration for the auto scaling group. The new configuration overwrites the original load balancer configuration.
* If you want to clear the load balancer for the auto scaling group, specify only the auto scaling group ID but not the specific load balancer when calling this API.
* This API modifies the load balancer of the auto scaling group and generate a scaling activity to asynchronously modify the load balancer of the existing instances.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: ModifyLoadBalancers |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoScalingGroupId | Yes | String | Auto scaling group ID |
| LoadBalancerIds.N | No | Array of String | Traditional load balancer ID list; currently, the maximum length is 5. You cannot specify both LoadBalancerIds and ForwardLoadBalancers at the same time |
| ForwardLoadBalancers.N | No | Array of [ForwardLoadBalancer](/document/api/377/20453#ForwardLoadBalancer) | Application load balancer list; currently, the maximum length is 5. You cannot specify both LoadBalancerIds and ForwardLoadBalancers at the same time |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| ActivityId | String | Scaling activity ID |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Changing the Load Balancer of an Auto Scaling Group to Classic Load Balancer lb-crhgatrf

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=ModifyLoadBalancers
&AutoScalingGroupId=asg-12wjuh0s
&LoadBalancerIds.0=lb-crhgatrf
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "ActivityId": "asa-67izy66g",
    "RequestId": "bd3c91e8-3051-4c02-ac58-54d47b9c9d63"
  }
}
```

### Sample 2. Changing the Load Balancer of an Auto Scaling Group to Application Load Balancer lb-23aejgcv with Listener lbl-ncw704sn

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=ModifyLoadBalancers
&AutoScalingGroupId=asg-12wjuh0s
&ForwardLoadBalancers.0.LoadBalancerId=lb-23aejgcv
&ForwardLoadBalancers.0.ListenerId=lbl-ncw704sn
&ForwardLoadBalancers.0.LocationId=loc-l3hmaev9
&ForwardLoadBalancers.0.TargetAttributes.0.Port=8080
&ForwardLoadBalancers.0.TargetAttributes.0.Weight=10
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "ActivityId": "asa-9asddelc",
    "RequestId": "8d78668d-61eb-456d-855b-f34f91371089"
  }
}
```

### Sample 3. Clearing the Load Balancer of an Auto Scaling Group

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=ModifyLoadBalancers
&AutoScalingGroupId=asg-12wjuh0s
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "ActivityId": "asa-rp63a5q8",
    "RequestId": "7de5a82f-b781-4302-b723-e7a879c20767"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyLoadBalancers)

### SDK

TencentCloud API 3.0 comes with SDKs that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameterValue.ForwardLb | Invalid application-based load balancer |
| InvalidParameterValue.LbProjectInconsistent | The load balancer is in a different project. |
| InvalidParameterValue.LbVpcInconsistent | The load balancer and the auto scaling group are in different VPCs. |
| ResourceNotFound.AutoScalingGroupIdNotFound | The auto scaling group does not exist |
| ResourceNotFound.LoadBalancerNotFound | The specified load balancer is not found |
| ResourceUnavailable.AutoScalingGroupInActivity | The auto scaling group is active. |
