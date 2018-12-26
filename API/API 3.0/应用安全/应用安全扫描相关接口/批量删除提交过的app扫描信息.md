## 1. 接口描述

接口请求域名： ms.tencentcloudapi.com 。

删除一个或者多个app扫描信息

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见[公共请求参数](/document/api/283/17745)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DeleteScanInstances |
| Version | 是 | String | 公共参数，本接口取值：2018-04-08 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| AppSids.N | 是 | Array of String | 删除一个或多个扫描的app，最大支持20个 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| Progress | Integer | 任务状态: 1-已完成,2-处理中,3-处理出错,4-处理超时|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 根据AppSid对扫描实例进行删除

#### 输入示例

```
https://ms.tencentcloudapi.com/?Action=DeleteScanInstances
&AppSids.0=hhussxu-hui2677-kk
&AppSids.1=xyuu-csu-ee78236l
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "Progress": 1,
    "RequestId": "5e93a212-ca01-0fdc-eedd-5a1fce5e83e6"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=ms&Version=2018-04-08&Action=DeleteScanInstances)

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
| LimitExceeded | 超过配额限制 |
