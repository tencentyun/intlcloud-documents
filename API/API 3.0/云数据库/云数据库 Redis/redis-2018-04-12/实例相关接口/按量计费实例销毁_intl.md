## 1. API Description

API domain name: redis.tencentcloudapi.com.

Terminate a pay-as-you-go instance

Default API request rate limit: 20 requests/sec.

Note: This API supports financial availability zones. As financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), it is necessary to specify a domain name with the financial availability zone too, preferably in the same region as specified in Region, such as redis.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/239/20005).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DestroyPostpaidInstance |
| Version | Yes | String | Common parameter; the value for this API: 2018-04-12 |
| Region | Yes | String | Common parameters; for details, see the [List of Regions](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TaskId | Integer | Task ID |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided during troubleshooting. |

## 4. Sample

### Sample 1. Terminating a Pay-as-you-go Instance

#### Input Sample Code

```
https://redis.tencentcloudapi.com/?Action=DestroyPostpaidInstance
&InstanceId=crs-5a4py64p
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TaskId": "6954227",
    "RequestId": "4daddc97-0005-45d8-b5b8-38514ec1e97c"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DestroyPostpaidInstance)

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

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/239/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.DbOperationFailed | Internal system error with the DB operation, which may be update, insert, select, etc. |
| InternalError.InternalError | Internal error. |
| InvalidParameter | Parameter error |
| InvalidParameter.PermissionDenied | The API has no CAM permissions. |
| ResourceNotFound.InstanceNotExists | No Redis instance found by the serialId. |
| UnauthorizedOperation | Unauthorized operation. |
| UnauthorizedOperation.NoCAMAuthed | No CAM permissions. |
| UnauthorizedOperation.UserNotInWhiteList | User is not in the whitelist. |
