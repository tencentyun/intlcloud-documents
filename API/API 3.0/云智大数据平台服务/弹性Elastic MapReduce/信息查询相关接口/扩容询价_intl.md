## 1. API Description

API domain name: emr.tencentcloudapi.com.

This API inquires about the price of scaling out the specified instance

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/589/33974).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: InquiryPriceScaleOutInstance |
| Version | Yes | String | Common parameter. The version of this API: 2019-01-03 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/589/33974#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| TimeUnit | Yes | String | Time unit, which is second in pay-as-you-go use cases. |
| TimeSpan | Yes | Integer | Time span, which is 3,600 in pay-as-you-go use cases. |
| ZoneId | Yes | Integer | Zone ID |
| PayMode | Yes | Integer | Billing method |
| InstanceId | Yes | String | Instance ID |
| CoreCount | Yes | Integer | Number of core nodes to add |
| TaskCount | Yes | Integer | Number of task nodes to add|
| Currency | Yes | String | Currency |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Result | [InquiryPriceResult](/document/api/589/33981#InquiryPriceResult) | Scale-out price |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Examples

### Example 1. Inquiring About the Price of Scale-out

#### Input Sample Code

```
https://emr.tencentcloudapi.com/?Action=InquiryPriceScaleOutInstance
&TimeUnit=m
&TimeSpan=1
&ZoneId=190001
&Currency=CNY
&PayMode=0
&CoreCount=0
&TaskCount=1
&InstanceId=emr-amz3wvz1
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "Result": {
      "OriginalCost": 0.09,
      "DiscountCost": 0.09,
      "TimeUnit": "m",
      "TimeSpan": 1
    },
    "RequestId": "40c941da-fe3e-4f52-b816-dbddff308c47"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=emr&Version=2019-01-03&Action=InquiryPriceScaleOutInstance)

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

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/589/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.Test | The selected spec is sold out. |
