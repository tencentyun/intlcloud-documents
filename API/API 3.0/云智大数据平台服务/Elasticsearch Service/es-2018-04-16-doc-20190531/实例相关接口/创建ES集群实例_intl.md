## 1. API Description

API domain name: es.tencentcloudapi.com.

This API creates an ES cluster instance with the specified specification.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if a financial region, such as ap-shanghai-fsi, is assigned to the common parameter Region, we recommend you include that financial region in your domain name  , such as es.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/845/30623).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: CreateInstance |
| Version | Yes | String | Common parameter. The version of this API: 2018-04-16 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/845/30623#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Zone | Yes | String | Availability zone |
| NodeNum | Yes | Integer | Number of nodes (2-50) |
| EsVersion | Yes | String | Instance version ("5.6.4" or "6.4.3") |
| NodeType | Yes | String | Node specification <li>ES.S1.SMALL2: 1-core 2 GB </li><li>ES.S1.MEDIUM4: 2-core 4 GB </li><li>ES.S1.MEDIUM8: 2-core 8 GB </li><li>ES.S1.LARGE16: 4-core 16 GB </li><li>ES.S1.2XLARGE32: 8-core 32 GB </li><li>ES.S1.4XLARGE32: 16-core 32 GB </li><li>ES.S1.4XLARGE64: 16-core 64 GB </li> |
| DiskSize | Yes | Integer | Node disk size in GB |
| VpcId | Yes | String | VPC ID |
| SubnetId | Yes | String | Subnet ID |
| Password | Yes | String | Access password, which must contain 8 to 16 characters, including at least two out of the following three types of characters: [a-z,A-Z], [0-9] and [-!@#$%&^*+=_:;,.?] |
| InstanceName | No | String | Instance name, which can contain 1 to 50 English letters, Chinese characters, digits, dashes - or underscores _ |
| ChargeType | No | String | Billing method <li>PREPAID: Monthly subscription </li><li>POSTPAID_BY_HOUR: Pay-as-you-go on an hourly basis </li>POSTPAID_BY_HOUR by default |
| ChargePeriod | No | Integer | Purchased duration for monthly subscription (in the unit determined by the TimeUint parameter) |
| RenewFlag | Yes | String | Auto-renewal flag <li>RENEW_FLAG_AUTO: Auto-renewal enabled </li><li>RENEW_FLAG_MANUAL: Auto-renewal disabled </li>This parameter has to be set if ChargeType is PREPAID. If it is not passed in, auto-renewal is disabled for regular users and enabled for SVIP users by default |
| DiskType | No | String | Node disk type <li>CLOUD_SSD: SSD cloud disk </li><li>CLOUD_PREMIUM: Premium cloud disk </li>CLOUD_SSD by default |
| TimeUnit | No | String | Billing duration unit, which has to be set if ChargeType is PREPAID. The default value is "m" (month), and only "m" is supported currently |
| AutoVoucher | No | Integer | Whether to automatically use vouchers <li>0: No </li><li>1: Yes </li>0 by default |
| VoucherIds.N | No | Array of String | List of voucher IDs (currently, only one voucher can be specified at a time) |
| EnableDedicatedMaster | No | Boolean | Whether to create a dedicated master node <li>true: Yes </li><li>false: No </li>false by default |
| MasterNodeNum | No | Integer | Number of dedicated master nodes (only 3 and 5 are supported. This value must be passed in if EnableDedicatedMaster is true) |
| MasterNodeType | No | String | Dedicated master node type, which must be passed in if EnableDedicatedMaster is true <li>ES.S1.SMALL2: 1-core 2 GB</li><li>ES.S1.MEDIUM4: 2-core 4 GB</li><li>ES.S1.MEDIUM8: 2-core 8 GB</li><li>ES.S1.LARGE16: 4-core 16 GB</li><li>ES.S1.2XLARGE32: 8-core 32 GB</li><li>ES.S1.4XLARGE32: 16-core 32 GB</li><li>ES.S1.4XLARGE64: 16-core 64 GB</li> |
| MasterNodeDiskSize | No | Integer | Dedicated master node disk size in GB, which is optional. If passed in, it can only be 50 and cannot be customized currently |
| ClusterNameInConf | No| String | ClusterName in the cluster configuration file, which is the instance ID by default and cannot be customized currently |
| DeployMode | No | Integer | Cluster deployment mode <li>0: Single-AZ deployment </li><li>1: Multi-AZ deployment </li>0 by default |
| MultiZoneInfo.N | No | Array of [MultiZoneInfo](/document/api/845/30634#MultiZoneInfo) | Details of AZs in multi-AZ deployment mode, which has to be passed in if DeployMode is 1 |
| LicenseType | No | String | License type <li>oss: Open Source Edition </li><li>basic: Basic Edition </li><li>platinum: Platinum Edition </li>platinum by default |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| InstanceId | String | Instance ID |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Examples

### Example 1. Creating an ES Cluster Instance

Create an ES cluster instance based on the input parameters

#### Input Sample Code

```
https://es.tencentcloudapi.com/?Action=CreateInstance?
InstanceName=es_test
&Zone=ap-guangzhou-2
&NodeNum=2
&EsVersion=5.6.4
&ChargeType=PREPAID
&ChargePeriod=1
&NodeType=ES.S1.SMALL2
&DiskSize=100
&VpcId=vpc-63g206gx
&SubnetId=subnet-ap0jf4gg
&Password=elastic_123
&EnableDedicatedMaster=true
&MasterNodeNum=3
&MasterNodeType=ES.S1.SMALL2
&MasterNodeDiskSize=50
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "InstanceId": "es-qlpn5o2a",
    "RequestId": "d7b76d5e-ad7d-4abd-b3b2-43b96dd08d16"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=es&Version=2018-04-16&Action=CreateInstance)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/845/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.NoPayment | No credit card or PayPal account is bound to the current account. Unable to make a payment. |
| InternalError | Internal error. |
| InvalidParameter | Incorrect parameter. |
| ResourceInUse | Resource is occupied. |
| ResourceInsufficient | Insufficient resource. |
| ResourceInsufficient.Balance | Insufficient account balance. |
