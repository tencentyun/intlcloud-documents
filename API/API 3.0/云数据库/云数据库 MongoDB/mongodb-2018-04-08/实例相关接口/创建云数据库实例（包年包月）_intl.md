## 1. API Description

Domain name for API request: mongodb.tencentcloudapi.com.

This API (CreateDBInstance) is used to create a monthly subscription MongoDB database instance.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mongodb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/240/31800).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: CreateDBInstance. |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-08 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/240/31800#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| SecondaryNum | Yes | Integer | Number of slave nodes per replica set |
| Memory | Yes | Integer | Memory capacity of the instance (in GB) |
| Volume | Yes | Integer | Disk capacity of the instance (in GB) |
| MongoVersion | Yes | String | Version number. Only MONGO_3_WT is supported. |
| MachineCode | Yes | String | Server type. GIO: High IO; TGIO: High IO (10 GB). |
| GoodsNum | Yes | Integer | Number of instances. The default value is 1, minimum is 1, and maximum is 10. |
| Zone | Yes | String | Name of the region to which the instance belongs, e.g. ap-guangzhou-2. |
| TimeSpan | Yes | Integer | Purchased usage period (in month) |
| Password | Yes | String | Instance password |
| ProjectId | No | Integer | Project ID. If this is left empty, default project is used. |
| SecurityGroup.N | No | Array of String | Security group parameters |
| UniqVpcId | No | String | VPC ID. If it is left empty, the basic network is used by default. |
| UniqSubnetId | No | String | Subnet ID under VPC. If VpcId is set, SubnetId is required. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| DealId | String | Order ID |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Create a monthly subscription database instance

You need to create a monthly subscription database instance using an API.

#### Input example

```
https://mongodb.tencentcloudapi.com/?Action=CreateDBInstance
&Memory=4
&Volume=250
&GoodsNum=1
&Zone=ap-guangzhou-2
&UniqVpcId=vpc-0akbol5v
&UniqSubnetId=subnet-fyrtjbqw
&ProjectId=0
&MongoVersion=MONGO_3_WT
&MachineCode=TGIO
&SecondaryNum=2
&TimeSpan=1
&Password=pwd123456
&<Common request parameters>
```

#### Output example

```
{
    "Response": {
        "RequestId": "be8f4a30-ea2e-4623-8b6b-0ccce04cd9f7",
        "DealId": "19297475"
    }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mongodb&Version=2018-04-08&Action=CreateDBInstance)

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

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/240/31803#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameter | Invalid parameter |

