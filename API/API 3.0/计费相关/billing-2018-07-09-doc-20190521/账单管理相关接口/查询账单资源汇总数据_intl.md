## 1. API Description

Domain name: billing.tencentcloudapi.com. 

This API is used to query the bill details by resource ID.

Default request rate limit: 5 requests/sec.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/555/19173). 

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeBillResourceSummary |
| Version | Yes | String | Common parameter; the value for this API: 2018-07-09 |
| Region | No | String | Common parameter; optional for this API. |
| Offset | Yes | Integer | Offset |
| Limit | Yes | Integer | Quantity; up to 1,000 |
| PeriodType | Yes | String | Period type; byUsedTime means by billing period while byPayTime means by deduction period. It must be the same as the period type of the particular month’s bill in **Billing Center**. |
| Month | Yes | String | Month; format: yyyy-mm. It cannot be earlier than the month when Bill 2.0 is activated and you can pull the data in 24 months only. |

## 3. Input Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| ResourceSummarySet | Array of [BillResourceSummary](/document/api/555/19183#BillResourceSummary) | Resource summary list|
| RequestId | String | A unique request ID which is returned for every request. RequestId for the current request needs to be provided for troubleshooting. |

## 4. Sample

### Sample 1 Getting the Bill Details by Resource ID

#### Input Sample Code

```
https://billing.tencentcloudapi.com/?Action=DescribeBillResourceSummary
&Month=2018-07
&PeriodType=byPayTime
&Offset=0
&Limit=1
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "ResourceSummarySet": [
      {
        "BusinessCodeName": "CVM",
        "ProductCodeName": "Standard S1",
        "PayModeName": "Pay-as-you-go resource",
        "ProjectName": "Default project",
        "RegionName": "South China (Guangzhou)",
        "ZoneName": “Guangzhou Zone 1",
        "ResourceId": "ins-abcdefgh",
        "ResourceName": "Test server",
        "ActionTypeName": "Monthly settlement",
        "OrderId": "20180808110089",
        "PayTime": "2018-08-08 11:22:33",
        "FeeBeginTime": "2018-08-08 11:25:00",
        "FeeEndTime": "2018-09-08 11:25:00",
        "ConfigDesc": "CPU:1 core; memory: 2 GB",
        "ExtendField1": "-",
        "ExtendField2": "-",
        "TotalCost": "1200",
        "Discount": "1",
        "ReduceType": "Discount",
        "RealTotalCost": "1200",
        "VoucherPayAmount": "300",
        "CashPayAmount": "400",
        "IncentivePayAmount": "500"
      }
    ]
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick API retrieval to greatly improve the efficiency of using TencentCloud APIs.** 

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=billing&Version=2018-07-09&Action=DescribeBillResourceSummary)

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

## 6. Error Code

The following only lists the error code related to the API business logic. For other error codes, see [Common Error Codes](/document/api/555/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81). 

| Error Code | Description |
|---------|---------|
| FailedOperation.SummaryDataNotReady | The summary list is being built, please retry later. |