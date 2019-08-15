## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API (InquiryPriceResizeDisk) is used to query the price for expanding the capacity of a cloud disk.

* Only monthly subscription cloud disks are supported for this API.

Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: InquiryPriceResizeDisk |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| DiskId | Yes | String | ID of the cloud disk, which can be queried via the API [DescribeDisks](/document/product/362/16315). |
| DiskSize | Yes | Integer | The desired cloud disk capacity (in GB). It cannot be smaller than the current size of the cloud disk. For the value range of the cloud disk sizes, see cloud disk [Product Types](/document/product/362/2353). |
| ProjectId | No | Integer | ID of the project to which the cloud disk belongs. This parameter is only used for authentication. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| DiskPrice | [Price](/document/api/362/15669#Price) | Indicates the price for expanding capacity for the cloud disk |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1. Querying the Price for Expanding the Capacity of a Cloud Disk to 200 GB

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=InquiryPriceResizeDisk
&DiskId=disk-dw0bbzws
&DiskSize=200
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "DiskPrice": {
      "DiscountPrice": 210.09,
      "OriginalPrice": 210.09
    },
    "RequestId": "2ba7b520-ddb4-f5ea-34d1-5a1f80434911"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=InquiryPriceResizeDisk)

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
| InvalidDisk.Expire | The cloud disk has expired. |
| InvalidDisk.NotPortable | Non-elastic cloud disks are not supported. |
| InvalidInstanceId.NotFound | The `InstanceId` of the instance does not exist. |
| InvalidParameterValue | Invalid parameter value. Parameter value is in an incorrect format or is not supported. |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |
