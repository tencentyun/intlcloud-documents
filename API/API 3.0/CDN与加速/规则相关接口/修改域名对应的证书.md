## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

本接口（ModifyCertificate）用于修改监听器下的域名对应的证书。该接口仅适用于version3.0的通道。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：ModifyCertificate |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| ListenerId | 是 | String | 监听器实例ID |
| Domain | 是 | String | 需要修改证书的域名 |
| CertificateId | 是 | String | 新的服务器证书ID。其中：<br/>当CertificateId=default时，表示使用监听器的证书。 |
| ClientCertificateId | 否 | String | 新的客户端证书ID。其中：<br/>当ClientCertificateId=default时，表示使用监听器的证书。<br/>仅当采用双向认证方式时，需要设置该参数。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 修改域名对应的证书

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=ModifyCertificate
&ListenerId=listener-xxx
&Domain=www.test.com
&CertificateId=cert-12345678
&ClientCertificateId=cert-abcdefgh
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "c7bfcad5-3f20-472f-9afc-13a66faebad8"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=ModifyCertificate)

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
| FailedOperation.ListenerHasTask | 监听器正在操作中，请勿重复操作。 |
| FailedOperation.ProxyVersionNotSupport | 不支持该版本通道。 |
| InternalError | 内部错误 |
| InvalidParameter | 参数错误 |
| InvalidParameterValue | 参数取值错误 |
| MissingParameter | 缺少参数错误 |
| ResourceNotFound | 资源不存在 |
| ResourceUnavailable | 资源不可用 |
| UnknownParameter | 未知参数错误 |
