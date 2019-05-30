## 1. API Description

Domain name: billing.tencentcloudapi.com. 

This API queries the bill details by resource ID.

Default request rate limit: 5 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/555/19173). 

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeBillResourceSummary |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-09 |
| Region | No | String | Common parameter; optional for this API. |
| Offset | Yes | Integer | Offset |
| Limit | Yes | Integer | Quantity; maximum 1,000 |
| PeriodType | Yes | String | Billing period type. *byUsedTime*: By usage period; *byPayTime*: by payment period. This value must be the same as the billing period type in **Billing Center** for that particular month. |
| Month | Yes | String | Month; format: yyyy-mm. This value must be no earlier than the month when Bill 2.0 is activated; last 24 months data is available. |

## 3. Input Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| ResourceSummarySet | Array of [BillResourceSummary](/document/api/555/19183#BillResourceSummary) | Resource summary list|
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

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
**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**


* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=billing&Version=2018-07-09&Action=DescribeBillResourceSummary)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Code

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/555/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81). 

| Error Code | Description |
|---------|---------|
| FailedOperation.SummaryDataNotReady | The summary is not ready yet, please retry later. |
