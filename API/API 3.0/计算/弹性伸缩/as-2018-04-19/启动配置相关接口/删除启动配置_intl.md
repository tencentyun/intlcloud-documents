## 1. API Description

API request domain name: as.tencentcloudapi.com.

This API (DeleteLaunchConfiguration) deletes the specified launch configuration.

* If the launch configuration is active in a scaling group, it cannot be deleted.


Default API request frequency limit: 10 times/second.

Note: This API supports financial availability zones. Because financial availability zones and non-financial availability zones are isolated. When specifying a financial availability zone (e.g., ap-shanghai-fsi) in the Region (a common parameter), you should also choose the financial availability zone preferably in the same region as that one specified in Region for the domain, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/377/20426).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DeleteLaunchConfiguration |
| Version | Yes | String | Common parameter; the value for this API: 2018-04-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| LaunchConfigurationId | Yes | String | ID of the launch configuration to be deleted. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |

## 4. Sample

### Deleting a Launch Configuration

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DeleteLaunchConfiguration
&LaunchConfigurationId=asc-fdz8j7dh
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "RequestId": "dfc4da00-b643-405c-bb4f-d590cfa48b92"
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DeleteLaunchConfiguration)

### SDK

TencentCloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to this API are listed below. For other error codes, see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidLaunchConfiguration | Invalid launch configuration. |
| InvalidLaunchConfigurationId | The launch configuration ID is invalid. |
| InvalidLaunchConfigurationId.InUse | The launch configuration is in use. |
| InvalidLaunchConfigurationId.NotFound | The launch configuration was not found. |
