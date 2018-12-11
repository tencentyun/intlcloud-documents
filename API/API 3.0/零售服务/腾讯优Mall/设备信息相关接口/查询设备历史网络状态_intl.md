## 1. API Description

API request domain name: youmall.tencentcloudapi.com.

This API returns historical network status data of the current shop.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/860/18451).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; its value for this API: DescribeHistoryNetworkInfo |
| Version | Yes | String | Common parameter; its value for this API: 2018-02-28 |
| Region | No | String | Common parameter; not passed in for this API |
| Time | Yes | Integer | Request timestamp |
| CompanyId | Yes | String | Company ID in YouMall; obtained using the DescribeShopInfo API |
| ShopId | Yes | Integer | Shop ID in YouMall; obtained using the DescribeShopInfo API; if 0, all shops of the current company are pulled |
| StartDay | Yes | String | Pull start date; format example: 2018-09-05 |
| EndDay | Yes | String | Pull end date; format example: 2018-09-05; if over 90 days after StartDay, defaulted to StartDay+90 days |
| Limit | No | Integer | Number of pulled entries; default value: 10 |
| Offset | No | Integer | Pull offset; data after the offset is returned |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| InstanceSet | [NetworkHistoryInfo](/document/api/860/18465#NetworkHistoryInfo) | Network status data |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Pulling Network Status History of a Specified Shop

#### Input Example

```
https://youmall.tencentcloudapi.com/?Action=DescribeHistoryNetworkInfo
&Time=1536135402
&CompanyId=tencent
&ShopId=10086
&StartDay=2018-09-04
&EndDay=2018-09-05
&Limit=3
&Offset=1
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "InstanceSet": {
      "City": "Pudong",
      "CompanyId": "tencent",
      "Count": 48,
      "Infos": [
        {
          "AvgRtt": -1,
          "Download": 221.29,
          "Loss": 100,
          "MaxRtt": -1,
          "MdevRtt": -1,
          "MinRtt": -1,
          "UpdateTime": 1536071030,
          "Upload": 29.15
        },
        {
          "AvgRtt": -1,
          "Download": 1.22,
          "Loss": 100,
          "MaxRtt": -1,
          "MdevRtt": -1,
          "MinRtt": -1,
          "UpdateTime": 1536067912,
          "Upload": 2.47
        },
        {
          "AvgRtt": -1,
          "Download": 230.16,
          "Loss": 100,
          "MaxRtt": -1,
          "MdevRtt": -1,
          "MinRtt": -1,
          "UpdateTime": 1536066884,
          "Upload": 74.33
        }
      ],
      "Province": "Shanghai",
      "ShopId": 10086,
      "ShopName": "YouTu Lab"
    },
    "RequestId": "08f44066-6850-4a77-b663-166fff95fb7b"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=youmall&Version=2018-02-28&Action=DescribeHistoryNetworkInfo)

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
| FailedOperation.NoRight | Merchant has no permissions. |
| FailedOperation.ParameterError | Error processing request parameters. |
| FailedOperation.ProcessFail | Processing failed. |
| InvalidParameter | Parameter error |

