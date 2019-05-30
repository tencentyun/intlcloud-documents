## 1. API Description

API domain name: redis.tencentcloudapi.com.

This API queries the list of parameter modifications records.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial availability zones. Because financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), you need to specify a domain name with the financial availability zone as well, which preferably in the same region as the specified Region, for example: vod.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/239/20005).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeInstanceParamRecords |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-12 |
| Region | Yes | String | Common parameters; for details, see the [List of Regions](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID |
| Limit | No | Integer | Page size |
| Offset | No | Integer | Offset, which should be a multiplier of Limit |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of modifications. |
| InstanceParamHistory | Array of [InstanceParamHistory](/document/api/239/20022#InstanceParamHistory) | Information of modifications. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Querying the List of Parameter Modifications

#### Input Sample Code

```
https://redis.tencentcloudapi.com/?Action=DescribeInstanceParamRecords
&InstanceId=crs-5a4py64p
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "InstanceParamHistory": [
      {
        "ModifyTime": "2019-01-07 11:28:58",
        "NewValue": "511",
        "ParamName": "hash-max-ziplist-entries",
        "PreValue": "512",
        "Status": 2
      },
      {
        "ModifyTime": "2019-01-07 11:28:48",
        "NewValue": "15001",
        "ParamName": "cluster-node-timeout",
        "PreValue": "15000",
        "Status": 2
      }
    ],
    "RequestId": "e546784b-709c-401d-aba6-73037eb4e522",
    "TotalCount": 2
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**


* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeInstanceParamRecords)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/239/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.SystemError | Internal system error, irrelevant to the business. |
| InternalError.DbOperationFailed | Internal database operation (e.g., update, insert, or select) errors. |
| InternalError.InternalError | Internal error. |
| UnauthorizedOperation.NoCAMAuthed | The operation performed is not authorized by CAM. |
| UnauthorizedOperation.NoCAMAuthed | No CAM permissions. |
| UnauthorizedOperation.UserNotInWhiteList | The user is not on the whitelist. |
| UnsupportedOperation.ClusterInstanceAccessedDeny | The Redis cluster edition is not allowed to access a security group. |
