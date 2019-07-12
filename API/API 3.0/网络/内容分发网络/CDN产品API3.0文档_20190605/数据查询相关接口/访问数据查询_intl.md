## 1. API Description

API request domain name: cdn.tencentcloudapi.com.

DescribeCdnData is used to query CDN real-time access monitoring data and supports the following metrics:

+ Traffic (in bytes)
+ Bandwidth (in bps)
+ Number of requests
+ Traffic hit rate (in % with two decimal digits)
+ Aggregated list of 2xx status codes and the details of status codes starting with 2 (in entries)
+ Aggregated list of 3xx status codes and the details of status codes starting with 3 (in entries)
+ Aggregated list of 4xx status codes and the details of status codes starting with 4 (in entries)
+ Aggregated list of 5xx status codes and the details of status codes starting with 5 (in entries)

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/228/30977).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter, the value for this API: DescribeCdnData |
| Version | Yes | String | Common parameter, the value for this API: 2018-06-06 |
| Region | No | String | Common parameter; not passed in for this API. |
| StartTime | Yes | Timestamp | Query start time, such as 2018-09-04 10:40:00; the returned result is later than or equal to the specified time <br/>According to the specified time granularity, forward rounding is applied; for example, if the query start time is 2018-09-04 10:40:00 and the query time granularity is 1 hour, the time for the first returned entry is 2018-09-04 10:00:00 <br/>The gap between the start time and end time should be less than or equal to 90 days |
| EndTime | Yes | Timestamp | Query end time, such as 2018-09-04 10:40:00; the returned result is earlier than or equal to the specified time <br/>According to the specified time granularity, forward rounding is applied; for example, if the query end time is 2018-09-04 10:40:00 and the query time granularity is 1 hour, the time for the last returned entry is 2018-09-04 10:00:00 <br/>The gap between the start time and end time should be less than or equal to 90 days |
| Metric | Yes | String | Specify the query metric, which can be: <br/>flux: Traffic (in bytes) <br/>bandwidth: Bandwidth (in bps) <br/>request: Number of requests <br/>fluxHitRate: Traffic hit rate (in %) <br/>statusCode: Status code (in entries); return the aggregated data for 2xx, 3xx, 4xx, and 5xx status codes <br/>2xx: Return the aggregated list of 2xx status codes and the data for status codes starting with 2 (in entries) <br/>3xx: Return the aggregated list of 3xx status codes and the data for status codes starting with 3 (in entries) <br/>4xx: Return the aggregated list of 4xx status codes and the data for status codes starting with 4 (in entries) <br/>5xx: Return the aggregated list of 5xx status codes and the data for status codes starting with 5 (in entries) <br/>It supports the query of a specific status code; the return is empty if the status code has not been generated |
| Domains.N | No | Array of String | Specify the list of domain names to be queried <br/>Up to 30 domain names can be queried at a time |
| Project | No | Integer | Specify the project ID to be queried, and you can [view project IDs](https://console.cloud.tencent.com/project) <br/>Please note that if domain names are specified, this parameter will be ignored |
| Interval | No | String | Time granularity, which can be: <br/>min: 1 minute; specify the query interval as within 24 hours (inclusive), and it can return the details for the 1-minute granularity <br/>5min: 5 minutes; specify the query interval as within 31 days (inclusive), and it can return the details for the 5-minute granularity <br/>hour: 1 hour; specify the query interval as within 31 days (inclusive), and it can return the details for the 1-hour granularity <br/>day: 1 day; specify the query interval as more than 31 days, and it can return the details for the 1-day granularity |
| Detail | No | Boolean | The aggregated data for multiple domain names is returned by default (false) during a multi-domain-name query <br/>You can set it to true as required to return the details for each Domain (the statusCode metric is currently not supported) |
| Isp | No | Integer | Specify the ISP to be queried; if you leave it blank, all ISPs will be queried <br/>To view ISP codes, see [ISP Code Mappings](https://cloud.tencent.com/document/product/228/6316#.E8.BF.90.E8.90.A5.E5.95.86.E6.98.A0.E5.B0.84) |
| District | No | Integer | Specify the district to be queried; if you leave it blank, all districts will be queried <br/>To view district codes, see [District Code Mappings](https://cloud.tencent.com/document/product/228/6316#.E7.9C.81.E4.BB.BD.E6.98.A0.E5.B0.84) |
| Protocol | No | String | Specify the protocol to be queried; if you leave it blank, all protocols will be queried <br/>all: All protocols <br/>http: Specify the HTTP metric to be queried <br/>https: Specify the HTTPS metric to be queried |
| DataSource | No | String | Specify the data source to be queried, which can be seen as the whitelisting function |
| IpProtocol | No | String | Specify the IP protocol to be queried; if you leave it blank, all IP protocols will be queried <br/>all: All IP protocols <br/>ipv4: Specify the ipv4 metric to be queried <br/>ipv6: Specify the ipv6 metric to be queried |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Interval | String | Time granularity of the returned data. Specify one of the following during querying: <br/>min: 1 minute <br/>5min: 5 minutes <br/>hour: 1 hour <br/>day: 1 day |
| Data | Array of [ResourceData](/document/api/228/30987#ResourceData) | Returned data details of the specified conditional query |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided during troubleshooting. |

## 4. Sample

### Sample 1. Querying CDN Access Data

#### Input Sample Code

```
https://cdn.tencentcloudapi.com/?Action=DescribeCdnData
&StartTime=2018-09-04 00:00:00
&EndTime=2018-09-04 12:00:00
&Metric=flux
&Domains.0=www.test.com
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "123",
    "Data": [
      {
        "Resource": "www.test.com",
        "CdnData": [
          {
            "Metric": "flux",
            "DetailData": [
              {
                "Time": "2018-09-03 00:00:00",
                "Value": 10
              },
              {
                "Time": "2018-09-03 00:05:00",
                "Value": 20
              }
            ],
            "SummarizedData": {
              "Name": "sum",
              "Value": 30
            }
          }
        ]
      }
    ],
    "Interval": "5min"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdn&Version=2018-06-06&Action=DescribeCdnData)

### SDK

TencentCloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to this API are listed below. For other error codes, see [Common Error Codes](/document/api/228/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.CdnDbError | Internal data error. Please submit a ticket for troubleshooting. |
| InternalError.CdnSystemError | System error. Please submit a ticket for troubleshooting. |
| InvalidParameter.CdnHostInvalidParam | Invalid domain name format. Please check and try again. |
| InvalidParameter.CdnInterfaceError | Internal API error. Please submit a ticket for troubleshooting. |
| InvalidParameter.CdnParamError | Parameter error. Please see the sample parameters in the documentation. |
| InvalidParameter.CdnStatInvalidDate | Invalid date. Please see the sample date in the documentation. |
| InvalidParameter.CdnStatInvalidMetric | Invalid statistical type. Please see the sample statistical analysis in the documentation. |
| InvalidParameter.CdnStatInvalidProjectId | Incorrect project ID. Please check and try again. |
| LimitExceeded.CdnHostOpTooOften | Domain name operations are too frequent. |
| ResourceNotFound.CdnHostNotExists | This domain name does not exist under the account. Please check and try again. |
| ResourceNotFound.CdnUserNotExists | The CDN service has not been activated. Please activate it first before using this API. |
| UnauthorizedOperation.CdnAccountUnauthorized | The sub-account is unauthorized to query full data. |
| UnauthorizedOperation.CdnUserIsSuspended | The CDN service has been suspended. Please restart it and try again. |
| UnauthorizedOperation.CdnUserNoWhitelist | You are not in the beta whitelist and thus have no permission to use this function. |
