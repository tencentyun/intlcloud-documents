## 1. API Description

Domain name for API request: sqlserver.tencentcloudapi.com

This API (DescribeDBInstances) is used to query the list of instances.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: sqlserver.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/238/19930).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeDBInstances |
| Version | Yes | String | Common parameter. The value used for this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| ProjectId | No | Integer | Project ID |
| Status | No | Integer | Instance status. Supported values: <br/><li>1: In application; </li><li>2: In operation; </li><li>3: In restricted operation (switching between master and salve); </li><li>4: Isolated; </li><li>5: Reclaiming; </li><li>6: Reclaimed; </li><li>7: Task is running (backing up, rolling back, etc.); </li><li>8: Deactivated; </li><li>9: Expanding capacity; </li><li>10: Migrating; </li><li>11: Read only; </li><li>12: Restarting</li> |
| Offset | No | Integer | Offset. It defaults to 0. |
| Limit | No | Integer | Number of returned results. It defaults to 50. |
| InstanceIdSet.N | No | Array of String | One or more instance IDs, such as: mssql-si2823jyl |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| Total Count | Integer | Total number of the instances matching the condition. If the results are returned in pages, this value indicates the number of all instances matching the condition, instead of the number of instances returned based on the Limit and Offset values. |
| DBInstances | Array of [DBInstance](/document/api/238/19976#DBInstance) | List of instances |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query the instance list

#### Input example

```
https://sqlserver.tencentcloudapi.com/?Action=DescribeDBInstances
&ProjectId=0
&InstanceIdSet.0=mssql-njj2mtpl
&Status=2
&Offset=0
&Limit=3
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "DBInstances": [
      {
        "CreateTime": "2018-01-29 11:45:57",
        "EndTime": "2018-05-29 11:45:57",
        "InstanceId": "mssql-njj2mtpl",
        "IsolateTime": "",
        "Memory": 2000,
        "Model": 1,
        "Name": "8b0d6a95-4453-4a39-b484-ba94765a081b",
        "ProjectId": 0,
        "Region": "ap-guangzhou",
        "RegionId": 1,
        "RenewFlag": 0,
        "StartTime": "2018-01-29 11:45:57",
        "Status": 2,
        "Storage": 10,
        "SubnetId": 0,
        "UpdateTime": "2018-04-10 16:35:07",
        "UsedStorage": 8,
        "VersionName": "SQL Server 2008 R2",
        "Vip": "10.66.19.118",
        "VpcId": 0,
        "Vport": 1433,
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002
      }
    ],
    "RequestId": "e4d6e59c-fdca-4694-bfc3-890f2eadc109",
    "TotalCount": 1
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeDBInstances)

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
| InternalError.UnknownError | Unknown error. |
| InvalidParameter | Incorrect parameter. |
| InvalidParameter.InputIllegal | Invalid input parameter |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion failed |

