## 1. 接口描述

接口请求域名： redis.tencentcloudapi.com 。

查询备份Rdb下载地址

默认接口请求频率限制：20次/秒。

注意：本接口支持金融区地域。由于金融区和非金融区是隔离不互通的，因此当公共参数 Region 为金融区地域（例如 ap-shanghai-fsi）时，需要同时指定带金融区地域的域名，最好和 Region 的地域保持一致，例如：redis.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](https://cloud.tencent.com/document/api/239/20005)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeBackupUrl |
| Version | 是 | String | 公共参数，本接口取值：2018-04-12 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| InstanceId | 是 | String | 实例Id |
| BackupId | 是 | String | 备份Id，通过DescribeInstanceBackups接口可查 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| DownloadUrl | Array of String | 外网下载地址（6小时）|
| InnerDownloadUrl | Array of String | 内网下载地址（6小时）|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询备份Rdb下载地址

#### 输入示例

```
https://redis.tencentcloudapi.com/?Action=DescribeBackupUrl
&InstanceId=crs-4y9t57vt
&BackupId=678362566696298532848117
&<公共请求参数>
```

#### 输出示例

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


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeBackupUrl)

### SDK

云 API 3.0 提供了配套的开发工具集（SDK），支持多种编程语言，能更方便的调用 API。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### 命令行工具

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. 错误码

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](https://cloud.tencent.com/document/api/239/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| FailedOperation.SystemError | 内部系统错误，和业务无关。 |
| InternalError.InternalError | 内部错误。 |
| InvalidParameter.PermissionDenied | 接口没有cam权限。 |
| ResourceNotFound.InstanceNotExists | 根据 serialId 没有找到对应 redis。 |
| UnauthorizedOperation.NoCAMAuthed | 无cam 权限。 |
| UnauthorizedOperation.UserNotInWhiteList | 户不在白名单中。 |
| UnsupportedOperation.ClusterInstanceAccessedDeny | redis 集群版不允许接入安全组。 |
| UnsupportedOperation.IsAutoRenewError | 自动续费标识错误。 |
| UnsupportedOperation.OnlyClusterInstanceCanExportBackup | 只有集群版实例支持导出备份。 |
