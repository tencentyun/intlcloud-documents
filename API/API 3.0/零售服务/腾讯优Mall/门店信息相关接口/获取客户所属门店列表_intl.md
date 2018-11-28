## 1. API Description

API request domain name: youmall.tencentcloudapi.com.

This API gets the information of all shops of a company based on the company ID.

Default API request frequency limit: 100 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/860/18451).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; its value for this API: DescribeShopInfo |
| Version | Yes | String | Common parameter; its value for this API: 2018-02-28 |
| Region | No | String | Common parameter; not passed in for this API |
| Offset | Yes | Integer | Offset: Pagination control parameter; 0 is passed in for the first page; Offset for the nth page = (n-1)*Limit |
| Limit | Yes | Integer | Limit: Data items per page; maximum value: 100; if over 100, the value will be force specified as 100 |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of shops |
| ShopInfoSet | Array of [ShopInfo](/document/api/860/18465#ShopInfo) | Shop information list |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Getting Shop List of a Company - Success

#### Input Example

```
https://youmall.tencentcloudapi.com/?Action=DescribeShopInfo
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "RequestId": "6ec80684-0879-405e-8932-72e7c0c48ef8",
    "ShopInfoSet": [
      {
        "City": "Beijing",
        "CompanyId": "testCompany1",
        "CompanyName": "Test 1",
        "Province": "Beijing",
        "ShopCode": "xxx",
        "ShopId": 2,
        "ShopName": "Shop XXX"
      },
      {
        "City": "Chengdu",
        "CompanyId": "testCompany1",
        "CompanyName": "Test 1",
        "Province": "Sichuan",
        "ShopCode": "xxx1",
        "ShopId": 2,
        "ShopName": "Shop XXX1"
      }
    ],
    "TotalCount": 100
  }
}
```

### Example 2. Getting Shop List of a Company - Failure

#### Input Example

```
https://youmall.tencentcloudapi.com/?Action=DescribeShopInfo
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "Error": {
      "Code": "FailedOperation.NoRight",
      "Message": "have no right access"
    },
    "RequestId": "eac6b301-a322-493a-8e36-83b295459397"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=youmall&Version=2018-02-28&Action=DescribeShopInfo)

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

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/860/18453#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.NoData | No data. |
| FailedOperation.NoRight | Merchant has no permissions. |
| InternalError | Internal error |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Wrong parameter value |

