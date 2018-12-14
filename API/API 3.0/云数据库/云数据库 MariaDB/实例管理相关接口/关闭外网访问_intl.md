## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (CloseDBExtranetAccess) is used to disable the access to a database instance from public network. After the public network access is disabled, the public network addresses cannot be accessed. The information of the public network domain and port of corresponding instances will not be returned via the "Query Instance List" API.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mariadb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: CloseDBExtranetAccess. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/237/16147#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID to be disabled the access from public network, such as tdsql-ow728lmc. It can be obtained by querying instance details via DescribeDBInstances. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| FlowId | Integer | Asynchronous task ID, which can be used to query task status through DescribeFlow. |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Disable the access to a database instance from public network

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=CloseDBExtranetAccess
&InstanceId=tdsql-avw0207d
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "FlowId": 3324,
    "RequestId": "2d1e21a2-b29a-490a-8be0-b61287d92e28"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=CloseDBExtranetAccess)

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
| FailedOperation.CreateFlowFailed | Failed to create the process |
| InternalError.CamAuthFailed | CAM authentication request failed |
| InvalidParameter.GenericParameterError | Failed to pass the parameter validity verification |
| ResourceNotFound.NoInstanceFound | The specified database instance is not found |
| ResourceUnavailable.InstanceAlreadyDeleted | The database instance has been deleted |
| ResourceUnavailable.InstanceStatusAbnormal | The database instance is in an invalid status and cannot be operated |
| UnauthorizedOperation.PermissionDenied | No permission to perform operations on the API or resource |

