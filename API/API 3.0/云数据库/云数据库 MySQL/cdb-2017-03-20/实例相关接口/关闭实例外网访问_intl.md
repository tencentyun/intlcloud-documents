## 1. API Description

Domain name for API request: cdb.tencentcloudapi.com.

This API (CloseWanService) is used to disable the access to a database instance from public network. After public network access is disabled, the database cannot be accessed from public IPs.

A maximum of 100 requests can be initiated per second for this API.

Note: This API supports Finance regions. Since Finance regions and non-Finance regions are isolated and not interconnected. If the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region that should be identical to the value of Region field, for example: cdb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/236/15692).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: CloseWanService |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-20 |
| Region | Yes |  String | Common parameter. For more information, please see the [list of regions](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/236/15692#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID, such as: cdb-c1nl9rpv. It is identical to the instance ID displayed in the database console page and can be obtained via API [Query Instance List](https://cloud.tencent.com/document/api/236/15872). Its value equals the InstanceId field value in the output parameters. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| AsyncRequestId | String | ID of async task request, which can be used to query the execution result of the async task. |
| RequestId | String | The unique request ID, which is returned for each request. RequestId is required for locating a problem. |

## 4. Error Codes

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/236/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameter | Parameter error. |
| InvalidParameter.InstanceNotFound | The instance does not exist. |
| OperationDenied | The operation is not allowed. |
| OperationDenied.WrongStatus | The backend task status is invalid. |

## 5. Example

### Example 1 Disable the access to an instance from public network

#### Input example

```
https://cdb.tencentcloudapi.com/?Action=CloseWanService
&InstanceId=cdb-ezq1vzem
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "AsyncRequestId": "841592f6-dd318344-aea19230-38912726",
    "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7"
  }
}
```


## 6. Other Resources

Cloud API 3.0 comes with the following development tools to make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)
* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

