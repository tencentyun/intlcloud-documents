﻿## 1. API Description

API request domain name: live.tencentcloudapi.com.

To create a screencapture rule, you need to first call the [CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834) API to create a screencapture template and bind the returned template ID to the stream.
<br>Screenshot-related document: [LVB screencapture](https://intl.cloud.tencent.com/document/product/267/31072).

Default API request rate limit: 200 requests/second.

## 2. Request Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](https://cloud.tencent.com/document/api/267/20459).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: CreateLiveSnapshotRule |
| Version | Yes | String | Common parameter; the version of this API: 2018-08-01 |
| Region | No | String | Common parameter; optional for this API |
| DomainName | Yes | String | Push domain name |
| AppName | Yes | String | Push path |
| StreamName | Yes | String | Stream name |
| TemplateId | Yes | Integer | Template ID. |

## 3. Return Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.|

## 4. Sample

### Request Sample

#### Input Sample Code

```
https://live.tencentcloudapi.com/?Action=CreateLiveSnapshotRule
&DomainName=5000.livepush.myqcloud.com
&AppName=live
&StreamName=stream1
&TemplateId=1000
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=live&Version=2018-08-01&Action=CreateLiveSnapshotRule)

### SDK

Cloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/267/20461#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InternalError.ArgsNotMatch | For the API that is used for adding transcoding template |
| InternalError.ConfInUsed | The template is in use. |
| InternalError.ConfNotFound | The template does not exist. |
| InternalError.ConfOutLimit | The number of templates exceeds the display. |
| InternalError.InvalidInput | Parameter check failed. |
| InternalError.NotFound | The record does not exist. |
| InternalError.RuleAlreadyExist | The rule has already been configured. |
| InternalError.RuleInUsing | The rule is in use. |
| InternalError.RuleNotFound | The rule does not exist. |
| InternalError.RuleOutLimit | The rule exceeds the limit. |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Incorrect parameter value |
| MissingParameter | Missing parameter |

