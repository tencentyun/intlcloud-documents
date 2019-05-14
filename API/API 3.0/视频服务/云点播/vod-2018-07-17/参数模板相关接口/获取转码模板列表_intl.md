## 1. API Description
API domain name: vod.tencentcloudapi.com.
This API gets the list of transcoding template details by unique transcoding template ID. The return result includes all eligible custom transcoding templates and [preset templates](https://cloud.tencent.com/document/product/266/11701#.E9.A2.84.E7.BD.AE.E8.BD.AC.E7.A0.81.E6.A8.A1.E6.9D.BF).
Default API request rate limit: 100 requests/sec.
## 2. Input Parameters
The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/266/31756).
| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeTranscodeTemplates |
| Version | Yes | String | Common parameter; the value for this API: 2018-07-17 |
| Region | No | String | Common parameter; not passed in for this API |
| Definitions.N | No | Array of Integer | Unique ID filter of the transcoding template; array length limit: 100. |
| Type | No | String | Filter of template type; value range: <br/><li>Preset: Preset template; </li><li>Custom: Custom template. </li> |
| ContainerType | No | String | Filter of container; value range: <br/><li>Video: Video container that can contain both video stream and audio stream; </li><li>PureAudio: Audio container that can contain only audio stream. </li> |
| Offset | No | Integer | Paged offset; 0 by default. |
| Limit | No | Integer | Number of returned entries; 10 by default, up to 100. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). If you need to access a resource in a sub-application, enter the sub-application ID in this field; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of eligible entries. |
| TranscodeTemplateSet | Array of [TranscodeTemplate](/document/api/266/31773#TranscodeTemplate) | List of transcoding template details. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |
## 4. Sample
### Sample 1. Getting a Transcoding Template
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=DescribeTranscodeTemplates
&Definitions.0=10
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "TotalCount": 1,
    "TranscodeTemplateSet": [
      {
        "Definition": 1008,
        "Container": "mp4",
        "Name": "Template 1",
        "Comment": null,
        "Type": 0,
        "RemoveVideo": 0,
        "RemoveAudio": 0,
        "VideoTemplate": {
          "Codec": "libx264",
          "Fps": 24,
          "Bitrate": 256,
          "ResolutionAdaptive": "open",
          "Width": 0,
          "Height": 0,
          "MinGop": 1,
          "MaxGop": 10,
          "VideoProfile": "high",
          "ColorSpace": "yuv420p"
        },
        "AudioTemplate": {
          "Codec": "libfdk_aac",
          "Bitrate": 48,
          "SampleRate": 48000,
          "AudioChannel": 2,
          "AudioProfile": "aac_lc"
        },
        "CreateTime": "2018-10-01T10:00:00Z",
        "UpdateTime": "2018-10-01T10:00:00Z"
      }
    ],
    "RequestId": "12ae8d8e-dce3-4151-9d4b-5594145287e1"
  }
}
```
## 5. Developer Resources
### API Explorer
**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=DescribeTranscodeTemplates)
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
| InvalidParameterValue.ContainerType | Incorrect parameter value: ContainerType. |
| InvalidParameterValue.Definitions | Incorrect parameter value: Definitions. |
| InvalidParameterValue.Limit | Parameter error: Limit. |
| InvalidParameterValue.Type | Incorrect Type parameter value. |

