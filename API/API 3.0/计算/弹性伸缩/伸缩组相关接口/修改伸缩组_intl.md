## 1. API Description

Domain name for API request: as.tencentcloudapi.com.

This API (ModifyAutoScalingGroup) is used to modify a scaling group.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter `Region` is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​ used for this API: ModifyAutoScalingGroup |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoScalingGroupId | Yes | String | Scaling group ID |
| AutoScalingGroupName | No | String | Scaling group name, which is unique in your account. The name can contain up to 55 characters, including letters, numbers, underscores, hyphens ("-") and decimal points. |
| DefaultCooldown | No | Integer | Default cooldown period (in sec). It is 300 by default. |
| DesiredCapacity | No | Integer | Desired number of instances, which is between the minimum and maximum numbers of instances. |
| LaunchConfigurationId | No | String | Launch configuration ID |
| MaxSize | No | Integer | Maximum number of instances. Value range: 0-2000. |
| MinSize | No | Integer | Minimum number of instances. Value range: 0-2000. |
| ProjectId | No | Integer | Project ID |
| SubnetIds.N | No | Array of String | Subnet ID list |
| TerminationPolicies.N | No | Array of String | Termination policies. The number of policies is limited to 1. |
| VpcId | No | String | VPC ID. Leave this field blank if you want to use basic network. While changing the network of the scaling group to a VPC, you should also specify `SubnetIds`. While changing the network to basic network, you need to specify `Zones` |
| Zones.N | No | Array of String | List of availability zones |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Modify the VPC subnet information of a scaling group

#### Input example

```
https://as.tencentcloudapi.com/?Action=ModifyAutoScalingGroup
&AutoScalingGroupId=asg-ka0s0q80
&VpcId=vpc-hy436tmc
&SubnetIds.0=subnet-3tmerl37
&SubnetIds.1=subnet-b0vxjhot
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "RequestId": "c503ddc6-496c-44c9-8cec-e9f1c3f9c11c"
  }
}
```

### Example 2 Modify the desired, maximum and minimum numbers of instances

#### Input example

```
https://as.tencentcloudapi.com/?Action=ModifyAutoScalingGroup
&AutoScalingGroupId=asg-ka0s0q80
&DesiredCapacity=3
&MaxSize=10
&MinSize=1
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "RequestId": "b41d8d30-21d4-412c-b7f3-53041879968c"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyAutoScalingGroup)

### SDK

Cloud API 3.0 comes with the software development kit (SDK) that supports multiple programming languages and makes it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameter.InScenario | Invalid parameter in specific scenarios |
| InvalidParameterValue.CvmError | Verification exception occurred with CVM parameter |
| InvalidParameterValue.GroupNameDuplicate | Duplicate scaling group name |
| InvalidParameterValue.LaunchConfigurationNotFound | The specified launch configuration is not found |
| InvalidParameterValue.LbProjectInconsistent | Inconsistent load balancer projects |
| InvalidParameterValue.LbVpcInconsistent | The VPC of the load balancer is different from that of the scaling group |
| InvalidParameterValue.LimitExceeded | Parameter value exceeds the limit |
| InvalidParameterValue.OnlyVpc | Only VPC is supported for the current account |
| InvalidParameterValue.Range | Parameter value is out of the specified range |
| InvalidParameterValue.Size | The desired, maximum and minimum numbers of instances are invalid |
| InvalidParameterValue.SubnetIds | Invalid subnet information |
| InvalidParameterValue.TooLong | Too many parameter values |
| LimitExceeded | Quota limit is exceeded |
| LimitExceeded.MaxSizeLimitExceeded | The maximum number of instances exceeds the upper limit |
| LimitExceeded.MinSizeLimitExceeded | The minimum number of instances falls below the lower limit |
| MissingParameter | A parameter is missing |
| MissingParameter.InScenario | A parameter is missing in specific scenarios |
| ResourceNotFound.AutoScalingGroupIdNotFound | The scaling group does not exist |
| ResourceUnavailable.LaunchConfigurationStatusAbnormal | Launch configuration is exceptional |
| ResourceUnavailable.ProjectInconsistent | Inconsistent projects |

