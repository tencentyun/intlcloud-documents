## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (InquiryPriceUpgradeDBInstance) inquires the price to upgrade the specified database instance.

API request rate limit: 20 requests/sec.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: InquiryPriceUpgradeDBInstance |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID in the format of mssql-njj2mtpl |
| Memory | Yes | Integer | Memory size after instance upgrade in GB, which cannot be smaller than the current instance memory size |
| Storage | Yes | Integer | Storage capacity after instance upgrade in GB, which cannot be smaller than the current instance storage capacity |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| OriginalPrice | Integer | Price before discount. This value divided by 100 indicates the price |
| Price | Integer | The actual price to be paid. This value divided by 100 indicates the price |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Inquiring the Scaling Price of an Instance

#### Input Sample Code

```
https://sqlserver.tencentcloudapi.com/?Action=InquiryPriceUpgradeDBInstance
&InstanceId=mssql-njj2mtpl
&Memory=8
&Storage=300
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "dcff5304-324e-4cd6-a5f2-02cb16bde2da",
    "OriginalPrice": 149696,
    "Price": 149696
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=InquiryPriceUpgradeDBInstance)

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
| InvalidParameterValue.InstanceExpandVolumeLow | The expansion capacity of the instance is lower than the current capacity. |
| InvalidParameterValue.ParameterTypeError | Incorrect parameter type. |
| ResourceNotFound.InstanceNotFound | The instance does not exist. |
