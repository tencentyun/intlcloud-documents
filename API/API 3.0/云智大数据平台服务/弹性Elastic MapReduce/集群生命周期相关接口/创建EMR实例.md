## 1. 接口描述

接口请求域名： emr.tencentcloudapi.com 。

创建EMR实例

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/589/33974)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：CreateInstance |
| Version | 是 | String | 公共参数，本接口取值：2019-01-03 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](/document/api/589/33974#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| ProductId | 是 | Integer | 产品ID |
| VPCSettings | 是 | [VPCSettings](/document/api/589/33981#VPCSettings) | VPC设置参数 |
| Software.N | 是 | Array of String | 软件列表 |
| ResourceSpec | 是 | [ResourceSpec](/document/api/589/33981#ResourceSpec) | 资源描述 |
| SupportHA | 是 | Integer | 支持HA |
| InstanceName | 是 | String | 实例名称 |
| PayMode | 是 | Integer | 计费类型 |
| Placement | 是 | [Placement](/document/api/589/33981#Placement) | 集群位置信息 |
| TimeSpan | 是 | Integer | 时间长度 |
| TimeUnit | 是 | String | 时间单位 |
| LoginSettings | 是 | [LoginSettings](/document/api/589/33981#LoginSettings) | 登录配置 |
| ClientToken | 是 | String | 客户端Token |
| COSSettings | 否 | [COSSettings](/document/api/589/33981#COSSettings) | COS设置参数 |
| SgId | 否 | String | 安全组ID |
| PreExecutedFileSettings | 否 | [PreExecuteFileSettings](/document/api/589/33981#PreExecuteFileSettings) | 预执行脚本设置 |
| AutoRenew | 否 | Integer | 自动续费 |
| NeedMasterWan | 否 | String | 是否需要外网Ip。支持填NEED_MASTER_WAN，不支持使用NOT_NEED_MASTER_WAN，默认使用NEED_MASTER_WAN |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| Result | [CreateInstanceResult](/document/api/589/33981#CreateInstanceResult) | 创建实例结果信息|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 创建实例

#### 输入示例

```
https://emr.tencentcloudapi.com/?Action=CreateInstance
&ProductId=2
&SupportHA=0
&InstanceName=jaco2
&PayMode=1
&Placement.Zone=ap-chongqing-1
&Placement.ProjectId=0
&AutoRenew=0
&Software.0=hadoop-2.7.3
&Software.1=zookeeper-3.4.9
&ResourceSpec.MasterResourceSpec.Memory=8192
&ResourceSpec.MasterResourceSpec.CPUCores=4
&ResourceSpec.MasterResourceSpec.Volume=100
&ResourceSpec.MasterResourceSpec.DiskType=CLOUD_PREMIUM
&ResourceSpec.MasterResourceSpec.Spec=CVM.S3
&ResourceSpec.MasterResourceSpec.RootDiskVolume=100
&ResourceSpec.MasterResourceSpec.StorageType=5
&ResourceSpec.CoreResourceSpec.Memory=8192
&ResourceSpec.CoreResourceSpec.CPUCores=4
&ResourceSpec.CoreResourceSpec.Volume=100
&ResourceSpec.CoreResourceSpec.DiskType=CLOUD_PREMIUM
&ResourceSpec.CoreResourceSpec.Spec=CVM.S3
&ResourceSpec.CoreResourceSpec.RootDiskVolume=100
&ResourceSpec.CoreResourceSpec.StorageType=5
&ResourceSpec.MasterCount=1
&ResourceSpec.CoreCount=2
&VPCSettings.VpcId=vpc-5p4i6ned
&VPCSettings.SubnetId=subnet-r19p3f8k
&LoginSettings.Password=emr%40cloud
&ClientToken=jaco1
&TimeSpan=1
&TimeUnit=m
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "Result": {
      "ClientToken": "jaco1",
      "InstanceName": "jaco2",
      "DealNames": [
        "20190314261409",
        "20190314261410",
        "20190314261411",
        "20190314261412",
        "20190314261413",
        "20190314261414"
      ]
    },
    "RequestId": "701453be-7257-40e6-b5fd-4bbb01baae36"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=emr&Version=2019-01-03&Action=CreateInstance)

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

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](/document/api/589/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| InternalError | 内部错误。 |
