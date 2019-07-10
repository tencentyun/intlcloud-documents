## 1. API Description

API request domain name: as.tencentcloudapi.com.

This API (ModifyAutoScalingGroup) modifies the specified scaling group.

Default API request frequency limit: 20 times/second.

Note: Because financial availability zones and non-financial availability zones are isolated. When specifying a financial availability zone (e.g., ap-shanghai-fsi) in the Region (a common parameter), you should also choose the financial availability zone preferably in the same region as that one specified in Region for the domain, such as as.ap-shanghai-fsi.tencentcloudapi.com.


## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/377/20426).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ModifyAutoScalingGroup |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| AutoScalingGroupId | Yes | String | Scaling group ID |
| AutoScalingGroupName | No | String | Name of the scaling group. The name must be unique in your account. The name can be up to 55 bytes in size and can contain Chinese characters, letters, numbers, underscores, separators ("-"), and decimal points. |
| DefaultCooldown | No | Integer | Default cooldown period in seconds; 300 by default |
| DesiredCapacity | No | Integer | Desired number of instances. The number should be no larger than the maximum number of instances and no smaller than minimum number of instances |
| LaunchConfigurationId | No | String | Launch configuration ID |
| MaxSize | No | Integer | Maximum number of instances; value range: 0-2,000. |
| MinSize | No | Integer | Minimum number of instances; value range: 0-2,000. |
| ProjectId | No | Integer | Project ID |
| SubnetIds.N | No | Array of String | Subnet ID List |
| TerminationPolicies.N | No | Array of String | Termination policy; currently, the maximum length is 1; value range: OLDEST_INSTANCE, NEWEST_INSTANCE. <br/><br><li> OLDEST_INSTANCE: The oldest instance in the scaling group will be terminated first. <br/><br><li> NEWEST_INSTANCE: The newest instance in the scaling group will be terminated first. |
| VpcId | No | String | VPC ID; if on a basic network, enter an empty string. When changing to a specific VPC ID, you need to specify the corresponding SubnetIds; when changing to a basic network, you need to specify the corresponding Zones. |
| Zones.N | No | Array of String | Availability zone list |
| RetryPolicy | No | String | Retry policy; valid values: IMMEDIATE_RETRY, INCREMENTAL_INTERVALS; IMMEDIATE_RETRY by default. <br/><br><li> IMMEDIATE_RETRY: Retry immediately. Retry again quickly in a short period of time. Continuous failures will not be retried after more than a certain number of times (5 times). <br/><br><li> INCREMENTAL_INTERVALS: Retry in incrementing intervals. As the number of consecutive failures increases, the intervals between each attempt increases gradually. Interval ranges from seconds to 1 day. |
| ZonesCheckPolicy | No | String | Availability zone verification policy; valid values: ALL, ANY; ANY by default. This will work when the resource-related fields (start configuration, availability zone, or subnet) of the scaling group are actually modified. <br/><br><li> ALL: The verification will success only if all availability zones (Zone) or subnets (SubnetId) are available; otherwise, an error will be returned. <br/><br><li> ANY: The verification will success if any availability zone (Zone) or subnet (SubnetId) is available; otherwise, an error will be returned. <br/><br/>Common reasons why an availability zone or subnet is unavailable include running out of CVM instances or CBS cloud disks in the availability zone, insufficient quota in the availability zone, or insufficient IPs in the subnet. <br/>If an availability zone or subnet in Zones/SubnetIds does not exist, a verification error will be returned regardless of the value of ZonesCheckPolicy. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues |

## 4. Sample

### Modifying the VPC Subnet Information of a Scaling Group

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=ModifyAutoScalingGroup
&AutoScalingGroupId=asg-ka0s0q80
&VpcId=vpc-hy436tmc
&SubnetIds.0=subnet-3tmerl37
&SubnetIds.1=subnet-b0vxjhot
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "RequestId": "c503ddc6-496c-44c9-8cec-e9f1c3f9c11c"
    }
}
```

### Modifying the Desired, Maximum, and Minimum Numbers of Instances in a Scaling Group

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=ModifyAutoScalingGroup
&AutoScalingGroupId=asg-ka0s0q80
&DesiredCapacity=3
&MaxSize=10
&MinSize=1
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "RequestId": "b41d8d30-21d4-412c-b7f3-53041879968c"
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyAutoScalingGroup)

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

The following error codes are API business logic-related. For other error codes,  see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameter.InScenario | The parameter is invalid in a specific scenario. |
| InvalidParameterValue.CvmError | Exception with CVM parameter validation. |
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
| LimitExceeded.MaxSizeLimitExceeded | The maximum number of instances exceeds the limit. |
| LimitExceeded.MinSizeLimitExceeded | The minimum number of instances is below the limit. |
| MissingParameter | Missing parameter |
| MissingParameter.InScenario | A parameter is missing in a specific scenario. |
| ResourceNotFound.AutoScalingGroupIdNotFound | The scaling group does not exist. |
| ResourceUnavailable.LaunchConfigurationStatusAbnormal | The launch configuration is exceptional. |
| ResourceUnavailable.ProjectInconsistent | Project inconsistency. |
