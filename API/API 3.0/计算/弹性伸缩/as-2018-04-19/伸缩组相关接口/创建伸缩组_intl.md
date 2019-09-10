## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (CreateAutoScalingGroup) is used to create an auto scaling group.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: CreateAutoScalingGroup |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoScalingGroupName | Yes | String | Auto scaling group name, which is unique in your account. The name can only contain letters, numbers, underscores, hyphens ("-") and decimal points, with a length of not more than 55 characters. |
| LaunchConfigurationId | Yes | String | Launch configuration ID |
| MaxSize | Yes | Integer | Maximum number of instances. Value range: 0-2000. |
| MinSize | Yes | Integer | Minimum number of instances. Value range: 0-2000. |
| VpcId | Yes | String | VPC ID; if on a basic network, enter an empty string |
| DefaultCooldown | No | Integer | Default cooldown period in seconds. Default value: 300 |
| DesiredCapacity | No | Integer | Desired number of instances. The number should be no larger than the maximum and no smaller than minimum number of instances |
| LoadBalancerIds.N | No | Array of String | Traditional load balancer ID list; currently, the maximum length is 5. You cannot specify both LoadBalancerIds and ForwardLoadBalancers at the same time |
| ProjectId | No | Integer | Project ID |
| ForwardLoadBalancers.N | No | Array of [ForwardLoadBalancer](/document/api/377/20453#ForwardLoadBalancer) | Application load balancer list; currently, the maximum length is 5. You cannot specify both LoadBalancerIds and ForwardLoadBalancers at the same time |
| SubnetIds.N | No | Array of String | Subnet ID list. A subnet must be specified in the VPC scenario |
| TerminationPolicies.N | No | Array of String | Termination policy; currently, the maximum length is 1. Value range: OLDEST_INSTANCE, NEWEST_INSTANCE. Default value: OLDEST_INSTANCE. <br/><br><li> OLDEST_INSTANCE: The oldest instance in the auto scaling group will be terminated first. <br/><br><li> NEWEST_INSTANCE: The newest instance in the auto scaling group will be terminated first.
| Zones.N | No | Array of String | Availability zone list. Availability zone must be specified in a basic network scenario |
| RetryPolicy | No | String | Retry policy. Value range: IMMEDIATE_RETRY, INCREMENTAL_INTERVALS, NO_RETRY. Default value: IMMEDIATE_RETRY. <br/><br><li> IMMEDIATE_RETRY: Retrying immediately in a short period of time and stopping after a number of consecutive failures (5). <br/><br><li> INCREMENTAL_INTERVALS: Retrying at incremental intervals, i.e., as the number of consecutive failures increases, the retry interval gradually increases, ranging from one second to one day. <br/><br><li> NO_RETRY: No retry until a call or alarm message is received again. |
| ZonesCheckPolicy | No | String | Availability zone verification policy. Value range: ALL, ANY. Default value: ANY. <br/><br><li> ALL: The verification will succeed only if all availability zones (Zone) or subnets (SubnetId) are available; otherwise, an error will be reported. <br/><br><li> ANY: The verification will succeed if any availability zone (Zone) or subnet (SubnetId) is available; otherwise, an error will be reported. <br/><br/>Common reasons why an availability zone or subnet is unavailable include stock-out of CVM instances or CBS cloud disks in the availability zone, insufficient quota in the availability zone, or insufficient IPs in the subnet. <br/>If an availability zone or subnet in Zones/SubnetIds does not exist, a verification error will be reported regardless of the value of ZonesCheckPolicy. |
| Tags.N | No | Array of [Tag](/document/api/377/20453#Tag) | Tag description list. This parameter is used to bind a tag to an auto scaling group as well as the corresponding resource instances. |
| ServiceSettings | No | [ServiceSettings](/document/api/377/20453#ServiceSettings) | Service settings such as unhealthy instance replacement. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| AutoScalingGroupId | String | Auto scaling group ID |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Creating an Auto Scaling Group

This is to create an auto scaling group in a VPC and configure a layer-7 load balancer.

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CreateAutoScalingGroup
&AutoScalingGroupName=asg-vpc-7layer-lb
&DefaultCooldown=300
&DesiredCapacity=0
&LaunchConfigurationId=asc-7vucy6ae
&MaxSize=10
&MinSize=0
&ProjectId=0
&VpcId=vpc-hy436tmc
&SubnetIds.0=subnet-3tmerl37
&SubnetIds.1=subnet-b0vxjhot
&TerminationPolicies.0=OLDEST_INSTANCE
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
    "AutoScalingGroupId": "asg-nkdwoui0",
    "RequestId": "a5d66fed-85b9-4f43-8243-597337ba896e"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CreateAutoScalingGroup)

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
| InternalError | Internal error. |
| InvalidParameter.InScenario | Invalid parameter in specific scenarios |
| InvalidParameterValue.CvmError | Verification exception occurred with CVM parameter |
| InvalidParameterValue.ForwardLb | Invalid application-based load balancer |
| InvalidParameterValue.GroupNameDuplicated | The auto scaling group name already exists. |
| InvalidParameterValue.InvalidScheduledActionNameIncludeIllegalChar | The specified launch configuration was not found. |
| InvalidParameterValue.LbProjectInconsistent | The load balancer is in a different project. |
| InvalidParameterValue.LbVpcInconsistent | The load balancer and the auto scaling group are in different VPCs. |
| InvalidParameterValue.LimitExceeded | The value exceeds the limit. |
| InvalidParameterValue.OnlyVpc | Only VPC is supported for the current account |
| InvalidParameterValue.Range | Parameter value is out of the specified range |
| InvalidParameterValue.Size | The value of maximum, minimum, or desired number of instances in the auto scaling group is invalid. |
| InvalidParameterValue.SubnetIds | Invalid subnet information. |
| InvalidParameterValue.TooLong | Too many parameter values. |
| LimitExceeded | Quota is exceeded. |
| LimitExceeded.AutoScalingGroupLimitExceeded | The number of auto scaling groups exceeds the limit |
| LimitExceeded.MaxSizeLimitExceeded | The maximum number of instances exceeds the upper limit |
| LimitExceeded.MinSizeLimitExceeded | The minimum number of instances falls below the lower limit |
| MissingParameter.InScenario | A parameter is missing in specific scenarios |
| ResourceNotFound.LoadBalancerNotFound | The specified load balancer is not found |
| ResourceUnavailable.LaunchConfigurationStatusAbnormal | Launch configuration is exceptional |
| ResourceUnavailable.ProjectInconsistent | Inconsistent projects |
