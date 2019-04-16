## 1. API Description

Domain name for API request: mongodb.tencentcloudapi.com.

This API (CreateDBInstanceHour) is used to create pay-as-you-go MongoDB database instances (including master instances, disaster recovery instances and read-only instances) by passing such information as instance specification, instance type, MongoDB version, purchased usage period and quantity.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mongodb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/240/31800).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: CreateDBInstanceHour. |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-08 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/240/31800#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Memory | Yes | Integer | Memory capacity of the instance (in GB) |
| Volume | Yes | Integer | Disk capacity of the instance (in GB) |
| ReplicateSetNum | Yes | Integer | Number of replica sets. The value of 1 refers to a single replica set instance. A value greater than 1 refers to a sharding cluster instance. The value shall not be greater than 10. |
| SecondaryNum | Yes | Integer | Number of slave nodes per replica set. Only 2 is supported now. |
| EngineVersion | Yes | String | MongoDB engine version. Supported values include: MONGO_2, MONGO_3_MMAP, MONGO_3_WT, MONGO_3_ROCKS, and MONGO_36_WT. |
| Machine | Yes | String | Instance type. GIO: High IO; TGIO: High IO (10 GB). |
| GoodsNum | Yes | Integer | Number of instances. The default value is 1, minimum is 1, and maximum is 10. |
| Zone | Yes | String | Availability zone information, such as ap-guangzhou-2. |
| InstanceRole | Yes | String | Instance role. Supported values include: MASTER - Master instance; DR - Disaster recovery instance; RO - Read-only instance. |
| InstanceType | Yes | String | Instance type. REPLSET - Replica set; SHARD - Sharding cluster. |
| Encrypt | No | Integer | Indicates whether to encrypt the data. Only when the engine version is MONGO_3_ROCKS can you choose to encrypt the data. |
| VpcId | No | String | VPC ID. If it is left empty, the basic network is used by default. |
| SubnetId | No | String | Subnet ID under VPC. If VpcId is set, SubnetId is required. |
| ProjectId | No | Integer | Project ID. If this is left empty, default project is used. |
| SecurityGroup.N | No | Array of String | Security group parameters |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| DealId | String | Order ID |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Create a database instance (pay-as-you-go)

You need to create a pay-as-you-go database instance using an API.

#### Input example

```
https://mongodb.tencentcloudapi.com/?Action=CreateDBInstanceHour
&Memory=4
&Volume=250
&ReplicateSetNum=1
&SecondaryNum=2
&EngineVersion=MONGO_3_WT
&Machine=TGIO
&GoodsNum=1
&Zone=ap-guangzhou-3
&InstanceRole=MASTER
&InstanceType=REPLSET
&<Common request parameters>
```

#### Output example

```
{
    "Response": {
        "RequestId": "d3aecf52-5abf-49e4-bf79-1a6c47a406d4",
        "DealId": "28920"
    }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mongodb&Version=2018-04-08&Action=CreateDBInstanceHour)

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

There is no error code related to the API business logic. For other error codes, see [Common Error Codes](/document/api/240/31803#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

