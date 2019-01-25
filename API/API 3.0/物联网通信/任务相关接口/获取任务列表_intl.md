## 1. API Description

API request domain name: iotcloud.tencentcloudapi.com.

This API (DescribeTasks) is used to query the list of tasks that have been created. The tasks are retained for one month.

Default API request frequency limit: 100 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/634/19472).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeTasks |
| Version | Yes | String | Common parameter; the value for this API: 2018-06-14 |
| Region | No | String | Common parameter; not passed for this API |
| Offset | Yes | Integer | Page offset, starting at 0 |
| Limit | Yes | Integer | Page size; value range: 1-250 |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of tasks created by the user in one month |
| Tasks | Array of [TaskInfo](/document/api/634/19497#TaskInfo) | Array of task objects in this page, sorted by creation time |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Getting Task List

#### Input Example

```
https://iotcloud.tencentcloudapi.com/?Action=DescribeTasks
&Offset=0
&Limit=10
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "TotalCount": 1,
    "Tasks": [
      {
        "Status": 3,
        "UpdateTime": 1523958284,
        "RetCode": 0,
        "Id": "5ad5b9a53332ea3de678ea52",
        "Type": "PublishMessage",
        "CreateTime": 1523956133,
        "ErrMsg": "",
        "ProductId": "ABCDE12345"
      }
    ],
    "RequestId": "xxxxxxxxxxxxxxxxxxxxxxx"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using Cloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=iotcloud&Version=2018-06-14&Action=DescribeTasks)

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
