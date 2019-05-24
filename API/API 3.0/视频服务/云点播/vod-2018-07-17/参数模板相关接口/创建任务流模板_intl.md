## 1. API Description
API domain name: vod.tencentcloudapi.com.  
This API creates up to 50 custom task flow templates.  
Default API request rate limit: 100 requests/sec.

## 2. Input Parameters
The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/266/31756).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ModifyTranscodeTemplate |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-17 |
| Region | No | String | Common parameter; optional for this API |
| Name | Yes | String | Task flow name ( maximum allowed size: 40 bytes). |
| MediaProcessTask | No | [MediaProcessTaskInput](/document/api/266/31773#MediaProcessTaskInput) | Parameter of the video processing task. |
| AiContentReviewTask | No | [AiContentReviewTaskInput](/document/api/266/31773#AiContentReviewTaskInput) | Parameter of the AI-based content review task. |
| AiAnalysisTask | No | [AiAnalysisTaskInput](/document/api/266/31773#AiAnalysisTaskInput) | Parameter of the AI-based content analysis task. |
| AiRecognitionTask | No | [AiRecognitionTaskInput](/document/api/266/31773#AiRecognitionTaskInput) | Parameter of the AI-based content recognition task. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). Input the ID of the sub-application that has the desired resources; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

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
| InvalidParameter | A parameter is not valid or cannot be used for the request.  |
| InvalidParameter.ExistedProcedureName | The name of the task flow template already exists. |
| InvalidParameterValue.SubAppId | The sub-application ID is invalid or unfounded. |

