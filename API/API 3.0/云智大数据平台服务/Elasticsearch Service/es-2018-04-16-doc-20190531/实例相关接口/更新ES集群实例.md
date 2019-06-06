## 1. 接口描述

接口请求域名： es.tencentcloudapi.com 。

对集群进行扩缩容，修改实例名称，修改配置，重置密码， 添加Kibana黑白名单等操作。参数中InstanceId为必传参数，ForceRestart为选填参数，剩余参数传递组合及含义如下：
- InstanceName：修改实例名称(仅用于标识实例)
- NodeNum：集群数据节点横向扩缩容
- NodeType, DiskSize：集群数据节点纵向扩缩容
- MasterNodeNum: 集群专用主节点横向扩缩容
- MasterNodeType, MasterNodeDiskSize: 集群专用主节点纵向扩缩容
- EsConfig：修改集群配置
- Password：修改默认用户elastic的密码
- EsAcl：修改访问控制列表
- CosBackUp: 设置集群COS自动备份信息
以上参数组合只能传递一种，多传或少传均会导致请求失败

默认接口请求频率限制：20次/秒。

注意：本接口支持金融区地域。由于金融区和非金融区是隔离不互通的，因此当公共参数 Region 为金融区地域（例如 ap-shanghai-fsi）时，需要同时指定带金融区地域的域名，最好和 Region 的地域保持一致，例如：es.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/845/30623)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：UpdateInstance |
| Version | 是 | String | 公共参数，本接口取值：2018-04-16 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](/document/api/845/30623#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| InstanceId | 是 | String | 实例ID |
| InstanceName | 否 | String | 实例名称（1-50 个英文、汉字、数字、连接线-或下划线_） |
| NodeNum | 否 | Integer | 节点个数（2-50个） |
| EsConfig | 否 | String | 配置项（JSON格式字符串）。当前仅支持以下配置项：<li>action.destructive_requires_name</li><li>indices.fielddata.cache.size</li><li>indices.query.bool.max_clause_count</li> |
| Password | 否 | String | 默认用户elastic的密码（8到16位，至少包括两项（[a-z,A-Z],[0-9]和[-!@#$%&^*+=_:;,.?]的特殊符号） |
| EsAcl | 否 | [EsAcl](/document/api/845/30634#EsAcl) | 访问控制列表 |
| DiskSize | 否 | Integer | 磁盘大小（单位GB） |
| NodeType | 否 | String | 节点规格<li>ES.S1.SMALL2：1核2G</li><li>ES.S1.MEDIUM4：2核4G</li><li>ES.S1.MEDIUM8：2核8G</li><li>ES.S1.LARGE16：4核16G</li><li>ES.S1.2XLARGE32：8核32G</li><li>ES.S1.4XLARGE32：16核32G</li><li>ES.S1.4XLARGE64：16核64G</li> |
| MasterNodeNum | 否 | Integer | 专用主节点个数（只支持3个或5个） |
| MasterNodeType | 否 | String | 专用主节点规格<li>ES.S1.SMALL2：1核2G</li><li>ES.S1.MEDIUM4：2核4G</li><li>ES.S1.MEDIUM8：2核8G</li><li>ES.S1.LARGE16：4核16G</li><li>ES.S1.2XLARGE32：8核32G</li><li>ES.S1.4XLARGE32：16核32G</li><li>ES.S1.4XLARGE64：16核64G</li> |
| MasterNodeDiskSize | 否 | Integer | 专用主节点磁盘大小（单位GB系统默认配置为50GB,暂不支持自定义） |
| ForceRestart | 否 | Boolean | 更新配置时是否强制重启<li>true强制重启</li><li>false不强制重启</li>当前仅更新EsConfig时需要设置，默认值为false |
| CosBackup | 否 | [CosBackup](/document/api/845/30634#CosBackup) | COS自动备份信息 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 修改ES集群实例名称

用以修改指定ES集群实例的名称

#### 输入示例

```
https://es.tencentcloudapi.com/?Action=UpdateInstance
&InstanceId=es-4texbn20
&InstanceName=newName
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "c96a110c-7493-452d-a99b-683d0711dada"
  }
}
```

### 示例2 ES集群横向扩缩容

用以对指定ES集群实例进行横向扩缩容操作（当前仅支持横向扩容）

#### 输入示例

```
https://es.tencentcloudapi.com/?Action=UpdateInstance
&InstanceId=es-4texbn20
&NodeNum=5
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "6001962a-17c5-4604-a0af-0d4719c2ddca"
  }
}
```

### 示例3 修改ES集群实例配置

用以对指定的ES集群实例的配置进行修改操作

#### 输入示例

```
https://es.tencentcloudapi.com/?Action=UpdateInstance
&InstanceId=es-4texbn20
&EsConfig={"action.destructive_requires_name":"true"}
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "e7c1bb22-e5f2-42f1-8a12-a97a6de62798"
  }
}
```

### 示例4 重置Kibana密码

重置指定ES集群实例Kibana密码

#### 输入示例

```
https://es.tencentcloudapi.com/?Action=UpdateInstance
&InstanceId=es-qlpn5o2a
&Password=newPwd_123
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "1b72089e-720f-4f95-a4ae-4da4611bdb10"
  }
}
```

### 示例5 设置Kibana访问控制黑白名单

用以对指定的ES集群实例的Kibana设置访问控制黑白名单

#### 输入示例

```
https://es.tencentcloudapi.com/?Action=UpdateInstance
&InstanceId=es-qlpn5o2a
&EsAcl.BlackIpList.0=127.0.0.1
&EsAcl.BlackIpList.1=0.0.0.0
&EsAcl.WhiteIpList.0=127.0.0.1
&EsAcl.WhiteIpList.1=0.0.0.0
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "3b90bdbf-6f73-443e-958a-0b81e57ff6cb"
  }
}
```

### 示例6 ES集群纵向扩缩容

用以对集群的节点规格（核数、内存大小）和磁盘大小进行扩缩容操作（当前仅支持纵向扩容）

#### 输入示例

```
https://es.tencentcloudapi.com/?Action=UpdateInstance
&InstanceId=es-qlpn5o2a
&NodeType=ES.S1.MEDIUM4
&DiskSize=150
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "dd3f624d-9a72-4057-85cb-f5d32e7b3c7b"
  }
}
```

### 示例7 ES设置COS自动备份

#### 输入示例

```
https://es.tencentcloudapi.com/?Action=UpdateInstance
&InstanceId=es-qlpn5o2a
&CosBackup.IsAutoBackup=true
&CosBackup.BackupTime=23:00
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "dd3f624d-9a72-4057-85cb-f5d32e7b3c7b"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=es&Version=2018-04-16&Action=UpdateInstance)

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
| UnsupportedOperation | 操作不支持。 |
