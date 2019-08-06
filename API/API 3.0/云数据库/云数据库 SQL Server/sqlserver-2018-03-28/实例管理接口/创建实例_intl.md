## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (CreateDBInstances) creates an database instance.

API request rate limit: 20 requests/sec.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: CreateDBInstances |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Zone | Yes | String | Instance Availability Zone, such as ap-guangzhou-1 (Guangzhou Zone 1). Purchasable AZs for an instance can be obtained through the DescribeZones API |
| Memory | Yes | Integer | Instance memory size in GB |
| Storage | Yes | Integer | Instance storage capacity in GB |
| InstanceChargeType | No | String | Billing method. Valid values include PREPAID and POSTPAID |
| ProjectId | No | Integer | Project ID |
| GoodsNum | No | Integer | Number of instances purchased this time. 1 by default; up to 10 |
| SubnetId | No | String | VPC subnet ID in the format of subnet-bdoe83fa. SubnetId and VpcId should be set or ignored simultaneously |
| VpcId | No| String | VPC ID in the format of vpc-dsp338hz. SubnetId and VpcId should be set or ignored simultaneously |
| Period | No | Integer | Length of purchase of the instance. The default value is 1, indicating one month. The value cannot exceed 48 |
| AutoVoucher | No | Integer | Whether to automatically use vouchers. 0: no, 1: yes. No by default |
| VoucherIds.N | No | Array of String | Array of voucher IDs (currently, only one voucher can be used for one order) |
| DBVersion | No | String | Database version number. Valid values: 2012SP3 (SQL Server 2012), 2008R2 (SQL Server 2008 R2), and 2016SP1 (SQL Server 2016 SP1). The version purchasable varies by region and can be queried by calling the DescribeZones API. If this is left blank, 2008R2 is used by default |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| DealName | String | Order name |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1 Create an instance

#### Input Sample Code

```
https://sqlserver.tencentcloudapi.com/?Action=CreateDBInstances
&Zone=ap-guangzhou-1
&Memory=2
&Storage=100
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "4be5990d-a4b5-49dc-b2b4-e713b6aa7ba3",
    "DealName": "201806261980"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=CreateDBInstances)

### SDK

TencentCloud API 3.0 integrates SDKs that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/238/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.CreateOrderFailed | Failed to create the order. |
| FailedOperation.CreateOrderFailed | Failed to get VPC information. |
| InternalError.DBError | Database error. |
| InvalidParameter.InputIllegal | Invalid input. |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion error. |
| InvalidParameterValue.IllegalRegion | Invalid region. |
| InvalidParameterValue.IllegalSpec | Invalid instance specification information. |
| InvalidParameterValue.IllegalZone | Invalid AZ ID. |
| ResourceNotFound.VpcNotExist | The VPC does not exist. |
