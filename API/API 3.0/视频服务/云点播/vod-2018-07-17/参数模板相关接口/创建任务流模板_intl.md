## 1. API Description
API domain name: vod.tencentcloudapi.com.
This API creates a custom task flow template. Up to 50 ones can be created.
Default API request rate limit: 100 requests/sec.
## 2. Input Parameters
The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/266/31756).
| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: CreateProcedureTemplate |
| Version | Yes | String | Common parameter; the value for this API: 2018-07-17 |
| Region | No | String | Common parameter; not passed in for this API |
| Name | Yes | String | Task flow name (supports letters with a length of up to 40 bytes). |
| MediaProcessTask | No | [MediaProcessTaskInput](/document/api/266/31773#MediaProcessTaskInput) | Parameter of the video processing task. |
| AiContentReviewTask | No | [AiContentReviewTaskInput](/document/api/266/31773#AiContentReviewTaskInput) | Parameter of the AI-based content review task. |
| AiAnalysisTask | No | [AiAnalysisTaskInput](/document/api/266/31773#AiAnalysisTaskInput) | Parameter of the AI-based content analysis task. |
| AiRecognitionTask | No | [AiRecognitionTaskInput](/document/api/266/31773#AiRecognitionTaskInput) | Parameter of the AI-based content recognition task. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). If you need to access a resource in a sub-application, enter the sub-application ID in this field; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |
## 4. Sample
### Sample 1. Creating a Task Flow Template that Initiates a Transcoding Task
Create a task flow template named "My Task Flow" to transcode a video into three formats of 20, 30, and 40.
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=CreateProcedureTemplate
&Name=My Task Flow
&MediaPrcoessTask.TranscodeTaskSet.0.Definition=20
&MediaPrcoessTask.TranscodeTaskSet.1.Definition=30
&MediaPrcoessTask.TranscodeTaskSet.2.Definition=40
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "RequestId": "6ca31e3a-6b8e-4b4e-9256-fdc700064ef3"
  }
}
```
### Sample 2. Creating a Task Flow Template That Initiates a Transcoding Task with Watermark
Create a task flow template named "My Task Flow" to transcode a video into three formats of 20, 30, and 40, where each output video has a watermark added by watermarking template ID 15780.
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=CreateProcedureTemplate
&Name=My Task Flow
&MediaPrcoessTask.TranscodeTaskSet.0.Definition=20
&MediaPrcoessTask.TranscodeTaskSet.0.Watermarks.0.Definition=15780
&MediaPrcoessTask.TranscodeTaskSet.1.Definition=30
&MediaPrcoessTask.TranscodeTaskSet.1.Watermarks.0.Definition=15780
&MediaPrcoessTask.TranscodeTaskSet.2.Definition=40
&MediaPrcoessTask.TranscodeTaskSet.2.Watermarks.0.Definition=15780
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "RequestId": "6ca31e3a-6b8e-4b4e-9256-fdc700064ef3"
  }
}
```
### Sample 3. Creating a Task Flow Template that Initiates a Transcoding and Sampling-based Screencapturing Task
Create a task flow template named "My Task Flow" to transcode a video into three formats of 20, 30, and 40 and screencapture the video with sampling-based screencapturing template ID 10.
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=CreateProcedureTemplate
&Name=My Task Flow
&MediaPrcoessTask.TranscodeTaskSet.0.Definition=20
&MediaPrcoessTask.TranscodeTaskSet.1.Definition=30
&MediaPrcoessTask.TranscodeTaskSet.2.Definition=40
&MediaPrcoessTask.SampleSnapshotTaskSet.0.Definition=10
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "RequestId": "6ca31e3a-6b8e-4b4e-9256-fdc700064ef3"
  }
}
```
### Sample 4. Creating a Task Flow Template that Initiates an Intelligent Content Review Task
Create a task flow template named "My Task Flow" to initiate an intelligent content review task (including detection of pornographic, politically sensitive, and terrorism information) using content review template ID 10.
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=CreateProcedureTemplate
&Name=My Task Flow
&AiContentReviewTask.Definition=10
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "RequestId": "6ca31e3a-6b8e-4b4e-9256-fdc700064ef3"
  }
}
```
## 5. Developer Resources
### API Explorer
**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=CreateProcedureTemplate)
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
| InvalidParameter | Parameter error |
| InvalidParameter.ExistedProcedureName | The task flow template name already exists. |
| InvalidParameterValue.SubAppId | Incorrect parameter value: Sub-application ID |

