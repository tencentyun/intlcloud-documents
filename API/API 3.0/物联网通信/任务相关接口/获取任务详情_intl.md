## 1. API Description

API request domain name: iotcloud.tencentcloudapi.com.

This API (DescribeTask) is used to query the details of a created task. The task is retained for one month.

Default API request frequency limit: 100 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/634/19472).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeTask |
| Version | Yes | String | Common parameter; the value for this API: 2018-06-14 |
| Region | No | String | Common parameter; not passed for this API |
| Id | Yes | String | Task ID |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Type | String | Task type; value: "UpdateShadow" or "PublishMessage" |
| Id | String | Task ID |
| ProductId | String | Product ID |
| Status | Integer | Status. 1 - waiting for processing, 2 - scheduling, 3 - completed, 4 - failed, 5 - canceled |
| CreateTime | Integer | Task creation time; a Unix timestamp |
| UpdateTime | Integer | Last update time of the task; a Unix timestamp |
| DoneTime | Integer | Task completion time; a Unix timestamp |
| ScheduleTime | Integer | Scheduled time; a Unix timestamp |
| RetCode | Integer | Error code returned |
| ErrMsg | String | Error messages returned |
| Percent | Integer | Proportion of devices that have completed the tasks |
| AllDeviceCnt | Integer | Number of devices matched to task execution |
| DoneDeviceCnt | Integer | Number of devices that have completed the tasks |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Getting Task Details

#### Input Example

```
https://iotcloud.tencentcloudapi.com/?Action=DescribeTask
&Id=5ad5aa513332ea4cb86e9ad5
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "Status": 3,
    "UpdateTime": 1523958284,
    "RetCode": 0,
    "DoneDeviceCnt": 2,
    "ScheduleTime": 1523956133,
    "DoneTime": 1523956134,
    "Percent": 0,
    "Id": "5ad5b9a53332ea3de678ea52",
    "RequestId": "xxxxxxxxxxxxxxxxxxxxxxx",
    "AllDeviceCnt": 2,
    "Type": "PublishMessage",
    "CreateTime": 1523956133,
    "ErrMsg": "",
    "ProductId": "ABCDE12345"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using Cloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=iotcloud&Version=2018-06-14&Action=DescribeTask)

### SDK

Cloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/634/19474#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameterValue | Wrong parameter value |
| ResourceNotFound.TaskNotExist | Task does not exist. |
