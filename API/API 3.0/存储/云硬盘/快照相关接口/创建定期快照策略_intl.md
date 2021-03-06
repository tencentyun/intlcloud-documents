## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API (CreateAutoSnapshotPolicy) is used to create a scheduled snapshot policy.

* For the limits on the number of scheduled snapshot policies that can be created in each region, see [Scheduled Snapshots](https://intl.cloud.tencent.com/document/product/362/35238).
* The quantity and capacity of the snapshots that can be created in each region are limited. For more information, see the **Snapshots** page on the Tencent Cloud Console. If the number of snapshots exceeds the quota, the creation of the scheduled snapshots will fail.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: cbs.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: CreateAutoSnapshotPolicy |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Policy.N | Yes | Array of [Policy](https://cloud.tencent.com/document/api/362/15669#Policy) | The execution policy for scheduled snapshots. |
| AutoSnapshotPolicyName | No | String | Name of the scheduled snapshot policy to create. If it is not specified, the default is “Not Named”. The length cannot exceed 60 characters. |
| IsActivated | No | Boolean | Whether the scheduled snapshot policy is activated. FALSE: Not activated. True: Activated. The default value is TRUE. |
| IsPermanent | No | Boolean | Whether the snapshot created by this scheduled snapshot policy is retained permanently. FALSE: Not retained permanently. TRUE: Retained permanently. The default value is FALSE. |
| RetentionDays | No | Integer | The number of days that a snapshot created by this scheduled snapshot policy is retained. The default value is 7. If this parameter is specified, the IsPermanent input parameter can not be TRUE, otherwise a conflict will occur. I
| DryRun | No | Boolean | Whether to create an execution policy for the scheduled snapshot. TRUE: Only obtain the time of the first snapshot but not to create a scheduled snapshot policy. FALSE: Create a scheduled snapshot policy. The default value is FALSE. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| AutoSnapshotPolicyId | String | ID of the newly created scheduled snapshot policy |
| NextTriggerTime | String | The time of first snapshot backup|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1. Creating a Scheduled Snapshot Policy

Create a scheduled snapshot policy. The cloud disk that is bound to the scheduled snapshot policy will create a snapshot every Friday at 00:00.

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=CreateAutoSnapshotPolicy
&AutoSnapshotPolicyName=backup_data_friday
&Policy.0.DayOfWeek.0=4
&Policy.0.Hour.0=0
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "AutoSnapshotPolicyId": "asp-1lebc9r3",
    "NextTriggerTime": "2018-08-08 16:00:00",
    "RequestId": "88d95732-c4e9-bd97-4a23-5a1f978d3b72"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=CreateAutoSnapshotPolicy)

### SDK

TencentCloud API 3.0 comes with SDKs that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/362/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| AutoSnapshotPolicyOutOfQuota | The number of scheduled snapshot policies has reached the limit. |
| InvalidParameterValue | Invalid parameter value. Parameter value is in an incorrect format or is not supported. |
| InvalidParameterValue.LimitExceeded | The number of parameter values exceeds the limit. |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |
