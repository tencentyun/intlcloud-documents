## 1. API Description
API request domain name: cws.tencentcloudapi.com.

This API (DescribeSites) is used to query the details of one or more websites.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/692/16736).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeSites |
| Version | Yes | String | Common parameter; the value for this API: 2018-03-12 |
| Region | No | String | Common parameter; not passed in for this API |
| SiteIds.N | No | Array of Integer | List of website IDs |
| Filters.N | No | Array of [Filter](/document/api/692/16759#Filter) | Filters |
| Offset | No | Integer | Offset; 0 by default |
| Limit | No | Integer | Number of returns; 10 by default, up to 100 |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of websites. |
| Sites | Array of [Site](/document/api/692/16759#Site) | List of website information. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing Website List

#### Input Example

```
https://cws.tencentcloudapi.com/?Action=DescribeSites
&Filters.0.Name=Name
&Filters.0.Values.0=QQ
&Filters.0.Values.1=WeChat
&Filters.1.Name=Url
&Filters.1.Values.0=http%3A%2F%2Fdemo.aisec.cn
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "RequestId": "354f4ac3-8546-4516-8c8a-69e3ab73aa8a",
    "Sites": [
      {
        "Appid": 1251001047,
        "CreatedAt": "2018-03-19T16:33:45+08:00",
        "Id": 4,
        "LastScanCancelTime": "",
        "LastScanExtsCount": "",
        "LastScanFinishTime": "2018-03-19T17:38:56+08:00",
        "LastScanNoticeNum": 1,
        "LastScanPageCount": 0,
        "LastScanScannerType": "",
        "LastScanStartTime": "2018-03-22T00:00:00+08:00",
        "LastScanTaskId": 0,
        "LastScanVulsHighNum": 0,
        "LastScanVulsLowNum": 0,
        "LastScanVulsMiddleNum": 0,
        "LastScanVulsNoticeNum": 0,
        "LastScanVulsNum": 10,
        "LoginCheckKw": "",
        "LoginCheckUrl": "",
        "LoginCookie": "",
        "LoginCookieValid": 0,
        "MonitorId": 0,
        "MonitorStatus": 0,
        "Name": "Spqs6w6el",
        "NeedLogin": 0,
        "Progress": 0,
        "ScanDisallow": "",
        "ScanStatus": 0,
        "UpdatedAt": "2018-03-19T17:38:56+08:00",
        "Url": "http://demo.aisec.cn/demo/aisec/",
        "UserAgent": "",
        "VerifyStatus": 0
      }
    ],
    "TotalCount": 1
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer)

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

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/692/16738#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameter.Malformed | Incorrect data format. |
| InvalidParameter.NotFound | The requested data does not exist. |

