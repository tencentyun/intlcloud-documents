## 1. API Description
API domain name: vod.tencentcloudapi.com.
This API initiates a task to process audio or video files in Tencent Cloud VOD. The tasks include:
1. Transcodes the video with watermark;
2. Generates animated images;
3. Captures video clips at specified points of time;
4. Randomly captures video clips;
5. Generates sprites from captured video clips;
6. Captures a clip and use it as the cover of the video;
7. Sets up encrypted adaptive bitrate streaming;
8. Intelligent content review (detection of pornographic, terrorism, and politically sensitive information);
9. Intelligent content analysis (e.g. tag, category, cover).  

Default API request rate limit: 100 requests/sec.

### 2. Input Parameters
The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/266/31756).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ProcessMedia |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-17 |
| Region | No | String | Common parameter; optional for this API |
| FileId | Yes | String | Media file ID. |
| MediaProcessTask | No | [MediaProcessTaskInput](/document/api/266/31773#MediaProcessTaskInput) | Parameter of the video processing task. |
| AiContentReviewTask | No | [AiContentReviewTaskInput](/document/api/266/31773#AiContentReviewTaskInput) | Parameter of the video content review task. |
| AiAnalysisTask | No | [AiAnalysisTaskInput](/document/api/266/31773#AiAnalysisTaskInput) | Parameter of the video content analysis task. |
| TasksPriority | No | Integer | Priority of the task flow. The higher the value, the higher the priority. Value range: -10 to 10; if you leave this field blank, the API will recognize it as 0. |
| TasksNotifyMode | No | String | Mode of task flow status notification. Valid values : Finish, Change and None; if you leave this field blank, the API will recognize it as Finish. |
| SourceContext | No | String | The source context passed along with the request. The upload callback API will return this value. Maximum 250 characters allowed. |
| SessionId | No | String | The ID used for deduplication. If there was a request with the same ID in the past seven days, the current request will return an error. Up to 50 characters. If missing or with a blank string, no deduplication is performed. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). Input the ID of the sub-application that has the desired resources; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| TaskId | String | Task ID |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample
### Sample 1. Initiating a Transcoding Task
Initiate a transcoding task for the video with the fileId of 5285485487985271487 to output in three formats of 20, 30, and 40.
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=ProcessMedia
&FileId=5285485487985271487
&MediaProcessTask.TranscodeTaskSet.0.Definition=20
&MediaProcessTask.TranscodeTaskSet.1.Definition=30
&MediaProcessTask.TranscodeTaskSet.2.Definition=40
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "RequestId": "6ca31e3a-6b8e-4b4e-9256-fdc700064ef3",
    "TaskId": "125xxx65-procedurev2-bffb15f07530b57bc1aabb01fac74bca"
  }
}
```
### Sample 2. Initiating a Transcoding Task with Watermark
Initiate a transcoding task for the video with the fileId of 5285485487985271487 to output in three formats of 20, 30, and 40, where each output video has a watermark added by watermarking template ID 15780.
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=ProcessMedia
&FileId=5285485487985271487
&MediaProcessTask.TranscodeTaskSet.0.Definition=20
&MediaProcessTask.TranscodeTaskSet.0.WatermarkSet.0.Definition=15780
&MediaProcessTask.TranscodeTaskSet.1.Definition=30
&MediaProcessTask.TranscodeTaskSet.1.WatermarkSet.0.Definition=15780
&MediaProcessTask.TranscodeTaskSet.2.Definition=40
&MediaProcessTask.TranscodeTaskSet.2.WatermarkSet.0.Definition=15780
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "RequestId": "6ca31e3a-6b8e-4b4e-9256-fdc700064ef3",
    "TaskId": "125xxx65-procedurev2-bffb15f07530b57bc1aabb01fac74bca"
  }
}
```
### Sample 3. Initiating a Transcoding and Sampling-based Screencapturing Task
Initiate a transcoding task for the video with the fileId of 5285485487985271487 to output in three formats of 20, 30, and 40 and screencapture the video with sampling-based screencapturing template ID 10.
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=ProcessMedia
&FileId=5285485487985271487
&MediaProcessTask.TranscodeTaskSet.0.Definition=20
&MediaProcessTask.TranscodeTaskSet.1.Definition=30
&MediaProcessTask.TranscodeTaskSet.2.Definition=40
&MediaProcessTask.SampleSnapshotTaskSet.0.Definition=10
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "RequestId": "6ca31e3a-6b8e-4b4e-9256-fdc700064ef3",
    "TaskId": "125xxx65-procedurev2-bffb15f07530b57bc1aabb01fac74bca"
  }
}
```
### Sample 4. Initiating an Intelligent Content Review Task
Initiate an intelligent content review task (including detection of pornographic, politically sensitive, and terrorism information) for the video with fileId of 5285485487985271487 using content review template ID 10.
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=ProcessMedia
&FileId=5285485487985271487
&AiContentReviewTask.Definition=10
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "RequestId": "6ca31e3a-6b8e-4b4e-9256-fdc700064ef3",
    "TaskId": "125xxx65-procedurev2-bffb15f07530b57bc1aabb01fac74bca"
  }
}
```
### Sample 5. Initiating an Intelligent Content Analysis Task
Initiate a content analysis task (including intelligently generating of category, tag, and cover) for the video with fileId of 5285485487985271487 using content analysis template ID 10.
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=ProcessMedia
&FileId=5285485487985271487
&AiAnalysisTask.Definition=10
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "RequestId": "6ca31e3a-6b8e-4b4e-9256-fdc700064ef3",
    "TaskId": "125xxx65-procedurev2-bffb15f07586237bcecodb01fac7kdikk"
  }
}
```
## 5. Developer Resources
### API Explorer
**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=ProcessMedia)

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
| FailedOperation.TaskDuplicate | The operation is failed: The task already exists. |
| InternalError | The error is caused internally. |
| InvalidParameter | A parameter is not valid or cannot be used for the request.  |
| InvalidParameterValue.AiAnalysisTaskDefinition |The input value of AI-analyzed *Definition* is invalid. |
| InvalidParameterValue.AiContentReviewTaskDefinition | The value of *Definition* of AI-reviewed content is invalid. |
| InvalidParameterValue.FileId | The specified file ID  does not exist. |
| InvalidParameterValue.SessionContextTooLong | The length of session context exceeds the limit.|
| InvalidParameterValue.SessionId | The session ID already exists. The request is removed due to duplication. |
| InvalidParameterValue.SessionIdTooLong | The length of the session ID is too long. |
| InvalidParameterValue.SubAppId | The sub-application ID is invalid or unfounded. |

