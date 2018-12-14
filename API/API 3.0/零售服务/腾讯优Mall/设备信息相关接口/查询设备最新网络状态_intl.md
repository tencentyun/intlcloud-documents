## 1. API Description

API request domain name: youmall.tencentcloudapi.com.

This API returns the latest network status data of the current shop.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/860/18451).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeNetworkInfo |
| Version | Yes | String | Common parameter; the value for this API: 2018-02-28 |
| Region | No | String | Common parameter; not passed in for this API |
| Time | Yes | Integer | Request timestamp |
| CompanyId | Yes | String | Company ID in YouMall; obtained using the DescribeShopInfo API |
| ShopId | No | Integer | Shop ID in YouMall; obtained using the DescribeShopInfo API; if left blank, all shops of the current company are pulled |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| InstanceSet | [NetworkLastInfo](/document/api/860/18465#NetworkLastInfo) | Network status details |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Requesting Current Network Status of a Shop

#### Input Example

```
https://youmall.tencentcloudapi.com/?Action=DescribeNetworkInfo
&Time=1536139452
&CompanyId=tencent
&ShopId=10086
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "InstanceSet": {
      "Count": 1,
      "Infos": [
        {
          "AvgRtt": -1,
          "City": "Pudong",
          "CompanyId": "tencent",
          "Download": 1.01,
          "Loss": 100,
          "MaxRtt": -1,
          "MdevRtt": -1,
          "MinRtt": -1,
          "Province": "Shanghai",
          "ShopId": 10086,
          "ShopName": "YouTu Lab",
          "UpdateTime": 1536136734,
          "Upload": 2.29
        }
      ]
    },
    "RequestId": "fd2705d2-7444-4522-a9af-46c4b2911b40"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=youmall&Version=2018-02-28&Action=DescribeNetworkInfo)

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

