## 1. API Description
API domain name: vod.tencentcloudapi.com.
This API initiates a processing task for audio or video media in Tencent Cloud VOD, including:
1. Transcoding the video (with watermark);
2. Generating animated images;
3. Screencapturing the video at specified time points;
4. Screencapturing the video by sampling;
5. Generating image sprites by screencapturing the video;
6. Taking a screenshot of the video as the cover;
7. Converting the video for adaptive bitrate (and encrypt it);
8. Intelligent content review (detection of pornographic, terrorism, and politically sensitive information);
9. Intelligent content analysis (tag, category, an cover).
Default API request rate limit: 100 requests/sec.
## 2. Input Parameters
The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/266/31756).
| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: ProcessMedia |
| Version | Yes | String | Common parameter; the value for this API: 2018-07-17 |
| Region | No | String | Common parameter; not passed in for this API |
| FileId | Yes | String | Media file ID. |
| MediaProcessTask | No | [MediaProcessTaskInput](/document/api/266/31773#MediaProcessTaskInput) | Parameter of the video processing task. |
| AiContentReviewTask | No | [AiContentReviewTaskInput](/document/api/266/31773#AiContentReviewTaskInput) | Parameter of the video content review task. |
| AiAnalysisTask | No | [AiAnalysisTaskInput](/document/api/266/31773#AiAnalysisTaskInput) | Parameter of the video content analysis task. |
| TasksPriority | No | Integer | Priority of the task flow. The higher the value, the higher the priority. Value range: -10 to 10; if left blank, 0. |
| TasksNotifyMode | No | String | Notification mode for the change in task flow status; value range: Finish, Change and None; if left blank, Finish. |
| SessionContext | No | String | The source context which is used to pass through the user request information. The task flow status change callback returns the value of this field. Up to 250 characters. |
| SessionId | No | String | The ID used for deduplication. If there was a request with the same ID in the past seven days, the current request will return an error. Up to 50 characters. If missing or with a blank string, no deduplication is performed. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). If you need to access a resource in a sub-application, enter the sub-application ID in this field; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| TaskId | String | Task ID |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |
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
**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=ProcessMedia)
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
| FailedOperation.TaskDuplicate | Operation failed: The task already exists. |
| InternalError | Internal error |
| InvalidParameter | Parameter error |
| InvalidParameterValue.AiAnalysisTaskDefinition | Incorrect parameter value: AI-based analysis definition. |
| InvalidParameterValue.AiContentReviewTaskDefinition | Incorrect parameter value: AI-based content review definition. |
| InvalidParameterValue.FileId | FileId does not exist. |
| InvalidParameterValue.SessionContextTooLong | SessionContext is too long. |
| InvalidParameterValue.SessionId | The deduplication ID already exists. The request is removed due to duplication. |
| InvalidParameterValue.SessionIdTooLong | SessionId is too long. |
| InvalidParameterValue.SubAppId | Incorrect parameter value: Sub-application ID |

