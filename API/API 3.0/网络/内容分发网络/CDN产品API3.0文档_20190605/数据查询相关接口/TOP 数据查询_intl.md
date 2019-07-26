## 1. API Description

API request domain name: cdn.tencentcloudapi.com.

ListTopData sorts data by using different combinations of  `Metric` and `Filter`:

+ Sort access URLs by total traffic and total requests and return top 1,000 URLs in descending order
+ Sort client districts by total traffic and total requests and return the list of districts in descending order
+ Sort client ISPs by total traffic and total requests and return the list of ISPs in descending order
+ Sort domain names by total traffic, peak bandwidth, total requests, average hit rate, and 2XX/3XX/4XX/5XX status codes and return the list of domain names in descending order
+ Sort domain names by total origin-pull traffic, peak origin-pull bandwidth, total origin-pull requests, average origin-pull failure rate, and 2XX/3XX/4XX/5XX origin-pull status codes and return the list of domain names in descending order

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/228/30977).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter, the name of this API: ListTopData |
| Version | Yes | String | Common parameter, the version of this API: 2018-06-06 |
| Region | No | String | Common parameter; optional for this API. |
| StartTime | Yes | Timestamp | Query start date and time, such as: 2018-09-09 00:00:00 |
| EndTime | Yes | Timestamp | Query end date and time, such as: 2018-09-10 00:00:00 |
| Metric | Yes | String | Sort object. The following objects are supported: <br/>Url: Sort by access URL (including parameters after the question mark), and the supported Filters are flux and request (beta period now) <br/>Path: Sort by access URLs (excluding parameters after the question mark), and the supported Filters are flux and request <br/>District: Sort by district, and the supported Filters are flux and request <br/>Isp: Sort by ISP, and the supported Filters are flux and request <br/>Host: Sort by domain name access data, and the supported Filters are flux, request, bandwidth, fluxHitRate, and statistics of specific 2XX, 3XX, 4XX, and 5XX status codes <br/>originHost: Sort by domain name origin-pull data, and the supported Filters are flux, request, bandwidth, and statistics of specific origin_2XX, origin_3XX, oringin_4XX, and origin_5XX origin-pull status codes |
| Filter | Yes | String | Metric name used for sorting: <br/>flux: If Metric is `host`, it indicates the access traffic; if Metric is `originHost`, it indicates the origin-pull traffic <br/>bandwidth: If Metric is `host`, it indicates the access bandwidth; if Metric is `originHost`, it indicates the origin-pull bandwidth <br/>request: If Metric is `host`, it indicates the number of access requests; if Metric is `originHost`, it indicates the number of origin-pull requests <br/>fluxHitRate: Average traffic hit rate <br/>2XX: Access 2XX status code <br/>3XX: Access 3XX status code <br/>4XX: Access 4XX status code <br/>5XX: Access 5XX status code <br/>origin_2XX: Origin-pull 2XX status code <br/>origin_3XX: Origin-pull 3XX status code <br/>origin_4XX: Origin-pull 4XX status code <br/>origin_5XX: Origin-pull 5XX status code <br/>statusCode: Statistics of a specific access status code which is specified in the Code parameter <br/>OriginStatusCode: Statistics of a specific origin-pull status code which is specified in the Code parameter |
| Domains.N | No | Array of String | Specify the list of domain names to be queried; up to 30 domain names can be queried at a time |
| Project | No | Integer | Specify the project ID to be queried, and you can [view project IDs](https://console.cloud.tencent.com/project) <br/>Please note that if domain names are specified, this parameter will be ignored |
| Detail | No | Boolean | The default value is False, which means that the sorted results of all domain names are returned. <br/>If Metric is Url, Path, District, or Isp and Filter is flux or request, the value can be set to True to return the sorted results of each Domain |
| Code | No | String | When Filter is `statusCode` or `OriginStatusCode`, enter a code to query and sort|

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Data | Array of [TopData](/document/api/228/30987#TopData) | Return the top access data details of each resource |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Querying Top URL Access Data

#### Input Sample Code

```
https://cdn.tencentcloudapi.com/?Action=ListTopData
&StartTime=2018-09-04 00:00:00
&EndTime=2018-09-04 12:00:00
&Metric=Url
&Filter=flux
&Domains.0=www.test.com
&Domains.1=www.test.com
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "123",
    "Data": [
      {
        "Resource": "www.test1.com",
        "DetailData": [
          {
            "Name": "www.test1.com/1.jpg?abc=123",
            "Value": 13838
          }
        ]
      },
      {
        "Resource": "www.test2.com",
        "DetailData": [
          {
            "Name": "http://www.test2.com/1.jpg?abc=123",
            "Value": 2501
          }
        ]
      }
    ]
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdn&Version=2018-06-06&Action=ListTopData)

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
| InvalidParameter.CdnStatInvalidFilter | Invalid statistical dimension. Please see the sample statistical analysis in the documentation. |
| InvalidParameter.CdnStatInvalidMetric | Invalid statistical type. Please see the sample statistical analysis in the documentation. |
| InvalidParameter.CdnStatInvalidProjectId | Incorrect project ID. Please check and try again. |
| InvalidParameter.CdnStatTooManyDomains | The number of queried domain names exceeds the limit. |
| LimitExceeded.CdnHostOpTooOften | Too frequent operations on domain name. |
| ResourceNotFound.CdnHostNotExists | This domain name does not exist under the account. Please check and try again. |
| ResourceNotFound.CdnUserNotExists | The CDN service has not been activated. Please activate it first before using this API. |
| UnauthorizedOperation.CdnAccountUnauthorized | The sub-account is unauthorized to query full data. |
| UnauthorizedOperation.CdnUserIsSuspended | The CDN service has been suspended. Please restart it and try again. |
| UnauthorizedOperation.CdnUserNoWhitelist | You are not on the whitelist, so the operation is prohibited. |
