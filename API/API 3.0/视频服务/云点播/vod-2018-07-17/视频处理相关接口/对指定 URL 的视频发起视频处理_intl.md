## 1. API Description
API domain name: vod.tencentcloudapi.com.  
This API initiates a task to process a audio or video files downloaded from a URL. The tasks include:
1. Intelligent content review (detection of pornographic, terrorism, and politically sensitive information);
2. Intelligent content analysis (tag, category, an cover). 

Default API request rate limit: 100 requests/sec.

## 2. Input Parameters
The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/266/31756).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ProcessMediaByUrl |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-17 |
| Region | No | String | Common parameter; optional for this API |
| InputInfo | No | [MediaInputInfo](/document/api/266/31773#MediaInputInfo) | Information of the input video, including video's URL, name, and custom ID. |
| OutputInfo | No | [MediaOutputInfo](/document/api/266/31773#MediaOutputInfo) | Information of the COS path for the output file. |
| AiContentReviewTask | No | [AiContentReviewTaskInput](/document/api/266/31773#AiContentReviewTaskInput) | Parameter of the video content review task. |
| AiAnalysisTask | No | [AiAnalysisTaskInput](/document/api/266/31773#AiAnalysisTaskInput) | Parameter of the video content analysis task. |
| TasksPriority | No | Integer | Priority of the task flow. The higher the value, the higher the priority. Value range: -10 to 10; if you leave this field blank, the API will recognize it as 0. |
| TasksNotifyMode | No | String | Mode of task flow status notification . Valid values : Finish, Change and None; if you leave this field blank, the API will recognize it as Finish. |
| SourceContext | No | String | The source context passed along with the request. The upload callback API will return this value. Maximum 250 characters allowed. |
| SessionId | No | String | The ID used for deduplication. If there was a request with the same ID in the past seven days, the current request will return an error. Up to 50 characters. If missing or with a blank string, no deduplication is performed. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). Input the ID of the sub-application that has the desired resources; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| TaskId | String | Task ID |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

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
**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=ProcessMediaByUrl)

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
| InternalError.GetFileInfoError | Failed to get media file information. |
| InvalidParameter | A parameter is not valid or cannot be used for the request.  |
| InvalidParameterValue.AiAnalysisTaskDefinition |The input value of AI-analyzed *Definition* is invalid. |
| InvalidParameterValue.AiContentReviewTaskDefinition | The value of *Definition* of AI-reviewed content is invalid. |
| InvalidParameterValue.SessionContextTooLong | The length of session context exceeds the limit.|
| InvalidParameterValue.SessionId | The session ID already exists. The request is removed due to duplication. |
| InvalidParameterValue.SessionIdTooLong | The length of the session ID is too long. |
| InvalidParameterValue.SubAppId | The sub-application ID is invalid or unfounded. |

