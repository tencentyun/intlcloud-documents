## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API (ModifyAutoSnapshotPolicyAttribute) is used to modify the attributes of a scheduled snapshot policy.

* You can use this API to modify the attributes of a scheduled snapshot policy, including the execution policy, name, and activation.
* When modifying the number of days for retention, please ensure that it is not conflict with the permanent retention attribute. Otherwise, the entire operation will fail and a specific error code will be returned.

Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: ModifyAutoSnapshotPolicyAttribute |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoSnapshotPolicyId | Yes | String | The ID of the scheduled snapshot policy. |
| Policy.N | No | Array of [Policy](/document/api/362/15669#Policy) | The execution policy for scheduled snapshots. |
| AutoSnapshotPolicyName | No | String | The name of the scheduled snapshot policy that you want to create. If this is not passed, the default is “Not Named”. The length cannot exceed 60 characters. |
| IsActivated | No | Boolean | Whether the scheduled snapshot policy is activated. FALSE: Not activated. True: Activated. The default value is TRUE. |
| IsPermanent | No | Boolean | Whether the snapshot created by this scheduled snapshot policy is retained permanently. FALSE: Not retained permanently. TRUE: Retained permanently. The default value is FALSE. |
| RetentionDays | No | Integer | The number of days for which snapshots created by this policy are retained. This parameter cannot clash with `IsPermanent`. That is, if the scheduled snapshot policy is configured to retain permanently, `RetentionDays` must be 0. 

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1 Modifying the Attributes of an Scheduled Snapshot Policy

The name of the scheduled snapshot policy to be modified is `data_disk_auto_snapshot`. `IsPermanent` is set to `TRUE`. Snapshots created by this scheduled snapshot policy are retained permanently.

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=ModifyAutoSnapshotPolicyAttribute
&AutoSnapshotPolicyId=asp-nqu08k2l
&AutoSnapshotPolicyName=data_disk_auto_snapshot
&IsPermanent=TRUE
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "384c1fa8-6973-9623-b6bf-5a1fa9a7ad88"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=ModifyAutoSnapshotPolicyAttribute)

### SDK

TencentCloud API 3.0 comes with SDKs that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/362/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidAutoSnapshotPolicyId.NotFound | The `AutoSnapshotPolicyId` does not exist. |
| InvalidParameter | Invalid parameter |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |
| UnsupportedOperation.StateError | The current status of the resource does not support this operation. |
