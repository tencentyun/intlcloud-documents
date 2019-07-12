## 1. API Description

API request domain name: cdn.tencentcloudapi.com.

DescribeIpVisit is used to query the number of users who remain active for 5 minutes and the detailed number of daily active users.

+ Number of users who remain active for 5 minutes: Collect deduplicated statistics based on client IP addresses in the log with the 5-minute granularity
+ Number of daily active users: Collect deduplicated statistics based on client IP addresses in the log with the 1-day granularity

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/228/30977).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter, the value for this API: DescribeIpVisit |
| Version | Yes | String | Common parameter, the value for this API: 2018-06-06 |
| Region | No | String | Common parameter; not passed in for this API. |
| StartTime | Yes | Timestamp | Query start time, such as 2018-09-04 10:40:10; the returned result is later than or equal to the specified time <br/>According to the specified time granularity, forward rounding is applied; for example, if the query start time is 2018-09-04 10:40:10 and the query time granularity is 5 minutes, the time for the first returned entry is 2018-09-04 10:40:00 |
| EndTime | Yes | Timestamp | Query end time, such as 2018-09-04 10:40:10; the returned result is earlier than or equal to the specified time <br/>According to the specified time granularity, forward rounding is applied; for example, if the query end time is 2018-09-04 10:40:10 and the query time granularity is 5 minutes, the time for the last returned entry is 2018-09-04 10:40:00 |
| Domains.N | No | Array of String | Specify the list of domain names to be queried; up to 30 domain names can be queried at a time |
| Project | No | Integer | Specify the project ID to be queried, and you can [view project IDs](https://console.cloud.tencent.com/project) <br/>Please note that if domain names are specified, this parameter will be ignored |
| Interval | No | String | Time granularity, which can be: <br/>5min: 5 minutes. If the query period is within 24 hours, `5min` is used by default. <br/>day: 1 day. If the query period is longer than 24 hours, `day` is used by default|

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Interval | String | Time granularity of data statistics, which supports 5min (5 minutes) and day (1 day) |
| Data | Array of [ResourceData](/document/api/228/30987#ResourceData) | Origin-pull data details of each resource |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided during troubleshooting. |

## 4. Sample

### Sample 1. Querying the Details of Active IP Addresses

#### Input Sample Code

```
https://cdn.tencentcloudapi.com/?Action=DescribeIpVisit
&StartTime=2018-09-04 00:00:00
&EndTime=2018-09-04 12:00:00
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
        "Resource": "multiDomains",
        "CdnData": [
          {
            "Metric": "ipVisit",
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
    "Interval": 5
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdn&Version=2018-06-06&Action=DescribeIpVisit)

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
| ResourceNotFound.CdnHostNotExists | This domain name does not exist under the account. Please check and try again. |
| ResourceNotFound.CdnUserNotExists | The CDN service has not been activated. Please activate it first before using this API. |
| UnauthorizedOperation.CdnUserIsSuspended | The CDN service has been suspended. Please restart it and try again. |
| UnauthorizedOperation.CdnUserNoWhitelist | You are not in the beta whitelist and thus have no permission to use this function. |
