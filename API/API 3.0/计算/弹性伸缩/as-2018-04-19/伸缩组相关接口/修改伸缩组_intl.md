## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (ModifyAutoScalingGroup) is used to modify an auto scaling group.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: ModifyAutoScalingGroup |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoScalingGroupId | Yes | String | Auto scaling group ID |
| AutoScalingGroupName | No | String | Auto scaling group name, which is unique in your account. The name can only contain letters, numbers, underscores, hyphens ("-") and decimal points, with a length of not more than 55 characters. |
| DefaultCooldown | No | Integer | Default cooldown period in seconds. Default value: 300 |
| DesiredCapacity | No | Integer | Desired number of instances. The number should be no larger than the maximum and no smaller than minimum number of instances |
| LaunchConfigurationId | No | String | Launch configuration ID |
| MaxSize | No | Integer | Maximum number of instances. Value range: 0-2000. |
| MinSize | No | Integer | Minimum number of instances. Value range: 0-2000. |
| ProjectId | No | Integer | Project ID |
| SubnetIds.N | No | Array of String | Subnet ID List |
| TerminationPolicies.N | No | Array of String | Termination policy; currently, the maximum length is 1. Value range: OLDEST_INSTANCE, NEWEST_INSTANCE. <br/><br><li> OLDEST_INSTANCE: The oldest instance in the auto scaling group will be terminated first. <br/><br><li> NEWEST_INSTANCE: The newest instance in the auto scaling group will be terminated first. |
| VpcId | No | String | VPC ID. This field is left empty for basic networks. You need to specify SubnetIds when modifying the network of the auto scaling group to a VPC with a specified VPC ID. Specify Zones when modifying the network to a basic network. |
| Zones.N | No | Array of String | Availability zone list |
| RetryPolicy | No | String | Retry policy. Value range: IMMEDIATE_RETRY, INCREMENTAL_INTERVALS, NO_RETRY. Default value: IMMEDIATE_RETRY. <br/><br><li> IMMEDIATE_RETRY: Retrying immediately in a short period of time and stopping after a number of consecutive failures (5). <br/><br><li> INCREMENTAL_INTERVALS: Retrying at incremental intervals, i.e., as the number of consecutive failures increases, the retry interval gradually increases, ranging from one second to one day. <br/><br><li> NO_RETRY: No retry until a call or alarm message is received again. |
| ZonesCheckPolicy | No | String | Availability zone verification policy. Value range: ALL, ANY. Default value: ANY. This will work when the resource-related fields (launch configuration, availability zone, or subnet) of the auto scaling group are actually modified. <br/><br><li> ALL: The verification will succeed only if all availability zones (Zone) or subnets (SubnetId) are available; otherwise, an error will be reported. <br/><br><li> ANY: The verification will succeed if any availability zone (Zone) or subnet (SubnetId) is available; otherwise, an error will be reported. <br/><br/>Common reasons why an availability zone or subnet is unavailable include stock-out of CVM instances or CBS cloud disks in the availability zone, insufficient quota in the availability zone, or insufficient IPs in the subnet. <br/>If an availability zone or subnet in Zones/SubnetIds does not exist, a verification error will be reported regardless of the value of ZonesCheckPolicy. |
| ServiceSettings | No | [ServiceSettings](/document/api/377/20453#ServiceSettings) | Service settings such as unhealthy instance replacement. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Modifying the VPC Subnet Information of an Auto Scaling Group

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

### Sample 2. Modifying the Desired, Maximum, and Minimum Numbers of Instances in an Auto Scaling Group

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

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyAutoScalingGroup)

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
| InvalidParameter.InScenario | Invalid parameter in specific scenarios |
| InvalidParameterValue.CvmError | Verification exception occurred with CVM parameter |
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
| LimitExceeded.MaxSizeLimitExceeded | The maximum number of instances exceeds the upper limit |
| LimitExceeded.MinSizeLimitExceeded | The minimum number of instances falls below the lower limit |
| MissingParameter | Missing parameter. |
| MissingParameter.InScenario | A parameter is missing in specific scenarios |
| ResourceNotFound.AutoScalingGroupIdNotFound | The auto scaling group does not exist |
| ResourceUnavailable.LaunchConfigurationStatusAbnormal | Launch configuration is exceptional |
| ResourceUnavailable.ProjectInconsistent | Inconsistent projects |
