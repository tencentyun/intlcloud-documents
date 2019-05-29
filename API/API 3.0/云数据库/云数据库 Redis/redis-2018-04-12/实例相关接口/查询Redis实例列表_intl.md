## 1. API Description

API domain name: redis.tencentcloudapi.com.

Query the list of Redis instances

Default API request rate limit: 20 requests/sec.

Note: This API supports financial availability zones. As financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), it is necessary to specify a domain name with the financial availability zone too, preferably in the same region as specified in Region, such as redis.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/239/20005).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeInstances |
| Version | Yes | String | Common parameter; the value for this API: 2018-04-12 |
| Region | Yes | String | Common parameters; for details, see the [List of Regions](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Limit | No | Integer | Instance list size; 20 by default |
| Offset | No | Integer | Offset, which is an integral multiple of Limit |
| InstanceId | No | String | Instance ID, such as crs-6ubhgouj |
| OrderBy | No | String | Enumeration range: projectId,createtime,instancename,type,curDeadline |
| OrderType | No | Integer | 1: reverse; 0: sequential; reverse by default |
| VpcIds.N | No | Array of String | Array of VPC IDs such as 47525. The array subscript starts from 0. If this parameter is not passed in, the basic network is selected by default |
| SubnetIds.N | No | Array of String | Array of subnet IDs such as 56854. The array subscript starts from 0 |
| ProjectIds.N | No | Array of Integer | Array of project IDs. The array subscript starts from 0 |
| SearchKey | No | String | ID of the instance to be searched for. |
| InstanceName | No | String | Instance name |
| UniqVpcIds.N | No | Array of String | Array of VPC IDs such as vpc-sad23jfdfk. The array subscript starts from 0. If this parameter is not passed in, the basic network is selected by default |
| UniqSubnetIds.N | No | Array of String | Array of subnet IDs such as subnet-fdj24n34j2. The array subscript starts from 0 |
| RegionIds.N | No | Array of Integer | Region ID, which has already been obsoleted. The corresponding region can be queried through the common parameter Region |
| Status.N | No | Array of Integer | Instance status. 0: to be initialized; 1: in process; 2: running; -2: isolated; -3: to be deleted |
| TypeVersion | No | Integer | Type edition. 1: standalone edition; 2: master-slave edition; 3: cluster edition |
| EngineName | No | String | Engine information: Redis-2.8, Redis-4.0, CKV |
| AutoRenew.N | No | Array of Integer | Renewal mode. 0: default status (manual renewal); 1: auto-renewal; 2: auto-renewal clearly banned |
| BillingMode | No | String | Billing method. postpaid: pay-as-you-go; prepaid: prepaid |
| Type | No | Integer | Instance type. 1: legacy Redis cluster edition; 2: Redis 2.8 master-slave edition; 3: CKV master-slave edition; 4: CKV cluster edition; 5: Redis 2.8 standalone edition; 7: Redis 4.0 cluster edition |
| SearchKeys.N | No | Array of String | Search keyword, which can be instance ID, instance name, or complete IP |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of instances |
| InstanceSet | Array of [InstanceSet](/document/api/239/20022#InstanceSet) | List of instance details |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided during troubleshooting. |

## 4. Sample

### Sample 1. Request Example

#### Input Sample Code

```
https://redis.tencentcloudapi.com/?Action=DescribeInstances
&Offset=0&Limit=1
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "InstanceSet": [
      {
        "Appid": 1251006373,
        "AutoRenewFlag": 0,
        "BillingMode": 0,
        "CloseTime": "0000-00-00 00:00:00",
        "Createtime": "0000-00-00 00:00:00",
        "DeadlineTime": "0000-00-00 00:00:00",
        "Engine": "Redis community edition",
        "InstanceId": "crs-7ponppu3",
        "InstanceName": "crs-7ponppu3",
        "InstanceNode": [],
        "InstanceTags": [
          {
            "TagKey": "aaa",
            "TagValue": "111"
          }
        ],
        "InstanceTitle": "Instance running",
        "OfflineTime": "",
        "Port": 6379,
        "PriceId": 13380,
        "ProductType": "Redis4.0 cluster edition",
        "ProjectId": 0,
        "RedisReplicasNum": 1,
        "RedisShardNum": 3,
        "RedisShardSize": 1024,
        "RegionId": 1,
        "Size": 3072,
        "SizeUsed": 0,
        "SlaveReadWeight": 0,
        "Status": 2,
        "SubStatus": 19,
        "SubnetId": 0,
        "Tags": [],
        "Type": 7,
        "UniqSubnetId": "",
        "UniqVpcId": "",
        "VpcId": 0,
        "WanIp": "10.66.153.160",
        "ZoneId": 100002
      }
    ],
    "RequestId": "e3d683fc-f2ff-43c9-980d-fae7a1166abc",
    "TotalCount": 1
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeInstances)

### SDK

TencentCloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/239/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.DbOperationFailed | Internal system error with the DB operation, which may be update, insert, select, etc. |
| InvalidParameter | Parameter error |
| InvalidParameter.EmptyParam | Parameter is empty. |
| InvalidParameter.InvalidParameter | Business parameter error. |
| InvalidParameter.PermissionDenied | The API has no CAM permissions. |
| UnauthorizedOperation.NoCAMAuthed | No CAM permissions. |
