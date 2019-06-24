## 1. API Description

API domain name: redis.tencentcloudapi.com.

This API upgrades an instance.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial availability zones. Because financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), you need to specify a domain name with the financial availability zone as well, which preferably in the same region as the specified Region, for example: vod.ap-shanghai-fsi.tencentcloudapi.com.


## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/239/20005).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: UpgradeInstance |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-12 |
| Region | Yes | String | Common parameters; for details, see the [List of Regions](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID |
| MemSize | Yes | Integer | Shard size in MB |
| RedisShardNum | No | Integer | Number of shards. Leave this parameter blank when using Redis 2.8 master-slave, CKV master-slave, and Redis 2.8 standalone. |
| RedisReplicasNum | No | Integer | Number of replicas. Leave this parameter blank when using Redis 2.8 master-slave, CKV master-slave, and Redis 2.8 standalone. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| DealId | String | Order ID |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |


## 4. Sample

### Sample 1. Request Example

#### Input Sample Code

```
https://redis.tencentcloudapi.com/?Action=UpgradeInstance
&InstanceId=crs-5qlrlhux
&MemSize=4096
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "DealId": "6954227",
    "RequestId": "4daddc97-0005-45d8-b5b8-38514ec1e97c"
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=UpgradeInstance)

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

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/239/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameter.PermissionDenied | The API has no CAM permissions. |
| InvalidParameterValue.MemSizeNotInRange | The requested capacity is out of the purchasable capacity range. |
| InvalidParameterValue.ReduceCapacityNotAllowed | The requested capacity is smaller than the minimum amount required. Reducing capacity is not supported. |
| LimitExceeded.InvalidMemSize | The requested capacity does not satisfies the capacity specification (memSize should be a multiplier of 1,024 in MB). |
| ResourceNotFound.InstanceNotExists | No Redis instance found by the specified serialId. |
| ResourceUnavailable.AccountBalanceNotEnough | The order number of the request does not exist. |
| ResourceUnavailable.InstanceStatusAbnormal | The Redis status is abnormal, and the corresponding process cannot be executed. |
| UnauthorizedOperation.NoCAMAuthed | No CAM permissions. |
