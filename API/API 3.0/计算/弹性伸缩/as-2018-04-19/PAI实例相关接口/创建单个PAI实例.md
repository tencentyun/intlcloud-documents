## 1. 接口描述

接口请求域名： as.tencentcloudapi.com 。

本接口 (CreatePaiInstance) 用于创建一个指定配置的PAI实例。

默认接口请求频率限制：20次/秒。

注意：本接口支持金融区地域。由于金融区和非金融区是隔离不互通的，因此当公共参数 Region 为金融区地域（例如 ap-shanghai-fsi）时，需要同时指定带金融区地域的域名，最好和 Region 的地域保持一致，例如：as.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/377/20426)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：CreatePaiInstance |
| Version | 是 | String | 公共参数，本接口取值：2018-04-19 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| DomainName | 是 | String | PAI实例的域名。 |
| InternetAccessible | 是 | [InternetAccessible](/document/api/377/20453#InternetAccessible) | 公网带宽相关信息设置。 |
| InitScript | 否 | String | 启动脚本的base64编码字符串。 |
| Zones.N | 否 | Array of String | 可用区列表。 |
| VpcId | 否 | String | VpcId。 |
| SubnetIds.N | 否 | Array of String | 子网列表。 |
| InstanceName | 否 | String | 实例显示名称。 |
| InstanceTypes.N | 否 | Array of String | 实例机型列表。 |
| LoginSettings | 否 | [LoginSettings](/document/api/377/20453#LoginSettings) | 实例登录设置。 |
| InstanceChargeType | 否 | String | 实例计费类型。 |
| InstanceChargePrepaid | 否 | [InstanceChargePrepaid](/document/api/377/20453#InstanceChargePrepaid) | 预付费模式，即包年包月相关参数设置。通过该参数可以指定包年包月实例的购买时长、是否设置自动续费等属性。若指定实例的付费模式为预付费则该参数必传。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| InstanceIdSet | Array of String | 当通过本接口来创建实例时会返回该参数，表示一个或多个实例`ID`。返回实例`ID`列表并不代表实例创建成功，可根据 [DescribeInstances](https://cloud.tencent.com/document/api/213/15728) 接口查询返回的InstancesSet中对应实例的`ID`的状态来判断创建是否完成；如果实例状态由“准备中”变为“正在运行”，则为创建成功。|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 创建单个PAI实例

通过指定的域名等参数，创建单个PAI实例

#### 输入示例

```
https://as.tencentcloudapi.com/?Action=CreatePaiInstance
&DomainName=apple-gz012345.pai.tcloudbase.com
&InitScript=IyEvYmluL2Jhc2gKZWNobyAiaGVsbG8iCg==
&Zones.0=ap-guangzhou-2
&InstanceChargeType=POSTPAID_BY_HOUR
&InstanceTypes.0=S4.SMALL2
&SystemDisk.DiskType=CLOUD_BASIC
&SystemDisk.DiskSize=50
&InternetAccessible.InternetChargeType=TRAFFIC_POSTPAID_BY_HOUR
&InternetAccessible.InternetMaxBandwidthOut=10
&InstanceName=PAI-TEST
&LoginSettings.Password=PAI@Test123
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "InstanceIdSet": [
      "ins-bmmk7d75"
    ],
    "RequestId": "843518b0-43bb-4066-a00b-d95b338b3142"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CreatePaiInstance)

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

该接口暂无业务逻辑相关的错误码，其他错误码详见 [公共错误码](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。
