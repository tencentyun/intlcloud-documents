## 1. API Description

API domain name: cloudaudit.tencentcloudapi.com.

Parameter requirements:
1. If the value of IsCreateNewBucket exists, cosRegion and cosBucketName are required.
2. If the value of IsEnableCmqNotify is 1, IsCreateNewQueue, CmqRegion, and CmqQueueName are required.
3. If the value of IsEnableCmqNotify is 0, IsCreateNewQueue, CmqRegion, and CmqQueueName cannot be passed in.
4. If the value of IsEnableKmsEncry is 1, both KmsRegion and KeyId are required.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/1021/34192).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: CreateAudit. |
| Version | Yes | String | Common parameter. The value used for this API: 2019-03-19. |
| Region | Yes | String | Common parameter. For more information, please see the [list of regions](https://intl.cloud.tencent.com/document/api/1021/34192#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AuditName | Yes | String | Tracking set name, which can contain 3–128 ASCII letters (a–z; A–Z), digits (0–9), and underscores (_). |
| CosBucketName | Yes | String | User-defined COS bucket name, which can only contain 1–40 lowercase letters (a–z), digits (0–9), and dashes (-) and cannot begin or end with "-". If a bucket is not newly created, CloudAudit will not verify whether it actually exists. Please enter the name with caution so as to avoid log delivery failure and consequent data loss. |
| CosRegion | Yes | String | COS region. Supported regions can be queried using the ListCosEnableRegion API. |
| IsCreateNewBucket | Yes | Integer | Whether to create a COS bucket. 1: yes; 0: no. |
| IsEnableCmqNotify | Yes | Integer | Whether to enable CMQ message notification. 1: yes; 0: no. Only CMQ queue service is currently supported. If CMQ message notification is enabled, CloudAudit will deliver your log contents to the designated queue in the specified region in real time. |
| ReadWriteAttribute | Yes | Integer | Manages the read/write attribute of an event. Valid values: 1 (read-only), 2 (write-only), 3 (read/write). |
| CmqQueueName | No | String | Queue name, which must begin with a letter and can contain up to 64 letters, digits, and dashes (-). This field is required if the value of IsEnableCmqNotify is 1. If a queue is not newly created, CloudAudit will not verify whether it actually exists. Please enter the name with caution so as to avoid log delivery failure and consequent data loss. |
| CmqRegion | No | String | Region where the queue is located. Supported CMQ regions can be queried using the ListCmqEnableRegion API. This field is required if the value of IsEnableCmqNotify is 1. |
| IsCreateNewQueue | No | Integer | Whether to create a queue. 1: yes; 0: no. This field is required if the value of IsEnableCmqNotify is 1. |
| IsEnableKmsEncry | No | Integer | Whether to enable KMS encryption. 1: yes, 0: no. If KMS encryption is enabled, the data will be encrypted when delivered to COS. |
| KeyId | No | String | Globally unique ID of the CMK. This value is required if it is not a newly created KMS element. It can be obtained through ListKeyAliasByRegion. CloudAudit will not verify the validity of the KeyId. Please enter it carefully to avoid data loss. |
| KmsRegion | No | String | KMS region. Currently supported regions can be obtained through ListKmsEnableRegion. This must be the same as the COS region. |
| LogFilePrefix | No | String | Prefix of a log file, which can only contain 3–40 ASCII letters (a–z; A–Z) and digits (0–9). It can be left empty and is the account ID by default. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| IsSuccess | Integer | Whether creation is successful. |
| RequestId | String | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Creating a tracking set

This example shows you how to create a tracking set.

#### Input sample code

```
https://cloudaudit.tencentcloudapi.com/?Action=CreateAudit
&AuditName=auditTest_1
&CmqQueueName=cmq-01
&CmqRegion=sh
&CosBucketName=cos-01
&CosRegion=ap-shanghai
&IsCreateNewBucket=1
&IsCreateNewQueue=1
&IsEnableCmqNotify=1
&LogFilePrefix=akshsb1j
&ReadWriteAttribute=2
&<Common request parameters>
```

#### Output sample code

```
{
  "Response": {
    "IsSuccess": 1,
    "RequestId": "e9501707-784a-474c-b524-67ed9d3a6b50"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cloudaudit&Version=2019-03-19&Action=CreateAudit)

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
| FailedOperation.CreateBucketFail | Failed to create the COS bucket. |
| InternalError.CmqError | An exception occurred during CMQ queue creation, probably because the CMQ queue to be created already exists, or your account has no permission or is in arrears. |
| InternalError.CreateAuditError | Error creating the tracking set. Please submit a ticket. |
| InvalidParameterValue.AuditNameError | Tracking set name is non-compliant. |
| InvalidParameterValue.CmqRegionError | CloudAudit currently does not support the entered CMQ region. |
| InvalidParameterValue.CosNameError | The entered COS bucket name is non-compliant. |
| InvalidParameterValue.CosRegionError | CloudAudit currently does not support the entered COS region. |
| InvalidParameterValue.IsCreateNewBucketError | The value of IsCreateNewBucket can be 0 or 1. 0 represents not creating a bucket, while 1 creating a bucket. |
| InvalidParameterValue.IsCreateNewQueueError | The value of IsCreateNewQueue can be 0 or 1. 0 represents not creating a queue, while 1 creating a queue. |
| InvalidParameterValue.IsEnableCmqNotifyError | The value of IsEnableCmqNotify can be 0 or 1. 0 represents not enabling CMQ delivery, while 1 enabling. |
| InvalidParameterValue.LogFilePrefixError | Incorrect log prefix format. |
| InvalidParameterValue.QueueNameError | The entered queue name is non-compliant. |
| InvalidParameterValue.ReadWriteAttributeError | Valid values of the read/write attribute: 1 (read-only), 2 (write-only), 3 (read/write). |
| LimitExceeded.OverAmount | The maximum number of tracking sets is exceeded. |
| MissingParameter.MissAuditName | Tracking set name is missing. |
| MissingParameter.MissCosBucketName | COS bucket parameter is missing. |
| MissingParameter.MissCosRegion | COS region parameter is missing. |
| MissingParameter.cmq | If the value of IsEnableCmqNotify is 1, IsCreateNewQueue, CmqQueueName, and CmqRegion are required. |
| ResourceInUse.AlreadyExistsSameAudit | A tracking set with the same name already exists. |
| ResourceInUse.AlreadyExistsSameAuditCmqConfig | A tracking set with the same CMQ delivery configuration already exists. |
| ResourceInUse.AlreadyExistsSameAuditCosConfig | A tracking set with the same COS delivery configuration already exists. |
| ResourceInUse.CosBucketExists | The COS bucket already exists. |
