## 1. API Description

Domain name: billing.tencentcloudapi.com. 

This API queries the bill details.

Default request rate limit: 5 requests/sec. 

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/555/19173). 

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeBillDetail |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-09 |
| Region | No | String | Common parameter; optional for this API. |
| Offset | Yes | Integer | Offset |
| Limit | Yes | Integer | Quantity; maximum 100 |
| PeriodType | Yes | String | Billing period type. *byUsedTime*: By usage period; *byPayTime*: by payment period. This value must be the same as the billing period type in **Billing Center** for that particular month. |
| Month | No | String | Month; format: yyyy-mm. You only have to enter either Month or BeginTime&EndTime. When you enter values for BeginTime&EndTime, Month becomes invalid. This value must be no earlier than the month when Bill 2.0 is activated; last 24 months data is available. |
| BeginTime | No | String | The start time of the period; format: Y-m-d H:i:s. You only have to enter either Month or BeginTime&EndTime. When you enter values for BeginTime&EndTime, Month becomes invalid. BeginTime and EndTime must be inputed as a pair. This value must be no earlier than the month when Bill 2.0 is activated; last 24 months data is available. |
| EndTime | No | String | The end time of the period; format: Y-m-d H:i:s. You only have to enter either Month or BeginTime&EndTime. When you enter values for BeginTime&EndTime, Month becomes invalid. BeginTime and EndTime must be inputed as a pair. This value must be no earlier than the month when Bill 2.0 is activated; last 24 months data is available. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| DetailSet | Array of [BillDetail](/document/api/555/19183#BillDetail) | Detail list|
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1 Getting the Bill Details

#### Input Sample Code

```
https://billing.tencentcloudapi.com/?Action=DescribeBillDetail
&Month=2018-07
&PeriodType=byPayTime
&Offset=0
&Limit=1
&BeginTime=2018-11-01 00:00:00
&EndTime=2018-11-01 23:59:59
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "DetailSet": [
      {
        "PayerUin": "762217882",
        "OwnerUin": "762217882",
        "OperateUin": "762217882",
        "BusinessCodeName": "CLB",
        "ProductCodeName": "Public Application CLB",
        "PayModeName": “Pay-as-you-go resource",
        "ProjectName": "Default project",
        "RegionName": "Southeast Asia (Singapore)",
        "ZoneName": “Singapore Zone 1",
        "ResourceId": "lb-qgs9bc56",
        "ResourceName": "Test CLB",
        "ActionTypeName": "Monthly settlement",
        "OrderId": "20180808110089",
        "BillId": "20180810030000181855232162282358",
        "PayTime": "2018-08-08 11:22:33",
        "FeeBeginTime": "2018-08-08 11:25:00",
        "FeeEndTime": "2018-09-08 11:25:00",
        "ComponentSet": [
          {
            "ComponentCodeName": "Instance",
            "ItemCodeName": "Public Application CLB-instance",
            "SinglePrice": 36,
            "SpecifiedPrice": 36,
            "PriceUnit": "USD/unit/month",
            "UsedAmount": 1,
            "UsedAmountUnit": "Unit",
            "TimeSpan": 2,
            "TimeUnitName": "Month",
            "Cost": 72,
            "Discount": 0.5,
            "ReduceType": "Discount",
            "RealCost": 36,
            "VoucherPayAmount": 11,
            "CashPayAmount": 12,
            "IncentivePayAmount": 13
          }
        ]
      }
    ]
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=billing&Version=2018-07-09&Action=DescribeBillDetail)

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
