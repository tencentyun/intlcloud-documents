## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API (DescribeInstancesDiskNum) is used to query the number of cloud disks mounted to the specified instances.

* Batch operations are supported. If multiple CVM instance IDs are specified, the returned results will list the number of cloud disks mounted on each CVM.

Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. Value used in this API: DescribeInstancesDiskNum |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceIds.N | Yes | Array of String | CVM instance ID, which can be queried via the API [DescribeInstances](/document/product/213/15728) |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| AttachDetail | Array of [AttachDetail](/document/api/362/15669#AttachDetail) | The number of mounted and mountable elastic cloud disks of each Cloud Virtual Machine.|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1. Querying the Number of Mounted Cloud Disks of Multiple Instances

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=DescribeInstancesDiskNum
&InstanceIds.0=ins-9w5d2buw
&InstanceIds.1=ins-jw0vit58
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "AttachDetail": [
      {
        "InstanceId": "ins-9w5d2buw",
        "AttachedDiskCount": 1,
        "MaxAttachCount": 10
      },
      {
        "InstanceId": "ins-jw0vit58",
        "AttachedDiskCount": 2,
        "MaxAttachCount": 10
      }
    ],
    "RequestId": "55db49cf-b9d7-da27-825b-5a02ba6884ca"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=DescribeInstancesDiskNum)

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
| InvalidDisk.NotPortable | Non-elastic cloud disks are not supported. |
| InvalidDiskId.NotFound | The `DiskId` does not exist. |
| InvalidParameterValue | Invalid parameter value. Parameter value is in an incorrect format or is not supported. |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |
