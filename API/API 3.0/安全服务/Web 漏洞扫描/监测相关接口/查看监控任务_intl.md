## 1. API Description
API request domain name: cws.tencentcloudapi.com.

This API (DescribeMonitors) is used to query the details of one or more monitoring tasks.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/692/16736).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeMonitors |
| Version | Yes | String | Common parameter; the value for this API: 2018-03-12 |
| Region | No | String | Common parameter; not passed in for this API |
| MonitorIds.N | No | Array of Integer | List of monitoring task IDs |
| Filters.N | No | Array of [Filter](/document/api/692/16759#Filter) | Filters |
| Offset | No | Integer | Offset; 0 by default |
| Limit | No | Integer | Number of returns; 10 by default, up to 100 |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Monitors | Array of [MonitorsDetail](/document/api/692/16759#MonitorsDetail) | List of monitoring tasks. |
| TotalCount | Integer | Number of monitoring tasks. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing Monitoring Task

#### Input Example

```
https://cws.tencentcloudapi.com/?Action=DescribeMonitors
&Filters.0.Name=Name
&Filters.0.Values.0=QQ
&Filters.0.Values.1=WeChat
&Filters.1.Name=MonitorStatus
&Filters.1.Values.0=1
&<Common request parameter>
```

#### Output Example

```
{
"Response": {
"Monitors": [
{
"Basic": {
"Appid": 1251001047,
"CreatedAt": "2018-03-24T15:25:37+08:00",
"Crontab": 2,
"CurrentScanStartTime": "2018-03-25T15:43:46+08:00",
"FirstScanStartTime": "2018-03-23T02:23:34+08:00",
"Id": 1,
"IncludedVulsTypes": "",
"LastScanFinishTime": "2018-03-25T15:44:00+08:00",
"MonitorStatus": 1,
"Name": "aisec-related",
"RateLimit": 20,
"ScanStatus": 2,
"ScannerType": "normal",
"UpdatedAt": "2018-03-25T15:44:00+08:00"
},
"ImpactSiteNumber": 2,
"ImpactSites": [
{
"SiteId": "1",
"Url": "http://demo.aisec.cn/demo/aisec/"
},
{
"SiteId": "2",
"Url": "http://demo.aisec.cn/demo/wvs/"
}
],
"SiteNumber": 2,
"Sites": [
{
"SiteId": "1",
"Url": "http://demo.aisec.cn/demo/aisec/"
},
{
"SiteId": "2",
"Url": "http://demo.aisec.cn/demo/wvs/"
}
],
"VulsHighNumber": 8,
"VulsLowNumber": 0,
"VulsMiddleNumber": 2,
"VulsNoticeNumber": 2
}
],
"RequestId": "354f4ac3-8546-4516-8c8a-69e3ab73aa8a",
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

Only the error codes related to this API are listed below. For other error codes, see [Common Error Codes](/document/api/692/16738#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameter.Malformed | Incorrect data format. |
| InvalidParameter.NotFound | The requested data does not exist. |

