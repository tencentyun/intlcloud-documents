## 1. API Description

API request domain name: iotcloud.tencentcloudapi.com.

This API (DescribeMultiDevices) is used to query the execution result of batch device creation.

Default API request frequency limit: 100 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/634/19472).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeMultiDevices |
| Version | Yes | String | Common parameter; the value for this API: 2018-06-14 |
| Region | No | String | Common parameter; not passed for this API |
| ProductId | Yes | String | The globally unique ID of the product assigned to the user by Tencent Cloud upon product creation |
| TaskId | Yes | String | Task ID, returned by the batch device creation API |
| Offset | Yes | Integer | Page offset |
| Limit | Yes | Integer | Page size; number of devices returned per page |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TaskId | String | Task ID, returned by the batch device creation API |
| DevicesInfo | Array of [MultiDevicesInfo](/document/api/634/19497#MultiDevicesInfo) | List of device details |
| TotalDevNum | Integer | Total number of devices created by this task |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Getting Result of Batch Device Creation

#### Input Example

```
https://iotcloud.tencentcloudapi.com/?Action=DescribeMultiDevices
&ProductId=ABCDE12345
&TaskId=abcdefghijklmn
&Offset=0
&Limit=10
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "DevicesInfo": [
      {
        "DevicePrivateKey": "-----BEGIN PRIVATE KEY-----\n-----END PRIVATE KEY-----\n",
        "DeviceName": "test_device1",
        "Result": 0,
        "DeviceCert": "-----BEGIN CERTIFICATE-----\n-----END CERTIFICATE-----"
      },
      {
        "DeviceName": "test_device2",
        "Result": 2001
      }
    ],
    "TotalDevNum": 2,
    "TaskId": "abcdedf123456789",
    "RequestId": "xxxxxxxxxxxxxxxxxxxxxxx"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using Cloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=iotcloud&Version=2018-06-14&Action=DescribeMultiDevices)

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
| FailedOperation.TaskIDNotMatch | User or product does not match the task ID. |
| InternalError | Internal error |
| InvalidParameterValue | Wrong parameter value |
| InvalidParameterValue.DeviceAlreadyExist | Name of the created device already exists. |
| LimitExceeded.DeviceExceedLimit | Number of devices exceeds the limit. |
| ResourceNotFound.TaskNotExist | Task does not exist. |
