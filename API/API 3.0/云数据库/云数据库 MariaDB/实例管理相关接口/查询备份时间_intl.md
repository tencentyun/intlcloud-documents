## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (DescribeBackupTime) is used to get the backup time of a database. The backend system makes periodic backup of instances based on the configuration.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mariadb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeBackupTime. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/237/16147#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceIds.N | Yes | Array of String | Instance ID, such as tdsql-ow728lmc. It can be obtained by querying instance details via DescribeDBInstances. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Returns the number of configurations |
| Items | [DBBackupTimeConfig](/document/api/237/16191#DBBackupTimeConfig) | Configurations of instance backup time |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query the configurations of backup time window for database instances

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=DescribeBackupTime
&InstanceIds.0=tdsql-fdpjf5zh
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "Items": [
      {
        "EndBackupTime": "23:59",
        "InstanceId": "tdsql-33y5ai5p",
        "StartBackupTime": "00:00"
      }
    ],
    "RequestId": "caca6ca7-9ef0-48e0-aa7a-4327a1ac001c",
    "TotalCount": 1
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=DescribeBackupTime)

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
| FailedOperation.OssOperationFailed | Failed to request backend APIs |
| InternalError.CamAuthFailed | CAM authentication request failed |
| InternalError.DbOperationFailed | Failed to query the database |
| InternalError.GetInstanceDetailFailed | Failed to obtain instance details |
| InternalError.InnerSystemError | Internal system error |
| InvalidParameter.GenericParameterError | Failed to pass the parameter validity verification |
| UnauthorizedOperation.PermissionDenied | No permission to perform operations on the API or resource |

