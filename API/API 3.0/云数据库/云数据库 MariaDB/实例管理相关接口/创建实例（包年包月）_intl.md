## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (CreateDBInstance) is used to create prepaid database instances by passing such information as instance specification, database version number, purchased usage period and quantity.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mariadb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: CreateDBInstance. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/237/16147#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Zones.N | Yes | Array of String | Availability zones for instance nodes. Up to two availability zones are allowed. If the shard specification is one master node with two salve nodes, two of these nodes are in the first availability zone. |
| NodeCount | Yes | Integer | Number of nodes, which can be obtained by querying the instance specification <br/>(DescribeDBInstanceSpecs) |
| Memory | Yes | Integer | Memory (in GB), which can be obtained by querying instance specification <br/>(DescribeDBInstanceSpecs). |
| Storage | Yes | Integer | Storage space (in GB). You can query the instance specification using DescribeDBInstanceSpecs<br/> to get the lower limit and upper limit of the disk for different memory sizes. |
| Period | No | Integer | Usage period to be purchased (in month) |
| Count | No | Integer | Quantity to be purchased. The price of one instance is queried by default. |
| AutoVoucher | No | Boolean | Indicates whether to use vouchers automatically. Vouchers are not used by default. |
| VoucherIds.N | No | Array of String | List of voucher IDs. Only one voucher is supported now. |
| VpcId | No | String | VPC ID. 0 or empty value means to create a basic network. |
| SubnetId | No | String | Subnet ID of VPC. It is required when VpcId is not 0. |
| ProjectId | No | Integer | Project ID, which can be obtained via "View Project List" API. If this parameter is left empty, the default project will be associated. |
| DbVersionId | No | String | Version of database engine. Version 10.0.10, 10.1.9 and 5.7.17 are available. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| DealName | String | Long order number. You can call DescribeOrders<br/> to query the order details, or make the payment by calling the relevant API of the user account if payment is failed. |
| InstanceIds | Array of String | List of instance IDs corresponding to the order. If there is no instance ID returned, you can call the API "Query Order". The API "Query Instance" can be used to see if the instance is created. |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Create a prepaid database instance

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=CreateDBInstance
&Zones.0=ap-guangzhou-2
&Zones.1=ap-guangzhou-2
&Memory=2000
&Storage=10000
&NodeCount=1
&Count=1
&Period=1
&AutoVoucher=true
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "DealName": "20171103110163",
    "InstanceIds": [
      "tdsql-avw0207d"
    ],
    "RequestId": "8c4fba95-01e4-61d9-4146-59fc5afdf962"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=CreateDBInstance)

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
| InternalError.CamAuthFailed | CAM authentication request failed |
| InternalError.GetSubnetFailed | Failed to query the information of VPC subnets |
| InternalError.GetVpcFailed | Failed to query the information of a VPC |
| InvalidParameter.GenericParameterError | Failed to pass the parameter validity verification |
| InvalidParameter.SubnetNotFound | Unable to find the specified VPC subnet |
| InvalidParameter.VpcNotFound | Unable to find the specified VPC |
| InvalidParameterValue.IllegalCount | Product quantity exceeds the limit |
| InvalidParameterValue.IllegalQuantity | Product quantity exceeds the limit |
| InvalidParameterValue.IllegalZone | No corresponding information of the availability zone was found |
| InvalidParameterValue.SpecIdIllegal | No specification of a database instance found |
| UnauthorizedOperation.PermissionDenied | No permission to perform operations on the API or resource |

