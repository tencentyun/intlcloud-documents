## 1. API Description
API request domain name: cws.tencentcloudapi.com.

This API (DescribeVulsNumber) is used to query the total number of vulnerabilities in the user's websites.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/692/16736).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeVulsNumber |
| Version | Yes | String | Common parameter; the value for this API: 2018-03-12 |
| Region | No | String | Common parameter; not passed in for this API |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| ImpactSiteNumber | Integer | Total number of websites affected. |
| SiteNumber | Integer | Total number of websites verified. |
| VulsHighNumber | Integer | Total number of high-risk vulnerabilities. |
| VulsMiddleNumber | Integer | Total number of medium-risk vulnerabilities. |
| VulsLowNumber | Integer | Total number of low-risk vulnerabilities. |
| VulsNoticeNumber | Integer | Total number of risk notices. |
| PageCount | Integer | Total number of pages scanned. |
| Sites | Array of [MonitorMiniSite](/document/api/692/16759#MonitorMiniSite) | List of websites verified. |
| ImpactSites | Array of [MonitorMiniSite](/document/api/692/16759#MonitorMiniSite) | List of websites affected. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing Total Number of Current Vulnerabilities

#### Input

```
https://cws.tencentcloudapi.com/?Action=DescribeVulsNumber
&<Common request parameter>
```

#### Output

```
{
  "Response": {
    "ImpactSiteNumber": 1,
    "PageCount": 33,
    "RequestId": "de766e0c-963f-4984-b145-f1085ff165a0",
    "SiteNumber": 8,
    "VulsHighNumber": 8,
    "VulsLowNumber": 0,
    "VulsMiddleNumber": 2,
    "VulsNoticeNumber": 0
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

