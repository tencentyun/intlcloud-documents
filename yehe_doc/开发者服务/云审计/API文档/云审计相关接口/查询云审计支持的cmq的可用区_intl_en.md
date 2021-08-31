## 1. API Description

API domain name: cloudaudit.tencentcloudapi.com.

This API is used to query CloudAudit-enabled CMQ AZs.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/1021/34192).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: ListCmqEnableRegion. |
| Version | Yes | String | Common parameter. The value used for this API: 2019-03-19. |
| Region | Yes | String | Common parameter. For more information, please see the [list of regions](https://intl.cloud.tencent.com/document/api/1021/34192#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| WebsiteType | No | String | Website type. zh: Mainland China (default); en: outside Mainland China. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| EnableRegions | Array of [CmqRegionInfo](https://intl.cloud.tencent.com/document/api/1021/34209#CmqRegionInfo) | CloudAudit-enabled CMQ AZs |
| RequestId | String | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying CloudAudit-enabled CMQ AZs

This example shows you how to query CloudAudit-enabled CMQ AZs.

#### Input sample code

```
https://cloudaudit.tencentcloudapi.com/?Action=ListCmqEnableRegion
&WebsiteType=zh
&<Common request parameters>
```

#### Output sample code

```
{
  "Response": {
    "RequestId": "b69a7b60-e58f-4d27-a2b7-722fe01109c1",
    "EnableRegions": [
      {
        "CmqRegion": "sh",
        "CmqRegionName": "Shanghai"
      },
      {
        "CmqRegion": "hk",
        "CmqRegionName": "Hong Kong (China)"
      }
    ]
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cloudaudit&Version=2019-03-19&Action=ListCmqEnableRegion)

### SDK

TencentCloud API 3.0 comes with SDKs that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for Node.js](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, please see [Common Error Codes](https://intl.cloud.tencent.com/document/api/1021/34195#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.ListCmqEnableRegionError | Internal error. Please submit a ticket. |
