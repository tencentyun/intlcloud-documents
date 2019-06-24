## 1. API Description

Domain name for API request: yunjing.tencentcloudapi.com.

This API (InquiryPriceOpenProVersionPrepaid) is used to inquire the price for activating HS Pro (prepaid).

Default request rate limit: 20/sec.

## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/296/19828).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: InquiryPriceOpenProVersionPrepaid. |
| Version | Yes | String | Common parameter. The value used for this API: 2/28/2018 |
| Region | No | String | Common parameter. This parameter is not required for this API. |
| ChargePrepaid | Yes | [ChargePrepaid](/document/api/296/19867#ChargePrepaid) | Parameter for setting prepaid mode. |
| Machines.N | Yes | Array of [ProVersionMachine](/document/api/296/19867#ProVersionMachine) | Array of the hosts with HS Pro activated. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| OriginalPrice | Float | Original price of prepaid fees (in CNY). |
| DiscountPrice | Float | Discount price of prepaid fees (in CNY). |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Inquire the price for activating HS Pro (prepaid)

#### Input example

```
https://yunjing.tencentcloudapi.com/?Action=InquiryPriceOpenProVersionPrepaid
&ChargePrepaid.Period=1
&Machines.0.MachineType=CVM
&Machines.0.MachineRegion=ap-guangzhou
&Machines.0.Quuid=add4a78a-0d59-11e8-b7ab-00e081e1a5c5
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "DiscountPrice": 88.88,
    "RequestId": "354f4ac3-8546-4516-8c8a-69e3ab73aa8a",
    "OriginalPrice": 100
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=yunjing&Version=2018-02-28&Action=InquiryPriceOpenProVersionPrepaid)

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

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/296/19830#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.InquiryPrice | Price query failed. |
| InternalError | Internal error. |
| InvalidParameter.InvalidFormat | Incorrect parameter format. |

