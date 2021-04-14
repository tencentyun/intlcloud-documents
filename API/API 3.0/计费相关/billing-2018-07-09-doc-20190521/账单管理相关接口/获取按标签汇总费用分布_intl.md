## 1. API Description

Domain name for API request: billing.tencentcloudapi.com.

This API is used to get the bill summarized by tag.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/555/19173).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value used for this API: DescribeBillSummaryByTag |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-09 |
| Region | No | String | Common parameter; this parameter is not required for this API. |
| PayerUin | Yes | String | Query payer’s UIN |
| BeginTime | Yes | String | Currently only supports starting from the current month, and the month must be the same as that set for EndTime. For example, 2018-09-01 00:00:00. |
| EndTime | Yes | String | Currently only supports ending in the current month, and the month must be the same as that set for BeginTime. For example, 2018-09-30 23:59:59. |
| TagKey | Yes | String | Cost allocation tag key |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| Ready | Integer | Indicates whether the data is ready. 0 = not ready, 1 = ready |
| SummaryOverview | [TagSummaryOverviewItem](https://cloud.tencent.com/document/api/555/19183#TagSummaryOverviewItem) | Detailed cost distribution for all tags<br/>Note: This field may return null, indicating that no valid values can be obtained. |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Examples

### Example 1: Getting the bill summarized by tag

#### Input example

```
https://billing.tencentcloudapi.com/?Action=DescribeBillSummaryByTag
&PayerUin=100000007615
&BeginTime=2019-09-01 00:00:00
&EndTime=2019-09-30 23:59:59
&TagKey=province
&<Common Request Parameters>
```

#### Output example

```
{
  "Response": {
    "Ready": 1,
    "SummaryOverview": [
      {
        "TagValue": "",
        "RealTotalCost": "0.30",
        "RealTotalCostRatio": "17.08"
      },
      {
        "TagValue": "shanghai",
        "RealTotalCost": "0.26",
        "RealTotalCostRatio": "15.21"
      },
      {
        "TagValue": "beijing",
        "RealTotalCost": "0.26",
        "RealTotalCostRatio": "15.21"
      },
      {
        "TagValue": "guangdong",
        "RealTotalCost": "0.26",
        "RealTotalCostRatio": "15.21"
      },
      {
        "TagValue": "xiamen",
        "RealTotalCost": "0.22",
        "RealTotalCostRatio": "12.43"
      },
      {
        "TagValue": "tianjin",
        "RealTotalCost": "0.22",
        "RealTotalCostRatio": "12.43"
      },
      {
        "TagValue": "sichuan",
        "RealTotalCost": "0.22",
        "RealTotalCostRatio": "12.43"
      }
    ],
    "SummaryTotal": {
      "RealTotalCost": "1.74"
    },
    "RequestId": "b7649c63-59e5-49d3-bbde-64292cc4174d"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=billing&Version=2018-07-09&Action=DescribeBillSummaryByTag)

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

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/555/19175#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.TagKeyNotExist | The cost allocation tag key does not exist |
