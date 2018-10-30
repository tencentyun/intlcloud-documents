## 1. API Description

Domain name for API request: sqlserver.tencentcloudapi.com

This API (DescribeMigrations) is used to query the list of migration tasks that meet the entered criteria.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: sqlserver.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/238/19930).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeMigrations |
| Version | Yes | String | Common parameter. The value used for this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| StatusSet.N | No | Array of Integer | Status set. Any migration tasks in a specified status in the set can be queried. |
| MigrateName | No | String | Migration task name. Fuzzy match is supported. |
| Limit | No | Integer | Number of records per page |
| Offset | No | Integer | The page on which the records are queried |
| OrderBy | No | String | The keyword by which the results are sorted. Available values: name, createTime, startTime, endTime, and status |
| OrderByType | No | String | Sorting mode. Available values: desc and asc |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of query results |
| MigrateTaskSet | Array of [MigrateTask](/document/api/238/19976#MigrateTask) | The list of query results |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query the list of migration tasks

#### Input example

```
https://sqlserver.tencentcloudapi.com/?Action=DescribeMigrations
&MigrateName=Test
&Limit=10
&Offset=0
&OrderBy=name
&OrderByType=desc
&StatusSet.0=1
&StatusSet.1=4
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "MigrateTaskSet": [
      {
        "AppId": 1251006373,
        "CheckFlag": 0,
        "CreateTime": "2018-08-09 11:46:15",
        "EndTime": "0000-00-00 00:00:00",
        "Message": "",
        "MigrateDetail": {
          "Progress": 0,
          "StepName": ""
        },
        "MigrateId": 2734,
        "MigrateName": "Test migration",
        "Progress": 0,
        "Region": "ap-guangzhou",
        "SourceType": 5,
        "StartTime": "0000-00-00 00:00:00",
        "Status": 1
      },
      {
        "AppId": 1251006373,
        "CheckFlag": 0,
        "CreateTime": "2018-08-08 21:03:09",
        "EndTime": "0000-00-00 00:00:00",
        "Message": "",
        "MigrateDetail": {
          "Progress": 0,
          "StepName": ""
        },
        "MigrateId": 2732,
        "MigrateName": "Test API",
        "Progress": 0,
        "Region": "ap-guangzhou",
        "SourceType": 5,
        "StartTime": "0000-00-00 00:00:00",
        "Status": 1
      }
    ],
    "RequestId": "728ba95f-0443-41ec-82c9-44bc8bfc0802",
    "TotalCount": 2
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeMigrations)

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
| InternalError.SystemError | System error |
| InternalError.UnknownError | Unknown error |
| InvalidParameter | Incorrect parameter. |
| InvalidParameter.InputIllegal | Invalid input parameter |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion failed |

