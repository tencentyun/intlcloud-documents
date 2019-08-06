## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (RenewDBInstance) renews the specified database instance.

API request rate limit: 20 requests/sec.

Note: This API supports financial regions. Because financial regions and non-financial regions are isolated, when the common parameter Region is specified as financial region, such as ap-shanghai-fsi, you need to also specify a financial region preferably the same as Region in the domain name, for example, sqlserver.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: RenewDBInstance |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID, for example, mssql-j8kv137v |
| Period | No | Integer | Length of renewal cycle in month. Value range: 1-48.  Default is 1. |
| AutoVoucher | No | Integer | Whether to automatically use vouchers. 0: no, 1: yes. No by default |
| VoucherIds.N | No | Array of String | Array of voucher IDs (currently, only one voucher can be used at a time) |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| DealName | String | Order name |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Renewing an Instance

#### Input Sample Code

```
https://sqlserver.tencentcloudapi.com/?Action=RenewDBInstance
&InstanceId=mssql-j8kv137v
&Period=2
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "4be5990d-a4b5-49dc-b2b4-e713b6aa7ba3",
    "DealName": "201806261980"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=RenewDBInstance)

### SDK

TencentCloud API 3.0 integrates SDKs that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/238/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.CreateOrderFailed | Failed to create the order. |
| InternalError.DBError | Database error. |
| InvalidParameter.InputIllegal | Invalid input. |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion error. |
| InvalidParameterValue.IllegalSpec | Invalid instance specification information. |
| ResourceNotFound.InstanceNotFound | The instance does not exist. |
