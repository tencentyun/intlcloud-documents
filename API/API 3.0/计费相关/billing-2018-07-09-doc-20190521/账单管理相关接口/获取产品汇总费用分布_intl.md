## 1. API Description

Domain name for API request: billing.tencentcloudapi.com.

This API is used to get the bill summarized by product.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/555/19173).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value used for this API: DescribeBillSummaryByProduct |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-09 |
| Region | No | String | Common parameter; this parameter is not required for this API. |
| PayerUin | Yes | String | Query payer’s UIN |
| BeginTime | Yes | String | Currently only supports starting from the current month, and the month must be the same as that set for EndTime. For example, 2018-09-01 00:00:00. |
| EndTime | Yes | String | Currently only supports ending in the current month, and the month must be the same as that set for BeginTime. For example, 2018-09-30 23:59:59. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| Ready | Integer | Indicates whether the data is ready. 0 = not ready, 1 = ready |
| SummaryTotal | [BusinessSummaryTotal](https://cloud.tencent.com/document/api/555/19183#BusinessSummaryTotal) | Total cost details<br/>Note: This field may return null, indicating that no valid values can be obtained. |
| SummaryOverview | Array of [BusinessSummaryOverviewItem](https://cloud.tencent.com/document/api/555/19183#BusinessSummaryOverviewItem) | Cost distribution of all products<br/>Note: This field may return null, indicating that no valid values can be obtained.|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Examples

### Example 1: Getting the bill summarized by product

#### Input example

```
https://billing.tencentcloudapi.com/?Action=DescribeBillSummaryByProduct
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
    "SummaryTotal": {
      "RealTotalCost": "1596.49",
      "VoucherPayAmount": "176.00",
      "IncentivePayAmount": "0.00",
      "CashPayAmount": "1420.49"
    },
    "SummaryOverview": [
      {
        "BusinessCode": "p_cvm",
        "RealTotalCost": "540.00",
        "CashPayAmount": "540.00",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "33.77",
        "BillMonth": "2018-11",
        "BusinessCodeName": "CVM"
      },
      {
        "BusinessCode": "p_cbs",
        "RealTotalCost": "536.54",
        "CashPayAmount": "536.54",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "33.57",
        "BillMonth": "2018-11",
        "BusinessCodeName": "CBS"
      },
      {
        "BusinessCode": "p_cos",
        "RealTotalCost": "219.44",
        "CashPayAmount": "219.44",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "13.73",
        "BillMonth": "2018-11",
        "BusinessCodeName": "COS"
      },
      {
        "BusinessCode": "p_ai_image_ocr",
        "RealTotalCost": "169.83",
        "CashPayAmount": "0.01",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "169.82",
        "RealTotalCostRatio": "10.62",
        "BillMonth": "2018-11",
        "BusinessCodeName": "OCR"
      },
      {
        "BusinessCode": "p_yunjing",
        "RealTotalCost": "81.00",
        "CashPayAmount": "81.00",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "5.07",
        "BillMonth": "2018-11",
        "BusinessCodeName": "Host Security"
      },
      {
        "BusinessCode": "p_blackstone_eip",
        "RealTotalCost": "45.00",
        "CashPayAmount": "45.00",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "2.82",
        "BillMonth": "2018-11",
        "BusinessCodeName": "BM EIP"
      },
      {
        "BusinessCode": "p_ai_image",
        "RealTotalCost": "4.78",
        "CashPayAmount": "0.00",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "4.78",
        "RealTotalCostRatio": "0.30",
        "BillMonth": "2018-11",
        "BusinessCodeName": "Image recognition"
      },
      {
        "BusinessCode": "p_ai_image_facerecognize",
        "RealTotalCost": "1.39",
        "CashPayAmount": "0.00",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "1.39",
        "RealTotalCostRatio": "0.09",
        "BillMonth": "2018-11",
        "BusinessCodeName": "Face recognition"
      },
      {
        "BusinessCode": "p_cdn",
        "RealTotalCost": "0.46",
        "CashPayAmount": "0.46",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "0.03",
        "BillMonth": "2018-11",
        "BusinessCodeName": "CDN"
      },
      {
        "BusinessCode": "p_ci",
        "RealTotalCost": "0.00",
        "CashPayAmount": "0.00",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "0.00",
        "BillMonth": "2018-11",
        "BusinessCodeName": "CI"
      },
      {
        "BusinessCode": "p_cmq",
        "RealTotalCost": "0.00",
        "CashPayAmount": "0.00",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.00",
        "RealTotalCostRatio": "0.00",
        "BillMonth": "2018-11",
        "BusinessCodeName": "CMQ"
      },
      {
        "BusinessCode": "billVirtualId",
        "RealTotalCost": "-1.95",
        "CashPayAmount": "-1.96",
        "IncentivePayAmount": "0.00",
        "VoucherPayAmount": "0.01",
        "RealTotalCostRatio": "0.00",
        "BillMonth": "2018-11",
        "BusinessCodeName": "Monthly billing precision discrepancy"
      }
    ],
    "RequestId": "8a57841e-ef77-413d-a8ba-4c607173663c"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=billing&Version=2018-07-09&Action=DescribeBillSummaryByProduct)

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
