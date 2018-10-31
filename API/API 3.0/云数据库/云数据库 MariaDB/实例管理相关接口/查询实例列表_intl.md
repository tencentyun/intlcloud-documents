## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (DescribeDBInstances) is used to query the database instance list, and supports filtering instances by project ID, instance ID, private network address, and instance name.
If you do not specify any filter condition, 20 instance records will be returned by default. A maximum of 100 instance records will be returned for a single request.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mariadb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeDBInstances. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/237/16147#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceIds.N | No | Array of String | Queries according to one or more instance IDs, such as tdsql-ow728lmc. A maximum of 100 instances are allowed for each request. |
| SearchName | No | String | The field name for search. "instancename", "vip" and "all" are supported. The "instancename" means to search by instance names. The "vip" means to search by private IPs. The "all" means to search by instance IDs, instance names and private IPs. |
| SearchKey | No | String | The keyword for search. Fuzzy search is available. Multiple keywords are separated by the line break '\n'. |
| ProjectIds.N | No | Array of Integer | Queries by project IDs |
| IsFilterVpc | No | Boolean | Whether to search by VPC network |
| VpcId | No | String | VPC ID, valid when IsFilterVpc is 1. |
| SubnetId | No | String | VPC subnet ID, valid when IsFilterVpc is 1. |
| OrderBy | No | String | Sorting field (projectId, createtime or instancename) |
| OrderByType | No | String | Sorting type (desc or asc) |
| Offset | No | Integer | Offset. It is 0 by default. |
| Limit | No | Integer | Number of results to be returned. Default is 20. Maximum is 100. |
| OriginSerialIds.N | No | Array of String | Queries by OriginSerialId |
| IsFilterExcluster | No | Boolean | Identifies whether to use ExclusterType. False: Do not use the field; true: Use the field. |
| ExclusterType | No | Integer | 1: non-exclusive clusters; 2: exclusive clusters; 0: all clusters. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of instances that meet the condition |
| Instances | Array of [DBInstance](/document/api/237/16191#DBInstance) | Instance details list |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query the instance list based on the instance ID

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=DescribeDBInstances
&InstanceIds.0=tdsql-722d255z
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "Instances": [
      {
        "AppId": 1251006373,
        "AutoRenewFlag": 0,
        "CreateTime": "2018-04-24 21:40:59",
        "ExclusterId": "",
        "Id": 40964,
        "InstanceId": "tdsql-722d255z",
        "InstanceName": "tdsql-722d255z",
        "IsTmp": 0,
        "Memory": 2,
        "NodeCount": 2,
        "OriginSerialId": "set_1524577391_54095887",
        "PeriodEndTime": "2018-05-02 21:40:59",
        "Pid": 10890,
        "ProjectId": 0,
        "Qps": 2100,
        "Region": "ap-guangzhou",
        "Status": 2,
        "Storage": 30,
        "SubnetId": 45109,
        "TdsqlVersion": " is based on MariaDB 10.1.9 (compatible with MySQL 5.6)",
        "Uin": "20548499",
        "UniqueSubnetId": "subnet-6ffate6q",
        "UniqueVpcId": "vpc-5rkcp0wb",
        "UpdateTime": "2018-04-24 22:25:59",
        "Vip": "172.17.0.8",
        "VpcId": 75203,
        "Vport": 3306,
        "WanDomain": "",
        "WanPort": 0,
        "WanVip": "",
        "Zone": "ap-guangzhou-1"
      }
    ],
    "RequestId": "6838d283-fdd9-419c-aabe-df6ee5cf42a7",
    "TotalCount": 1
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=DescribeDBInstances)

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
| InternalError.CamAuthFailed | CAM authentication request failed |
| InternalError.DbOperationFailed | Failed to query the database |
| InternalError.FenceError | Failed to query exclusive cluster information |
| InvalidParameter.GenericParameterError | Failed to pass the parameter validity verification |
| InvalidParameterValue.IllegalExclusterID | No exclusive cluster of the database instance is found |
| InvalidParameterValue.SpecIdIllegal | No specification of a database instance found |
| UnauthorizedOperation.PermissionDenied | No permission to perform operations on the API or resource |

