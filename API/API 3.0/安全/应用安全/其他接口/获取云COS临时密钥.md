## 1. 接口描述

接口请求域名： ms.tencentcloudapi.com 。

获取云COS文件存储临时密钥，密钥仅限于临时上传文件，有访问限制和时效性。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见[公共请求参数](/document/api/283/17745)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：CreateCosSecKeyInstance |
| Version | 是 | String | 公共参数，本接口取值：2018-04-08 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| CosRegion | 否 | String | 地域信息，例如广州：ap-guangzhou，上海：ap-shanghai，默认为广州。 |
| Duration | 否 | Integer | 密钥有效时间，默认为1小时。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| CosAppid | Integer | COS密钥对应的AppId|
| CosBucket | String | COS密钥对应的存储桶名|
| CosRegion | String | 存储桶对应的地域|
| ExpireTime | Integer | 密钥过期时间|
| CosId | String | 密钥ID信息|
| CosKey | String | 密钥KEY信息|
| CosTocken | String | 密钥TOCKEN信息|
| CosPrefix | String | 密钥可访问的文件前缀人。例如：CosPrefix=test/123/666，则该密钥只能操作test/123/666为前缀的文件，例如test/123/666/1.txt|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 获取COS临时密钥

#### 输入示例

```
https://ms.tencentcloudapi.com/?Action=CreateCosSecKeyInstance
&CosRegion=ap-guangzhou
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "ExpireTime": 3600,
    "CosKey": "55VuqLWV4HKvuYom4tYkn6FdXpVoM7hz",
    "CosBucket": "ms-shield",
    "CosRegion": "ap-guangzhou",
    "CosAppid": 123456,
    "CosPrefix": "pctool/123456789/1542613158",
    "RequestId": "ce5e66e0-aab5-4d31-9b98-c52caf0fdfae",
    "CosTocken": "13606435fd46b2765dd01aa4eaf356dfca88817030001",
    "CosId": "AKIDzgG3O5Cm9ii31sTgph1XhFISnvKPw0Zi"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=ms&Version=2018-04-08&Action=CreateCosSecKeyInstance)

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

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见[公共错误码](/document/api/283/17747#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| InternalError | 内部错误。 |
| InternalError.ServerError | 服务端无法响应。 |
| ResourceUnavailable | 资源不可用。 |
