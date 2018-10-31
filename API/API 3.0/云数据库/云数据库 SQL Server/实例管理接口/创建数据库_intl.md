## 1. API Description

Domain name for API request: sqlserver.tencentcloudapi.com

This API (CreateDB) is used to create a database.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: sqlserver.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/238/19930).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: CreateDB |
| Version | Yes | String | Common parameter. The value used for this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID |
| DBs.N | Yes | Array of [DBCreateInfo](/document/api/238/19976#DBCreateInfo) | Information required for database creation |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| FlowId | Integer | Task flow ID |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Create the database test_db

#### Input example

```
https://sqlserver.tencentcloudapi.com/?Action=CreateDB
&InstanceId=mssql-i1z41iwd
&DBs.0.DBName=test_db
&DBs.0.Charset=Chinese_PRC_CI_AS
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "FlowId": 123,
    "RequestId": "4be5990d-a4b5-49dc-b2b4-e713b6aa7ba3"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=CreateDB)

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
| InternalError.SystemError | System error |
| InvalidParameter.InputIllegal | Invalid input parameter |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion failed. |
| ResourceNotFound.InstanceNotFound | Instance does not exist |
| ResourceUnavailable.InstanceStatusInvalid | Invalid instance status |

