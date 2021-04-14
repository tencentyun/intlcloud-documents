## 1. API Description

Domain name for API request: billing.tencentcloudapi.com.

This API is used to get the bill summarized by region.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/555/19173).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value used for this API: DescribeBillSummaryByRegion |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-09 |
| Region | No | String | Common parameter; this parameter is not required for this API. |
| PayerUin | Yes | String | Query payer’s UIN |
| BeginTime | Yes | String | Currently only supports starting from the current month, and the month must be the same as that set for EndTime. For example, 2018-09-01 00:00:00. |
| EndTime | Yes | String | Currently only supports ending in the current month, and the month must be the same as that set for BeginTime. For example, 2018-09-30 23:59:59. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| Ready | Integer | Indicates whether the data is ready. 0 = not ready, 1 = ready |
| SummaryOverview | Array of [RegionSummaryOverviewItem](https://cloud.tencent.com/document/api/555/19183#RegionSummaryOverviewItem) | Detailed cost distribution for all regions<br/>Note: This field may return null, indicating that no valid values can be obtained. |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Examples

### Example 1: Getting the bill summarized by region

### Input example

```
https://billing.tencentcloudapi.com/?Action=DescribeBillSummaryByRegion
&PayerUin=909619400
&BeginTime=2018-11-01 00:00:00
&EndTime=2018-11-01 23:59:59
&<Common Request Parameters>
```

#### Output example

```
{
  "Response": {
    "Ready": 1,
    "SummaryOverview": [
      {
        "RegionId": "4",
        "RealTotalCost": "1330.52",
        "CashPayAmount": "1330.52",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "83.26",
        "BillMonth": "2018-11",
        "RegionName": "East China (Shanghai)"
      },
      {
        "RegionId": "1",
        "RealTotalCost": "200.85",
        "CashPayAmount": "24.87",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "175.99",
        "RealTotalCostRatio": "12.57",
        "BillMonth": "2018-11",
        "RegionName": "South China (Guangzhou)",
      },
      {
        "RegionId": "8",
        "RealTotalCost": "66.58",
        "CashPayAmount": "66.58",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "4.17",
        "BillMonth": "2018-11",
        "RegionName": "North China (Beijing)",
      },
      {
        "RegionId": "16",
        "RealTotalCost": "0.02",
        "CashPayAmount": "0.02",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "0.00",
        "BillMonth": "2018-11",
        "RegionName": "Southwest China (Chengdu)"
      },
      {
        "RegionId": "19",
        "RealTotalCost": "0.00",
        "CashPayAmount": "0.00",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "0.00",
        "BillMonth": "2018-11",
        "RegionName": "Southwest China (Chongqing)"
      },
      {
        "RegionId": "24",
        "RealTotalCost": "0.00",
        "CashPayAmount": "0.00",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "0.00",
        "BillMonth": "2018-11",
        "RegionName": "Europe (Moscow)"
      },
      {
        "RegionId": "6",
        "RealTotalCost": "0.00",
        "CashPayAmount": "0.00",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "0.00",
        "BillMonth": "2018-11",
        "RegionName": "North America (Toronto)",
      },
      {
        "RegionId": "9",
        "RealTotalCost": "0.00",
        "CashPayAmount": "0.00",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "0.00",
        "BillMonth": "2018-11",
        "RegionName": "Southeast Asia (Singapore)",
      },
      {
        "RegionId": "17",
        "RealTotalCost": "0.00",
        "CashPayAmount": "0.00",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "0.00",
        "BillMonth": "2018-11",
        "RegionName": "Europe (Germany)"
      },
      {
        "RegionId": "5",
        "RealTotalCost": "0.00",
        "CashPayAmount": "0.00",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "0.00",
        "BillMonth": "2018-11",
        "RegionName": "Hong Kong/Macao/Taiwan (Hong Kong, China)"
      },
      {
        "RegionId": "0",
        "RealTotalCost": "-1.49",
        "CashPayAmount": "-1.50",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.01",
        "RealTotalCostRatio": "0.00",
        "BillMonth": "2018-11",
        "RegionName": "Other"
      }
    ],
    "RequestId": "88268803-850d-44bc-8d64-df857c2d7487"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=billing&Version=2018-07-09&Action=DescribeBillSummaryByRegion)

### SDK

TencentCloud API 3.0 integrates SDKs that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. Error Codes

There are no error codes related to this API. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/555/19175#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).
