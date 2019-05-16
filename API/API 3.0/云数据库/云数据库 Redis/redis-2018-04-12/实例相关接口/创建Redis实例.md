## 1. 接口描述

接口请求域名： redis.tencentcloudapi.com 。

创建redis实例

默认接口请求频率限制：20次/秒。

注意：本接口支持金融区地域。由于金融区和非金融区是隔离不互通的，因此当公共参数 Region 为金融区地域（例如 ap-shanghai-fsi）时，需要同时指定带金融区地域的域名，最好和 Region 的地域保持一致，例如：redis.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/239/20005)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：CreateInstances |
| Version | 是 | String | 公共参数，本接口取值：2018-04-12 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| ZoneId | 是 | Integer | 实例所属的可用区id |
| TypeId | 是 | Integer | 实例类型：2 – Redis2.8主从版，3 – Redis3.2主从版(CKV主从版)，4 – Redis3.2集群版(CKV集群版)，5-Redis2.8单机版，7 – Redis4.0集群版， |
| MemSize | 是 | Integer | 实例容量，单位MB， 取值大小以 查询售卖规格接口返回的规格为准 |
| GoodsNum | 是 | Integer | 实例数量，单次购买实例数量以 查询售卖规格接口返回的规格为准 |
| Period | 是 | Integer | 购买时长，在创建包年包月实例的时候需要填写，按量计费实例填1即可，单位：月，取值范围 [1,2,3,4,5,6,7,8,9,10,11,12,24,36] |
| Password | 是 | String | 实例密码，密码规则：1.长度为8-16个字符；2:至少包含字母、数字和字符!@^*()中的两种 |
| BillingMode | 是 | Integer | 付费方式:0-按量计费，1-包年包月。 |
| VpcId | 否 | String | 私有网络ID，如果不传则默认选择基础网络，请使用私有网络列表查询，如：vpc-sad23jfdfk |
| SubnetId | 否 | String | 基础网络下， subnetId无效； vpc子网下，取值以查询子网列表，如：subnet-fdj24n34j2 |
| ProjectId | 否 | Integer | 项目id，取值以用户账户>用户账户相关接口查询>项目列表返回的projectId为准 |
| AutoRenew | 否 | Integer | 自动续费标识。0 - 默认状态（手动续费）；1 - 自动续费；2 - 明确不自动续费 |
| SecurityGroupIdList.N | 否 | Array of String | 安全组id数组 |
| VPort | 否 | Integer | 用户自定义的端口 不填则默认为6379 |
| RedisShardNum | 否 | Integer | 实例分片数量，Redis2.8主从版、CKV主从版和Redis2.8单机版不需要填写 |
| RedisReplicasNum | 否 | Integer | 实例副本数量，Redis2.8主从版、CKV主从版和Redis2.8单机版不需要填写 |
| ReplicasReadonly | 否 | Boolean | 是否支持副本只读，Redis2.8主从版、CKV主从版和Redis2.8单机版不需要填写 |
| InstanceName | 否 | String | 实例名称 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| DealId | String | 交易的Id|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 请求示例

#### 输入示例

```
https://redis.tencentcloudapi.com/?Action=CreateInstances
&ZoneId=100002
&TypeId=2
&MemSize=1024
&GoodsNum=1
&Period=1
&Password=********
&BillingMode=1
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "DealId": "123456",
    "RequestId": "d4e2fd95-eac5-41ef-a7a9-7d30024d5507"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=CreateInstances)

### SDK

云 API 3.0 提供了配套的开发工具集（SDK），支持多种编程语言，能更方便的调用 API。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### 命令行工具

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. 错误码

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](/document/api/239/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| InternalError.InternalError | 内部错误。 |
| InvalidParameter.OnlyVPCOnSpecZoneId | 上海金融只提供vpc网络。 |
| InvalidParameter.PermissionDenied | 接口没有cam权限。 |
| InvalidParameterValue.InvalidInstanceTypeId | 请求购买的实例类型错误（TypeId 1:集群版；2:主从版,即原主从版)。 |
| InvalidParameterValue.InvalidSubnetId | vpc网络下，vpcid 子网id 非法。 |
| InvalidParameterValue.PasswordEmpty | 密码为空。 |
| InvalidParameterValue.PasswordRuleError | 置密码时，MC 传入的 old password 与先前设定密码不同。 |
| LimitExceeded.InvalidMemSize | 求的容量不在售卖规格中（memSize应为1024的整数倍，单位：MB）。 |
| LimitExceeded.InvalidParameterGoodsNumNotInRange | 一次请求购买的实例数不在售卖数量限制范围内。 |
| LimitExceeded.PeriodExceedMaxLimit | 购买时长超过3年,请求时长超过最大时长。 |
| LimitExceeded.PeriodLessThanMinLimit | 购买时长非法，时长最少1个月。 |
| ResourceNotFound.AccountDoesNotExists | uin 值为空。 |
| ResourceNotFound.InstanceNotExists | 根据 serialId 没有找到对应 redis。 |
| ResourceUnavailable.InstanceDeleted | 实例已经被回收了。 |
| ResourceUnavailable.NoEnoughVipInVPC | vpc网络IP资源不足。 |
| ResourceUnavailable.NoRedisService | 请求的区域暂时不提供请求类型的redis服务。 |
| ResourceUnavailable.NoTypeIdRedisService | 请求的区域暂时不提供请求类型的redis服务。 |
| UnauthorizedOperation.NoCAMAuthed | 无cam 权限。 |
| UnauthorizedOperation.UserNotInWhiteList | 户不在白名单中。 |
