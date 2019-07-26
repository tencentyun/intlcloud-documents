## 1. API Description

API request domain name: cdn.tencentcloudapi.com.

DescribePayType describes billing details of the current account, including billing type and billing cycle.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/228/30977).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter, the name of this API: DescribePayType |
| Version | Yes | String | Common parameter, the version of this API: 2018-06-06 |
| Region | No | String | Common parameter; optional for this API. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| PayType | String | Billing type: <br/>flux: Bill-by-traffic <br/>bandwidth: Bill-by-bandwidth |
| BillingCycle | String | Billing cycle: <br/>day: Daily settlement<br/>month: Monthly settlement |
| StatType | String | Billing method: <br/>monthMax: Billed by the monthly average of daily peak traffic (monthly settlement) <br/>day95: Billed by the daily 95th percentile bandwidth (monthly settlement) <br/>month95: Billed by the monthly 95th percentile bandwidth (monthly settlement) <br/>sum: Billed by the total traffic (daily or monthly settlement) <br/>max: Billed by the peak bandwidth (daily settlement) |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.|

## 4. Sample

### Sample 1. Querying the Billing Method

#### Input Sample Code

```
https://cdn.tencentcloudapi.com/?Action=DescribePayType
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "1732a0dd-48d8-4ff1-8dcb-7f04ca139825",
    "PayType": "flux",
    "StatType": "sum",
    "BillingCycle": "day"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdn&Version=2018-06-06&Action=DescribePayType)

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

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/228/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.CdnDbError | Internal data error. Please submit a ticket for troubleshooting. |
| InternalError.CdnSystemError | System error. Please submit a ticket for troubleshooting. |
| InvalidParameter.CdnInterfaceError | Internal API error. Please submit a ticket for troubleshooting. |
| ResourceNotFound.CdnUserNotExists | The CDN service has not been activated. Please activate it first before using this API. |
| UnauthorizedOperation.CdnUserNoWhitelist | You are not on the whitelist, so using this function is prohibited. |

