## 1. API Description

API domain name: cam.tencentcloudapi.com.

This API (DetachUserPolicy) unbinds a policy from a user.

Default API request rate limit: 10 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/598/33158).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DetachUserPolicy |
| Version | Yes | String | Common parameter; the version of this API: 2019-01-16 |
| Region | No | String | Common parameter; optional for this API. |
| PolicyId | Yes | Integer | Policy ID |
| DetachUin | Yes | Integer | Sub-account uin |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Unbinding a Policy from a User

Unbind policy 16313162 from user 3449203261

#### Input Sample Code

```
https://cam.tencentcloudapi.com/?Action=DetachUserPolicy
&PolicyId=16313162
&DetachUin=3449203261
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "1a21f666-d00e-4df8-92f7-7121f9012e43"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cam&Version=2019-01-16&Action=DetachUserPolicy)

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
| InvalidParameter.AttachmentFull | The number of policies associated with the authorization object of the principal field has reached the upper limit. |
| InvalidParameter.ParamError | Invalid input parameter. |
| InvalidParameter.PolicyIdError | The input parameter PolicyId is invalid. |
| InvalidParameter.PolicyIdNotExist | The policy ID does not exist. |
| InvalidParameter.UserNotExist | The authorization object of the principal field does not exist. |
| ResourceNotFound.PolicyIdNotFound | The resource specified by PolicyId does not exist. |
| ResourceNotFound.UserNotExist | The user does not exist. |