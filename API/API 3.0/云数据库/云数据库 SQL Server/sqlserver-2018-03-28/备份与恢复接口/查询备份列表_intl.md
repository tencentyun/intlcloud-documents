## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (DescribeBackups) describes the backups list.

API request rate limit: 20 requests/sec.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: DescribeBackups |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| StartTime | Yes | Timestamp | Start time (yyyy-MM-dd HH:mm:ss) |
| EndTime | Yes | Timestamp | End time (yyyy-MM-dd HH:mm:ss) |
| InstanceId | Yes | String | Instance ID in the format of mssql-njj2mtpl |
| Limit | No | Integer | Number of results per page; 20 by default, up to 100 |
| Offset | No | Integer | Offset. 0 by default |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of backups |
| Backups | Array of [Backup](/document/api/238/19976#Backup) | Backup list details |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying the Backup List

#### Input Sample Code

```
https://sqlserver.tencentcloudapi.com/?Action=DescribeBackups
&InstanceId=mssql-njj2mtpl
&StartTime=2018-03-28 00:00:00
&EndTime=2018-04-20 00:00:00
&Limit=20
&Offset=0
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "863b2797-858b-49f3-88e9-50159e564cbc",
    "TotalCount": 2,
    "Backups": [
      {
        "Id": 49760,
        "FileName": "manual_instance_58001_20180702160920.bak.tar",
        "StartTime": "2018-07-02 16:09:20",
        "EndTime": "2018-07-02 16:09:20",
        "Size": 192,
        "Strategy": 0,
        "Status": 1,
        "DBs": [
          "testdbvictornew"
        ],
        "InternalAddr": "http://10.66.0.88:58366/download/backup_49760.tar?YJW3gzNLKt2LCrywP9JslJXZo6TXiqprJ6x+tRJfDqzgJRdDrKF8j2V0XGk/MyyS00h9hexVea0A3GvpPf2aoq80DbnTNfZrLB+Ys00Glvzfv7CfaHRsoM95IpqVGrfNMrxomN6lVfnj6qb8Y3duxg==",
        "ExternalAddr": "https://gz-dl-sqlserver.cloud.tencent.com/download/backup_49760.tar?YJW3gzNLKt2LCrywP9JslJXZo6TXiqprJ6x+tRJfDqzgJRdDrKF8j2V0XGk/MyyS00h9hexVea0A3GvpPf2aoq80DbnTNfZrLB+Ys00Glvzfv7CfaHRsoM95IpqVGrfNMrxomN6lVfnj6qb8Y3duxg=="
      },
      {
        "Id": 49759,
        "FileName": "manual_instance_58001_20180702010430.bak.tar",
        "StartTime": "2018-07-02 01:04:30",
        "EndTime": "2018-07-02 01:04:30",
        "Size": 192,
        "Strategy": 0,
        "Status": 1,
        "DBs": [
          "testdbvictornew"
        ],
        "InternalAddr": "http://10.66.0.88:58366/download/backup_49759.tar?YJW3gzNLKt2LCrywP9JslJXZo6TXiqprJ6x+tRJfDqzgJRdDrKF8j2V0XGk/MyyS00h9hexVea0A3GvpPf2aoq80DbnTNfZrvuFmWRKDML0cICOu7LASU2gWXlUkKcHfj/tspGhVGw8RX0OKecEUIQ==",
        "ExternalAddr": "https://gz-dl-sqlserver.cloud.tencent.com/download/backup_49759.tar?YJW3gzNLKt2LCrywP9JslJXZo6TXiqprJ6x+tRJfDqzgJRdDrKF8j2V0XGk/MyyS00h9hexVea0A3GvpPf2aoq80DbnTNfZrvuFmWRKDML0cICOu7LASU2gWXlUkKcHfj/tspGhVGw8RX0OKecEUIQ=="
      }
    ]
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeBackups)

### SDK

TencentCloud API 3.0 integrates SDKs that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/238/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InternalError.DBError | Database error. |
| InternalError.GcsError | GCS API error. |
| InternalError.SystemError | System error. |
| InternalError.UnknownError | Unknown error. |
| InvalidParameter | Incorrect parameter. |
| InvalidParameter.InputIllegal | Invalid input. |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion error. |
| ResourceNotFound.InstanceNotFound | The instance does not exist. |
