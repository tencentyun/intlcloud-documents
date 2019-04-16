## 1. API Description

API request domain name: live.tencentcloudapi.com.

This API queries streaming events.

Default API request frequency limit: 500 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/267/20459).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeLiveStreamEventList |
| Version | Yes | String | Common parameter; the value for this API: 2018-08-01 |
| Region | No | String | Common parameter; not passed in for this API |
| StartTime | Yes | String | Start time In UTC format, for example: 2018-12-29T19:00:00Z. <br/>This supports querying the history of 60 days. |
| EndTime | Yes | String | End time In UTC format, for example: 2018-12-29T20:00:00Z. <br/>This cannot be after the current time and cannot be more than 30 days after the start time. |
| AppName | No | String | Application name |
| DomainName | No | String | Push domain name.  |
| StreamName | No | String | Stream name; query with wildcard (*) is not supported; fuzzy match by default. <br/>The IsStrict field can be used to change to exact query. |
| PageNum | No | Integer | The page number to get. <br/>Default value: 1. <br/>Note: Currently, query for up to 10,000 entries is supported. |
| PageSize | No | Integer | Page size. <br/>Maximum value: 100. <br/>Value range: any integer between 1 and 100. <br/>Default value: 10. <br/>Note: Currently, query for up to 10,000 entries is supported. |
| IsFilter | No | Integer | Whether to filter; no filtering by default. <br/>0: No filtering at all. <br/>1: Filter out the failed streams and return only the successful ones. |
| IsStrict | No | Integer | Whether to query exactly; fuzzy match by default. <br/>0: Fuzzy match. <br/>1: Exact query. <br/>Note: This parameter takes effect when StreamName is used. |
| IsAsc | No | Integer | Whether to display in ascending order by end time; descending order by default. <br/>0: Descending. <br/>1: Ascending. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| EventList | Array of [StreamEventInfo](/document/api/267/20474#StreamEventInfo) | Streaming event list |
| PageNum | Integer | Page number. |
| PageSize | Integer | Size per page |
| TotalNum | Integer | Total number of eligible ones. |
| TotalPage | Integer | Total number of pages. |
| RequestId | String | The unique request ID which is returned for each request The RequestId for the current request needs to be provided when troubleshooting |

## 4. Sample

### Request Sample

#### Input Sample Code

```
https://live.tencentcloudapi.com/?Action=DescribeLiveStreamEventList
&DomainName=5000.livepush.com
&AppName=live
&StreamName=stream1
&StartTime=2019-01-04T12:00:00Z
&EndTime=2019-01-04T20:00:00Z
&PageNum=1
&PageSize=10
&IsFilter=1
&IsStrict=0
&IsAsc=0
&<Common request parameter>
```

#### Output Sample Code

```
{
	"Response": {
		"EventList": [
                       {
                              "AppName": "live",
                              "ClientIp": "180.163.8.244",
                              "DomainName": "5000.livepush.myqcloud.com",
                              "Duration": 0,
                              "Resolution": "640*352",
                              "StopReason": "Client actively interrupts the push (3)",
                              "StreamEndTime": "2019-01-04T11:59:58Z",
                              "StreamName": "5000_b6c808121b0d11e6b91fa4dcbef5e35a",
                              "StreamStartTime": "2019-01-04T11:59:58Z",
                              "Url": "rtmp://22318.livepush.myqcloud.com/live/stream_id_2"
                       }
                ],
		"PageNum": 1,
		"PageSize": 10,
		"TotalNum": 100,
		"TotalPage": 10,
		"RequestId": "8e50cdb5-56dc-408b-89b0-31818958d424"
	}
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=live&Version=2018-08-01&Action=DescribeLiveStreamEventList)

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

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/267/20461#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameterValue | Incorrect parameter value |
| MissingParameter | Missing parameter |

