## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (UpgradeDBInstance) is used to expand the capacity of a database instance. This API completes two actions of placing an order and making payments. If there is an error during the payment, you can call the API PayDeals in the relevant APIs of your account to pay again.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mariadb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: UpgradeDBInstance. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/237/16147#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID to be upgraded, such as tdsql-ow728lmc. It can be obtained by querying instance details via DescribeDBInstances. |
| Memory | Yes | Integer | Memory (in GB), which can be obtained by querying instance specification <br/>(DescribeDBInstanceSpecs). |
| Storage | Yes | Integer | Storage space (in GB). You can query the instance specification using DescribeDBInstanceSpecs<br/> to get the lower limit and upper limit of the disk for different memory sizes. |
| AutoVoucher | No | Boolean | Indicates whether to use vouchers automatically. Vouchers are not used by default. |
| VoucherIds.N | No | Array of String | List of voucher IDs. Only one voucher is supported now. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| DealName | String | Long order number. You can call DescribeOrders<br/> to query the order details, or make the payment by calling the relevant API of the user account if payment is failed. |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Expand the capacity of a database instance

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=UpgradeDBInstance
&InstanceId=tdsql-avw0207d
&Memory=2000
&Storage=20000
&AutoVoucher=true
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "DealName": "20171103110035",
    "RequestId": "9b59ee51-0e13-1c2f-dedb-59fabe9d7f4a"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=UpgradeDBInstance)

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

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](/document/api/237/16149#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.CreateOrderFailed | Failed to create the order |
| FailedOperation.PayFailed | Failed to pay the order |
| InternalError.DbOperationFailed | Failed to query the database |
| InvalidParameterValue.SpecIdIllegal | No specification of a database instance found |
| ResourceNotFound.NoInstanceFound | The specified database instance is not found |
| ResourceUnavailable.InstanceStatusAbnormal | The database instance is in an invalid status and cannot be operated |

