## 1. API Description

Domain name for API request: sqlserver.tencentcloudapi.com

This API (InquiryPriceCreateDBInstances) is used to query the price of the instance you apply for.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: sqlserver.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/238/19930).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: InquiryPriceCreateDBInstances |
| Version | Yes | String | Common parameter. The value used for this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Zone | Yes | String | Availability zone ID. You can obtain it from the Zone field in the returned value of API DescribeZones. |
| Memory | Yes | Integer | Memory capacity of the instance (in GB) |
| Storage | Yes | Integer | Capacity of the instance (in GB) |
| InstanceChargeType | No | String | Billing method. Only PREPAID (default) is supported. |
| Period | No | Integer | Purchased validity period of the instance (months). The value should range from 1 to 48, and defaults to 1. |
| GoodsNum | No | Integer | The number of instances purchased this time. The value should range from 1 to 100, and defaults to 1. |
| DBVersion | No | String | DB for SQLServer version. Supported values include 2008R2 (SQL Server 2008 R2), 2012SP3 (SQL Server 2012) and 2016SP1 (SQL Server 2016 SP1). It defaults to 2008R2. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| OriginalPrice | Integer | Indicates the original price before discount, which is obtained by dividing the value by 100. For example, 10010 indicates CNY 100.10. |
| Price | Integer | Indicates the actual price to be paid after discount, which is obtained by dividing the value by 100. For example, 10010 indicates CNY 100.10. |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query the price of the DB for SQL Server instance you apply for.

#### Input example

```
https://sqlserver.tencentcloudapi.com/?Action=InquiryPriceCreateDBInstances
&Zone=ap-guangzhou-2
&Memory=2
&Storage=300
&Period=1
&GoodsNum=1
&DBVersion=2008R2
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "OriginalPrice": 20988,
    "Price": 20988,
    "RequestId": "6ace8140-6b9e-4e81-a8ad-ef3f92b2aa90"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=InquiryPriceCreateDBInstances)

### SDK

Cloud API 3.0 comes with the software development kit (SDK) that supports multiple programming languages and makes it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](/document/api/238/19932#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.QueryPriceFailed | Billing error. Failed to query the price. |
| InternalError.DBError | Database error |
| InvalidParameter.InputIllegal | Invalid input parameter |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion failed |
| InvalidParameterValue.BadGoodsNum | Incorrect number of purchased instances |
| InvalidParameterValue.IllegalRegion | Invalid region |
| InvalidParameterValue.IllegalSpec | Invalid instance specification |
| InvalidParameterValue.IllegalZone | Invalid availability zone ID |
| InvalidParameterValue.ParameterTypeError | Invalid parameter type |

