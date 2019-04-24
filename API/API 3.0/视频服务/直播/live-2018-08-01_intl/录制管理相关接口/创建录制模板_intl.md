## 1. API Description

API request domain name: live.tencentcloudapi.com.

After a recording template is created and a template ID is successfully returned, you need to call the [CreateLiveRecordRule](/document/product/267/32615) API and bind the template ID to the stream.
<br>Recording-related document: [LVB Recording](/document/product/267/32739).

Default API request rate limit: 200 requests/second.

## 2. Request Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all  requests, see [Common Request Parameters](/document/api/267/20459).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: CreateLiveRecordTemplate |
| Version | Yes | String | Common parameter; the version of this API: 2018-08-01 |
| Region | No | String | Common parameter; optional for this API |
| TemplateName | Yes | String | Template name. Non-empty string. |
| Description | No | String | Description information |
| FlvParam | No | [RecordParam](/document/api/267/20474#RecordParam) | FLV recording parameter, which is set when FLV recording is enabled. |
| HlsParam | No | [RecordParam](/document/api/267/20474#RecordParam) | HLS recording parameter, which is set when HLS recording is enabled. |
| Mp4Param | No | [RecordParam](/document/api/267/20474#RecordParam) | MP4 recording parameter, which is set when MP4 recording is enabled. |
| AacParam | No | [RecordParam](/document/api/267/20474#RecordParam) | AAC recording parameter, which is set when AAC recording is enabled. |

## 3. Return Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TemplateId | Integer | Template ID |
| RequestId | String | The unique ID for this request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Request Sample

#### Input Sample Code

```
https://live.tencentcloudapi.com/?Action=CreateLiveRecordTemplate
&TemplateName=templat
&Description=test
&FlvParam.RecordType=0
&FlvParam.RecordInterval=1800
&FlvParam.StorageTime=600
&HlsParam.RecordType=0
&HlsParam.RecordInterval=1800
&HlsParam.StorageTime=600
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TemplateId": 1000,
    "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment. **

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=live&Version=2018-08-01&Action=CreateLiveRecordTemplate)

### SDK

Cloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes. For other error codes, see [Common Error Codes](/document/api/267/20461#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

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

