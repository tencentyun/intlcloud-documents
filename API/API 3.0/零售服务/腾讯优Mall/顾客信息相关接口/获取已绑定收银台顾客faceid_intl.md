## 1. API Description

API request domain name: youmall.tencentcloudapi.com.

This API queries the visitor's FaceID using the cashier desk ID reported by the DescribeCameraPerson API. The best query time is after 01:00 on the next day after reported by the cashier desk.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/860/18451).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; its value for this API: DescribeFaceIdByTempId |
| Version | Yes | String | Common parameter; its value for this API: 2018-02-28 |
| Region | No | String | Common parameter; not passed in for this API |
| CompanyId | Yes | String | Company ID in YouMall; obtained using the DescribeShopInfo API |
| ShopId | Yes | Integer | Shop ID in YouMall; obtained using the DescribeShopInfo API |
| TempId | Yes | String | Temporary ID |
| CameraId | Yes | Integer | Camera ID |
| PosId | No | String | POS terminal ID |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| CompanyId | String | Company ID |
| ShopId | Integer | Shop ID |
| CameraId | Integer | Camera ID |
| PosId | String | POS terminal ID |
| TempId | String | Temporary ID of the request |
| FaceId | Integer | Face ID corresponding to the temporary ID |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Getting Face ID Based on Temporary ID

#### Input Example

```
https://youmall.tencentcloudapi.com/?Action=DescribeFaceIdByTempId
&CompanyId=tencent
&ShopId=10086
&TempId=tencent_10086_21_20180722080857_2677813760953992720_306_271_39_39
&CameraId=21
&PosId=test
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "CameraId": 21,
    "CompanyId": "tencent",
    "FaceId": 120,
    "PosId": "test",
    "RequestId": "4060c99c-47e7-4706-ab51-a00f91baac39",
    "ShopId": 10086,
    "TempId": "tencent_10086_21_20180722080857_2677813760953992720_306_271_39_39"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=youmall&Version=2018-02-28&Action=DescribeFaceIdByTempId)

### SDK

Cloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to the API are listed below. For other error codes, see [Common Error Codes](/document/api/860/18453#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.NoData | No data. |
| FailedOperation.ParameterError | Error processing request parameters. |
| FailedOperation.ProcessFail | Processing failed. |

