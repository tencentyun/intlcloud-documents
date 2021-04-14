## 1. API Description

Domain name for API request: billing.tencentcloudapi.com.

This API is used to query bill resources summary. 

Default API request rate limit: 5 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/555/19173).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value used for this API: DescribeBillResourceSummary |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-09 |
| Region | No | String | Common parameter; this parameter is not required for this API. |
| Offset | Yes | Integer | Offset |
| Limit | Yes | Integer | Quantity, maximum is 1,000 |
| PeriodType | Yes | String | The period type. byUsedTime: By usage period.|
| Month | Yes | String | Month; format: yyyy-mm. This value must be no earlier than March 2019, when Bill 2.0 was launched; only the last 24 months data can be retrieved. |
| NeedRecordNum | No | Integer | Indicates whether the total number of records is required, used for pagination. <br/>1 = required,  0 = not required |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| ResourceSummarySet | Array of [BillResourceSummary](https://cloud.tencent.com/document/api/555/19183#BillResourceSummary) | Resource summary list|
| Total | Integer | Total number of resource summary lists <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Examples

### Example 1: Getting bill resources summary

#### Input example

```
https://billing.tencentcloudapi.com/?Action=DescribeBillResourceSummary
&Month=2018-08
&PeriodType=byPayTime
&Offset=0
&Limit=1
&<Common Request Parameters>
```

#### Output example

```
{
  "Response": {
    "ResourceSummarySet": [
      {
        "PayerUin": "2384822478",
        "OwnerUin": "-",
        "OperateUin": "-",
        "BusinessCodeName": "CVM",
        "ProductCodeName": "-",
        "PayModeName": "Pay-as-You-Go",
        "ProjectName": "Default project",
        "RegionName": "North America (Toronto)",
        "ZoneName": "Toronto Zone 1",
        "ResourceId": "ins-o0z91q0p",
        "ResourceName": "Not named",
        "ActionTypeName": "Pay-as-You-Go deduction",
        "OrderId": "-",
        "PayTime": "-",
        "FeeBeginTime": "2018-08-28 21:00:00",
        "FeeEndTime": "2018-08-28 21:00:02",
        "ConfigDesc": "CPU: 1 core; Memory: 1GiB; System disk: 50GB; ",
        "ExtendField1": "-",
        "ExtendField2": "-",
        "ExtendField3": "-",
        "ExtendField4": "-",
        "ExtendField5": "-",
        "TotalCost": "155.04348856",
        "Discount": "0.6",
        "ReduceType": "Discount",
        "RealTotalCost": "93.039956",
        "VoucherPayAmount": "0",
        "CashPayAmount": "93.039956",
        "IncentivePayAmount": "0"
      }
    ],
    "Total": 103,
    "RequestId": "02917e78-03af-4a7a-855d-d48705108ab2"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=billing&Version=2018-07-09&Action=DescribeBillResourceSummary)

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
| FailedOperation.SummaryDataNotReady | Summary is in compilation. Please try again later. |
