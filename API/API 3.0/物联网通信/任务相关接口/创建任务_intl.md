## 1. API Description

API request domain name: iotcloud.tencentcloudapi.com.

This API (CreateTask) is used to create a batch task. Currently, this API can create tasks for batch updating shadows and batch publishing messages.

Default API request frequency limit: 100 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/634/19472).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: CreateTask |
| Version | Yes | String | Common parameter; the value for this API: 2018-06-14 |
| Region | No | String | Common parameter; not passed for this API |
| TaskType | Yes | String | Task type; value: "UpdateShadow" or "PublishMessage" |
| ProductId | Yes | String | ID of the product that executes the task |
| DeviceNameFilter | Yes | String | Regular expression for the name of the device that executes the task |
| ScheduleTimeInSeconds | Yes | Integer | The time at which the task starts execution. The value is a Unix timestamp in seconds, which should be greater than or equal to the current timestamp. 0 is the current timestamp of the system, meaning immediate execution. The maximum value is 86400 seconds after the current time, and if exceeded, the value would be 86400 seconds after the current time |
| Tasks | Yes | [Task](/document/api/634/19497#Task) | Task description details (see Task below) |
| MaxExecutionTimeInSeconds | No | Integer | The maximum execution time in seconds. If no result is presented after this time lapses after scheduling, the task is considered to have failed. Value range: 0-86400; 86400 by default |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TaskId | String | ID of the created task |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Creating a Task

#### Input Example

```
https://iotcloud.tencentcloudapi.com/?Action=CreateTask
&TaskType=UpdateShadow
&ProductId=ABCDE12345
&DeviceNameFilter=
&ScheduleTimeInSeconds=0
&MaxExecutionTimeInSeconds=
&Tasks.UpdateShadowTask.Desired={\"color\":\"red\"}
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "RequestId": "xxxxxxxxxxxxxxxxxxxxxxx",
    "TaskId": "dsaudhuisadhada"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using Cloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=iotcloud&Version=2018-06-14&Action=CreateTask)

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
| LimitExceeded.PengingOrProcessingTasksExceedLimit | Too many tasks in waiting and processing status. |
| ResourceNotFound.ProductNotExist | Product does not exist. |
