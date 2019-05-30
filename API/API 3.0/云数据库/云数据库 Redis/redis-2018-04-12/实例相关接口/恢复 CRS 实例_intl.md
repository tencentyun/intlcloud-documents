## 1. API Description

API domain name: redis.tencentcloudapi.com.

This API restores a Redis instance.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial availability zones. Because financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), you need to specify a domain name with the financial availability zone as well, which preferably in the same region as the specified Region, for example: vod.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/239/20005).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: RestoreInstance |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-12 |
| Region | Yes | String | Common parameters; for details, see the [List of Regions](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | ID of the operated instance. You can find this value at the output parameter redisId returned by API DescribeRedis. |
| Password | String | Yes | Instance password, which needs to be validated for instance restoration. |
| BackupId | Yes | String | Backup ID. You can find this value at the output parameter backupId returned by API GetRedisBackupList. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TaskId | Integer | Task ID, which can be used to query the task execution status through the DescribeTaskInfo API |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Restoring a Redis Instance

#### Input Sample Code

```
https://redis.tencentcloudapi.com/?Action=RestoreInstance
&InstanceId=crs-5a4py64p
&Password=mypassword
&BackupId=678362566696298532848117
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TaskId": "6954227",
    "RequestId": "4daddc97-0005-45d8-b5b8-38514ec1e97c"
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=RestoreInstance)

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
| InternalError.InternalError | Internal error. |
| InvalidParameter.InvalidParameter | Business parameter error. |
| InvalidParameter.PermissionDenied | The API has no CAM permissions. |
| InvalidParameterValue.BackupNotExists | The backup does not exist. |
| InvalidParameterValue.PasswordError | Wrong password. |
| ResourceNotFound.InstanceNotExists | No Redis instance found by the serialId. |
| ResourceUnavailable.BackupLockedError | The backup has been locked by another task, and the action cannot be performed temporarily. |
| ResourceUnavailable.BackupStatusAbnormal | Exception with the backup status. The action cannot be performed temporarily. The backup may have expired or been deleted. |
| ResourceUnavailable.InstanceLockedError | Redis has been locked by another process. |
| ResourceUnavailable.InstanceStatusAbnormal | The Redis status is exceptional, and the corresponding process cannot be executed. |
| UnauthorizedOperation.NoCAMAuthed | No CAM permissions. |
