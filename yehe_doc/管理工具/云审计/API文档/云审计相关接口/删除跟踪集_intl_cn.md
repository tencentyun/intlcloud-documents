## 1. 接口描述

接口请求域名： cloudaudit.tencentcloudapi.com 。

删除跟踪集

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](https://intl.cloud.tencent.com/document/api/1021/34192)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DeleteAudit。 |
| Version | 是 | String | 公共参数，本接口取值：2019-03-19。 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](https://intl.cloud.tencent.com/document/api/1021/34192#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| AuditName | 是 | String | 跟踪集名称 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| IsSuccess | Integer | 是否删除成功|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 删除跟踪集

删除跟踪集

#### 输入示例

```
https://cloudaudit.tencentcloudapi.com/?Action=DeleteAudit
&AuditName=xxxxxx
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "IsSuccess": 1,
    "RequestId": "e27d42d6-855a-40fa-9b5f-462059502463"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cloudaudit&Version=2019-03-19&Action=DeleteAudit)

### SDK

云 API 3.0 提供了配套的开发工具集（SDK），支持多种编程语言，能更方便的调用 API。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### 命令行工具

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013)

## 6. 错误码

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](https://intl.cloud.tencent.com/document/api/1021/34195#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| InternalError.DeleteAuditError | 删除跟踪集失败，请联系开发人员 |
| ResourceNotFound.AuditNotExist | 跟踪集不存在 |
