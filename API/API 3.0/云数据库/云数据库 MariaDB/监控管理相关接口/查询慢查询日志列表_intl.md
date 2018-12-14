## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (DescribeDBSlowLogs) is used to query the list of slow logs.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mariadb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeDBSlowLogs. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/237/16147#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID, such as tdsql-ow728lmc. |
| Offset | Yes | Integer | Starting offset of the first data entry of the returned results |
| Limit | Yes | Integer | Number of results to be returned |
| StartTime | Yes | Timestamp | Start time for the query, such as: 2016-07-23 14:55:20. |
| EndTime | No | Timestamp | End time for the query, such as: 2016-08-22 14:55:20. |
| Db | No | String | Name of the database to be queried |
| OrderBy | No | String | Sorting field (query_time_sum or query_count) |
| OrderByType | No | String | Sorting type (desc or asc) |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| Data | Array of [SlowLogData](/document/api/237/16191#SlowLogData) | Data of slow logs |
| LockTimeSum | Float | Total lock time for all statements |
| QueryCount | Integer | Total count of queries for all statements |
| Total | Integer | Total number of records |
| QueryTimeSum | Float | Total query time for all statements |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query the list of slow logs

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=DescribeDBParameters
&InstanceId=tdsql-ige1a5k3
&Offset=0
&Limit=20
&StartTime=2017-08-06 00:00:00
&EndTime=2017-08-07 23:59:59
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "Data": [
      {
        "CheckSum": "14090621765287179955",
        "Db": "",
        "FingerPrint": "replace into sysdb.statustable set ts = from_unixtime(?),ip=?,port=?",
        "LockTimeAvg": "0.00",
        "LockTimeMax": "0.00",
        "LockTimeMin": "0.00",
        "LockTimeSum": "0.00",
        "QueryCount": "1",
        "QueryTimeAvg": "1.13",
        "QueryTimeMax": "1.13",
        "QueryTimeMin": "1.13",
        "QueryTimeSum": "1.13",
        "RowsExaminedSum": "0.00",
        "RowsSentSum": "0.00",
        "TsMax": "2016-08-06 11:32:10",
        "TsMin": "2016-08-06 11:32:10",
        "User": "agent"
      }
    ],
    "InstanceId": "tdsql-ige1a5k3",
    "LockTimeSum": 0,
    "QueryCount": 1,
    "QueryTimeSum": 1.13,
    "RequestId": "1e74e824-6d2b-495d-b347-5250cdf8e964",
    "Total": 1
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=DescribeDBSlowLogs)

### SDK

Cloud API 3.0 comes with the software development kit (SDK) that supports multiple programming languages and makes it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](/document/api/237/16149#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.CamAuthFailed | CAM authentication request failed |
| InternalError.DbOperationFailed | Failed to query the database |
| InternalError.GetInstanceInfoFailed | Failed to acquire the backend instance information |
| InternalError.LogDBFailed | Failed to obtain the SlowLog |
| InvalidParameter.GenericParameterError | Failed to pass the parameter validity verification |
| InvalidParameter.IllegalTime | Invalid time parameter |
| ResourceUnavailable.InstanceAlreadyDeleted | The database instance has been deleted |
| ResourceUnavailable.InstanceStatusAbnormal | The database instance is in an invalid status and cannot be operated |
| UnauthorizedOperation.PermissionDenied | No permission to perform operations on the API or resource |

