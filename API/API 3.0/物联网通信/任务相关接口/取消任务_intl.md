## 1. API Description

API request domain name: iotcloud.tencentcloudapi.com.

This API (CancelTask) is used to cancel an unscheduled task.

Default API request frequency limit: 100 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](https://cloud.tencent.com/document/api/634/19472).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: CancelTask |
| Version | Yes | String | Common parameter; the value for this API: 2018-06-14 |
| Region | No | String | Common parameter; not passed for this API |
| Id | Yes | String | Task ID |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Canceling a Task

#### Input Example

```
https://iotcloud.tencentcloudapi.com/?Action=CancelTask
&Id=5ad5aa513332ea4cb86e9ad5
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "RequestId": "xxxxxxxxxxxxxxxxxxxxxxx"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using Cloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=iotcloud&Version=2018-06-14&Action=CancelTask)

### SDK

Cloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. Error Codes

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/634/19474#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.AsyncTaskAlreadyStarted | The task has already started. |
| InternalError | Internal error |
| InvalidParameterValue | Wrong parameter value |
| ResourceNotFound.TaskNotExist | Task does not exist. |
