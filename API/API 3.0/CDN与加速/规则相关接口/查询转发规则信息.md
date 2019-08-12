## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

本接口（DescribeRules）用于查询监听器下的所有规则信息，包括规则域名，路径以及该规则下所绑定的源站列表。当通道版本为3.0时，该接口会返回该域名对应的高级认证配置信息。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeRules |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| ListenerId | 是 | String | 7层监听器Id。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| DomainRuleSet | Array of [DomainRuleSet](/document/api/608/37023#DomainRuleSet) | 按照域名分类的规则信息列表|
| TotalCount | Integer | 该监听器下的域名总数|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询转发规则信息

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=DescribeRules
&ListenerId=listener-9jt0rtv9
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "TotalCount": 1,
    "DomainRuleSet": [
      {
        "GaapCertificateAlias": "gaap-casfdgs",
        "Domain": "www.bbb.com",
        "CertificateId": "cert-mqkdxhcl",
        "RealServerCertificateId": "cert-76es2p6n",
        "CertificateAlias": "test1",
        "BasicAuth": 1,
        "GaapCertificateId": "cert-47teq6gt",
        "RealServerAuth": 1,
        "BasicAuthConfAlias": "basicAuth",
        "BasicAuthConfId": "cert-cqwokbyp",
        "ClientCertificateId": "cert-5n7ifekx",
        "RuleSet": [
          {
            "BindStatus": 1,
            "Domain": "www.bbb.com",
            "RealServerType": "IP",
            "RuleId": "rule-hh5xg2yd",
            "HealthCheck": 0,
            "ListenerId": "listener-9jt0rtv9",
            "CheckParams": {
              "Domain": "www.bbb.com",
              "ConnectTimeout": 2,
              "Path": "/",
              "Method": "HEAD",
              "DelayLoop": 30,
              "StatusCode": [
                100,
                200,
                300,
                400,
                500
              ]
            },
            "Scheduler": "rr",
            "Path": "/",
            "RuleStatus": 0,
            "RealServerSet": [
              {
                "RealServerStatus": 0,
                "RealServerPort": 234,
                "RealServerId": "rs-04v3s12c",
                "DownIPList": [],
                "RealServerWeight": 1,
                "RealServerIP": "4.4.4.4"
              },
              {
                "RealServerStatus": 0,
                "RealServerPort": 424,
                "RealServerId": "rs-10vtt5en",
                "DownIPList": [],
                "RealServerWeight": 1,
                "RealServerIP": "5.5.5.6"
              }
            ]
          }
        ],
        "GaapAuth": 1,
        "ClientCertificateAlias": "clientCA",
        "RealServerCertificateAlias": "rsca",
        "RealServerCertificateDomain": "www.bbb.com"
      }
    ],
    "RequestId": "6aecde5a-fd9a-4380-8fe9-1e9e4a98b7b5"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=DescribeRules)

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
| ResourceNotFound | 资源不存在 |
| UnauthorizedOperation | 未授权操作 |
