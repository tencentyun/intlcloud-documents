## 1. API Description

API domain name: redis.tencentcloudapi.com.

This API queries the download address of a backup RDB.
Default API request rate limit: 20 requests/sec.

Note: This API supports financial availability zones. Because financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), you need to specify a domain name with the financial availability zone as well, which preferably in the same region as the specified Region, for example: vod.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/239/20005).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeBackupUrl |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-12 |
| Region | Yes | String | Common parameters; for details, see the [List of Regions](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID |
| BackupId | Yes | String | Backup ID. You can query this value via API DescribeInstanceBackups. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| DownloadUrl | Array of String | Download address on the public network (valid for 6 hours) |
| InnerDownloadUrl | Array of String | Download address on the private network (valid for 6 hours) |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Querying the Download Address of a Backup RDB

#### Input Sample Code

```
https://redis.tencentcloudapi.com/?Action=DescribeBackupUrl
&InstanceId=crs-4y9t57vt
&BackupId=678362566696298532848117
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "DownloadUrl": [
      "https://redis-database-backup-1251937656.cos.ap-chengdu.myqcloud.com/251005863/redis/1001463/data/2019-03-07/-9527208-4633789-redis-server-4.0.8-1001463-ignore-1-ignore.rdb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKID21teFeP99yb1FI94vqutgJkFoQ1eBpKg%26q-sign-time%3D1551952863%3B1551974523%26q-key-time%3D1551952863%3B1551974523%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3D28cc6edebf7f9d8e34aa3daf19d30ec521c03b5b",
      "https://redis-database-backup-1251937656.cos.ap-chengdu.myqcloud.com/251005863/redis/1001463/data/2019-03-07/-9527208-4633789-redis-server-4.0.8-1001463-ignore-2-ignore.rdb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKID21teFeP99yb1FI94vqutgJkFoQ1eBpKg%26q-sign-time%3D1551952863%3B1551974523%26q-key-time%3D1551952863%3B1551974523%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3D2b081fdb65c591f8e000ed55625af24049b15795",
      "https://redis-database-backup-1251937656.cos.ap-chengdu.myqcloud.com/251005863/redis/1001463/data/2019-03-07/-9527208-4633789-redis-server-4.0.8-1001463-ignore-3-ignore.rdb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKID21teFeP99yb1FI94vqutgJkFoQ1eBpKg%26q-sign-time%3D1551952864%3B1551974524%26q-key-time%3D1551952864%3B1551974524%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3D87eda5611679fb9bc2529631ae97b218317e9598",
      "https://redis-database-backup-1251937656.cos.ap-chengdu.myqcloud.com/251005863/redis/1001463/data/2019-03-07/-9527208-4633789-redis-server-4.0.8-1001463-ignore-4-ignore.rdb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKID21teFeP99yb1FI94vqutgJkFoQ1eBpKg%26q-sign-time%3D1551952864%3B1551974524%26q-key-time%3D1551952864%3B1551974524%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Db17a8297bf5637f0ce7ddb970ffd566b484a5063",
      "https://redis-database-backup-1251937656.cos.ap-chengdu.myqcloud.com/251005863/redis/1001463/data/2019-03-07/-9527208-4633789-redis-server-4.0.8-1001463-ignore-5-ignore.rdb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKID21teFeP99yb1FI94vqutgJkFoQ1eBpKg%26q-sign-time%3D1551952865%3B1551974525%26q-key-time%3D1551952865%3B1551974525%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3De69f614cffd54c1be7d609e05d20be15eb82fc13"
    ],
    "InnerDownloadUrl": [
      "https://redis-database-backup-1251937656.cos.ap-chengdu.myqcloud.com/251005863/redis/1001463/data/2019-03-07/-9527208-4633789-redis-server-4.0.8-1001463-ignore-1-ignore.rdb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKID21teFeP99yb1FI94vqutgJkFoQ1eBpKg%26q-sign-time%3D1551952863%3B1551974523%26q-key-time%3D1551952863%3B1551974523%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3D28cc6edebf7f9d8e34aa3daf19d30ec521c03b5b",
      "https://redis-database-backup-1251937656.cos.ap-chengdu.myqcloud.com/251005863/redis/1001463/data/2019-03-07/-9527208-4633789-redis-server-4.0.8-1001463-ignore-2-ignore.rdb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKID21teFeP99yb1FI94vqutgJkFoQ1eBpKg%26q-sign-time%3D1551952863%3B1551974523%26q-key-time%3D1551952863%3B1551974523%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3D2b081fdb65c591f8e000ed55625af24049b15795",
      "https://redis-database-backup-1251937656.cos.ap-chengdu.myqcloud.com/251005863/redis/1001463/data/2019-03-07/-9527208-4633789-redis-server-4.0.8-1001463-ignore-3-ignore.rdb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKID21teFeP99yb1FI94vqutgJkFoQ1eBpKg%26q-sign-time%3D1551952864%3B1551974524%26q-key-time%3D1551952864%3B1551974524%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3D87eda5611679fb9bc2529631ae97b218317e9598",
      "https://redis-database-backup-1251937656.cos.ap-chengdu.myqcloud.com/251005863/redis/1001463/data/2019-03-07/-9527208-4633789-redis-server-4.0.8-1001463-ignore-4-ignore.rdb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKID21teFeP99yb1FI94vqutgJkFoQ1eBpKg%26q-sign-time%3D1551952864%3B1551974524%26q-key-time%3D1551952864%3B1551974524%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Db17a8297bf5637f0ce7ddb970ffd566b484a5063",
      "https://redis-database-backup-1251937656.cos.ap-chengdu.myqcloud.com/251005863/redis/1001463/data/2019-03-07/-9527208-4633789-redis-server-4.0.8-1001463-ignore-5-ignore.rdb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKID21teFeP99yb1FI94vqutgJkFoQ1eBpKg%26q-sign-time%3D1551952865%3B1551974525%26q-key-time%3D1551952865%3B1551974525%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3De69f614cffd54c1be7d609e05d20be15eb82fc13"
    ],
    "RequestId": "f1b5aabe-806a-4886-b839-9907baa24c85"
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeBackupUrl)

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
| InternalError.InternalError | Internal error. |
| InvalidParameter.PermissionDenied | The API has no CAM permissions. |
| ResourceNotFound.InstanceNotExists | No Redis instance found by the serialId. |
| UnauthorizedOperation.NoCAMAuthed | No CAM permissions. |
| UnauthorizedOperation.UserNotInWhiteList | User is not in the whitelist. |
| UnsupportedOperation.ClusterInstanceAccessedDeny | The Redis cluster edition is not allowed to access a security group. |
| UnsupportedOperation.IsAutoRenewError | Error with the auto-renewal flag. |
| UnsupportedOperation.OnlyClusterInstanceCanExportBackup | Only cluster edition instances support backup exporting. |
