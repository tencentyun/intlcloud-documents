## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API (CreateSnapshot) is used to create a snapshot of a specified cloud disk.

* Snapshot is only supported by certain cloud disks. To check whether a cloud disk is available for creating snapshots, see the SnapshotAbility field returned by the API [DescribeDisks](/document/product/362/16315).
* For the number of snapshots that can be created, please see [Use Limits](https://cloud.tencent.com/doc/product/362/5145).

Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: CreateSnapshot |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| DiskId | Yes | String | ID of the cloud disk, for which a snapshot needs to be created. It can be queried via the API [DescribeDisks](/document/product/362/16315). |
| SnapshotName | No | String | Snapshot name. If it is left empty, the default is "not named". |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| SnapshotId | String | The ID of the newly created snapshot. |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1. Creating a Snapshot

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=CreateSnapshot
&DiskId=disk-lzrg2pwi
&SnapshotName=snap_201711301015
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "SnapshotId": "snap-gybrif0z",
    "RequestId": "1bd35eca-0c9a-6e0b-938a-5a1f80511c19"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=CreateSnapshot)

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
| InsufficientSnapshotQuota | The snapshot quota is insufficient. |
| InvalidAccount.InsufficientBalance | Insufficient account balance. |
| InvalidDisk.Busy | The cloud disk is busy. Try again later. |
| InvalidDisk.NotSupportSnapshot | The cloud disk does not have the snapshot capability. |
| InvalidDisk.NotSupported | This operation is not supported for cloud disks. |
| InvalidDisk.SnapshotCreating | A snapshot is being created for the cloud disk. Try again later. |
| InvalidDisk.TypeError | Invalid cloud disk type |
| InvalidDiskId.NotFound | The `DiskId` does not exist. |
| LimitExceeded.InstanceAttachedDisk | The number of disks mounted to the instance exceeds the limit. |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |
| ResourceBusy | The resource is busy. Try again later. |
| ResourceInsufficient.OverQuota | The quota is insufficient. |
| ResourceUnavailable.TooManyCreatingSnapshot | There are currently too many snapshots being created across the network. |
| UnsupportedOperation.DiskEncrypt | The disk is encrypted. |
