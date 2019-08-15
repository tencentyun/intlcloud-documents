## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API (ApplySnapshot) is used to roll back a cloud disk to a previous version using snapshot.

* The snapshot can only be rolled back to the original cloud disk. If you want to duplicate data on a data disk snapshots to other cloud disks, please use the API [CreateDisks](/document/product/362/16312) to create one or more elastic cloud disks and then copy the snapshot data to the created cloud disks. 
* The snapshot for rollback must be in NORMAL status. The snapshot status can be queried in the SnapshotState field in the output parameter of API [DescribeSnapshots](/document/product/362/15647).
* For elastic cloud disks, the cloud disk must be in UNMOUNTED status. You can check the status in the `Attached` filed returned by API [DescribeDisks](/document/product/362/16315). For non-elastic cloud disks purchased together with instances, the instance must be in SHUTDOWN status. You can check the status using API [DescribeInstancesStatus](/document/product/213/15738).

Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. Value​used in this API: ApplySnapshot |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| SnapshotId | Yes | String | Snapshot ID, which can be queried via [DescribeSnapshots](/document/product/362/15647). |
| DiskId | Yes | String | ID of the original cloud disk corresponding to the snapshot, which can be queried via the API [DescribeDisks](/document/product/362/16315). |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1. Creating a Snapshot

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=ApplySnapshot
&DiskId=disk-lzrg2pwi
&SnapshotId=snap-gybrif0z
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "cc96242e-566c-ae6a-b74a-5a1f823683b2"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=ApplySnapshot)

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
| InvalidDisk.Busy | The cloud disk is busy. Try again later. |
| InvalidDisk.NotSupported | This operation is not supported for cloud disks. |
| InvalidDisk.SnapshotCreating | A snapshot is being created for the cloud disk. Try again later. |
| InvalidDiskId.NotFound | The `DiskId` does not exist. |
| InvalidInstanceId.NotFound | The `InstanceId` of the instance does not exist. |
| InvalidParameter.DiskSizeNotMatch | The size of the cloud disk does not match the snapshot size. |
| InvalidParameterValue | Invalid parameter value. Parameter value is in an incorrect format or is not supported. |
| InvalidSnapshot.NotSupported | This operation is not supported for the snapshot. |
| InvalidSnapshotId.NotFound | The `SnapshotId` does not exist. |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |
| ResourceBusy | The resource is busy. Try again later. |
