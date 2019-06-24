## 1. API Description
API request domain name: cws.tencentcloudapi.com.

This API (DescribeVulsNumberTimeline) is used to query the vulnerability statistics over time.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/692/16736).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeVulsNumberTimeline |
| Version | Yes | String | Common parameter; the value for this API: 2018-03-12 |
| Region | No | String | Common parameter; not passed in for this API |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of statistical records. |
| VulsTimeline | Array of [VulsTimeline](/document/api/692/16759#VulsTimeline) | User vulnerability statistics over time. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing Vulnerability Statistics over Time

#### Input

```
https://cws.tencentcloudapi.com/?Action=DescribeVulsNumberTimeline
&<Common request parameter>
```

#### Output

```
{
  "Response": {
    "RequestId": "33e45f0e-f971-4784-ab50-e8205e995355",
    "TotalCount": 2,
    "VulsTimeline": [
      {
        "Appid": 1251001047,
        "CreatedAt": "2018-06-12T22:25:00+08:00",
        "Date": "2018-06-11T00:00:00+08:00",
        "Id": 1,
        "ImpactSiteNum": 1,
        "PageCount": 33,
        "SiteNum": 8,
        "UpdatedAt": "2018-06-12T22:25:00+08:00",
        "VulsHighNum": 8,
        "VulsLowNum": 0,
        "VulsMiddleNum": 2,
        "VulsNoticeNum": 0
      },
      {
        "Appid": 1251001047,
        "CreatedAt": "2018-06-13T17:54:41.418296+08:00",
        "Date": "2018-06-13T00:00:00+08:00",
        "Id": 0,
        "ImpactSiteNum": 1,
        "PageCount": 33,
        "SiteNum": 8,
        "UpdatedAt": "2018-06-13T17:54:41.418298+08:00",
        "VulsHighNum": 8,
        "VulsLowNum": 0,
        "VulsMiddleNum": 2,
        "VulsNoticeNum": 0
      }
    ]
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

Only the error codes related to this API are listed below. For other error codes, see [Common Error Codes](/document/api/692/16738#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |

