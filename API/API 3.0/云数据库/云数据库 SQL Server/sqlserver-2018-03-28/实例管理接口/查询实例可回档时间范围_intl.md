## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (DescribeRollbackTime) describes the time range available for the specified database instance to rollback.

API request rate limit: 20 requests/sec.




## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: DescribeRollbackTime |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID |
| DBs.N | Yes | Array of String | List of databases to be queried |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Details | Array of [DbRollbackTimeInfo](/document/api/238/19976#DbRollbackTimeInfo) | Information of the time range available for database rollback |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying the Time Range Available for Rolling back db1 in the Instance mssql-j8kv137v

#### Input Sample Code

```
https://sqlserver.tencentcloudapi.com/?Action=DescribeRollbackTime
&InstanceId=mssql-j8kv137v
&DBs.0=db1
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "780339f6-30d7-419a-a30c-c2dc0933af1c",
    "Details": [
      {
        "DBName": "db1",
        "StartTime": "2018-08-07 11:09:03",
        "EndTime": "2018-08-09 11:09:03"
      }
    ]
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeRollbackTime)

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
| InternalError.SystemError | System error. |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion error. |
| ResourceNotFound.InstanceNotFound | The instance does not exist. |
