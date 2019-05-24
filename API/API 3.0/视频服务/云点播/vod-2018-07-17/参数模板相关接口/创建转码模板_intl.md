## 1. API Description
API domain name: vod.tencentcloudapi.com.  
This API creates up to 1000 custom transcoding templates.    
Default API request rate limit: 100 requests/sec.

# 2. Input Parameters
The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/266/31756).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ModifyTranscodeTemplate |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-17 |
| Region | No | String | Common parameter; optional for this API |
| Container | No | String |  Valid container formats: for both vedio and audio files: mp4, flv, hls; for audio files only: mp3, flac, ogg, m4a. |
| Name | No | String | The name of the transcoding template. Maximum 64 characters. |
| Comment | No | String | The description of the template. Maximum 256 bytes. |
| RemoveVideo | No | Integer | Whether to remove the video data: <br/><li>0: No </li><li>1: Yes </li><br/>Default value: 0. |
| RemoveAudio | No | Integer | Whether to remove the audio data: <br/><li>0: No </li><li>1: Yes </li><br/>Default value: 0. |
| VideoTemplate | No | [VideoTemplateInfo](/document/api/266/31773#VideoTemplateInfo) | Video stream configuration parameter. This field is required when RemoveVideo is 0. |
| AudioTemplate | No | [AudioTemplateInfo](/document/api/266/31773#AudioTemplateInfo) | Audio stream configuration parameter. This field is required when RemoveAudio is 0. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). Input the ID of the sub-application that has the desired resources; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| Definition | Integer | Unique ID of the transcoding template. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample
### Sample 1. Creating a Transcoding Template
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=CreateTranscodeTemplate
&Container=mp4
&Name=Transcoding Template 1
&RemoveVideo=0
&RemoveAudio=0
&VideoTemplate.Codec=libx264
&VideoTemplate.Fps=45
&VideoTemplate.Bitrate=256
&AudioTemplate.Codec=libfdk_aac
&AudioTemplate.Bitrate=200
&AudioTemplate.SampleRate=200
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "Definition": 1008,
    "RequestId": "12ae8d8e-dce3-4151-9d4b-5594145287e1"
  }
}
```
## 5. Developer Resources
## 5. Developer Resources
### API Explorer
**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=PullEvents)

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
The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/267/20461#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | The error is caused internally. |
| InvalidParameterValue | A value specified in a parameter is not valid or cannot be used for this request. |
| InvalidParameterValue.AudioBitrate | The specified audio stream bitrate is invalid.|
| InvalidParameterValue.AudioChannel | The audio channel specified is invalid. |
| InvalidParameterValue.AudioCodec | The audio stream codec specified is invalid. |
| InvalidParameterValue.AudioSampleRate |The audio stream sample rate specified is invalid. |
| InvalidParameterValue.Container | The container format is unsupported. |
| InvalidParameterValue.Fps | The the value of the frame rate is invalid. |
| InvalidParameterValue.RemoveAudio | The value of *RemoveAudio* is invalid. |
| InvalidParameterValue.RemoveVideo | The value of *RemoveVideo* is invalid. |
| InvalidParameterValue.Resolution | The specified resolution value is unsupported. |
| InvalidParameterValue.VideoBitrate | The specified video stream bitrate is invalid. |
| InvalidParameterValue.VideoCodec | The specified video stream codec is invalid|
| LimitExceeded | The usage exceeds the quota limit |
| LimitExceeded.TooMuchTemplate | The number of templates exceeds the limit. |
| ResourceNotFound.TemplateNotExist | The specified template does not exist or is not found. |

