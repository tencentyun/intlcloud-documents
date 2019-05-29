## 1. API Description

API domain name: redis.tencentcloudapi.com.

Create a Redis instance

Default API request rate limit: 20 requests/sec.

Note: This API supports financial availability zones. As financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), it is necessary to specify a domain name with the financial availability zone too, preferably in the same region as specified in Region, such as redis.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/239/20005).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: CreateInstances |
| Version | Yes | String | Common parameter; the value for this API: 2018-04-12 |
| Region | Yes | String | Common parameters; for details, see the [List of Regions](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| ZoneId | Yes | Integer | ID of the availability zone where the instance resides |
| TypeId | Yes | Integer | Instance type. 2: Redis 2.8 master-slave edition; 3: Redis 3.2 master-slave edition (CKV master-slave edition); 4: Redis 3.2 cluster edition (CKV cluster edition); 5: Redis 2.8 standalone edition; 7: Redis 4.0 cluster edition |
| MemSize | Yes | Integer | Instance capacity in MB. The actual value is subject to the specifications returned by the capacity specifications querying API |
| GoodsNum | Yes | Integer | Number of instances. The actual quantity purchasable at a time is subject to the specifications returned by the capacity specifications querying API |
| Period | Yes | Integer | Length of purchase in months, which needs to be entered when creating a prepaid instances. Value range: [1,2,3,4,5,6,7,8,9,10,11,12,24,36]. For pay-as-you-go instances, enter 1 |
| Password | Yes | String | Instance password. Rules: 1. It can contain 8-16 character; 2. It must contain at least two of the following three types of characters: letters, numbers, and special characters !@^*() |
| BillingMode | Yes | Integer | Billing method. 0 : pay-as-you-go; 1: prepaid |
| VpcId | No | String | VPC ID such as vpc-sad23jfdfk. If this parameter is not passed in, the basic network is selected by default. This can be queried through the VPC list |
| SubnetId | No | String | In a basic network, subnetId is invalid. In a VPC subnet, the value is the subnet ID, such as subnet-fdj24n34j2 |
| ProjectId | No | Integer | Project ID. The value is subject to the projectId returned by user account > user account-related querying APIs > project list |
| AutoRenew | No | Integer | Auto-renewal flag. 0: default status (manual renewal); 1: auto-renewal; 2: auto-renewal clearly banned |
| SecurityGroupIdList.N | No | Array of String | Array of security group IDs |
| VPort | No | Integer | User-defined port. If left blank, 6379 |
| RedisShardNum | No | Integer | Number of instance shards. This can be left blank for Redis 2.8 master-slave edition, CKV master-slave edition, or Redis 2.8 standalone edition |
| RedisReplicasNum | No | Integer | Number of instance replicas. This can be left blank for Redis 2.8 master-slave edition, CKV master-slave edition, or Redis 2.8 standalone edition |
| ReplicasReadonly | No | Boolean | Whether to support read-only replicas. This can be left blank for Redis 2.8 master-slave edition, CKV master-slave edition, or Redis 2.8 standalone edition |
| InstanceName | No | String | Instance name |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| DealId | String | Deal ID |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided during troubleshooting. |

## 4. Sample

### Sample 1. Request Example

#### Input Sample Code

```
https://redis.tencentcloudapi.com/?Action=CreateInstances
&ZoneId=100002
&TypeId=2
&MemSize=1024
&GoodsNum=1
&Period=1
&Password=********
&BillingMode=1
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "DealId": "123456",
    "RequestId": "d4e2fd95-eac5-41ef-a7a9-7d30024d5507"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=CreateInstances)

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
| InternalError.InternalError | Internal error. |
| InvalidParameter.OnlyVPCOnSpecZoneId | Only VPCs are provided in Shanghai financial availability zone. |
| InvalidParameter.PermissionDenied | The API has no CAM permissions. |
| InvalidParameterValue.InvalidInstanceTypeId | Error with the type of instances requested for purchase (TypeId - 1: cluster edition; 2: master-slave edition, i.e., the legacy master-slave edition). |
| InvalidParameterValue.InvalidSubnetId | In a VPC, vpcid or subnet ID is invalid. |
| InvalidParameterValue.PasswordEmpty | Password is empty. |
| InvalidParameterValue.PasswordRuleError | When the password is set, the old password passed in by MC does not match the previously set password. |
| LimitExceeded.InvalidMemSize | The requested capacity is not in the capacity specifications (memSize should be an integral multiple of 1,024 in MB). |
| LimitExceeded.InvalidParameterGoodsNumNotInRange | The number of instances requested for purchase at a time is out of the purchasable quantity range. |
| LimitExceeded.PeriodExceedMaxLimit | The requested length of purchase is more than 3 years and exceeds the maximum value. |
| LimitExceeded.PeriodLessThanMinLimit | The length of purchase is invalid. It must be at least one month. |
| ResourceNotFound.AccountDoesNotExists | The uin value is blank. |
| ResourceNotFound.InstanceNotExists | No Redis instance found by the serialId. |
| ResourceUnavailable.InstanceDeleted | The instance has already been reclaimed. |
| ResourceUnavailable.NoEnoughVipInVPC | Insufficient IP resources in the VPC. |
| ResourceUnavailable.NoRedisService | The requested region currently does not provide the requested type of Redis service. |
| ResourceUnavailable.NoTypeIdRedisService | The requested region currently does not provide the requested type of Redis service. |
| UnauthorizedOperation.NoCAMAuthed | No CAM permissions. |
| UnauthorizedOperation.UserNotInWhiteList | User is not in the whitelist. |
