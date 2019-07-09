## 1. API Description

API request domain name: as.tencentcloudapi.com.

This API (CreateAutoScalingGroup) creates a scaling group.

Default API request frequency limit: 20 times/second.

Note: Because financial availability zones and non-financial availability zones are isolated. When specifying a financial availability zone (e.g., ap-shanghai-fsi) in the Region (a common parameter), you should also choose the financial availability zone preferably in the same region as that one specified in Region for the domain, such as as.ap-shanghai-fsi.tencentcloudapi.com.


## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/377/20426).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: CreateAutoScalingGroup |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| AutoScalingGroupName | No String | Name of the scaling group. The name must be unique in your account. The name can be up to 55 bytes in size and can contain Chinese characters, letters, numbers, underscores, separators ("-"), and decimal points. |
| LaunchConfigurationId | Yes | String | Launch configuration ID |
| MaxSize | Yes | Integer | Maximum number of instances; value range: 0-2,000. |
| MinSize | Yes | Integer | Minimum number of instances; value range: 0-2,000. |
| VpcId | Yes | String | VPC ID; if on a basic network, enter an empty string |
| DefaultCooldown | No | Integer | Default cooldown period in seconds; 300 by default |
| DesiredCapacity | No | Integer | Desired number of instances between the minimum number of instances and maximum number of instances |
| LoadBalancerIds.N | No | Array of String | Classic load balancer ID list; currently, the maximum length is 1. You cannot specify both LoadBalancerIds and ForwardLoadBalancers at the same time |
| ProjectId | No | Integer | Project ID |
| ForwardLoadBalancers.N | No | Array of [ForwardLoadBalancer](/document/api/377/20453#ForwardLoadBalancer) | Application load balancer list; currently, the maximum length is 1. You cannot specify both LoadBalancerIds and ForwardLoadBalancers at the same time |
| SubnetIds.N | No | Array of String | Subnet ID list. A subnet must be specified in the VPC scenario |
| TerminationPolicies.N | No | Array of String | Termination policy; currently, the maximum length is 1; value range: OLDEST_INSTANCE, NEWEST_INSTANCE; OLDEST_INSTANCE by default. <br/><br><li> OLDEST_INSTANCE: The oldest instance in the scaling group will be terminated first. <br/><br><li> NEWEST_INSTANCE: The newest instance in the scaling group will be terminated first. |
| Zones.N | No | Array of String | Availability zone list. Availability zone must be specified in a basic network scenario |
| RetryPolicy | No | String | Retry policy; value range: IMMEDIATE_RETRY, INCREMENTAL_INTERVALS; IMMEDIATE_RETRY by default. <br/><br><li> IMMEDIATE_RETRY: Retry immediately. Retry again quickly in a short period of time. Continuous failures will not be retried after more than a certain number of times (5 times) <br/><br><li> INCREMENTAL_INTERVALS: Retry in incrementing intervals. As the number of consecutive failures increases, the intervals between each attempt increases gradually. Interval ranges from seconds to 1 day. |
| ZonesCheckPolicy | No | String | Availability zone verification policy; valid values: ALL, ANY; ANY by default. This will work when the resource-related fields (start configuration, availability zone, or subnet) of the scaling group are actually modified. <br/><br><li> ALL: The verification will success only if all availability zones (Zone) or subnets (SubnetId) are available; otherwise, an error will be returned. <br/><br><li> ANY: The verification will success if any availability zone (Zone) or subnet (SubnetId) is available; otherwise, an error will be returned. <br/><br/>Common reasons why an availability zone or subnet is unavailable include running out of CVM instances or CBS cloud disks in the availability zone, insufficient quota in the availability zone, or insufficient IPs in the subnet. <br/>If an availability zone or subnet in Zones/SubnetIds does not exist, a verification error will be returned regardless of the value of ZonesCheckPolicy. |
 
## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| AutoScalingGroupId | String | Scaling group ID|
| RequestId | String |The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues |

## 4. Sample

### Creating a Scaling Group

This is to create a scaling group in a VPC and configure a layer-7 load balancer.

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

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CreateAutoScalingGroup)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameter.InScenario | The parameter is invalid in a specific scenario. |
| InvalidParameterValue.CvmError | Exception with CVM parameter validation. |
| InvalidParameterValue.ForwardLb | An application load balancer is incorrectly specified. |
| InvalidParameterValue.GroupNameDuplicate | The scaling group name already exists. |
| InvalidParameterValue.InvalidScheduledActionNameIncludeIllegalChar | The specified launch configuration was not found. |
| InvalidParameterValue.LbProjectInconsistent | The load balancer is in a different project. |
| InvalidParameterValue.LbVpcInconsistent | The load balancer and the scaling group are in different VPCs. |
| InvalidParameterValue.LimitExceeded | The value exceeds the limit. |
| InvalidParameterValue.OnlyVpc | The account only supports VPCs. |
| InvalidParameterValue.Range | The value is outside the specified range. |
| InvalidParameterValue.Size | The value of maximum, minimum, or the desired number of instances is invalid. |
| InvalidParameterValue.SubnetIds | The subnet information is invalid. |
| InvalidParameterValue.TooLong | Too many values. |
| LimitExceeded | Quota is exceeded. |
| LimitExceeded.AutoScalingGroupLimitExceeded | The number of scaling groups exceeds the limit. |
| LimitExceeded.MaxSizeLimitExceeded | The maximum number of instances exceeds the limit. |
| LimitExceeded.MinSizeLimitExceeded | The minimum number of instances is below the limit. |
| MissingParameter.InScenario | A parameter is missing in a specific scenario. |
| ResourceNotFound.LoadBalancerNotFound | The specified load balancer was not found. |
| ResourceUnavailable.LaunchConfigurationStatusAbnormal | The launch configuration is exceptional. |
| ResourceUnavailable.ProjectInconsistent | Project inconsistency. |
