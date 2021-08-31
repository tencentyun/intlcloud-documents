## 1. API Description

API domain name: cloudaudit.tencentcloudapi.com.

This API is used to query the details of a tracking set.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/1021/34192).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeAudit. |
| Version | Yes | String | Common parameter. The value used for this API: 2019-03-19. |
| Region | Yes | String | Common parameter. For more information, please see the [list of regions](https://intl.cloud.tencent.com/document/api/1021/34192#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AuditName | Yes | String | Tracking set name |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| AuditName | String | Tracking set name. |
| AuditStatus | Integer | Tracking set status. 1: enabled, 0: disabled. |
| CmqQueueName | String | Queue name. |
| CmqRegion | String | Region where the queue is located. |
| CosBucketName | String | COS bucket name. |
| CosRegion | String | Region where the COS bucket is located. |
| IsEnableCmqNotify | Integer | Whether to enable CMQ message notification. 1: yes; 0: no. |
| IsEnableKmsEncry | Integer | Whether to enable KMS encryption. 1: yes, 0: no. If KMS encryption is enabled, the data will be encrypted when delivered to COS. |
| KeyId | String | Globally unique ID of the CMK. |
| KmsAlias | String | CMK alias. |
| KmsRegion | String | KMS region. |
| LogFilePrefix | String | Log prefix. |
| ReadWriteAttribute | Integer | Manages the read/write attribute of an event. Valid values: 1 (read-only), 2 (write-only), 3 (read/write) |
| RequestId | String | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying the details of tracking sets

This example shows you how to query tracking set details.

#### Input sample code

```
https://cloudaudit.tencentcloudapi.com/?Action=DescribeAudit
&AuditName=xxxxx_cloudaudit_2
&<Common request parameters>
```

#### Output sample code

```
{
  "Response": {
    "AuditName": "xxxxx_cloudaudit_2",
    "CmqQueueName": "xxxxx-cloudaudit-2",
    "CmqRegion": "hk",
    "CosBucketName": "xxxxx-cloudaudit-2",
    "CosRegion": "ap-hongkong",
    "IsEnableCmqNotify": 1,
    "LogFilePrefix": "xxx2312",
    "ReadWriteAttribute": 1,
    "AuditStatus": 1,
    "RequestId": "e23ee347-d011-482a-83fa-12e7d318dd9f"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cloudaudit&Version=2019-03-19&Action=DescribeAudit)

### SDK

TencentCloud API 3.0 comes with SDKs that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for Node.js](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, please see [Common Error Codes](https://intl.cloud.tencent.com/document/api/1021/34195#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.DescribeAuditError | Error querying tracking set details. Please submit a ticket. |
| ResourceNotFound.AuditNotExist | The tracking set does not exist. |
