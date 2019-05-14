## 1. API Description
API domain name: vod.tencentcloudapi.com.
* This API is used to query the task list;
* If there are many data entries in the list, one single call of the API may not be able to pull the entire list. The ScrollToken parameter can be used to pull the list in batches;
* Only tasks in the past three days (72 hours) can be queried.
Default API request rate limit: 100 requests/sec.
## 2. Input Parameters
The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/266/31756).
| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeTasks |
| Version | Yes | String | Common parameter; the value for this API: 2018-07-17 |
| Region | No | String | Common parameter; not passed in for this API |
| Status | Yes | String | Filter: Task status; value range: WAITING (waiting), PROCESSING (processing), FINISH (finished). |
| FileId | No | String | Filter: File ID. |
| Limit | No | Integer | Number of returned entries; 10 by default, up to 100. |
| ScrollToken | No | String | Scrolling identifier which is used for pulling in batches: If a single request cannot pull all the data entries, the API will return the ScrollToken, and if the next request carries it, the next pull will start from the next entry. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). If you need to access a resource in a sub-application, enter the sub-application ID in this field; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| TaskSet | Array of [TaskSimpleInfo](/document/api/266/31773#TaskSimpleInfo) | Task overview list. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| ScrollToken | String | Scrolling identifier. If the request does not return all the data entries, this field indicates the ID of the next entry. If this field is blank, there is no more data. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |
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
**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=DescribeTasks)
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
| InvalidParameterValue.Status | Incorrect parameter value: The value of human confirmation result is invalid. |

