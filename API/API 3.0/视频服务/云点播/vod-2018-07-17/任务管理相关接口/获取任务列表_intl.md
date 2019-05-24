## 1. API Description
API domain name: vod.tencentcloudapi.com.  
This API queries a list of tasks;
* When a list is too long, you may not be able to get a complete list through one API call. Instead, Add parameter ScrollToken to your request that allows you to retrieve the records in batches;
* You can only query the tasks in the most recent three days (72 hours).  
Default API request rate limit: 100 requests/sec.

## 2. Input Parameters
The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/266/31756).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ModifyTranscodeTemplate |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-17 |
| Region | No | String | Common parameter; optional for this API |
| Status | Yes | String | Filter the result by task status: WAITING, PROCESSING, FINISH. |
| FileId | No | String | Filter the result by file ID. |
| Limit | No | Integer | Number of returned entries; 10 by default, up to 100. |
| ScrollToken | No | String | The token for scrolling the result. The API returns a ScrollToken when it cannot retrieve all the result at once. Add this token to your next request to prevent getting repeated records. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). Input the ID of the sub-application that has the desired resources; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| TaskSet | Array of [TaskSimpleInfo](/document/api/266/31773#TaskSimpleInfo) | The list of the task overview. <br/>Note: Null means no valid values returned. |
| ScrollToken | String | The token for scrolling the result. If the request does not return all the data entries, this parameter returns a task ID following the last ID of the previous result. This parameter returns empty value means you have retrieved all of the records. <br/>Note: Null means no valid values returned. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample
### Sample 1. Getting Task List
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=DescribeTasks
&Status=FINISH
&Limit=5
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "TaskSet": [
      {
        "TaskId": "taskId1",
        "Type": "transcode",
        "CreateTime": "2018-12-27T13:57:15Z",
        "BeginProcessTime": "2018-12-27T13:57:15Z",
        "FinishTime": "2018-12-27T13:57:15Z"
      },
      {
        "TaskId": "taskId2",
        "Type": "transcode",
        "CreateTime": "2018-12-27T13:57:15Z",
        "BeginProcessTime": "2018-12-27T13:57:15Z",
        "FinishTime": "2018-12-27T13:57:15Z"
      },
      {
        "TaskId": "taskId3",
        "Type": "transcode",
        "CreateTime": "2018-12-27T13:57:15Z",
        "BeginProcessTime": "2018-12-27T13:57:15Z",
        "FinishTime": "2018-12-27T13:57:15Z"
      },
      {
        "TaskId": "taskId4",
        "Type": "transcode",
        "CreateTime": "2018-12-27T13:57:15Z",
        "BeginProcessTime": "2018-12-27T13:57:15Z",
        "FinishTime": "2018-12-27T13:57:15Z"
      },
      {
        "TaskId": "taskId5",
        "Type": "transcode",
        "CreateTime": "2018-12-27T13:57:15Z",
        "BeginProcessTime": "2018-12-27T13:57:15Z",
        "FinishTime": "2018-12-27T13:57:15Z"
      }
    ],
    "ScrollToken": "taskId6",
    "RequestId": "46311b39-10ce-47eb-b2b6-7ce82bb4476d"
  }
}
```
### Sample 2. Getting Task List - Scrolling
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=DescribeTasks
&Status=FINISH
&Limit=5
&ScrollToken=taskId6
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "TaskSet": [
      {
        "TaskId": "taskId6",
        "Type": "transcode",
        "CreateTime": "2018-12-27T13:57:15Z",
        "BeginProcessTime": "2018-12-27T13:57:15Z",
        "FinishTime": "2018-12-27T13:57:15Z"
      }
    ],
    "ScrollToken": null,
    "RequestId": "46311b39-10ce-47eb-b2b6-7ce82bb4476d"
  }
}
```
### Sample 3. Getting Task List - Processing
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=DescribeTasks
&Status=PROCESSING
&Limit=5
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "TaskSet": [
      {
        "TaskId": "taskId7",
        "Type": "transcode",
        "CreateTime": "2018-12-27T13:57:15Z",
        "BeginProcessTime": "2018-12-27T13:57:15Z",
        "FinishTime": null
      }
    ],
    "ScrollToken": null,
    "RequestId": "46311b39-10ce-47eb-b2b6-7ce82bb4476d"
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
| InvalidParameterValue.Status | We have confirmed that the input value of the parameter is invalid. |

