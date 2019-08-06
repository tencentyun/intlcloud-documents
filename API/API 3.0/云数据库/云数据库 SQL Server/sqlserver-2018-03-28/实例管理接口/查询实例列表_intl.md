## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (DescribeDBInstances) describes the database instance list.

API request rate limit: 20 requests/sec.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: DescribeDBInstances |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| ProjectId | No | Integer | Project ID |
| Status | No | Integer | Instance status. Value range: <br/><li>1: applying </li><li>2: running </li><li>3: restrictedly running (master/slave switching) </li><li>4: isolated </li><li>5: repossessing </li><li>6: repossessed </li><li>7: task running (e.g., backing up or rolling back the instance) </li><li>8: decommissioned </li><li>9: scaling </li><li>10: migrating </li><li>11: read-only </li><li>12: restarting </li> |
| Offset | No | Integer | Offset. 0 by default |
| Limit | No | Integer | Number of results returned; 50 by default |
| InstanceIdSet.N | No | Array of String | One or more instance IDs in the format of mssql-si2823jyl |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of eligible instances. If the results are returned in multiple pages, this value is the number of all eligible instances but not the number of instances returned according to the current values of Limit and Offset |
| DBInstances | Array of [DBInstance](/document/api/238/19976#DBInstance) | Instance list |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying the Instance List

#### Input Sample Code

```
https://sqlserver.tencentcloudapi.com/?Action=DescribeDBInstances
&ProjectId=0
&InstanceIdSet.0=mssql-njj2mtpl
&Status=2
&Offset=0
&Limit=3
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "e4d6e59c-fdca-4694-bfc3-890f2eadc109",
    "TotalCount": 1,
    "DBInstances": [
      {
        "InstanceId": "mssql-njj2mtpl",
        "Region": "ap-guangzhou",
        "Zone": "ap-guangzhou-2",
        "Name": "8b0d6a95-4453-4a39-b484-ba94765a081b",
        "ProjectId": 0,
        "RegionId": 1,
        "ZoneId": 100002,
        "VpcId": 0,
        "SubnetId": 0,
        "Status": 2,
        "Vip": "10.66.19.118",
        "Vport": 1433,
        "CreateTime": "2018-01-29 11:45:57",
        "UpdateTime": "2018-04-10 16:35:07",
        "Memory": 2000,
        "Storage": 10,
        "Model": 1,
        "VersionName": "SQL Server 2008 R2",
        "StartTime": "2018-01-29 11:45:57",
        "EndTime": "2018-05-29 11:45:57",
        "IsolateTime": "",
        "RenewFlag": 0,
        "UsedStorage": 8
      }
    ]
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeDBInstances)

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
