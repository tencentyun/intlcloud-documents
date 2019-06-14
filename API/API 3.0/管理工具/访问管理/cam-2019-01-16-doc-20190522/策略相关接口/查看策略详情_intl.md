## 1. API Description

API domain name: cam.tencentcloudapi.com.

This API (GetPolicy) queries and views policy details.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/598/33158).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: GetPolicy |
| Version | Yes | String | Common parameter; the version of this API: 2019-01-16 |
| Region | No | String | Common parameter; optional for this API. |
| PolicyId | Yes | Integer | Policy ID |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| PolicyName | String | Policy name <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| Description | String | Policy description <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| Type | Integer | 1: custom policy; 2: predefined policy <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| AddTime | Timestamp | Creation time <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| UpdateTime | Timestamp | Last update time <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| PolicyDocument | String | Policy document <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Viewing the Details of a Policy

#### Input Sample Code

```
https://cam.tencentcloudapi.com/?Action=GetPolicy
&PolicyId=17698703
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "PolicyDocument": "{\"version\":\"2.0\",\"statement\":[{\"effect\":\"allow\",\"action\":[\"name\\/cos:*\"],\"resource\":[\"*\"]}]}",
    "UpdateTime": "2019-04-29 21:28:32",
    "AddTime": "2019-04-29 21:18:40",
    "PolicyName": "test-2019-04-29",
    "Description": "Test policy",
    "Type": 1,
    "RequestId": "845b309d-e531-402d-a4f6-ec124f06738b"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cam&Version=2019-01-16&Action=GetPolicy)

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

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/598/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.SystemError | Internal error. |
| InvalidParameter.ParamError | Invalid input parameter. |
| InvalidParameter.PolicyIdError | The input parameter PolicyId is invalid. |
| ResourceNotFound.PolicyIdNotFound | The resource specified by PolicyId does not exist. |