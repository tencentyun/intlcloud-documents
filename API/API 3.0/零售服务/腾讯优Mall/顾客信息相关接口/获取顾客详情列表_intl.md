## 1. API Description

API request domain name: youmall.tencentcloudapi.com.

This API gets the details of visitors to a specified shop, including visitor ID, photo, age and gender.

Default API request frequency limit: 100 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/860/18451).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; its value for this API: DescribePersonInfo |
| Version | Yes | String | Common parameter; its value for this API: 2018-02-28 |
| Region | No | String | Common parameter; not passed in for this API |
| CompanyId | Yes | String | Company ID |
| ShopId | Yes | Integer | Shop ID |
| StartPersonId | Yes | Integer | Start ID; 0 is passed in for StartPersonId for the first pull; the PersonId of the last data item on the previous page is passed in for the next pull |
| Offset | Yes | Integer | Offset: Pagination control parameter; 0 is passed in for the first page; Offset for the nth page = (n-1)*Limit |
| Limit | Yes | Integer | Limit: Data items per page; maximum value: 100; if over 100, the value will be force specified as 100 |
| PictureExpires | No | Integer | Image URL expiration time: After the current time + PictureExpires seconds, the image URL cannot be accessed normally; unit: s; default value: 1*24*60*60 (1 day) |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| CompanyId | String | Company ID |
| ShopId | Integer | Shop ID |
| TotalCount | Integer | Total number |
| PersonInfoSet | Array of [PersonInfo](/document/api/860/18465#PersonInfo) | Visitor information |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Getting Visitor Details List - Success

#### Input Example

```
https://youmall.tencentcloudapi.com/?Action=DescribePersonInfo
&CompanyId=TestCompany
&ShopId=1
&StartPersonId=0
&Offset=0
&Limit=100
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "CompanyId": "TestCompany",
    "PersonInfoSet": [
      {
        "Age": 20,
        "Gender": 0,
        "PersonId": 1,
        "PersonPictureUrl": "xxxx"
      },
      {
        "Age": 20,
        "Gender": 0,
        "PersonId": 2,
        "PersonPictureUrl": "xxxx"
      }
    ],
    "RequestId": "6ec80684-0879-405e-8932-72e7c0c48ef8",
    "ShopId": "1",
    "TotalCount": 2
  }
}
```

### Example 2. Getting Visitor Details List - Failure

#### Input Example

```
https://youmall.tencentcloudapi.com/?Action=DescribePersonInfo
&CompanyId=TestCompany
&StartPersonId=0
&Offset=0
&Limit=100
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "Error": {
      "Code": "InvalidParameter",
      "Message": "Parameter ShopId is missing"
    },
    "RequestId": "eac6b301-a322-493a-8e36-83b295459397"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=youmall&Version=2018-02-28&Action=DescribePersonInfo)

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
| InternalError | Internal error |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Wrong parameter value |

