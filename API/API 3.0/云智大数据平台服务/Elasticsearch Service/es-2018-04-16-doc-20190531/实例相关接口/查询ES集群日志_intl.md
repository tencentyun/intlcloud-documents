## 1. API Description

API domain name: es.tencentcloudapi.com.

This API describes ES cluster logs eligible in the specified region.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if a financial region, such as ap-shanghai-fsi, is assigned to the common parameter Region, we recommend you include that financial region in your domain name  , such as es.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/845/30623).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: DescribeInstanceLogs |
| Version | Yes | String | Common parameter. The version of this API: 2018-04-16 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/845/30623#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Cluster instance ID |
| LogType | No | Integer | Log type; 1 by default <br/><li>1: Master log </li><li>2: Search slow log </li><li>3: Index slow log </li><li>4: GC log </li> |
| SearchKey | No | String | Search keyword, which supports LUCENE syntax, such as level:WARN, ip:1.1.1.1, and message:test-index |
| StartTime | No | String | Log start time; the format is YYYY-MM-DD HH:MM:SS, such as 2019-01-22 20:15:53 |
| EndTime | No | String | Log end time; the format is YYYY-MM-DD HH:MM:SS, such as 2019-01-22 20:15:53 |
| Offset | No | Integer | Pagination start value; 0 by default |
| Limit | No | Integer | Number of entries per page; 100 by default; up to 100 |
| OrderByType | No | Integer | Time sorting order; 0 by default <br/><li>0: Descending </li><li>1: Ascending </li> |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of returned logs |
| InstanceLogList | Array of [InstanceLog](/document/api/845/30634#InstanceLog) | List of log details |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Examples

### Example 1. Querying ES Cluster Logs

Query the latest master logs of a cluster

#### Input Sample Code

```
https://es.tencentcloudapi.com/?Action=DescribeInstanceLogs
&InstanceId=es-f5mwm28u
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalCount": 71633,
    "InstanceLogList": [
      {
        "Time": "2019-01-22T10:45:36.220+08:00",
        "Ip": "10.0.128.65",
        "Level": "INFO",
        "Message": "[o.e.p.o.OPackActionFilter] [1547723102001286009] forbidden request: { ID:cdc62072721547678872c0448c1ecaf9, TYP:MainRequest, USR:null, BRS:false, ACT:cluster:monitor/main, OA:10.0.128.43, IDX:, MET:GET, PTH:/, CNT:<OMITTED, LENGTH=0>, HDR:content-length, EFF:0 } Reason: null"
      },
      {
        "Time": "2019-01-22T10:45:35.730+08:00",
        "Ip": "10.0.128.65",
        "Level": "INFO",
        "Message": "[o.e.p.o.OPackActionFilter] [1547723102001286009] forbidden request: { ID:1a8a5b7ea41a485ebdd769586c1dcdf6, TYP:MainRequest, USR:null, BRS:false, ACT:cluster:monitor/main, OA:10.0.128.73, IDX:, MET:GET, PTH:/, CNT:<OMITTED, LENGTH=0>, HDR:content-length, EFF:0 } Reason: null"
      }
    ],
    "RequestId": "783d9290-dc60-4862-9340-10b632605374"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=es&Version=2018-04-16&Action=DescribeInstanceLogs)

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

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/845/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameter | Incorrect parameter. |
