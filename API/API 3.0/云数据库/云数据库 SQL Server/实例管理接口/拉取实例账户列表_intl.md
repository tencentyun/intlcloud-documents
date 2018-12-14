## 1. API Description

Domain name for API request: sqlserver.tencentcloudapi.com

This API (DescribeAccounts) is used to fetch the list of accounts for an instance.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: sqlserver.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/238/19930).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeAccounts |
| Version | Yes | String | Common parameter. The value used for this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID |
| Limit | No | Integer | Number of results returned per page. It should range from 1 to 100. Maximum is 20. |
| Offset | No | Integer | The starting page number for the results returned in pages. It defaults to 0. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| InstanceId | String | Instance ID |
| Accounts | Array of [AccountDetail](/document/api/238/19976#AccountDetail) | List of accounts |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Fetch the list of accounts for an instance

#### Input example

```
https://sqlserver.tencentcloudapi.com/?Action=DescribeAccounts
&InstanceId=mssql-j8kv137v
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "Accounts": [
      {
        "CreateTime": "2018-07-27 22:24:54",
        "Dbs": [],
        "InternalStatus": "enable",
        "Name": "wang",
        "PassTime": "2018-07-27 22:25:25",
        "Remark": "wang test account",
        "Status": 2,
        "UpdateTime": "2018-07-27 22:25:25"
      },
      {
        "CreateTime": "2018-08-07 15:28:00",
        "Dbs": [],
        "InternalStatus": "enable",
        "Name": "test",
        "PassTime": "0000-00-00 00:00:00",
        "Remark": "None",
        "Status": 2,
        "UpdateTime": "2018-08-07 15:28:00"
      }
    ],
    "InstanceId": "mssql-632eyp63",
    "RequestId": "5729760c-db94-4c71-a1ee-ebd43adae189"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeAccounts)

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
| InternalError.DBError | Database error |
| InternalError.SystemError | System error |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion failed |
| ResourceNotFound.InstanceNotFound | Instance does not exist |

