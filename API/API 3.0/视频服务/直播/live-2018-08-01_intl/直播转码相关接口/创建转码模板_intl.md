## 1. API Description

API request domain name: live.tencentcloudapi.com.

After a transcoding template is created and a template ID is successfully returned, you need to call the [CreateLiveTranscodeRule](/document/product/267/32647) API and bind the returned template ID to the stream.
<br>Transcoding-related document: [LVB Encapsulating and Transcoding](/document/product/267/32736).

Default API request rate limit: 200 requests/second.

## 2. Request Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/267/20459).


| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: CreateLiveTranscodeTemplate |
| Version | Yes | String | Common parameter; the version of this API: 2018-08-01 |
| Region | No | String | Common parameter; optional for this API |
| TemplateName | Yes | String | Template name, for example, 900 900p. This can be only a combination of letters and numbers. |
| VideoBitrate | Yes | Integer | Video bit rate |
| Vcodec | No | String | Video encoding: <br/>h264/h265. h264 by default |
| Acodec | No | String | Audio encoding: <br/>aac/mp3. Original audio format by default |
| AudioBitrate | No | Integer | Audio bit rate; 0 by default; value range: 0-500 |
| Description | No | String | Template description |
| Width | No | Integer | Width; 0 by default. |
| NeedVideo | No | Integer | Whether to keep the video; 0: no, 1: yes. 1 by default. |
| NeedAudio | No | Integer | Whether to keep the audio; 0: no, 1: yes. 1 by default. |
| Height | No | Integer | Height; 0 by default. |
| Fps | No | Integer | Frame rate; 0 by default. |
| Gop | No | Integer | Keyframe interval in seconds. Original interval by default |
| Rotate | No | Integer | Whether to rotate; 0: no, 1: yes. 0 by default. |
| Profile | No | String | Encoding quality: <br/>baseline/main/high. baseline by default |
| BitrateToOrig | No | Integer | Whether to not exceed the original bit rate; 0: no, 1: yes. 0 by default. |
| HeightToOrig | No | Integer | Whether to not exceed the original height; 0: no, 1: yes. 0 by default. |
| FpsToOrig | No | Integer | Whether to not exceed the original fps; 0: no, 1: yes. 0 by default. |

## 3. Return Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TemplateId | Integer | Template ID. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Request Sample

#### Input Sample Code

```
https://live.tencentcloudapi.com/?Action=CreateLiveTranscodeTemplate
&Vcodec=h264
&Acodec=aac
&AudioBitrate=500
&TemplateName=900m
&Description=test
&VideoBitrate=900
&Width=250
&NeedVideo=1
&NeedAudio=1
&Height=250
&Fps=30
&Gop=3
&Rotate=0
&Profile=main
&BitrateToOrig=0
&HeightToOrig=0
&FpsToOrig=0
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TemplateId":1000,
    "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=live&Version=2018-08-01&Action=CreateLiveTranscodeTemplate)

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

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/267/20461#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InternalError.ArgsNotMatch | For the API that is used for adding transcoding template |
| InternalError.ConfInUsed | The template is in use. |
| InternalError.ConfNotFound | The template does not exist. |
| InternalError.ConfOutLimit | The number of templates exceeds the display. |
| InternalError.InvalidInput | Parameter check failed. |
| InternalError.NotFound | The record does not exist. |
| InternalError.ProcessorAlreadyExist | The transcoding template name already exists. |
| InternalError.RuleAlreadyExist | The rule has already been configured. |
| InternalError.RuleInUsing | The rule is in use. |
| InternalError.RuleNotFound | The rule does not exist. |
| InternalError.RuleOutLimit | The rule exceeds the limit. |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Incorrect parameter value |
| MissingParameter | Missing parameter |

