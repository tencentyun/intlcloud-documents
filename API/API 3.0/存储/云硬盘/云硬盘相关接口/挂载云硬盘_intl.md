## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API (AttachDisks) is used to mount one or more cloud disks to one CVM instance.
 
* Batch operations are supported. You can multiple cloud disks to one CVM. If there is a cloud disk that does not allow this operation, the operation is not performed and a specific error code is returned.
* This API is an asynchronous API. If the request for mounting the cloud disk successfully returns results, the operation of mounting cloud disk has been initiated at the background. You can use the API [DescribeDisks](/document/product/362/16315) to query the cloud disk status. If the status changes from "ATTACHING" to "ATTACHED", the cloud disk is mounted.

Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. Value used in this API: AttachDisks |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| DiskIds.N | Yes | Array of String | ID of the elastic cloud disk to be mounted, which can be queried through the API [DescribeDisks](/document/product/362/16315). A maximum of 10 elastic cloud disks can be mounted in a single request. |
| InstanceId | Yes | String | ID of the CVM instance, which can be queried via the API [DescribeInstances](/document/product/213/15728). |
| DeleteWithInstance | No | Boolean | Indicates whether to release the cloud disk upon instance termination. If this is not specified, only the mount operation is executed. If `True` is passed, the cloud disk will be released when the instance is terminated. This is only valid for pay-as-you-go cloud disks. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1. Mounting a Cloud Disk

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=AttachDisks
&DiskIds.0=disk-lzrg2pwi
&InstanceId=ins-dyzmimrw
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "e0f140e5-14d6-c4a1-91e0-5a1f7f05a68a"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=AttachDisks)

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
| InternalError.ResourceOpFailed | The operation performed on the resource failed. For the specific error information, please see the Message field in the error description. Try again later or contact the customer service for help. |
| InvalidDisk.Attached | The cloud disk has been mounted. |
| InvalidDisk.NotPortable | Non-elastic cloud disks are not supported. |
| InvalidDisk.NotSupported | This operation is not supported for cloud disks. |
| InvalidDisk.TypeError | Invalid cloud disk type |
| InvalidDiskId.NotFound | The `DiskId` does not exist. |
| InvalidInstance.NotSupported | cloud disks cannot be mounted to the CVM. |
| InvalidInstanceId.NotFound | The `InstanceId` of the instance does not exist. |
| InvalidParameterValue | Invalid parameter value. Parameter value is in an incorrect format or is not supported. |
| InvalidParameterValue.LimitExceeded | The number of parameter values exceeds the limit. |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |
| ZoneNotMatch | The cloud disk and the instance are not in the same availability zone. |
