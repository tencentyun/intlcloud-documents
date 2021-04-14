## 1. API Description

API domain name: gme.tencentcloudapi.com.

This API (ModifyAppStatus) is used to change the status of an application's master switch.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/607/35367).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Version | Yes | String | Common parameter. The value used for this API: ModifyAppStatus |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-11 |
| Region | No | String | Common parameter. This parameter is not required for this API |
| BizId | Yes | Integer | Application ID, which is generated and returned by the backend after application creation |
| Status | Yes | String | Application status. Value range: open, close |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| BizId | Integer | GME application ID |
| Status | String | Application status. Value range: open, close |

## 4. Samples

### Sample 1. Turning off GME Application 140000001

#### Input Sample Code

```
https://gme.tencentcloudapi.com/?Action=ModifyAppStatus
&BizId=140000001
&Status=close
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "Data": {
      "BizId": 140000001,
      "Status": "close"
    },
    "RequestId": "e2900289-f21e-43a8-a3bf-0b439cdbbbb8"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gme&Version=2018-07-11&Action=ModifyAppStatus)

### SDK

TencentCloud API 3.0 comes with SDKs that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/607/35370#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation | Operation failed. |
| FailedOperation.UserFeeNegative | Operation failed due to arrears. |
| InternalError | Internal error. |
| InvalidParameter | Invalid parameter. |
| MissingParameter. | Parameter missing. |
| ResourceNotFound | Resource does not exist. |
| ResourceNotFound.BizidIsNotFound | Application ID does not exist. |
| UnauthorizedOperation | Unauthorized operation. |
| UnknownParameter | Unknown parameter. |
| UnsupportedOperation | Unsupported operation. |
