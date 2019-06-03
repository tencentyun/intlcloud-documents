## 1. API Description

API domain name: redis.tencentcloudapi.com.

This API gets the cluster mode instance shard information.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial availability zones. Because financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), you need to specify a domain name with the financial availability zone as well, which preferably in the same region as the specified Region, for example: vod.ap-shanghai-fsi.tencentcloudapi.com.


## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/239/20005).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeInstanceShards |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-12 |
| Region | Yes | String | Common parameters; for details, see the [List of Regions](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID |
| FilterSlave | No | Boolean | Whether to filter out the replica information |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| InstanceShards | Array of [InstanceClusterShard](/document/api/239/20022#InstanceClusterShard) | Information list of instance shards |
| TotalCount | Integer | Total number of instance shard nodes |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Request Example

#### Input Sample Code

```
https://redis.tencentcloudapi.com/?Action=DescribeInstanceShards
&InstanceId=crs-7ponppu3
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "InstanceShards": [
      {
        "Keys": 0,
        "Role": 0,
        "ShardId": "1",
        "ShardName": "crs-7ponppu3-003-01",
        "Slots": "[\"0-5460\"]",
        "Storage": 3096688,
        "StorageSlope": -0.002399486489594
      },
      {
        "Keys": 0,
        "Role": 1,
        "ShardId": "1",
        "ShardName": "crs-7ponppu3-003-02",
        "Slots": "[]",
        "Storage": 3035608,
        "StorageSlope": 0
      },
      {
        "Keys": 0,
        "Role": 0,
        "ShardId": "2",
        "ShardName": "crs-7ponppu3-001-01",
        "Slots": "[\"5461-10922\"]",
        "Storage": 3160280,
        "StorageSlope": 0.018086727708578
      },
      {
        "Keys": 0,
        "Role": 1,
        "ShardId": "2",
        "ShardName": "crs-7ponppu3-001-02",
        "Slots": "[]",
        "Storage": 3036632,
        "StorageSlope": 0
      },
      {
        "Keys": 0,
        "Role": 0,
        "ShardId": "3",
        "ShardName": "crs-7ponppu3-002-01",
        "Slots": "[\"10923-16383\"]",
        "Storage": 3055440,
        "StorageSlope": -0.015687562525272
      },
      {
        "Keys": 0,
        "Role": 1,
        "ShardId": "3",
        "ShardName": "crs-7ponppu3-002-02",
        "Slots": "[]",
        "Storage": 3035608,
        "StorageSlope": 0
      }
    ],
    "RequestId": "ca3000b6-bb8a-41fd-9074-11b5fda52d9f"
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeInstanceShards)

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
| FailedOperation.SystemError | Internal system error, irrelevant to the business. |
| InvalidParameter.PermissionDenied | The API has no CAM permissions. |
| InvalidParameterValue.UnSupportedType | The instance type is not supported. |
