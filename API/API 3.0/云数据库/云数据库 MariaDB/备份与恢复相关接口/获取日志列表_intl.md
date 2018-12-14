## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (DescribeDBLogFiles) is used to obtain various log lists of the database, including cold backup, binlog, errlog and slowlog.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mariadb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeDBLogFiles. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/237/16147#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID, such as tdsql-ow728lmc. |
| Type | Yes | Integer | Request log type, and can only be 1, 2, 3 or 4. 1-binlog, 2-cold backup, 3-errlog, 4-slowlog. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| InstanceId | String | Instance ID, such as tdsql-ow728lmc. |
| Type | Integer | Request log type, and can only be 1, 2, 3 or 4. 1-binlog, 2-cold backup, 3-errlog, 4-slowlog. |
| Total | Integer | Total number of request logs |
| Files | Array of [LogFileInfo](/document/api/237/16191#LogFileInfo) | Includes information such as uri, length, mtime (modification time). |
| VpcPrefix | String | If the instance is in a VPC network, the download address is the URI prefixed by this string. |
| NormalPrefix | String | If the instance is in an ordinary network, the download address is the URI prefixed by this string. |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 None

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=DescribeDBLogFiles
&InstanceId=tdsql-ow728lmc
&Type=1
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "Files": [
      {
        "Length": 5253724,
        "Mtime": 1468822981,
        "Uri": "/1/noshard_108/set_1468578840_203059/1468578832/859932065/000001/5ce7d1a8f26c2dfcf1de22d4e9792b11b0b0057450684d266e1bf9a8aa6ea272"
      }
    ],
    "InstanceId": "tdsql-ow728lmc",
    "NormalPrefix": "http://10.66.255.253:8083",
    "RequestId": "7212a9ec-a235-2144-98d4-59fbe6f14d79",
    "Total": 1,
    "Type": 1,
    "VpcPrefix": "http://169.254.0.27:8083"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=DescribeDBLogFiles)

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
| InternalError.DbOperationFailed | Failed to query the database |
| InternalError.GetInstanceInfoFailed | Failed to acquire the backend instance information |
| InternalError.HDFSError | Failed to read backup files |
| InternalError.InnerConfigurationMissing | Internal configuration missing |
| ResourceUnavailable.InstanceAlreadyDeleted | The database instance has been deleted |
| ResourceUnavailable.InstanceStatusAbnormal | The database instance is in an invalid status and cannot be operated |

