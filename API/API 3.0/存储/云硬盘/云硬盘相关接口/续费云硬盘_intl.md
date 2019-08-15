## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API (RenewDisk) is used to renew a cloud disk.

* Only prepaid (monthly subscription) cloud disks are supported. The type of the cloud disk can be queried using [DescribeDisks](/document/product/362/16315), and is specified in the DiskChargeType output parameter.
* You can renew a cloud disk together with the associated CVM instance. By specifying `CurInstanceDeadline` in [DiskChargePrepaid](/document/product/362/15669#DiskChargePrepaid) parameter, the cloud disk will be renewed according to the expiry time of the associated CVM.

Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: RenewDisk |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| DiskChargePrepaid | No | [DiskChargePrepaid](/document/api/362/15669#DiskChargePrepaid) | Specifies the billing information of monthly subscription cloud disks, including the validity period, auto-renewal status and more. <br>If you want to renew the cloud disk and its associated CVM instance together, please specify the parameter `CurInstanceDeadline`. In this case, the cloud disk will be renewed according to the expiration of the instance. |
| DiskId | Yes | String | ID of the cloud disk, which can be queried via the API [DescribeDisks](/document/product/362/16315). |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1. Renewing a Cloud Disk for One Month and Enabling Auto-Renewal

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=RenewDisk
&DiskId=disk-
&DiskChargePrepaid.Period=1
&DiskChargePrepaid.RenewFlag=NOTIFY_AND_AUTO_RENEW
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "6e2e5089-244a-4102-d347-5a1f8058b1db"
  }
}
```

### Sample 2. Renewing an instance together with the cloud disks mounted to it, making the cloud disk expiration time the same as that of the instance.

The current expiration time of the instance is: 2018-03-30 20:15:03, which needs to be renewed for one month. You can call this API to renew the prepaid cloud disk mounted on the instance to make its expiration time the same as that of the instance and enable the auto renewal for the cloud disk.

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=RenewDisk
&DiskId=disk-
&DiskChargePrepaid.Period=1
&DiskChargePrepaid.CurInstanceDeadline=2018-03-30 20:15:03
&DiskChargePrepaid.RenewFlag=NOTIFY_AND_AUTO_RENEW
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "55db49cf-b9d7-da27-825b-5a02ba6884ca",
    "DiskPrice": {
      "DiscountPrice": 9.0,
      "OriginalPrice": 9.0
    }
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=RenewDisk)

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
| InvalidDisk.NotPortable | Non-elastic cloud disks are not supported. |
| InvalidDiskId.NotFound | The `DiskId` does not exist. |
| InvalidParameterValue | Invalid parameter value. Parameter value is in an incorrect format or is not supported. |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |
