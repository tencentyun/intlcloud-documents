## 1. API Description

API request domain name: youmall.tencentcloudapi.com.

This API can be called to register the company's visit notification callback API address in YouMall. The API protocol is HTTP or HTTPS. After registration, if the company has visit notifications for special identities (such as frequent customers) configured, YouMall backend will proactively push the visit information to this API.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/860/18451).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; its value for this API: RegisterCallback |
| Version | Yes | String | Common parameter; its value for this API: 2018-02-28 |
| Region | No | String | Common parameter; not passed in for this API |
| CompanyId | Yes | String | Company ID; obtained using the DescribeShopInfo API |
| BackUrl | Yes | String | Notification callback address; a complete URL; for example, http://youmall.tencentcloudapi.com/ |
| Time | Yes | Integer | Request timestamp |
| NeedFacePic | No | Integer | Whether visitor photo is required; 1 - yes, other - no |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Registering Visit Notification Callback Address - Success

#### Input Example

```
https://youmall.tencentcloudapi.com/?Action=RegisterCallback
&CompanyId=TestCompany
&BackUrl=TestUrl
&Time=1529898082
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "RequestId": "6ec80684-0879-405e-8932-72e7c0c48ef8"
  }
}
```

### Example 2. Registering Visit Notification Callback Address - Failure

#### Input Example

```
https://youmall.tencentcloudapi.com/?Action=RegisterCallback
&CompanyId=TestCompany
&BackUrl=TestUrl
&Time=1529898082
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "Error": {
      "Code": "InvalidParameter ",
      "Message": "Parameter error"
    },
    "RequestId": "6ec80684-0879-405e-8932-72e7c0c48ef8"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=youmall&Version=2018-02-28&Action=RegisterCallback)

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
| FailedOperation.ProcessFail | Processing failed. |
| InvalidParameter | Parameter error |
| InvalidParameterValue.JsonParseErr | Error parsing the request JSON. |

