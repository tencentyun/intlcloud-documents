## 1. API Description
API domain name: vod.tencentcloudapi.com.  
This API uses task ID as a key to query the task status and result. You can only search for a task submitted in the most recent 3 days.  
Default API request rate limit: 100 requests/sec.

## 2. Input Parameters
The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/266/31756).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ModifyTranscodeTemplate |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-17 |
| Region | No | String | Common parameter; optional for this API |
| TaskId | Yes | String | ID of the video processing task. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). Input the ID of the sub-application that has the desired resources; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| TaskType | String | Task type: <br/><li>Process: Video processing; </li><li>EditMedia: Video editing; </li><li>WechatPublish: Video publishing on WeChat . </li><br/>Task types compatible with v2017: <br/><li>Transcode: Video transcoding; </li><li>SnapshotByTimeOffset: Screen capturing: </li><li>Concat: Video stitching; </li><li>Clip: Video clipping; </li><li>ImageSprites: Image sprite generating. </li>|
| Status | String | Task status: <br/><li>WAITING: The task is waiting to be processed; </li><li>PROCESSING: The task is being executed; </li><li>FINISH: The task is completed. </li>|
| CreateTime | String | Creation time of the task in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). |
| BeginProcessTime | String | Start time of the task in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). |
| FinishTime | String | End time of the task in [ISO date format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). |
| ProcedureTask | [ProcedureTask](/document/api/266/31773#ProcedureTask) | Information of the video processing task. This parameter is returned only when the TaskType is Procedure. <br/>Note: Null means no valid values returned. |
| EditMediaTask | [EditMediaTask](/document/api/266/31773#EditMediaTask) | Information of the video editing task. This parameter is returned only when the TaskType is EditMedia. <br/>Note: Null means no valid values returned. |
| WechatPublishTask | [WechatPublishTask](/document/api/266/31773#WechatPublishTask) | Information of the Wechat video publishing task. This parameter is returned only when the TaskType is WechatPublish. <br/>Note: Null means no valid values returned. |
| TranscodeTask | [TranscodeTask2017](/document/api/266/31773#TranscodeTask2017) | Information of the video transcoding task. This parameter is returned only when the TaskType is Transcode. <br/>Note: Null means no valid values returned. |
| SnapshotByTimeOffsetTask | [SnapshotByTimeOffsetTask2017](/document/api/266/31773#SnapshotByTimeOffsetTask2017) | Information of the screen capturing task. This parameter is returned only when the TaskType is SnapshotByTimeOffset. <br/>Note: Null means no valid values returned.  |
| ConcatTask | [ConcatTask2017](/document/api/266/31773#ConcatTask2017) | Information of the video stitching task.This parameter is returned only when the TaskType is Concat. <br/>Note: Null means no valid values returned. |
| ClipTask | [ClipTask2017](/document/api/266/31773#ClipTask2017) | Information of the video clipping task. This parameter is returned only when the TaskType is Clip. <br/>Note: Null means no valid values returned. |
| CreateImageSpriteTask | [CreateImageSpriteTask2017](/document/api/266/31773#CreateImageSpriteTask2017) | Information of the image sprite creating task. This parameter is returned only when the TaskType is CreateImageSprite. <br/>Note: Null means no valid values returned. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample
### Sample 1. Getting Task Details - Procedure
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=DescribeTaskDetail
&TaskId=12567683xx-Procedure-633031cd8293ef29d39251ea751b69f2t0
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "TaskType": "Procedure",
    "Status": "FINISH",
    "CreateTime": "2019-02-21T08:27:42Z",
    "BeginProcessTime": "2019-02-21T08:27:43Z",
    "FinishTime": "2019-02-21T08:27:44Z",
    "ProcedureTask": {
      "TaskId": "12567683xx-Procedure-2e1af2456351812be963e309cc133403t0",
      "Status": "FINISH",
      "ErrCode": 0,
      "Message": "",
      "FileId": "5285890784246869930",
      "FileName": "small",
      "FileUrl": "http://12567683xx.vod2.myqcloud.com/1c1ae5d2vodgzp12567683xx/c643347c5285890784246869930/AtUCmy6gmIYA.mp4",
      "MetaData": {
        "AudioDuration": 59.9900016784668,
        "AudioStreamSet": [
          {
            "Bitrate": 383854,
            "Codec": "aac",
            "SamplingRate": 48000
          }
        ],
        "Bitrate": 1021028,
        "Container": "mov,mp4,m4a,3gp,3g2,mj2",
        "Duration": 60,
        "Height": 480,
        "Rotate": 0,
        "Size": 7700180,
        "VideoDuration": 60,
        "VideoStreamSet": [
          {
            "Bitrate": 637174,
            "Codec": "h264",
            "Fps": 23,
            "Height": 480,
            "Width": 640
          }
        ],
        "Width": 640
      },
      "MediaProcessResultSet": null,
      "AiContentReviewResultSet": null,
      "AiAnalysisResultSet": null,
      "TasksPriority": 0,
      "TasksNotifyMode": ""
    },
    "EditMediaTask": null,
    "WechatPublishTask": null,
    "TranscodeTask": null,
    "SnapshotByTimeOffsetTask": null,
    "ConcatTask": null,
    "ClipTask": null,
    "CreateImageSpriteTask": null,
    "RequestId": "sdfadf"
  }
}
```
### Sample 2. Getting Task Details - Transcode
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=DescribeTaskDetail
&TaskId=12567683xx-transcode-58a1bc57b1c23ed1079597ec17a47666t0
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "TaskType": "Transcode",
    "Status": "FINISH",
    "CreateTime": "2019-01-22T06:50:31Z",
    "BeginProcessTime": "2019-01-22T06:50:32Z",
    "FinishTime": "2019-01-22T06:50:45Z",
    "ProcedureTask": null,
    "EditMediaTask": null,
    "TranscodeTask": {
      "TaskId": "12567683xx-transcode-58a1bc57b1c23ed1079597ec17a47666t0",
      "ErrCode": 0,
      "Message": "",
      "FileId": "5285890784246869930",
      "FileName": "small",
      "Duration": 60,
      "CoverUrl": "http://12567683xx.vod2.myqcloud.com/d042887avodtransgzp12567683xx/c643347c5285890784246869930/1546950643_4191274987.100_0.jpg",
      "PlayInfoSet": [
        {
          "Url": "http://12567683xx.vod2.myqcloud.com/1c1ae5d2vodgzp12567683xx/c643347c5285890784246869930/AtUCmy6gmIYA.mp4",
          "Definition": 0,
          "Bitrate": 1021028,
          "Height": 480,
          "Width": 640
        },
        {
          "Url": "http://12567683xx.vod2.myqcloud.com/d042887avodtransgzp12567683xx/c643347c5285890784246869930/v.f10.mp4",
          "Definition": 10,
          "Bitrate": 304695,
          "Height": 240,
          "Width": 320
        }
      ]
    },
    "SnapshotByTimeOffsetTask": null,
    "ConcatTask": null,
    "ClipTask": null,
    "CreateImageSpriteTask": null,
    "RequestId": "62597d15-3fad-4234-af1a-ed33602a6118"
  }
}
```
### Sample 3. Getting Task Details - EditMedia
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=DescribeTaskDetail
&TaskId=12530394xx-procedurev2-61c975da05662fd9d3bf9d89a63361c0t0
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "TaskType": "EditMedia",
    "Status": "FINISH",
    "CreateTime": "2019-02-25T10:56:02Z",
    "BeginProcessTime": "2019-02-25T10:56:02Z",
    "FinishTime": "2019-02-25T10:56:13Z",
    "ProcedureTask": null,
    "EditMediaTask": {
      "TaskId": "12530394xx-procedurev2-61c975da05662fd9d3bf9d89a63361c0t0",
      "Status": "FINISH",
      "ErrCode": 0,
      "Message": "",
      "Input": {
        "InputType": "Stream",
        "FileInfoSet": [
          {
            "FileId": "4565514956192708397",
            "StartTimeOffset": 0,
            "EndTimeOffset": 30
          },
          {
            "FileId": "4565514956192708396",
            "StartTimeOffset": 0,
            "EndTimeOffset": 30
          }
        ],
        "StreamInfoSet": [
          {
            "StreamId": "29920_stream",
            "StartTime": "2019-02-20T06:21:00Z",
            "EndTime": "2019-02-20T06:21:30Z"
          }
        ]
      },
      "Output": {
        "FileType": "",
        "FileId": "4565514956222184986",
        "FileUrl": "http://12530394xx.vod2.myqcloud.com/9395476dvodcq1253039488/f0e1f8314565514956222184986/playlist.f9.mp4"
      },
      "ProcedureTaskId": ""
    },
    "WechatPublishTask": null,
    "TranscodeTask": null,
    "SnapshotByTimeOffsetTask": null,
    "ConcatTask": null,
    "ClipTask": null,
    "CreateImageSpriteTask": null,
    "RequestId": "sdfadf"
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
|| InvalidParameter | A parameter is not valid or cannot be used for the request.  |
| InvalidParameterValue.SubAppId | The sub-application ID is invalid or unfounded. |
| InvalidParameterValue.TaskId | The task ID does not exist in our records. |
| ResourceNotFound | The specified resource does not exist or is not found. |


