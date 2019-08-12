## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

本接口（DescribeRealServers）用于查询源站信息，可以根据项目名查询所有的源站信息，此外支持指定IP机或者域名的源站模糊查询。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeRealServers |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| ProjectId | 是 | Integer | 查询源站的所属项目ID，-1表示所有项目 |
| SearchValue | 否 | String | 需要查询的源站IP或域名，支持模糊匹配 |
| Offset | 否 | Integer | 偏移量，默认值是0 |
| Limit | 否 | Integer | 返回数量，默认为20个，最大值为50个 |
| TagSet.N | 否 | Array of [TagPair](/document/api/608/37023#TagPair) | 标签列表，当存在该字段时，拉取对应标签下的资源列表。<br/>最多支持5个标签，当存在两个或两个以上的标签时，满足其中任意一个标签时，源站会被拉取出来。 |
| Filters.N | 否 | Array of [Filter](/document/api/608/37023#Filter) | 过滤条件。filter的name取值(RealServerName,RealServerIP) |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| RealServerSet | Array of [BindRealServerInfo](/document/api/608/37023#BindRealServerInfo) | 源站信息列表|
| TotalCount | Integer | 查询得到的源站数量|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询源站信息

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=DescribeRealServers
&ProjectId=0
&SearchValue='1.1.1.1'
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RealServerSet": [
      {
        "RealServerId": "rs123",
        "RealServerIP": "1.1.1.1",
        "RealServerName": "rsname",
        "ProjectId": 0,
        "TagSet": []
      }
    ],
    "TotalCount": 1,
    "RequestId": "5c680029-66b2-4be8-9630-7bd316ce70dd"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=DescribeRealServers)

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
| InternalError | 内部错误 |
| InvalidParameter | 参数错误 |
| InvalidParameterValue | 参数取值错误 |
| MissingParameter | 缺少参数错误 |
| ResourceUnavailable | 资源不可用 |
| UnknownParameter | 未知参数错误 |
