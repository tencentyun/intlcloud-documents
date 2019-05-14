## 1. API Description
API domain name: vod.tencentcloudapi.com.
This API creates a custom transcoding template. Up to 1,000 ones can be created.
Default API request rate limit: 100 requests/sec.
## 2. Input Parameters
The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/266/31756).
| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: CreateTranscodeTemplate |
| Version | Yes | String | Common parameter; the value for this API: 2018-07-17 |
| Region | No | String | Common parameter; not passed in for this API |
| Container | Yes | String | Container; value range: mp4, flv, hls, mp3, flac, ogg, and m4a. mp3, flac, ogg, and m4a are for audio files. |
| Name | No | String | Transcoding template name of up to 64 characters. |
| Comment | No | String | Template description of up to 256 characters. |
| RemoveVideo | No | Integer | Whether to remove the video data; value range: <br/><li>0: No </li><li>1: Yes </li><br/>Default value: 0. |
| RemoveAudio | No | Integer | Whether to remove the audio data; value range: <br/><li>0: No </li><li>1: Yes </li><br/>Default value: 0. |
| VideoTemplate | No | [VideoTemplateInfo](/document/api/266/31773#VideoTemplateInfo) | Video stream configuration parameter. This field is required if RemoveVideo is 0. |
| AudioTemplate | No | [AudioTemplateInfo](/document/api/266/31773#AudioTemplateInfo) | Audio stream configuration parameter. This field is required if RemoveAudio is 0. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). If you need to access a resource in a sub-application, enter the sub-application ID in this field; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| Definition | Integer | Unique ID of the transcoding template. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |
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
### API Explorer
**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=CreateTranscodeTemplate)
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
Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/266/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).
| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameterValue | Incorrect parameter value. |
| InvalidParameterValue.AudioBitrate | Parameter error: Audio stream bitrate. |
| InvalidParameterValue.AudioChannel | Incorrect parameter value: AudioChannel. |
| InvalidParameterValue.AudioCodec | Parameter error: Audio stream codec. |
| InvalidParameterValue.AudioSampleRate | Parameter error: Audio stream sample rate. |
| InvalidParameterValue.Container | Parameter error: Container. |
| InvalidParameterValue.Fps | Parameter error: Frame rate. |
| InvalidParameterValue.RemoveAudio | Incorrect parameter value: RemoveAudio. |
| InvalidParameterValue.RemoveVideo | Incorrect parameter value: RemoveVideo. |
| InvalidParameterValue.Resolution | Parameter error: Resolution. |
| InvalidParameterValue.VideoBitrate | Parameter error: Video stream bitrate. |
| InvalidParameterValue.VideoCodec | Parameter error: Video stream codec. |
| LimitExceeded | Quota limit is exceeded. |
| LimitExceeded.TooMuchTemplate | Limit exceeded: The number of templates exceeds the limit. |
| ResourceNotFound.TemplateNotExist | Resource does not exist: The template does not exist. |

