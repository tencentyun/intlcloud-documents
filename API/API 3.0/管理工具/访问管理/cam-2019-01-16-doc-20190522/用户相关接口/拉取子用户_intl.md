## 1. API Description

API domain name: cam.tencentcloudapi.com.

This API pulls a sub-user.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/598/33158).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ListUsers |
| Version | Yes | String | Common parameter; the version of this API: 2019-01-16 |
| Region | No | String | Common parameter; optional for this API. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Data | Array of [SubAccountInfo](/document/api/598/33167#SubAccountInfo) | Sub-user information |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Pulling a Sub-user

#### Input Sample Code

```
https://cam.tencentcloudapi.com/?Action=ListUsers
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "Data": [
      {
        "Uin": 100000546533,
        "Name": "test124",
        "Uid": 1001774,
        "Remark": "test",
        "ConsoleLogin": 1,
        "PhoneNum": "10086",
        "CountryCode": "86",
        "Email": "123@qq.com",
        "RequestId": "33674182-e53d-416b-b6ce-bd7e7536b5d6"
      }
    ]
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cam&Version=2019-01-16&Action=ListUsers)

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

This API has no error codes related to business logic. For other error codes, see [Common Error Codes](/document/api/598/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).