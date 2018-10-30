## 1. API Description

Domain name for API request: sqlserver.tencentcloudapi.com

This API (CreateDBInstances) is used to create an instance.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: sqlserver.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/238/19930).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: CreateDBInstances |
| Version | Yes | String | Common parameter. The value used for this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Zone | Yes | String | Availability zone of instance, such as ap-guangzhou-1 (Guangzhou Zone 1). You can obtain the availability zones of an instance via the API DescribeZones. |
| Memory | Yes | Integer | Memory capacity of the instance (in GB) |
| Storage | Yes | Integer | Disk capacity of the instance (in GB) |
| InstanceChargeType | No | String | Billing method (optional). Only PREPAID (default) is supported. |
| ProjectId | No | Integer | Project ID |
| GoodsNum | No | Integer | The number of instances purchased this time. It defaults to 1. Maximum is 10. |
| SubnetId | No | String | Subnet ID of VPC, such as subnet-bdoe83fa. SubnetId should be set in conjunction with VpcId. |
| VpcId | No | String | Network ID of VPC, such as vpc-dsp338hz. VpcId should be set in conjunction with SubnetId. |
| Period | No | Integer | Purchased validity period of the instance. It defaults to 1 (1 month). The maximum is 48. |
| AutoVoucher | No | Integer | Indicates whether to use vouchers automatically. 1: Yes; 0: No (default) |
| VoucherIds.N | No | Array of String | Array of voucher IDs. Only one voucher can be used for a single order. |
| DBVersion | No | String | Database version. Supported values include 2012SP3 (SQL Server 2012), 2008R2 (SQL Server 2008 R2), and 2016SP1 (SQL Server 2016 SP1). The supported version may vary with different regions and can be queried via the API DescribeZones. It defaults to 2008R2 if left empty. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| DealName | String | Order name |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Create an instance

#### Input example

```
https://sqlserver.tencentcloudapi.com/?Action=CreateDBInstances
&Zone=ap-guangzhou-1
&Memory=2
&Storage=100
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "DealName": "201806261980",
    "RequestId": "4be5990d-a4b5-49dc-b2b4-e713b6aa7ba3"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=CreateDBInstances)

### SDK

Cloud API 3.0 comes with the software development kit (SDK) that supports multiple programming languages and makes it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](/document/api/238/19932#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.CreateOrderFailed | Failed to create the order |
| FailedOperation.GetVpcFailed | Failed to obtain the VPC information |
| InternalError.DBError | Database error |
| InvalidParameter.InputIllegal | Invalid input parameter |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion failed. |
| InvalidParameterValue.IllegalRegion | Invalid region |
| InvalidParameterValue.IllegalSpec | Invalid instance specification |
| InvalidParameterValue.IllegalZone | Invalid availability zone ID |
| ResourceNotFound.VpcNotExist | The VPC does not exist |

