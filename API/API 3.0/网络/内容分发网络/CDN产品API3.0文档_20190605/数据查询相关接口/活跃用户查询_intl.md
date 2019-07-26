## 1. API Description

API request domain name: cdn.tencentcloudapi.com.

DescribeIpVisit describes the numbers of 5-minute and daily active users.

+ Number of 5-minute active users: Deduplicate client IP addresses in the log for every 5 minutes.
+ Number of daily active users: Deduplicated client IP addresses in the log for every day.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/228/30977).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter, the name of this API: DescribeIpVisit |
| Version | Yes | String | Common parameter, the version this API: 2018-06-06 |
| Region | No | String | Common parameter; optional for this API. |
| StartTime | Yes | Timestamp | Query start time, such as 2018-09-04 10:40:10; the returned result is later than or equal to the specified time <br/>According to the specified time granularity, forward rounding is applied; for example, if the query start time is 2018-09-04 10:40:10 and the query time granularity is 5 minutes, the time for the first returned entry is 2018-09-04 10:40:00 |
| EndTime | Yes | Timestamp | Query end time, such as 2018-09-04 10:40:10; the returned result is earlier than or equal to the specified time <br/>According to the specified time granularity, forward rounding is applied; for example, if the query end time is 2018-09-04 10:40:10 and the query time granularity is 5 minutes, the time for the last returned entry is 2018-09-04 10:40:00 |
| Domains.N | No | Array of String | Specify the list of domain names to be queried; up to 30 domain names can be queried at a time |
| Project | No | Integer | Specify the project ID to be queried, and you can [view project IDs](https://console.cloud.tencent.com/project) <br/>Please note that if domain names are specified, this parameter will be ignored |
| Interval | No | String | Data granularity: <br/>5min: 5-minute. If the time interval to be queried is the last 24 hours (inclusive), the default value is `5min`. <br/>day: 1-day.If the time interval to be queried is more than 24 hours, the default value is `day`.|

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Interval | String | Data granularity: <br/>min: 1-minute <br/>5min: 5-minute <br/>day: 1-day |
| Data | Array of [ResourceData](/document/api/228/30987#ResourceData) | Origin-pull data details of each resource |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

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

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/228/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

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
| UnauthorizedOperation.CdnUserNoWhitelist | You are not on the whitelist, so the operation is prohibited. |
