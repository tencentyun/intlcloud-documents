## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (ModifyMigration) is used to modify an existing migration task.

API request rate limit: 20 requests/sec.


## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: ModifyMigration |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| MigrateId | Yes | Integer | Migration task ID |
| MigrateName | No | String | New name of the migration task. If this is left blank, no modification will be made |
| MigrateType | No | Integer | New migration type (1: structure migration, 2: data migration, 3: incremental synchronization). If this is left blank, no modification will be made |
| SourceType | No | Integer | Type of migration source. 1: TencentDB for SQL Server, 2: SQL Server database created by CVM, 4: SQL Server backup restoration, 5: SQL Server backup restoration (in COS mode). If this is left blank, no modification will be made |
| Source | [MigrateSource](/document/api/238/19976#MigrateSource) | Migration source. If this is left blank, no modification will be made |
| Target | No | [MigrateTarget](/document/api/238/19976#MigrateTarget) | Migration target. If this is left blank, no modification will be made |
| MigrateDBSet.N | No | Array of [MigrateDB](/document/api/238/19976#MigrateDB) | Database objects to be migrated. This parameter is not used for offline migration (SourceType=4 or SourceType=5). If this is left blank, no modification will be made |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| MigrateId | Integer | Migration task ID |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Modifying a Migration Task

#### Input Sample Code

```
https://sqlserver.tencentcloudapi.com/?Action=ModifyMigration
&MigrateId=2728
&MigrateName=Test API
&MigrateType=2
&SourceType=5
&Source.Url.0=http://gz-oncvm-1254065710.cosgz.myqcloud.com/testdb.bak
&Target.InstanceId=mssql-si2823jyl
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "4be5990d-a4b5-49dc-b2b4-e713b6aa7ba3",
    "MigrateId": 2728
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=ModifyMigration)

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
| InternalError.CreateFlowFailed | Failed to create the flow. |
| InternalError.DBError | Database error. |
| InternalError.SystemError | System error. |
| InternalError.UnknownError | Unknown error. |
| InvalidParameter | Incorrect parameter. |
| InvalidParameter.InputIllegal | Invalid input. |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion error. |
| ResourceNotFound.InstanceNotFound | The instance does not exist. |
| ResourceUnavailable.InstanceMigrateRegionIllegal | Invalid instance migration region. |
| ResourceUnavailable.InstanceMigrateStatusInvalid | Invalid instance migration status. |
| ResourceUnavailable.InstanceStatusInvalid | Invalid instance status. |
