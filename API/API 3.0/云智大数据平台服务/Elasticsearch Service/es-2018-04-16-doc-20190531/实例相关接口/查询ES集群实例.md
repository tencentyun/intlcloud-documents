## 1. 接口描述

接口请求域名： es.tencentcloudapi.com 。

查询用户该地域下符合条件的所有实例

默认接口请求频率限制：20次/秒。

注意：本接口支持金融区地域。由于金融区和非金融区是隔离不互通的，因此当公共参数 Region 为金融区地域（例如 ap-shanghai-fsi）时，需要同时指定带金融区地域的域名，最好和 Region 的地域保持一致，例如：es.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/845/30623)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeInstances |
| Version | 是 | String | 公共参数，本接口取值：2018-04-16 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](/document/api/845/30623#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| Zone | 否 | String | 集群实例所属可用区，不传则默认所有可用区 |
| InstanceIds.N | 否 | Array of String | 集群实例ID列表 |
| InstanceNames.N | 否 | Array of String | 集群实例名称列表 |
| Offset | 否 | Integer | 分页起始值, 默认值0 |
| Limit | 否 | Integer | 分页大小，默认值20 |
| OrderByKey | 否 | Integer | 排序字段<li>1：实例ID</li><li>2：实例名称</li><li>3：可用区</li><li>4：创建时间</li>若orderKey未传递则按创建时间降序排序 |
| OrderByType | 否 | Integer | 排序方式<li>0：升序</li><li>1：降序</li>若传递了orderByKey未传递orderByType, 则默认升序 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| TotalCount | Integer | 返回的实例个数|
| InstanceList | Array of [InstanceInfo](/document/api/845/30634#InstanceInfo) | 实例详细信息列表|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询ES集群实例

根据给定条件查询符合条件的ES集群实例并返回详细信息

#### 输入示例

```
https://es.tencentcloudapi.com/?Action=DescribeInstances
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "TotalCount": 2,
    "InstanceList": [
      {
        "InstanceId": "es-sample",
        "InstanceName": "es-sample",
        "InstanceType": 2,
        "Region": "ap-guangzhou",
        "Zone": "ap-guangzhou-2",
        "AppId": 0,
        "Uin": "xxxxxxxx",
        "VpcUid": "vpc-sample",
        "SubnetUid": "subnet-sample",
        "Status": 1,
        "ChargeType": "PREPAID",
        "ChargePeriod": 1,
        "RenewFlag": "RENEW_FLAG_DEFAULT",
        "NodeType": "ES.S1.SMALL2",
        "NodeNum": 2,
        "CpuNum": 1,
        "MemSize": 2,
        "DiskType": "",
        "DiskSize": 100,
        "EsDomain": "es-sample.tencentelasticsearch.com",
        "EsVip": "0.0.0.0",
        "EsPort": 9200,
        "KibanaUrl": "https://es-sample.kibana.tencentelasticsearch.com:5601",
        "EsVersion": "5.6.4",
        "EsConfig": "{}",
        "EsAcl": {
          "WhiteIpList": [],
          "BlackIpList": []
        },
        "CreateTime": "2018-07-27 17:28:04",
        "UpdateTime": "2018-07-30 10:22:29",
        "Deadline": "2018-08-27 17:28:04"
      },
      {
        "InstanceId": "es-sample2",
        "InstanceName": "es-sample2",
        "InstanceType": 2,
        "Region": "ap-guangzhou",
        "Zone": "ap-guangzhou-4",
        "AppId": 0,
        "Uin": "xxxxxx",
        "VpcUid": "vpc-sample",
        "SubnetUid": "subnet-sample",
        "Status": 1,
        "ChargeType": "PREPAID",
        "ChargePeriod": 1,
        "RenewFlag": "RENEW_FLAG_DEFAULT",
        "NodeType": "ES.S1.MEDIUM4",
        "NodeNum": 2,
        "CpuNum": 2,
        "MemSize": 4,
        "DiskType": "",
        "DiskSize": 100,
        "EsDomain": "es-sample.tencentelasticsearch.com",
        "EsVip": "0.0.0.0",
        "EsPort": 9200,
        "KibanaUrl": "https://es-sample.kibana.tencentelasticsearch.com:5601",
        "EsVersion": "5.6.4",
        "EsConfig": "{}",
        "EsAcl": {
          "WhiteIpList": [],
          "BlackIpList": []
        },
        "CreateTime": "2018-07-26 17:47:47",
        "UpdateTime": "2018-07-26 18:16:50",
        "Deadline": "2018-08-26 17:47:47"
      }
    ],
    "RequestId": "5d5a201f-0a3d-485f-a82f-3c73ccca348a"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=es&Version=2018-04-16&Action=DescribeInstances)

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
| InternalError | 内部错误。 |
| InvalidParameter | 参数错误。 |
