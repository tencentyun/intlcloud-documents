## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

* Only the project ID of elastic cloud disk can be modified. The project ID of non-elastic cloud disk is changed subjected to its associated CVM instance. You can query whether the cloud disk is an elastic cloud disk in the `Portable` field returned by API [DescribeDisks](/document/product/362/16315).
* Cloud disk name is a user-customized alias of a cloud disk for easier management. Tencent Cloud does not use this name for ticket submission or cloud disk management.
* Batch operations are supported. If multiple cloud disk IDs are specified, all the specified cloud disks will be changed to the same attribute. If there is a cloud disk that does not allow this operation, the operation is not performed and a specific error code is returned.

Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. Value​used in this API: ModifyDiskAttributes |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| DiskIds.N | Yes | Array of String | ID(s) of one or more cloud disks to be operated. If multiple cloud disk IDs are specified, all the specified cloud disks can only have the same attribute. |
| ProjectId | No | Integer | The new project ID of the cloud disk. Only the project ID of elastic cloud disk can be modified. The available projects and their IDs can be queried via the API [DescribeProject](/document/api/378/4400). |
| DiskName | No | String | The new cloud disk name. |
| Portable | No | Boolean | Whether it is an elastic cloud disk. FALSE: non-elastic cloud disk; TRUE: elastic cloud disk. You can only change a non-elastic cloud disk to an elastic cloud disks, but not vice versa. |
| DeleteWithInstance | No | Boolean | Whether to release the mounted cloud disk when the associated CVM instance is terminated. `TRUE`: release the cloud disk upon instance termination. `FALSE`: do not release the cloud disk upon instance termination. This is only supported for paly-as-you-go data cloud disks. |
| DiskType | No | String | The new cloud disk type. Value range: <br><li>CLOUD_PREMIUM: Premium cloud disk.  <br><li>CLOUD_SSD: SSD cloud disk. <br>Currently, batch operations are not supported for changing type. That is, when `DiskType` is passed, only one cloud disk can be specified in `DiskIds`. <br>When the cloud disk type is changed, the changing of other attributes is not supported concurrently. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1. Modifying the Name of a Cloud Disk

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=ModifyDiskAttributes
&DiskIds.0=disk-fyctkqsf
&DiskName=test_data_disk
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "bf84fb00-6949-c0f6-aea8-5a1f806401c2"
  }
}
```

### Sample 2. Modifying the Type of the Cloud Disk

Upgrade an HDD elastic cloud disk to a premium cloud disk.

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=ModifyDiskAttributes
&DiskIds.0=disk-hdz4c824
&DiskType=CLOUD_PREMIUM
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "d010c751-3edb-4388-878c-1de0891aa1fd"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=ModifyDiskAttributes)

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
| InternalError.ComponentError | The request failed because of a dependent component. Contact customer service to resolve the issue. |
| InvalidDisk.NotSupported | This operation is not supported for cloud disks. |
| InvalidDiskId.NotFound | The `DiskId` does not exist. |
| InvalidParameterValue | Invalid parameter value. Parameter value is in an incorrect format or is not supported. |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |
