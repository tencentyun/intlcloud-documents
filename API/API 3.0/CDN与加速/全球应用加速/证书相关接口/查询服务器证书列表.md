## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

本接口（DescribeCertificates）用来查询可以使用的证书列表。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeCertificates |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| CertificateType | 否 | Integer | 证书类型。其中：<br/>0，表示基础认证配置；<br/>1，表示客户端CA证书；<br/>2，表示服务器SSL证书；<br/>3，表示源站CA证书；<br/>4，表示通道SSL证书。<br/>-1，所有类型。<br/>默认为-1。 |
| Offset | 否 | Integer | 偏移量，默认为0。 |
| Limit | 否 | Integer | 限制数量，默认为20。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| CertificateSet | Array of [Certificate](/document/api/608/37023#Certificate) | 服务器证书列表，包括证书ID 和证书名称。|
| TotalCount | Integer | 满足查询条件的服务器证书总数量。|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询服务器证书信息

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=DescribeCertificates
&CertificateType=2
&Offset=0
&Limit=1
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "TotalCount": 19,
    "RequestId": "35d85baa-eeb8-4eb5-96a9-b6d27f4ff92c",
    "CertificateSet": [
      {
        "CertificateId": "cert-8k1l0pat",
        "SubjectCN": "lagameft01.xyz",
        "CertificateAlias": "test",
        "CertificateName": "test",
        "BeginTime": 1554134400,
        "CertificateType": 2,
        "EndTime": 1585713600,
        "CreateTime": 1564557014,
        "IssuerCN": "TrustAsia TLS RSA CA"
      }
    ]
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=DescribeCertificates)

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
| UnauthorizedOperation | 未授权操作 |
| UnknownParameter | 未知参数错误 |
| UnsupportedOperation | 不支持该操作。 |
