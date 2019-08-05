## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (DescribeMigrations) describes a list of migration tasks based on the query criteria.

API request rate limit: 20 requests/sec.


## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: DescribeMigrations |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| StatusSet.N | No | Array of Integer | Status set. As long as a migration task is in a status therein, it will be listed |
| MigrateName | No | String | Migration task name (fuzzy match) |
| Limit | No | Integer | Number of results per page |
| Offset | No | Integer | Page number of the data to return  |
| OrderBy | No | String | Sort the results by keyword. Valid values: name, createTime, startTime, endTime, and status |
| OrderByType | No | String | Sorting order. Valid values: desc and asc |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of query results |
| MigrateTaskSet | Array of [MigrateTask](/document/api/238/19976#MigrateTask) | List of query results |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying the Migration Task List

#### Input Sample Code

```
https://sqlserver.tencentcloudapi.com/?Action=DescribeMigrations
&MigrateName=Test
&Limit=10
&Offset=0
&OrderBy=name
&OrderByType=desc
&StatusSet.0=1
&StatusSet.1=4
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "728ba95f-0443-41ec-82c9-44bc8bfc0802",
    "TotalCount": 2,
    "MigrateTaskSet": [
      {
        "MigrateId": 2734,
        "MigrateName": "Test migration",
        "AppId": 1251006373,
        "Region": "ap-guangzhou",
        "SourceType": 5,
        "CreateTime": "2018-08-09 11:46:15",
        "StartTime": "0000-00-00 00:00:00",
        "EndTime": "0000-00-00 00:00:00",
        "Status": 1,
        "Message": "",
        "CheckFlag": 0,
        "Progress": 0,
        "MigrateDetail": {
          "StepName": "",
          "Progress": 0
        }
      },
      {
        "MigrateId": 2732,
        "MigrateName": "Test API ",
        "AppId": 1251006373,
        "Region": "ap-guangzhou",
        "SourceType": 5,
        "CreateTime": "2018-08-08 21:03:09",
        "StartTime": "0000-00-00 00:00:00",
        "EndTime": "0000-00-00 00:00:00",
        "Status": 1,
        "Message": "",
        "CheckFlag": 0,
        "Progress": 0,
        "MigrateDetail": {
          "StepName": "",
          "Progress": 0
        }
      }
    ]
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeMigrations)

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
