## 1. API Description

Domain name: billing.tencentcloudapi.com. 

This API is used to query the bill details.

Default request rate limit: 5 requests/sec. 

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/555/19173). 

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeBillDetail |
| Version | Yes | String | Common parameter; the value for this API: 2018-07-09 |
| Region | No | String | Common parameter; optional for this API. |
| Offset | Yes | Integer | Offset |
| Limit | Yes | Integer | Quantity; up to 100 |
| PeriodType | Yes | String | Period type; byPayTime means by deduction period and byUsedTime means by billing period. It must be the same as the period type of the particular month’s bill in **Billing Center**. |
| Month | No | String | Month; format: yyyy-mm. At least Month or BeginTime and EndTime must be passed. If BeginTime and EndTime are passed, Month becomes invalid. It cannot be earlier than the month when Bill 2.0 is activated and you can pull the data in 24 months only. |
| BeginTime | No | String | The start time of the period; format: Y-m-d H:i:s. At least Month or BeginTime and EndTime must be passed. If BeginTime are passed, Month becomes invalid. BeginTime and EndTime must be passed together. It cannot be earlier than the month when Bill 2.0 is activated and you can pull the data in 24 month only. |
| EndTime | No | String | The end time of the period; format: Y-m-d H:i:s. At least Month or BeginTime and EndTime must be passed. If EndTime is passed, Month becomes invalid. BeginTime and EndTime must be passed together. It cannot be earlier than the month when Bill 2.0 is activated and you can pull the data in 24 months only. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| DetailSet | Array of [BillDetail](/document/api/555/19183#BillDetail) | Detail list|
| RequestId | String | A unique request ID which is returned for each request. RequestId for the current request needs to be provided for troubleshooting. |

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

**This tool allows online call, signature authentication, SDK code generation and quick API retrieval to greatly improve the efficiency of using TencentCloud APIs.** 

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=billing&Version=2018-07-09&Action=DescribeBillDetail)

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

Currently there is no error codes related to the API business logic. For other error codes, see [Common Error Codes](/document/api/555/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).