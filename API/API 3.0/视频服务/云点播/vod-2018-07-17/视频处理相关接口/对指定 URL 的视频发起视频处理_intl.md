## 1. API Description
API domain name: vod.tencentcloudapi.com.
This API initiates a processing task for audio or video media that are from a URL, including:
1. Intelligent content review (detection of pornographic, terrorism, and politically sensitive information);
2. Intelligent content analysis (tag, category, an cover).
Default API request rate limit: 100 requests/sec.
## 2. Input Parameters
The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/266/31756).
| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: ProcessMediaByUrl |
| Version | Yes | String | Common parameter; the value for this API: 2018-07-17 |
| Region | No | String | Common parameter; not passed in for this API |
| InputInfo | No | [MediaInputInfo](/document/api/266/31773#MediaInputInfo) | Information of the input video, including video's URL, name, and custom ID. |
| OutputInfo | No | [MediaOutputInfo](/document/api/266/31773#MediaOutputInfo) | Information of the COS path for the output file. |
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
### Sample 1. Creating a Content Review Task
Initiate a content review task for a video whose URL is http://www.abc.com/abc.mp4.
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=ProcessMediaByUrl
&InputInfo.Url=http://www.abc.com/abc.mp4
&InputInfo.Name=Major Country Diplomacy
&InputInfo.Id=872988202
&OutputInfo.Region=ap-guangzhou
&OutputInfo.Bucket=myoutputbucket-1256244234
&OutputInfo.Dir=/output/test/
&AiContentReviewTask.Definition=10
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "RequestId": "5ca61e3a-6b8e-4b4e-9256-fdc701190064ef0",
    "TaskId": "125xxxxxx07-procedurev2-893dc41e6fdc22dcf24aa6e9c61cp94"
  }
}
```
### Sample 2. Creating a Content Analysis Task
Initiate a content analysis task for a video whose URL is http://www.abc.com/abc.mp4.
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=ProcessMediaByUrl
&InputInfo.Url=http://www.abc.com/abc.mp4
&InputInfo.Name=Major Country Diplomacy
&InputInfo.Id=872988202
&OutputInfo.Region=ap-guangzhou
&OutputInfo.Bucket=myoutputbucket-1256244234
&OutputInfo.Dir=/output/test/
&AiAnalysisTask.Definition=10
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "RequestId": "5ca61e3a-6b8e-4b4e-9256-fdc701190064ef0",
    "TaskId": "125xxxxxx07-procedurev2-813dc41e6fdc22dcf24aa6e9c61cp92"
  }
}
```
## 5. Developer Resources
### API Explorer
**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=ProcessMediaByUrl)
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
| InternalError.GetFileInfoError | Internal error: Error getting media file information. |
| InvalidParameter | Parameter error |
| InvalidParameterValue.AiAnalysisTaskDefinition | Incorrect parameter value: AI-based analysis definition. |
| InvalidParameterValue.AiContentReviewTaskDefinition | Incorrect parameter value: AI-based content review definition. |
| InvalidParameterValue.SessionContextTooLong | SessionContext is too long. |
| InvalidParameterValue.SessionId | The deduplication ID already exists. The request is removed due to duplication. |
| InvalidParameterValue.SessionIdTooLong | SessionId is too long. |
| InvalidParameterValue.SubAppId | Incorrect parameter value: Sub-application ID |

