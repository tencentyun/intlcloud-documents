## 1. 接口描述

接口请求域名： emr.tencentcloudapi.com 。

查询EMR实例

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/589/33974)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeInstances |
| Version | 是 | String | 公共参数，本接口取值：2019-01-03 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](/document/api/589/33974#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| InstanceIds.N | 否 | Array of String | 查询列表,  如果不填写，返回该AppId下所有实例列表 |
| Offset | 否 | Integer | 查询偏移量，默认0 |
| Limit | 否 | Integer | 查询结果限制，默认值10 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| Result | [ClusterInfoResult](/document/api/589/33981#ClusterInfoResult) | 实例数量|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询实例详情

#### 输入示例

```
https://emr.tencentcloudapi.com/?Action=DescribeInstances
&Offset=0
&Limit=1
&InstanceIds.0=emr-b3zor8nr
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "Result": {
      "TotalCnt": 1,
      "ClusterList": [
        {
          "ClusterId": "emr-b3zor8nr",
          "StatusDesc": "集群运行中",
          "ClusterName": "jaco2",
          "ZoneId": 190001,
          "AppId": 1258469122,
          "Addtime": "2019-03-14 20:44:31",
          "Runtime": "0天3小时41分钟13秒",
          "Config": {
            "SoftInfo": [
              "zookeeper-3.4.9",
              "hadoop-2.7.3",
              "sys-1.0"
            ],
            "MasterNodeSize": 1,
            "CoreNodeSize": 2,
            "TaskNodeSize": 1,
            "ComNodeSize": 0,
            "MasterResourceSpec": {
              "CPUCores": 4,
              "DiskType": "CLOUD_PREMIUM",
              "Memory": 8192,
              "RootDiskVolume": 100,
              "Spec": "CVM.S3",
              "StorageType": 5,
              "Volume": 100,
              "SpecName": ""
            },
            "CoreResourceSpec": {
              "CPUCores": 4,
              "DiskType": "CLOUD_PREMIUM",
              "Memory": 8192,
              "RootDiskVolume": 100,
              "Spec": "CVM.S3",
              "StorageType": 5,
              "Volume": 100,
              "SpecName": ""
            },
            "TaskResourceSpec": {
              "CPUCores": 4,
              "DiskType": "CLOUD_PREMIUM",
              "Memory": 8192,
              "RootDiskVolume": 100,
              "Spec": "CVM.S3",
              "StorageType": 5,
              "Volume": 100,
              "SpecName": ""
            },
            "CommonResourceSpec": {
              "CPUCores": 0,
              "DiskType": "",
              "Memory": 0,
              "RootDiskVolume": 0,
              "Spec": "",
              "StorageType": 0,
              "Volume": 0,
              "SpecName": ""
            },
            "Oncos": false,
            "COSSettings": {
              "LogOnCosPath": "",
              "CosSecretId": "",
              "CosSecretKey": ""
            }
          },
          "MasterIp": "118.24.246.22",
          "EmrVersion": "EMR-V2.0.1",
          "ChargeType": 1
        }
      ]
    },
    "RequestId": "e83dffa2-34be-4069-bb35-5a62f11e6d45"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=emr&Version=2019-01-03&Action=DescribeInstances)

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
| InternalError.Test | the optional spec saled out。 |
