## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (DescribeMigrationDetail) describes data migration task details.

API request rate limit: 20 requests/sec.


## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: DescribeMigrationDetail |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| MigrateId | Yes | Integer | Migration task ID |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| MigrateId | Integer | Migration task ID |
| MigrateName | String | Migration task name |
| AppId | Integer | ID of the user who created the migration task |
| Region | String | Region of the migration task |
| SourceType | Integer | Type of migration source. 1: TencentDB for SQL Server, 2: SQL Server database created by CVM, 4: SQL Server backup restoration, 5: SQL Server backup restoration (in COS mode) |
| CreateTime | Timestamp | Migration task creation time |
| StartTime | Timestamp | Migration task start time |
| EndTime | Timestamp | Migration task end time |
| Status | Integer | Migration task status (1: initializing, 4: migrating, 5: migration failed, 6: migration succeeded) |
| Progress | Integer | Migration task progress |
| MigrateType | Integer | Migration type (1: structure migration, 2: data migration, 3: incremental synchronization) |
| Source | [MigrateSource](/document/api/238/19976#MigrateSource) | Migration source |
| Target | [MigrateTarget](/document/api/238/19976#MigrateTarget) | Migration target |
| MigrateDBSet | Array of [MigrateDB](/document/api/238/19976#MigrateDB) | Database objects to be migrated. This parameter is unavailable for offline migration (SourceType=4 or SourceType=5) |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying Migration Task Details

#### Input Sample Code

```
https://sqlserver.tencentcloudapi.com/?Action=DescribeMigrationDetail
&MigrateId=2728
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "4be5990d-a4b5-49dc-b2b4-e713b6aa7ba3",
    "MigrateId": 2728,
    "MigrateName": "Test API ",
    "AppId": 1254065710,
    "Region": "ap-guangzhou",
    "SourceType": 5,
    "CreateTime": "2018-08-06 17:44:58",
    "StartTime": "0000-00- 00 00:00:00",
    "EndTime": "0000-00-00 00:00:00",
    "Status": 1,
    "Progress": 0,
    "MigrateType": 2,
    "Source": {
      "InstanceId": "",
      "CvmId": "",
      "VpcId": "",
      "SubnetId": "",
      "UserName": "",
      "Password": "",
      "Ip": "",
      "Port": 0,
      "url": [
        "http://gz-oncvm-1254065710.cosgz.myqcloud.com/test4_20180724021516.bak",
        "http://gz-oncvm-1254065710.cosgz.myqcloud.com/testdb.bak"
      ],
      "urlPassword": ""
    },
    "Target": {
      "InstanceId ": "mssql-dr5843bdy",
      "UserName": "",
      "Password": ""
    },
    "MigrateDBSet": []
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeMigrationDetail)

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
| InternalError.SystemError | System error. |
| InternalError.UnknownError | Unknown error. |
| InvalidParameter | Incorrect parameter. |
| InvalidParameter.InputIllegal | Invalid input. |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion error. |
