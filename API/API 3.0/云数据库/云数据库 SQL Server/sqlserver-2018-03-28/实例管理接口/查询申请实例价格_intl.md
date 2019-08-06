## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (InquiryPriceCreateDBInstances) inquires the price to create an database instance.

API request rate limit: 20 requests/sec.


## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: InquiryPriceCreateDBInstances |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Zone | Yes | String | Availability Zone ID. You can call DescribeZones API and you will find this value in the Zone field in the output parameters |
| Memory | Yes | Integer | Memory size in GB |
| Storage | Yes | Integer | Instance storage capacity in GB |
| InstanceChargeType | No | String | Billing method. Valid values include PREPAID and POSTPAID |
| Period | No | Integer | Length of subscription in month. Value range: 1-48. The default is 1 |
| GoodsNum | No | Integer | Number of instances purchased at a time. Value range: 1-100. The default is 1 |
| DBVersion | No | String | SQL Server version. Currently, only the following versions are supported: 2008R2 (SQL Server 2008 Enterprise), 2012SP3 (SQL Server 2012 Enterprise), 2016SP1 (SQL Server 2016 Enterprise) and 201602 (SQL Server 2016 Standard). 2008R2 by default |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| OriginalPrice | Integer | Price before discount. This value divided by 100 indicates the price |
| Price | Integer | The actual price to be paid. This value divided by 100 indicates the price |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Inquiring the Price of the Requested SQL Server Instance

#### Input Sample Code

```
https://sqlserver.tencentcloudapi.com/?Action=InquiryPriceCreateDBInstances
&Zone=ap-guangzhou-2
&Memory=2
&Storage=300
&Period=1
&GoodsNum=1
&DBVersion=2008R2
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "6ace8140-6b9e-4e81-a8ad-ef3f92b2aa90",
    "OriginalPrice": 20988,
    "Price": 20988
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=InquiryPriceCreateDBInstances)

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
| InvalidParameter.InputIllegal | Invalid input. |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion error. |
| InvalidParameterValue.BadGoodsNum | Invalid number of purchased instances. |
| InvalidParameterValue.IllegalRegion | Invalid region. |
| InvalidParameterValue.IllegalSpec | Invalid instance specification information. |
| InvalidParameterValue.IllegalZone | Invalid AZ ID. |
| InvalidParameterValue.ParameterTypeError | Incorrect parameter type. |
