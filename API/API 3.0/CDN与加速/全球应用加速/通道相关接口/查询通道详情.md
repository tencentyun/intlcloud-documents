## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

本接口（DescribeProxyDetail）用于查询通道详情。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeProxyDetail |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| ProxyId | 是 | String | 需查询的通道ID。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| ProxyDetail | [ProxyInfo](/document/api/608/37023#ProxyInfo) | 通道详情信息。|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询通道详情

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=DescribeProxyDetail
&ProxyId=link-12345678
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "ProxyDetail": {
      "Status": "CREATING",
      "Domain": "",
      "InstanceId": "link-01vm81tj",
      "AccessRegion": "EastChina",
      "ProxyId": "link-01vm81tj",
      "ProjectId": 0,
      "AccessRegionInfo": {
        "RegionId": "EastChina",
        "RegionName": "中国大陆-华东"
      },
      "RealServerRegion": "NorthChina",
      "CreateTime": "2019-03-21 21:33:45",
      "SupportProtocols": [
        "TCP",
        "UDP",
        "HTTP",
        "HTTPS"
      ],
      "Concurrent": 2,
      "Bandwidth": 10,
      "Version": "2.0",
      "PolicyId": null,
      "Scalarable": 1,
      "IP": "",
      "ProxyName": "fff",
      "GroupId": null,
      "RealServerRegionInfo": {
        "RegionId": "NorthChina",
        "RegionName": "中国大陆-华北"
      },
      "TagSet": [
        {
          "TagKey": "gaaptest",
          "TagValue": "www"
        }
      ]
    },
    "RequestId": "1c54137e-e4da-42e1-8565-1bc2d99794a3"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=DescribeProxyDetail)

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

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](/document/api/608/36938#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| FailedOperation | 操作失败 |
| FailedOperation.ResourceCanNotAccess | 该资源不可访问。 |
| InternalError | 内部错误 |
| InvalidParameter | 参数错误 |
| InvalidParameterValue | 参数取值错误 |
| InvalidParameterValue.ProjectIdNotBelong | 项目不属于该用户。 |
| MissingParameter | 缺少参数错误 |
| ResourceNotFound | 资源不存在 |
| UnauthorizedOperation | 未授权操作 |
| UnknownParameter | 未知参数错误 |
