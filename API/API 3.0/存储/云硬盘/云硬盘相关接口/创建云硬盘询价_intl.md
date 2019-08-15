## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API (InquiryPriceCreateDisks) is used to query the price for creating one or more cloud disks.

* You can query the price for creating multiple cloud disks. In this case, the total price for the creation is returned.

Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: InquiryPriceCreateDisks |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| DiskType | Yes | String | Type of cloud disk. Value range: <br><li>HDD cloud storage: CLOUD_BASIC <br><li>Premium cloud storage: CLOUD_PREMIUM <br><li>SSD cloud storage: CLOUD_SSD |
| DiskSize | Yes | Integer | Cloud disk size (in GB). For the value range of the cloud disk sizes, see cloud disk [Product Types](/document/product/362/2353). |
| DiskChargeType | Yes | String | Cloud disk billing method. <br><li>PREPAID: Prepaid, that is, monthly subscription<br><li>POSTPAID_BY_HOUR: Postpaid by hour (pay-as-you-go). |
| DiskChargePrepaid | No | [DiskChargePrepaid](/document/api/362/15669#DiskChargePrepaid) | Specifies the billing information of monthly subscription cloud disks, including the validity period, auto-renewal status and more. <br>This parameter is required for monthly subscription cloud disks. Ignore this parameter if you want to create pay-as-you-go cloud disks. |
| DiskCount | No | Integer | The number of purchased cloud disks. If it is left empty, the default is 1. |
| ProjectId | No | Integer | ID of the project to which the cloud disk belongs |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| DiskPrice | [Price](/document/api/362/15669#Price) | This parameter indicates the price of the purchased cloud disk. |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1. Querying the Price for Purchasing an HDD Cloud Disk (50 GB) for 6 Months

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=InquiryPriceCreateDisks
&DiskType=CLOUD_BASIC
&DiskSize=50
&DiskChargeType=PREPAID
&DiskChargePrepaid.Period=6
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "55db49cf-b9d7-da27-825b-5a02ba6884ca",
    "DiskPrice": {
      "DiscountPrice": 79.2,
      "UnitPrice": null,
      "OriginalPrice": 90.0,
      "ChargeUnit": null
    }
  }
}
```

### Sample 2. Querying the Price for Purchasing a Pay-as-you-go Cloud Disk

Query the price for purchasing a pay-as-you-go premium cloud disk with a size of 100 GB.

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=InquiryPriceCreateDisks
&DiskType=CLOUD_PREMIUM
&DiskSize=100
&DiskCount=1
&DiskChargeType=POSTPAID_BY_HOUR
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "55db49cf-b9d7-da27-825b-5a02ba6884ca",
    "DiskPrice": {
      "DiscountPrice": null,
      "UnitPrice": 0.021,
      "OriginalPrice": null,
      "ChargeUnit": "HOUR"
    }
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=InquiryPriceCreateDisks)

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
| InvalidParameterValue | Invalid parameter value. Parameter value is in an incorrect format or is not supported. |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |
