## 1. API Description

API domain name: redis.tencentcloudapi.com.

This API queries the list of instance parameters.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial availability zones. Because financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), you need to specify a domain name with the financial availability zone as well, which preferably in the same region as the specified Region, for example: vod.ap-shanghai-fsi.tencentcloudapi.com.


## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/239/20005).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeInstanceParams |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-12 |
| Region | Yes | String | Common parameters; for details, see the [List of Regions](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of instance parameters |
| InstanceEnumParam | Array of [InstanceEnumParam](/document/api/239/20022#InstanceEnumParam) | Enumeration parameters of the instance |
| InstanceIntegerParam | Array of [InstanceIntegerParam](/document/api/239/20022#InstanceIntegerParam) | Integer parameters of the instance |
| InstanceTextParam | Array of [InstanceTextParam](/document/api/239/20022#InstanceTextParam) | Text parameters of the instance |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |


## 4. Sample

### Sample 1. Querying the List of Instance Parameters

#### Input Sample Code

```
https://redis.tencentcloudapi.com/?Action=DescribeInstanceParams
&InstanceId=crs-5a4py64p
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "InstanceEnumParam": [
      {
        "CurrentValue": "volatile-ttl",
        "DefaultValue": "noeviction",
        "EnumValue": [
          "volatile-lru",
          "allkeys-lru",
          "volatile-random",
          "allkeys-random",
          "volatile-ttl",
          "noeviction"
        ],
        "NeedRestart": "false",
        "ParamName": "maxmemory-policy",
        "Tips": "Select the memory swapping policy when the system reaches the set maximum memory value",
        "ValueType": "enum"
      }
    ],
    "InstanceIntegerParam": [
      {
        "CurrentValue": "15001",
        "DefaultValue": "15000",
        "Max": "120000",
        "Min": "15000",
        "NeedRestart": "false",
        "ParamName": "cluster-node-timeout",
        "Tips": "In cluster mode, a node is considered to fail if it is unreachable within the specified time period (in milliseconds)",
        "ValueType": "integer"
      },
      {
        "CurrentValue": "511",
        "DefaultValue": "512",
        "Max": "10000",
        "Min": "1",
        "NeedRestart": "false",
        "ParamName": "hash-max-ziplist-entries",
        "Tips": "If the number of hash entries does not exceed the specified number, the hashes are encoded using a memory efficient data structure",
        "ValueType": "integer"
      },
      {
        "CurrentValue": "61",
        "DefaultValue": "64",
        "Max": "10000",
        "Min": "1",
        "NeedRestart": "false",
        "ParamName": "hash-max-ziplist-value",
        "Tips": "If the largest item in the hashes does not exceed the specified threshold, the hashes are encoded using a memory efficient data structure",
        "ValueType": "integer"
      },
      {
        "CurrentValue": "511",
        "DefaultValue": "512",
        "Max": "10000",
        "Min": "1",
        "NeedRestart": "false",
        "ParamName": "set-max-intset-entries",
        "Tips": "If all the elements in the set are 64-bit signed decimal integers and do not exceed the set threshold, the hashes are encoded as an integer set",
        "ValueType": "integer"
      },
      {
        "CurrentValue": "10001",
        "DefaultValue": "10000",
        "Max": "1000000",
        "Min": "-1",
        "NeedRestart": "false",
        "ParamName": "slowlog-log-slower-than",
        "Tips": "Commands that exceed the specified time period of execution will be logged; a negative number indicates to disable this feature, and zero indicates to compulsorily log the executions of all commands",
        "ValueType": "integer"
      },
      {
        "CurrentValue": "4",
        "DefaultValue": "0",
        "Max": "7200",
        "Min": "0",
        "NeedRestart": "false",
        "ParamName": "timeout",
        "Tips": "The connection is closed after the client is idle for the specified length of time, and zero indicates to disable this feature",
        "ValueType": "integer"
      },
      {
        "CurrentValue": "121",
        "DefaultValue": "128",
        "Max": "10000",
        "Min": "1",
        "NeedRestart": "false",
        "ParamName": "zset-max-ziplist-entries",
        "Tips": "If the number of ordered set elements does not exceed the specified number, the hashes are encoded using a memory efficient data structure",
        "ValueType": "integer"
      },
      {
        "CurrentValue": "61",
        "DefaultValue": "64",
        "Max": "10000",
        "Min": "1",
        "NeedRestart": "false",
        "ParamName": "zset-max-ziplist-value",
        "Tips": "If the largest item in the ordered set does not exceed the specified threshold, the hashes are encoded using a memory efficient data structure",
        "ValueType": "integer"
      }
    ],
    "InstanceTextParam": [
      {
        "CurrentValue": "\"eK\"",
        "DefaultValue": "\"\"",
        "NeedRestart": "false",
        "ParamName": "notify-keyspace-events",
        "TextValue": [
          "K",
          "E",
          "g",
          "$",
          "l",
          "s",
          "h",
          "z",
          "x",
          "e",
          "A"
        ],
        "Tips": "Change the notification method of the client key space set by the system",
        "ValueType": "text"
      }
    ],
    "RequestId": "e546784b-709c-401d-aba6-73037eb4e522",
    "TotalCount": 10
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeInstanceParams)

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
| FailedOperation.UnSupportError | The instance does not support this API. |
| InternalError.DbOperationFailed | Internal system error with the DB operation, which may be update, insert, select, etc. |
| InternalError.InternalError | Internal error. |
| InvalidParameter | Parameter error |
| InvalidParameter.PermissionDenied | The API has no CAM permissions. |
| UnauthorizedOperation | Unauthorized operation. |
| UnauthorizedOperation.NoCAMAuthed | No CAM permissions. |
| UnauthorizedOperation.UserNotInWhiteList | User is not in the whitelist. |
| UnsupportedOperation.ClusterInstanceAccessedDeny | The Redis cluster edition is not allowed to access a security group. |
