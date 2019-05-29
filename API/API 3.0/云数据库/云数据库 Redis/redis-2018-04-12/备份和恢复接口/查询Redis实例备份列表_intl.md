## 1. API Description

API domain name: redis.tencentcloudapi.com.

Query the list of Redis instance backups

Default API request rate limit: 20 requests/sec.

Note: This API supports financial availability zones. As financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), it is necessary to specify a domain name with the financial availability zone too, preferably in the same region as specified in Region, such as redis.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/239/20005).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeInstanceBackups |
| Version | Yes | String | Common parameter; the value for this API: 2018-04-12 |
| Region | Yes | String | Common parameters; for details, see the [List of Regions](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | ID of the instance to be operated on, which can be obtained through the InstanceId in the return value of the DescribeInstance API. |
| Limit | No | Integer | Instance list size; 20 by default |
| Offset | No | Integer | Offset, which is an integral multiple of Limit |
| BeginTime | No | String | Start time in the format of 2017-02-08 16:46:34. This is used to query the list of instance backups started during the [beginTime, endTime] range. |
| EndTime | No | String | End time in the format of 2017-02-08 19:09:26. This is used to query the list of instance backups started during the [beginTime, endTime] range. |
| Status.N | No | Array of Integer | 1: backup in process; 2: backing up normally; 3: converting from backup to RDB file; 4: RDB conversion completed; -1: backup expired; -2: backup deleted. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of backups |
| BackupSet | Array of [RedisBackupSet](/document/api/239/20022#RedisBackupSet) | Array of instance backups |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided during troubleshooting. |

## 4. Sample

### Sample 1. Request Example

#### Input Sample Code

```
https://redis.tencentcloudapi.com/?Action=DescribeInstanceBackups
&Limit=5&Offset=0
&InstanceId=crs-5a4py64p
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "2d4387ee-2011-449e-a32b-87f9366f3ef4",
    "TotalCount": 2,
    "RedisBackupSet": [
      {
        "StartTime": "2018-09-04 12:51:21",
        "BackupId": "2e4127f8-affe-11e8-941e-4846fb00c75d",
        "BackupType": "0",
        "Status": 2,
        "Remark": "For testing",
        "Locked": 0
      },
      {
        "StartTime": "2018-09-04 12:53:06",
        "BackupId": "6cbbf53a-affe-11e8-905b-4846fb00c75d",
        "BackupType": "0",
        "Status": 2,
        "Remark": "xxx",
        "Locked": 0
      }
    ]
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeInstanceBackups)

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
| InvalidParameter.InvalidParameter | Business parameter error. |
| ResourceNotFound.InstanceNotExists | No Redis instance found by the serialId. |
| UnauthorizedOperation.NoCAMAuthed | No CAM permissions. |
