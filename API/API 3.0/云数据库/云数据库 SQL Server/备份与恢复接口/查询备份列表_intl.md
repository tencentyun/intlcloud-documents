## 1. API Description

Domain name for API request: sqlserver.tencentcloudapi.com

This API (DescribeBackups) is used to query the list of backups.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: sqlserver.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/238/19930).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeBackups |
| Version | Yes | String | Common parameter. The value used for this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| StartTime | Yes | Timestamp | Start time (yyyy-MM-dd HH:mm:ss) |
| EndTime | Yes | Timestamp | End time (yyyy-MM-dd HH:mm:ss) |
| InstanceId | Yes | String | Instance ID, such as mssql-njj2mtpl |
| Limit | No | Integer | Number of returned results per page. Its defaults to 20. The maximum is 100. |
| Offset | No | Integer | Offset. It is 0 by default. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of backups |
| Backups | Array of [Backup](/document/api/238/19976#Backup) | Details of backup list |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query the list of backups

#### Input example

```
https://sqlserver.tencentcloudapi.com/?Action=DescribeBackups
&InstanceId=mssql-njj2mtpl
&StartTime=2018-03-28 00:00:00
&EndTime=2018-04-20 00:00:00
&Limit=20
&Offset=0
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "Backups": [
      {
        "DBs": [
          "testdbvictornew"
        ],
        "EndTime": "2018-07-02 16:09:20",
        "ExternalAddr": "https://gz-dl-sqlserver.cloud.tencent.com/download/backup_49760.tar?YJW3gzNLKt2LCrywP9JslJXZo6TXiqprJ6x+tRJfDqzgJRdDrKF8j2V0XGk/MyyS00h9hexVea0A3GvpPf2aoq80DbnTNfZrLB+Ys00Glvzfv7CfaHRsoM95IpqVGrfNMrxomN6lVfnj6qb8Y3duxg==",
        "FileName": "manual_instance_58001_20180702160920.bak.tar",
        "Id": 49760,
        "InternalAddr": "http://10.66.0.88:58366/download/backup_49760.tar?YJW3gzNLKt2LCrywP9JslJXZo6TXiqprJ6x+tRJfDqzgJRdDrKF8j2V0XGk/MyyS00h9hexVea0A3GvpPf2aoq80DbnTNfZrLB+Ys00Glvzfv7CfaHRsoM95IpqVGrfNMrxomN6lVfnj6qb8Y3duxg==",
        "Size": 192,
        "StartTime": "2018-07-02 16:09:20",
        "Status": 1,
        "Strategy": 0
      },
      {
        "DBs": [
          "testdbvictornew"
        ],
        "EndTime": "2018-07-02 01:04:30",
        "ExternalAddr": "https://gz-dl-sqlserver.cloud.tencent.com/download/backup_49759.tar?YJW3gzNLKt2LCrywP9JslJXZo6TXiqprJ6x+tRJfDqzgJRdDrKF8j2V0XGk/MyyS00h9hexVea0A3GvpPf2aoq80DbnTNfZrvuFmWRKDML0cICOu7LASU2gWXlUkKcHfj/tspGhVGw8RX0OKecEUIQ==",
        "FileName": "manual_instance_58001_20180702010430.bak.tar",
        "Id": 49759,
        "InternalAddr": "http://10.66.0.88:58366/download/backup_49759.tar?YJW3gzNLKt2LCrywP9JslJXZo6TXiqprJ6x+tRJfDqzgJRdDrKF8j2V0XGk/MyyS00h9hexVea0A3GvpPf2aoq80DbnTNfZrvuFmWRKDML0cICOu7LASU2gWXlUkKcHfj/tspGhVGw8RX0OKecEUIQ==",
        "Size": 192,
        "StartTime": "2018-07-02 01:04:30",
        "Status": 1,
        "Strategy": 0
      }
    ],
    "RequestId": "863b2797-858b-49f3-88e9-50159e564cbc",
    "TotalCount": 2
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeBackups)

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

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](/document/api/238/19932#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InternalError.DBError | Database error |
| InternalError.GcsError | GCS API error |
| InternalError.SystemError | System error |
| InternalError.UnknownError | Unknown error |
| InvalidParameter | Incorrect parameter |
| InvalidParameter.InputIllegal | Invalid input parameter |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion failed |
| ResourceNotFound.InstanceNotFound | Instance does not exist |

