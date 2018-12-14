## 1. API Description

Domain name for API request: as.tencentcloudapi.com.

This API (CreateLaunchConfiguration) is used to create a launch configuration.

* The launch configuration cannot be edited or modified. If you want to use a new launch configuration, you must create one.

* You can create 20 launch configurations for each project. For more information, see [Use Limits](https://cloud.tencent.com/document/product/377/3120).


Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter `Region` is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: CreateLaunchConfiguration |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| LaunchConfigurationName | Yes | String | The display name of the launch configuration. It can contain up to 60 characters, including letters, numbers, underscores, hyphens ("-") and decimal points. |
| InstanceType | Yes | String | Instance model. Different instance models have different specifications. To check the latest specifications of models, please call the API [DescribeInstanceTypeConfigs](https://cloud.tencent.com/document/api/213/15749) or see [Instance Type](https://cloud.tencent.com/document/product/213/11518). |
| ImageId | Yes | String | Valid [image](https://cloud.tencent.com/document/product/213/4940) ID, such as `img-8toqc6s3`. There are four types of images:<br/><li>Public Images</li><li>Custom Images</li><li>Shared Images</li><li>Marketplace Images</li><br/>You can obtain the available image IDs by the following ways:<br/><li>For `public images`, `custom images` and `shared images`, log in to the [console](https://console.cloud.tencent.com/cvm/image?rid=1&imageType=PUBLIC_IMAGE) to query the image IDs; for `marketplace images`, query the image IDs through [Cloud Marketplace](https://market.cloud.tencent.com/list).</li><li>This value can be obtained from the `ImageId` field in the returned values of API [DescribeImages](https://cloud.tencent.com/document/api/213/15715).</li> |
| ProjectId | No | Integer | ID of the project to which the instance belongs. This parameter can be obtained from the `projectId` field in the returned values of [DescribeProject](https://cloud.tencent.com/document/api/378/4400). If this is left empty, default project is used. |
| SystemDisk | No | [SystemDisk](/document/api/377/20453#SystemDisk) | Configuration information of instance’s system disk. If the parameter is not specified, the default value is assigned to it. |
| DataDisks.N | No | Array of [DataDisk](/document/api/377/20453#DataDisk) | Configuration information of the instance data disk. If the parameter is not specified, no data disk will be purchased by default. You can specify only one data disk when purchasing the instance. |
| InternetAccessible | No | [InternetAccessible](/document/api/377/20453#InternetAccessible) | Configuration information of public network bandwidth. If this parameter is not specified, the default public network bandwidth is 0 Mbps. |
| LoginSettings | No | [LoginSettings](/document/api/377/20453#LoginSettings) | Login settings of the instance. This parameter is used to set the login password and key for the instance, or to keep the original login settings for the image. By default, a random password is generated and sent to the user via the internal message. |
| SecurityGroupIds.N | No | Array of String | The security group to which the instance belongs. This parameter can be obtained by calling the `SecurityGroupId` field in the returned value of [DescribeSecurityGroups](https://cloud.tencent.com/document/api/215/15808). If this parameter is not specified, the security group is not bound by default. |
| EnhancedService | No | [EnhancedService](/document/api/377/20453#EnhancedService) | Enhanced service. This parameter is used to specify whether to enable Tencent Cloud security and monitoring services. If this parameter is not specified, the Cloud Monitoring and Cloud Security are enabled by default. |
| UserData | No | String | Base64 encoded custom data, which is limited to 16 KB. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| LaunchConfigurationId | String | Launch configuration ID, which is returned when you create a launch configuration using this API. |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Create a launch configuration with simple parameters

#### Input example

```
https://as.tencentcloudapi.com/?Action=CreateLaunchConfiguration
&LaunchConfigurationName=as_test
&InstanceType=S2.SMALL1
&ImageId=img-8toqc6s3
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "LaunchConfigurationId": "asc-23h37kyn",
    "RequestId": "d639dd64-9e46-4246-b13c-80954f81c11b"
  }
}
```

### Example 2 Create a launch configuration with detailed parameters

#### Input example

```
https://as.tencentcloudapi.com/?Action=CreateLaunchConfiguration
&LaunchConfigurationName=as_test
&ImageId=img-8toqc6s3
&InstanceType=S2.SMALL1
&SystemDisk.DiskType=LOCAL_BASIC
&SystemDisk.DiskSize=50
&DataDisks.0.DiskType=CLOUD_BASIC
&DataDisks.0.DiskSize=100
&InternetAccessible.InternetChargeType=TRAFFIC_POSTPAID_BY_HOUR
&InternetAccessible.InternetMaxBandwidthOut=5
&InternetAccessible.PublicIpAssigned=TRUE
&LoginSettings.KeyIds.0=skey-k8eypc1l
&EnhancedService.SecurityService.Enabled=TRUE
&EnhancedService.MonitorService.Enabled=TRUE
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "LaunchConfigurationId": "asc-fdz8j7dh",
    "RequestId": "9a7209d3-2260-49d7-952a-dfa2001f8822"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CreateLaunchConfiguration)

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
| AccountQualificationRestrictions | The request account failed to pass the eligibility verification |
| CallCvmError | Failed to call the CVM API |
| InvalidImageId.NotFound | This image cannot be found |
| InvalidLaunchConfiguration.NameDuplicate | Duplicate launch configuration name |
| InvalidParameterConflict | The two parameters conflict with each other, and cannot be both specified. |
| InvalidPermission | This operation is not supported for the account |
| LaunchConfigurationQuotaLimitExceeded | Launch configuration quota exceeds the limit |

