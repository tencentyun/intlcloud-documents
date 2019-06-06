## 1. 接口描述

接口请求域名： es.tencentcloudapi.com 。

创建指定规格的ES集群实例

默认接口请求频率限制：20次/秒。

注意：本接口支持金融区地域。由于金融区和非金融区是隔离不互通的，因此当公共参数 Region 为金融区地域（例如 ap-shanghai-fsi）时，需要同时指定带金融区地域的域名，最好和 Region 的地域保持一致，例如：es.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/845/30623)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：CreateInstance |
| Version | 是 | String | 公共参数，本接口取值：2018-04-16 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](/document/api/845/30623#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| Zone | 是 | String | 可用区 |
| NodeNum | 是 | Integer | 节点数量（2-50个） |
| EsVersion | 是 | String | 实例版本（支持"5.6.4"、"6.4.3"） |
| NodeType | 是 | String | 节点规格<li>ES.S1.SMALL2：1核2G</li><li>ES.S1.MEDIUM4：2核4G</li><li>ES.S1.MEDIUM8：2核8G</li><li>ES.S1.LARGE16：4核16G</li><li>ES.S1.2XLARGE32：8核32G</li><li>ES.S1.4XLARGE32：16核32G</li><li>ES.S1.4XLARGE64：16核64G</li> |
| DiskSize | 是 | Integer | 节点磁盘容量（单位GB） |
| VpcId | 是 | String | 私有网络ID |
| SubnetId | 是 | String | 子网ID |
| Password | 是 | String | 访问密码（密码需8到16位，至少包括两项（[a-z,A-Z],[0-9]和[-!@#$%&^*+=_:;,.?]的特殊符号） |
| InstanceName | 否 | String | 实例名称（1-50 个英文、汉字、数字、连接线-或下划线_） |
| ChargeType | 否 | String | 计费类型<li>PREPAID：预付费，即包年包月</li><li>POSTPAID_BY_HOUR：按小时后付费</li>默认值POSTPAID_BY_HOUR |
| ChargePeriod | 否 | Integer | 包年包月购买时长（单位由参数TimeUint决定） |
| RenewFlag | 否 | String | 自动续费标识<li>RENEW_FLAG_AUTO：自动续费</li><li>RENEW_FLAG_MANUAL：不自动续费，用户手动续费</li>ChargeType为PREPAID时需要设置，如不传递该参数，普通用于默认不自动续费，SVIP用户自动续费 |
| DiskType | 否 | String | 节点磁盘类型<li>CLOUD_SSD：SSD云硬盘</li><li>CLOUD_PREMIUM：高硬能云硬盘</li>默认值CLOUD_SSD |
| TimeUnit | 否 | String | 计费时长单位（ChargeType为PREPAID时需要设置，默认值为“m”，表示月，当前只支持“m”） |
| AutoVoucher | 否 | Integer | 是否自动使用代金券<li>0：不自动使用</li><li>1：自动使用</li>默认值0 |
| VoucherIds.N | 否 | Array of String | 代金券ID列表（目前仅支持指定一张代金券） |
| EnableDedicatedMaster | 否 | Boolean | 是否创建专用主节点<li>true：开启专用主节点</li><li>false：不开启专用主节点</li>默认值false |
| MasterNodeNum | 否 | Integer | 专用主节点个数（只支持3个和5个，EnableDedicatedMaster为true时该值必传） |
| MasterNodeType | 否 | String | 专用主节点类型（EnableDedicatedMaster为true时必传）<li>ES.S1.SMALL2：1核2G</li><li>ES.S1.MEDIUM4：2核4G</li><li>ES.S1.MEDIUM8：2核8G</li><li>ES.S1.LARGE16：4核16G</li><li>ES.S1.2XLARGE32：8核32G</li><li>ES.S1.4XLARGE32：16核32G</li><li>ES.S1.4XLARGE64：16核64G</li> |
| MasterNodeDiskSize | 否 | Integer | 专用主节点磁盘大小（单位GB，非必传，若传递则必须为50，暂不支持自定义） |
| ClusterNameInConf | 否 | String | 集群配置文件中的ClusterName（系统默认配置为实例ID，暂不支持自定义） |
| DeployMode | 否 | Integer | 集群部署方式<li>0：单可用区部署</li><li>1：多可用区部署</li>默认为0 |
| MultiZoneInfo.N | 否 | Array of [MultiZoneInfo](/document/api/845/30634#MultiZoneInfo) | 多可用区部署时可用区的详细信息(DeployMode为1时必传) |
| LicenseType | 否 | String | License类型<li>oss：开源版</li><li>basic：基础版</li><li>platinum：白金版</li>默认值platinum |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| InstanceId | String | 实例ID|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 创建ES集群实例

根据输入参数创建ES集群实例

#### 输入示例

```
https://es.tencentcloudapi.com/?Action=CreateInstance?
InstanceName=es_test
&Zone=ap-guangzhou-2
&NodeNum=2
&EsVersion=5.6.4
&ChargeType=PREPAID
&ChargePeriod=1
&NodeType=ES.S1.SMALL2
&DiskSize=100
&VpcId=vpc-63g206gx
&SubnetId=subnet-ap0jf4gg
&Password=elastic_123
&EnableDedicatedMaster=true
&MasterNodeNum=3
&MasterNodeType=ES.S1.SMALL2
&MasterNodeDiskSize=50
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "InstanceId": "es-qlpn5o2a",
    "RequestId": "d7b76d5e-ad7d-4abd-b3b2-43b96dd08d16"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=es&Version=2018-04-16&Action=CreateInstance)

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

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](/document/api/845/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| FailedOperation.NoPayment | 账户未绑定信用卡或paypal，无法支付。 |
| InternalError | 内部错误。 |
| InvalidParameter | 参数错误。 |
| ResourceInUse | 资源被占用。 |
| ResourceInsufficient | 资源不足。 |
| ResourceInsufficient.Balance | 账户余额不足。 |
