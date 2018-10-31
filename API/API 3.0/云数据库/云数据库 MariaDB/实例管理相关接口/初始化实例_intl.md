## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (InitDBInstances) is used to initialize a database instance, including the settings of its default character set, and case sensitivity of table names.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mariadb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: InitDBInstances. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/237/16147#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceIds.N | Yes | Array of String | List of instance IDs to be initialized, such as tdsql-ow728lmc. It can be obtained by querying instance details via DescribeDBInstances. |
| Params.N | Yes | Array of [DBParamValue](/document/api/237/16191#DBParamValue) | List of parameters. Available values for this API are character_set_server (character set, which is required), lower_case_table_names (case sensitivity of table names, which is required), innodb_page_size (innodb data page, which is 16 KB by default) and sync_mode (synchronization mode: 0 - Async; 1 - Strongsync (default); 2 - Strongsync (degradable)). |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| FlowId | Integer | Asynchronous task ID, which can be used to query task status through DescribeFlow. |
| InstanceIds | Array of String | A pass-through input parameter |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Initialize database instances in batch

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=InitDBInstances
&InstanceIds.0=tdsql-fdpjf5zh
&InstanceIds.1=tdsql-avw0207d
&Params.0.Param=lower_case_table_names
&Params.0.Value=1
&Params.1.Param=innodb_page_size
&Params.1.Value=16384
&Params.2.Param=character_set_server
&Params.2.Value=utf8
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "FlowId": 3340,
    "InstanceIds": [
      "tdsql-fdpjf5zh",
      "tdsql-avw0207d"
    ],
    "RequestId": "d94ef093-ff84-4851-b2e0-a5c5920d618e"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=InitDBInstances)

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

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](/document/api/237/16149#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.CamAuthFailed | CAM authentication request failed |
| InternalError.DbOperationFailed | Failed to query the database |
| InternalError.InnerSystemError | Internal system error |
| InvalidParameter.GenericParameterError | Failed to pass the parameter validity verification |
| InvalidParameterValue.IllegalInitParam | Error on parameters when initializing database instances |
| ResourceUnavailable.BadInstanceStatus | Error on instance status. Failed to initialize. |
| UnauthorizedOperation.PermissionDenied | No permission to perform operations on the API or resource |

