## 1. 接口描述

接口请求域名： cdn.tencentcloudapi.com 。

DisableCaches 用于禁用 CDN 上指定 URL 的访问，禁用完成后，全网访问会直接返回 403。（接口尚在内测中，暂未全量开放使用）

默认接口请求频率限制：40次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见[公共请求参数](https://cloud.tencent.com/document/api/228/30977)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DisableCaches |
| Version | 是 | String | 公共参数，本接口取值：2018-06-06 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| Urls.N | 是 | Array of String | 需要禁用的 URL 列表<br/>每次最多可提交 100 条，每日最多可提交 3000 条 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| CacheOptResult | [CacheOptResult](https://cloud.tencent.com/document/api/228/30987#CacheOptResult) | 提交结果<br/>注意：此字段可能返回 null，表示取不到有效值。|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 封禁示例

#### 输入示例

```
https://cdn.tencentcloudapi.com/?Action=DisableCaches
&Urls.0=http://example.com/path/to.jpg
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "f13cf55b-69e6-4937-8856-bd8965beea8c",
    "CacheOptResult": {
      "SuccessUrls": [
        "http://example.com/path/to.jpg"
      ],
      "FailUrls": []
    }
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdn&Version=2018-06-06&Action=DisableCaches)

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

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见[公共错误码](https://cloud.tencent.com/document/api/228/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| InternalError.CdnDbError | 内部数据错误，请联系腾讯云工程师进一步排查 |
| InternalError.CdnSystemError | 系统错误，请联系腾讯云工程师进一步排查 |
| InvalidParameter.CDNStatusInvalidDomain | 域名状态不合法。 |
| InvalidParameter.CdnHostInvalidParam | 域名格式不合法，请确认后重试 |
| InvalidParameter.CdnInterfaceError | 内部接口错误，请联系腾讯云工程师进一步排查 |
| InvalidParameter.CdnParamError | 参数错误，请参考文档中示例参数填充 |
| InvalidParameter.CdnStatInvalidDate | 日期不合法，请参考文档中日期示例 |
| InvalidParameter.CdnStatInvalidProjectId | 项目ID错误，请确认后重试 |
| LimitExceeded.CdnHostOpTooOften | 域名操作过于频繁。 |
| ResourceNotFound.CdnHostNotExists | 账号下无此域名，请确认后重试 |
| ResourceNotFound.CdnUserNotExists | 未开通CDN服务，请开通后使用此接口 |
| UnauthorizedOperation.CdnAccountUnauthorized | 子账号禁止查询整体数据。 |
| UnauthorizedOperation.CdnCamUnauthorized | 子账号未配置cam策略。 |
| UnauthorizedOperation.CdnUserAuthFail | CDN用户认证失败。 |
| UnauthorizedOperation.CdnUserAuthWait | CDN用户待认证。 |
| UnauthorizedOperation.CdnUserIsSuspended | 加速服务已停服，请重启加速服务后重试 |
| UnauthorizedOperation.CdnUserNoWhitelist | 非内测白名单用户，无该功能使用权限 |
