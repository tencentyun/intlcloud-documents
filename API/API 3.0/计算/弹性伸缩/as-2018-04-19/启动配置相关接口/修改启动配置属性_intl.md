## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (ModifyLaunchConfigurationAttributes) is used to modify some attributes of a launch configuration.

* The changes of launch configuration do not affect the existing instances. New instances will be created based on the modified configuration.
* This API supports modifying certain simple types of launch configuration.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: ModifyLaunchConfigurationAttributes |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| LaunchConfigurationId | Yes | String | Launch configuration ID |
| ImageId | No | String | Valid [image](https://cloud.tencent.com/document/product/213/4940) ID in the format of `img-8toqc6s3`. There are four types of images: <br/><li>Public images </li><li>Custom images </li><li>Shared images </li><li>Marketplace images </li><br/>You can obtain the available image IDs in the following ways: <br/><li>For `public images`, `custom images`, and `shared images`, log in to the [console](https://console.cloud.tencent.com/cvm/image?rid=1&imageType=PUBLIC_IMAGE) to query the image IDs; for `marketplace images`, query the image IDs through [Cloud Marketplace](https://market.cloud.tencent.com/list). </li><li>This value can be obtained from the `ImageId` field in the return value of the [DescribeImages API](https://cloud.tencent.com/document/api/213/15715).</li> |
| InstanceTypes.N | No | Array of String | List of instance types. Different instance models specify different resource specifications. Up to 5 instance models can be supported. <br/>The launch configuration uses `InstanceType` to indicate one single instance type and `InstanceTypes` to indicate multiple instance types. After `InstanceTypes` is successfully specified for the launch configuration, the original `InstanceType` will be automatically invalidated. |
| InstanceTypesCheckPolicy | No | String | Instance type verification policy which works when `InstanceTypes` is actually modified. Value range: ALL, ANY. Default value: ANY. <br/><br><li> ALL: The verification will succeed only if all instance types `InstanceType` are available; otherwise, an error will be reported. <br/><br><li> ANY: The verification will succeed if any instance type `InstanceType` is available; otherwise, an error will be reported. <br/><br/>Common reasons why an instance type is unavailable include stock-out of the instance type or the corresponding cloud disk. <br/>If a model in `InstanceTypes` does not exist or has been deactivated, a verification error will be reported regardless of the value of `InstanceTypesCheckPolicy`. |
| LaunchConfigurationName | No | String | Display name of the launch configuration, which can contain Chinese characters, letters, numbers, underscores, separators ("-"), and decimal points with a maximum length of 60 bytes. |
| UserData | No | String | Base64-encoded custom data of up to 16 KB. If you want to clear `UserData`, specify it as an empty string. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Modifying the Image, Instance Type and Name of the Specified Launch Configuration

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=ModifyLaunchConfigurationAttributes
&LaunchConfigurationId=asc-291kq6ku
&ImageId=img-8toqc6s3
&InstanceTypes.0=S2.SMALL1
&LaunchConfigurationName=updated_config
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "07022dcb-5bba-48f0-a2b0-800ad006d031"
  }
}
```

### Sample 2. Clearing UserData

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=ModifyLaunchConfigurationAttributes
&LaunchConfigurationId=asc-291kq6ku
&UserData=
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "2c027f22-3a3b-489a-a77a-89c53fc15212"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyLaunchConfigurationAttributes)

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
| AccountQualificationRestrictions | The request account failed to pass the eligibility verification |
| CallCvmError | Failed to call the CVM API |
| InvalidImageId.NotFound | This image cannot be found |
| InvalidParameterValue.CvmConfigurationError | Exception with CVM parameter validation. |
| InvalidParameterValue.LaunchConfigurationNameDuplicated | The launch configuration name already exists. |
