## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (InquiryPriceRenewDBInstance) inquires the price to renew the specified database instance.

API request rate limit: 20 requests/sec.

Note: This API supports financial regions. Because financial regions and non-financial regions are isolated, when the common parameter Region is specified as financial region, such as ap-shanghai-fsi, you need to also specify a financial region preferably the same as Region in the domain name, for example, sqlserver.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: InquiryPriceRenewDBInstance |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID |
| Period | No | Integer | Length of renewal cycle; maximum 48 months. The default is one month |
| TimeUnit | No | String | Unit of renewal cycle. *month*: the renewal cycle is calculated on monthly basis. Currently, only monthly renewal price can be inquired |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| OriginalPrice | Integer | Price before discount. This value divided by 100 indicates the price; for example, 10094 means 100.94 CNY |
| Price | Integer | The actual price to be paid. This value divided by 100 indicates the price; for example, 10094 means 100.94 CNY |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Inquiring the Renewal Price of a Single Instance

#### Input Sample Code

```
https://sqlserver.tencentcloudapi.com/?Action=InquiryPriceRenewDBInstance
&InstanceId=mssql-njj2mtpl
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "41e0018d-857d-4c8c-9763-57afa2c062f9",
    "OriginalPrice": 42720,
    "Price": 42720
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=InquiryPriceRenewDBInstance)

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
| FailedOperation.QueryPriceFailed | Billing error. Failed to query the price. |
| InternalError.DBError | Database error. |
| InternalError.SystemError | System error. |
| InvalidParameter.InputIllegal | Invalid input. |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion error. |
| InvalidParameterValue.IllegalRegion | Invalid region. |
| InvalidParameterValue.ParameterTypeError | Incorrect parameter type. |
| ResourceNotFound.InstanceNotFound | The instance does not exist. |
