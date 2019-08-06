## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (DescribeDBs) describes the database list.

API request rate limit: 20 requests/sec.




## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: DescribeDBs |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceIdSet.N | Yes | Array of String | Instance ID |
| Limit | No | Integer | Number of results per page; up to 100; 20 by default |
| Offset | No | Integer | Page number, starting at 0 |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of databases |
| DBInstances | Array of [InstanceDBDetail](/document/api/238/19976#InstanceDBDetail) | Databases instance list |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying the Database List

#### Input Sample Code

```
https://sqlserver.tencentcloudapi.com/?Action=DescribeDBs
&InstanceId.0=mssql-njj2mtpl
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "5062de55-d048-4d3b-92f9-b98b6f244360",
    "TotalCount": 1,
    "DBInstances": [
      {
        "InstanceId": "mssql-632eyp63",
        "DBDetails": [
          {
            "Name": "ceshi1",
            "Charset": "Chinese_PRC_CI_AS",
            "Remark": "Test db1",
            "CreateTime": "2018-07-02 20:12:24",
            "Status": 2,
            "Accounts": [
              {
                "UserName": "victorwind",
                "Privilege": "ReadWrite"
              }
            ],
            "InternalStatus": "ONLINE"
          }
        ]
      }
    ]
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeDBs)

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
| InvalidParameter.InputIllegal | Invalid input. |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion error. |
| ResourceNotFound.InstanceNotFound | The instance does not exist. |
