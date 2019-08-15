## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API (BindAutoSnapshotPolicy) is used to bind the cloud disk to the specified scheduled snapshot policy.

* For the scheduled snapshot policy limit of each region, see [Scheduled Snapshots](/document/product/362/8191).
* Scheduled snapshots are not created when the cloud disk bound to an scheduled snapshot policy is not in used (that is, an elastic cloud disk is not mounted to a CVM instance, or the associated instance of an non-elastic disk is shut down) .

Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: BindAutoSnapshotPolicy |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoSnapshotPolicyId | Yes | String | ID of the scheduled snapshot policy to bind |
| DiskIds.N | Yes | Array of String | IDs of the cloud disks to bind. Up to 80 cloud disks can be bound in one time. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1 Binding an Automated Snapshot Policy to a Single Disk

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=BindAutoSnapshotPolicy
&AutoSnapshotPolicyId=asp-mrsrn243
&DiskIds.0=disk-dw0bbzws
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "bda8bd1a-754d-d71b-8300-5a1fa45c237f"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=BindAutoSnapshotPolicy)

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
| InvalidAutoSnapshotPolicyId.NotFound | The `AutoSnapshotPolicyId` that was entered does not exist. |
| InvalidDisk.AlreadyBound | The cloud disk is already bound to a scheduled snapshot policy. |
| InvalidDisk.NotSupported | This operation is not supported for cloud disks. |
| InvalidDiskId.NotFound | The `DiskId` does not exist. |
| InvalidParameterValue | Invalid parameter value. Parameter value is in an incorrect format or is not supported. |
| InvalidParameterValue.BindDiskLimitExceeded | The number of tags bound to the disk exceeds the limit. |
| InvalidParameterValue.LimitExceeded | The number of parameter values exceeds the limit. |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |
