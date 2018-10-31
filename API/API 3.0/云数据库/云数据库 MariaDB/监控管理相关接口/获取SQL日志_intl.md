## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (DescribeSqlLogs) is used to acquire the SQL logs of an instance.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mariadb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeSqlLogs. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/237/16147#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID, such as tdsql-ow728lmc. It can be obtained by querying instance details via DescribeDBInstances. |
| Offset | No | Integer | SQL log offset |
| Limit | No | Integer | Number of pulls (value range: 0-1,000. 0 indicates fetching the total number information) |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of SQL log entries in the current message queue |
| StartOffset | Integer | The SQL log start offset in the message queue |
| EndOffset | Integer | The SQL log end offset in the message queue |
| Offset | Integer | The offset of the first SQL log returned |
| Count | Integer | The number of SQL logs returned |
| SqlItems | Array of [SqlLogItem](/document/api/237/16191#SqlLogItem) | SQL log list |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Pull the SQL log start offset and the number of logs

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=DescribeSqlLogs
&InstanceId=tdsql-6a0lwzzj
&Limit=0
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "Count": 0,
    "EndOffset": 55766447,
    "Offset": 53560502,
    "RequestId": "f2ede2fd-34b9-4e44-95d5-3198c137b73b",
    "SqlItems": [],
    "StartOffset": 53560502,
    "TotalCount": 2205945
  }
}
```

### Example 2 Pull SQL log

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=DescribeSqlLogs
&InstanceId=tdsql-6a0lwzzj
&Offset=53560502
&Limit=1
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "Count": 1,
    "EndOffset": 55766782,
    "Offset": 53560502,
    "RequestId": "211bbabb-ffde-467f-b949-e4c61c64c6a6",
    "SqlItems": [
      {
        "AffectRowNum": 0,
        "Client": "10.10.10.32:34812",
        "DbName": "test",
        "Offset": 53560502,
        "ResultCode": 0,
        "SelectRowNum": 1,
        "Sql": "select * from t",
        "TimeCostMs": 0,
        "Timestamp": 1537542271,
        "User": "jkx_rsd"
      }
    ],
    "StartOffset": 53560502,
    "TotalCount": 2206280
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=DescribeSqlLogs)

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
| FailedOperation.MsgQueueOperationFailed | Message queue operation failed |
| InternalError.CamAuthFailed | CAM authentication request failed |
| InternalError.DbOperationFailed | Failed to query the database |
| InvalidParameter.GenericParameterError | Failed to pass the parameter validity verification |
| ResourceUnavailable.InstanceStatusAbnormal | The database instance is in an invalid status and cannot be operated |
| UnauthorizedOperation.PermissionDenied | No permission to perform operations on the API or resource |

