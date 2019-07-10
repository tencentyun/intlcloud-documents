## 1. API Description

API request domain name: as.tencentcloudapi.com.

This API (DescribeAccountLimits) describes Auto Scaling resource limits for the specified user account

Default API request frequency limit: 20 times/second.

Note: Because financial availability zones and non-financial availability zones are isolated. When specifying a financial availability zone (e.g., ap-shanghai-fsi) in the Region (a common parameter), you should also choose the financial availability zone preferably in the same region as that one specified in Region for the domain, such as as.ap-shanghai-fsi.tencentcloudapi.com.


## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/377/20426).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeAccountLimits |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| MaxNumberOfLaunchConfigurations | Integer | Maximum number of launch configurations allowed to create in the user account |
| NumberOfLaunchConfigurations | Integer | Number of launch configurations in the user account |
| MaxNumberOfAutoScalingGroups | Integer | Maximum number of scaling groups allowed to create in the user account |
| NumberOfAutoScalingGroups | Integer | Current number of scaling groups in the user account |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues |

## 4. Sample

### Querying the Limits for Launch Configuration and Scaling Group

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribeAccountLimits
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "NumberOfLaunchConfigurations": 15,
        "MaxNumberOfLaunchConfigurations": 20,
        "NumberOfAutoScalingGroups": 25,
        "MaxNumberOfAutoScalingGroups": 30,
        "RequestId": "0c243e3a-70e0-4365-98b1-5fe22b4498a1"
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeAccountLimits)

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
