## 1. 接口描述

接口请求域名： cam.tencentcloudapi.com 。

查询SAML身份提供商详情

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](https://cloud.tencent.com/document/api/598/33158)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：GetSAMLProvider |
| Version | 是 | String | 公共参数，本接口取值：2019-01-16 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| Name | 是 | String | SAML身份提供商名称 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| Name | String | SAML身份提供商名称|
| Description | String | SAML身份提供商描述|
| CreateTime | Timestamp | SAML身份提供商创建时间|
| ModifyTime | Timestamp | SAML身份提供商上次修改时间|
| SAMLMetadata | String | SAML身份提供商元数据文档|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询身份提供商详情

查询身份提供商详情

#### 输入示例

```
https://cam.tencentcloudapi.com/?Action=GetSAMLProvider
&Name=okta
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "Name": "okta",
    "Description": "okta",
    "CreateTime": "2018-09-17 17:18:03",
    "ModifyTime": "2018-09-17 17:18:03",
    "SAMLMetadata": "U0FNTE1ldGFkYXRh"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cam&Version=2019-01-16&Action=GetSAMLProvider)

### SDK

云 API 3.0 提供了配套的开发工具集（SDK），支持多种编程语言，能更方便的调用 API。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### 命令行工具

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. 错误码

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](https://cloud.tencent.com/document/api/598/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| ResourceNotFound.IdentityNotExist | 身份提供商不存在。 |
| ResourceNotFound.NotFound | 资源不存在。 |
