## 1. API Description

Domain name for API request: as.tencentcloudapi.com.

This API (CreateAutoScalingGroup) is used to create a scaling group.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter `Region` is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​ used for this API: CreateAutoScalingGroup |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoScalingGroupName | Yes | String | Scaling group name, which is unique in your account. The name can only contain letters, numbers, underscores, hyphens ("-") and decimal points, with a length of not more than 55 characters. |
| LaunchConfigurationId | Yes | String | Launch configuration ID |
| MaxSize | Yes | Integer | Maximum number of instances. Value range: 0-2000. |
| MinSize | Yes | Integer | Minimum number of instances. Value range: 0-2000. |
| VpcId | Yes | String | VPC ID. This field is left empty for basic networks |
| DefaultCooldown | No | Integer | Default cooldown period (in sec). It is 300 by default. |
| DesiredCapacity | No | Integer | Desired number of instances, which is between the minimum and maximum numbers of instances. |
| LoadBalancerIds.N | No | Array of String | List of traditional load balancer IDs. The ID is limited to 1 character. You cannot specify both LoadBalancerIds and ForwardLoadBalancers. |
| ProjectId | No | Integer | Project ID |
| ForwardLoadBalancers.N | No | Array of [ForwardLoadBalancer](/document/api/377/20453#ForwardLoadBalancer) | List of application-based load balancers. The ID is limited to 1 character. You cannot specify both LoadBalancerIds and ForwardLoadBalancers. |
| SubnetIds.N | No | Array of String | List of subnet IDs. You must specify subnets when creating a scaling group under a VPC. |
| TerminationPolicies.N | No | Array of String | Termination policies. Only one is allowed now. |
| Zones.N | No | Array of String | List of availability zones. You must specify availability zones when creating a scaling group under a VPC. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| AutoScalingGroupId | String | Scaling group ID |
| RequestId | String | Unique ID of the request, which is required for troubleshooting. |

## 4. Example

### Example 1 Create a scaling group

#### Input example

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
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "AutoScalingGroupId": "asg-nkdwoui0",
    "RequestId": "a5d66fed-85b9-4f43-8243-597337ba896e"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CreateAutoScalingGroup)

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
| InternalError | Internal error |
| InvalidParameter.InScenario | Invalid parameter in specific scenarios |
| InvalidParameterValue.CvmError | Verification exception occurred with CVM parameter |
| InvalidParameterValue.ForwardLb | Invalid application-based load balancer |
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
| LimitExceeded.AutoScalingGroupLimitExceeded | The number of scaling groups exceeds the limit |
| LimitExceeded.MaxSizeLimitExceeded | The maximum number of instances exceeds the upper limit |
| LimitExceeded.MinSizeLimitExceeded | The minimum number of instances falls below the lower limit |
| MissingParameter.InScenario | A parameter is missing in specific scenarios |
| ResourceNotFound.LoadBalancerNotFound | The specified load balancer is not found |
| ResourceUnavailable.LaunchConfigurationStatusAbnormal | Launch configuration is exceptional |
| ResourceUnavailable.ProjectInconsistent | Inconsistent projects |

