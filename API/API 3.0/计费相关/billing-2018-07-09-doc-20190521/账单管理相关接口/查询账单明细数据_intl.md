## 1. API Description

Domain name for API request: billing.tencentcloudapi.com.

This API is used to query bill details.

Default API request rate limit: 5 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/555/19173).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value used for this API: DescribeBillDetail |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-09 |
| Region | No | String | Common parameter; this parameter is not required for this API. |
| Offset | Yes | Integer | Offset |
| Limit | Yes | Integer | Quantity, maximum is 100 |
| PeriodType | Yes | String | The period type. byUsedTime: By usage period.|
|| Month | No | String | Month; format: yyyy-mm. You only have to enter either Month or BeginTime and EndTime. When you enter values for BeginTime and EndTime, Month becomes invalid. This value must be no earlier than March 2019, when Bill 2.0 was launched; only the last 24 months data can be retrieved.|
| BeginTime | No | String | The start time of the period; format: Y-m-d H:i:s. You only have to enter either Month or BeginTime and EndTime. When you enter values for BeginTime and EndTime, Month becomes invalid. BeginTime and EndTime must be inputted as a pair. This value must be no earlier than March 2019, when Bill 2.0 was launched; only the last 24 months data can be retrieved.|
| EndTime | No | String | The end time of the period; format: Y-m-d H:i:s. You only have to enter either Month or BeginTime and EndTime. When you enter values for BeginTime and EndTime, Month becomes invalid. BeginTime and EndTime must be inputted as a pair. This value must be no earlier than March 2019, when Bill 2.0 was launched; only the last 24 months data can be retrieved. |
| NeedRecordNum | No | Integer | Indicates whether the total number of records is required, used for pagination. <br/>1 = required, 0 = not required |
| ProductCode | No | String | Query specified product information |
| PayMode | No | String | Billing mode prePay/postPay |
| ResourceId | No | String | Query specified resource information |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| DetailSet | Array of [BillDetail](https://cloud.tencent.com/document/api/555/19183#BillDetail) | Details list|
| TotalNum | Integer | Total number of records <br/>Note: This field may return null, indicating that no valid values can be obtained.
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Examples

### Example 1: Getting bill details

#### Input example

```
https://billing.tencentcloudapi.com/?Action=DescribeBillDetail
&Month=2018-07
&PeriodType=byPayTime
&Offset=0
&Limit=1
&BeginTime=2018-11-01 00:00:00
&EndTime=2018-11-01 23:59:59
&NeedRecordNum=1
&ResourceId=ins-49zhx6z1
&<Common Request Parameters>
```

#### Output example

```
{
  "Response": {
    "DetailSet": [
      {
        "PayerUin": "2384822478",
        "OwnerUin": "2384822478",
        "OperateUin": "2384822478",
        "BusinessCodeName": "CVM",
        "ProductCodeName": "CVM-Standard S2",
        "PayModeName": "Pay-as-You-Go",
        "ProjectName": "Default project",
        "RegionName": "East China (Shanghai)",
        "ZoneName": "Shanghai Zone 2",
        "ResourceId": "ins-49zhx6z1",
        "ResourceName": "batch.env-g3bxot00",
        "ActionTypeName": "Pay-as-You-Go deduction",
        "OrderId": "2018110100",
        "BillId": "20181101020000206326013129313996",
        "PayTime": "2018-11-01 00:10:03",
        "FeeBeginTime": "2018-10-31 23:00:00",
        "FeeEndTime": "2018-11-01 00:00:00",
        "ComponentSet": [
          {
            "ComponentCodeName": "",
            "ItemCodeName": "",
            "SinglePrice": "0.25",
            "SpecifiedPrice": "0.25",
            "PriceUnit": "",
            "UsedAmount": "1",
            "UsedAmountUnit": "",
            "TimeSpan": "3600",
            "TimeUnitName": "Seconds",
            "Cost": "0.25",
            "Discount": "1",
            "ReduceType": "Discount",
            "RealCost": "0.25",
            "VoucherPayAmount": "0",
            "CashPayAmount": "0.25",
            "IncentivePayAmount": "0"
          }
        ]
      }
    ],
    "Total": 593,
    "RequestId": "001053bd-c491-404d-abd6-a737d92726f7"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=billing&Version=2018-07-09&Action=DescribeBillDetail)

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
