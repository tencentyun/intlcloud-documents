## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (UpgradeLaunchConfiguration) is used to upgrade launch configurations.

* This API is used to upgrade a launch configuration in a "completely overriding" manner, i.e., it uniformly sets a new configuration according to the API parameters regardless of the original parameters. If optional fields are left empty, their default values will be used.
* After the launch configuration is upgrade, the existing instances that have been created by it will not be changed, but new instances will be created according to the new configuration.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: UpgradeLaunchConfiguration |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| LaunchConfigurationId | Yes | String | Launch configuration ID |
| ImageId | Yes | String | Valid [image](https://cloud.tencent.com/document/product/213/4940) ID in the format of `img-8toqc6s3`. There are four types of images: <br/><li>Public images </li><li>Custom images </li><li>Shared images </li><li>Marketplace images </li><br/>You can obtain the available image IDs in the following ways: <br/><li>For `public images`, `custom images`, and `shared images`, log in to the [console](https://console.cloud.tencent.com/cvm/image?rid=1&imageType=PUBLIC_IMAGE) to query the image IDs; for `marketplace images`, query the image IDs through [Cloud Marketplace](https://market.cloud.tencent.com/list). </li><li>This value can be obtained from the `ImageId` field in the return value of the [DescribeImages API](https://cloud.tencent.com/document/api/213/15715).</li> |
| InstanceTypes.N | Yes | Array of String | List of instance models. Different instance models specify different resource specifications. Up to 5 instance models can be supported. |
| LaunchConfigurationName | Yes | String | The display name of the launch configuration. It can only contain letters, numbers, underscores, hyphens ("-") and decimal points, with a length of not more than 60 characters. |
| DataDisks.N | No | Array of [DataDisk](/document/api/377/20453#DataDisk) | Information of the instance's data disk configuration. If this parameter is not specified, no data disk is purchased by default. Up to 11 data disks can be supported. |
| EnhancedService | No | [EnhancedService](/document/api/377/20453#EnhancedService) | Enhanced service. This parameter is used to specify whether to enable Cloud Security, Cloud Monitor and other services. If this parameter is not specified, the Cloud Monitor and Cloud Security are enabled by default. |
| InstanceChargeType | No | String | Instance billing mode. CVM instances are POSTPAID_BY_HOUR by default. <br/><br><li>POSTPAID_BY_HOUR: Pay-as-you-go on an hourly basis <br/><br><li>SPOTPAID: Bidding |
| InstanceMarketOptions | No | [InstanceMarketOptionsRequest](/document/api/377/20453#InstanceMarketOptionsRequest) | Market-related options of the instance, such as the parameters related to spot instances. If the billing mode of instance is specified as bidding, this parameter must be passed in. |
| InstanceTypesCheckPolicy | No | String | Instance type verification policy. Value range: ALL, ANY. Default value: ANY. <br/><br><li> ALL: The verification will succeed only if all instance types `InstanceType` are available; otherwise, an error will be reported. <br/><br><li> ANY: The verification will succeed if any instance type `InstanceType` is available; otherwise, an error will be reported. <br/><br/>Common reasons why an instance type is unavailable include stock-out of the instance type or the corresponding cloud disk. <br/>If a model in `InstanceTypes` does not exist or has been deactivated, a verification error will be reported regardless of the value of `InstanceTypesCheckPolicy`. |
| InternetAccessible | No | [InternetAccessible](/document/api/377/20453#InternetAccessible) | Configuration information of public network bandwidth. If this parameter is not specified, the default public network bandwidth is 0 Mbps. |
| LoginSettings | No | [LoginSettings](/document/api/377/20453#LoginSettings) | Login settings of the instance. This parameter is used to set the login password and key for the instance, or to keep the original login settings for the image. By default, a random password is generated and sent to the user via the internal message. |
| ProjectId | No | Integer | ID of the project to which the instance belongs. This parameter can be obtained from the `projectId` field in the returned values of [DescribeProject](https://cloud.tencent.com/document/api/378/4400). If this is left empty, default project is used. |
| SecurityGroupIds.N | No | Array of String | The security group to which the instance belongs. This parameter can be obtained by calling the `SecurityGroupId` field in the returned value of [DescribeSecurityGroups](https://cloud.tencent.com/document/api/215/15808). If this parameter is not specified, the security group is not bound by default. |
| SystemDisk | No | [SystemDisk](/document/api/377/20453#SystemDisk) | Configuration information of instance’s system disk. If the parameter is not specified, the default value is assigned to it. |
| UserData | No | String | Base64 encoded custom data, which is limited to 16 KB. |
| InstanceTags.N | No | Array of [InstanceTag](/document/api/377/20453#InstanceTag) | Tag list. This parameter is used to bind up to 10 tags to newly added instances. |
| CamRoleName | No | String | CAM role name, which can be obtained from the `roleName` field in the return value of the DescribeRoleList API. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Upgrading a Launch Configuration with Simple Parameters

Only assign values for the required parameters (launch configuration name, instance model, and image ID) and use system default values for other parameters. The specific configuration is as follows: launch configuration name: as_test, instance model: Standard II 1C1G (S2.SMALL1), image ID: img-8toqc6s3.

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=UpgradeLaunchConfiguration
&LaunchConfigurationId=asc-gj14vczi
&LaunchConfigurationName=as_test
&InstanceTypes.0=S2.SMALL1
&ImageId=img-8toqc6s3
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "d68a3364-a933-4664-bee4-fb89b8c69b49"
  }
}
```

### Sample 2. Upgrading a Launch Configuration with Detailed Parameters

Launch configuration name: as_test; image ID: img-8toqc6s3; model: Standard II 1C1G (S2.SMALL1); system disk: 50 GB local disk; data disk: 100 GB HDD cloud disk; internet billing mode: pay-as-you-go by traffic on an hourly basis; upper limit for internet bandwidth: 5 Mbps; IP: public IP; login method: key; Cloud Monitor and Cloud Security: installed.

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=UpgradeLaunchConfiguration
&LaunchConfigurationId=asc-gj14vczi
&LaunchConfigurationName=as_test
&ImageId=img-8toqc6s3
&InstanceTypes.0=S2.SMALL1
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
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "1430a2d3-eb73-44c6-8316-218c4562a85c"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=UpgradeLaunchConfiguration)

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
| CallCvmError | Failed to call the CVM API |
| InternalError | Internal error. |
| InvalidImageId.NotFound | This image cannot be found |
| InvalidParameter.Conflict | The specified parameters conflict with each other and thus cannot be both specified |
| InvalidParameter.MustOneParameter | A parameter is missing. One of the two parameters must be specified. |
| InvalidParameterValue | Invalid parameter value |
| InvalidParameterValue.CvmConfigurationError | Exception with CVM parameter validation. |
| InvalidParameterValue.CvmError | Verification exception occurred with CVM parameter |
| InvalidParameterValue.LaunchConfigurationNameDuplicated | The launch configuration name already exists. |
