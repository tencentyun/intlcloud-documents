## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

本接口（ModifyRuleAttribute）用于修改转发规则的信息，包括健康检查的配置以及转发策略。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：ModifyRuleAttribute |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| ListenerId | 是 | String | 监听器ID |
| RuleId | 是 | String | 转发规则ID |
| Scheduler | 否 | String | 调度策略，其中：<br/>rr，轮询；<br/>wrr，加权轮询；<br/>lc，最小连接数。 |
| HealthCheck | 否 | Integer | 源站健康检查开关，其中：<br/>1，开启；<br/>0，关闭。 |
| CheckParams | 否 | [RuleCheckParams](/document/api/608/37023#RuleCheckParams) | 健康检查配置参数 |
| Path | 否 | String | 转发规则路径 |
| ForwardProtocol | 否 | String | 加速通道转发到源站的协议类型，支持：default, HTTP和HTTPS。<br/>当ForwardProtocol=default时，表示使用对应监听器的ForwardProtocol。 |
| ForwardHost | 否 | String | 加速通道转发到源站的请求中携带的host。<br/>当ForwardHost=default时，使用规则的域名，其他情况为该字段所设置的值。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 修改转发规则信息

修改转发规则信息

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=ModifyRuleAttribute
&RuleId=rule-5g8dh58
&ListenerId=listener-8fueuc9
&Path=/
&Scheduler=rr
&HealthCheck=0
&CheckParam=null
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

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=ModifyRuleAttribute)

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
| FailedOperation.InstanceStatusNotInRuning | 通道状态为非运行状态，无法操作。 |
| FailedOperation.ListenerHasTask | 监听器正在操作中，请勿重复操作。 |
| FailedOperation.RuleAlreadyExisted | 规则已经存在。 |
| InternalError | 内部错误 |
| InvalidParameter | 参数错误 |
| InvalidParameterValue | 参数取值错误 |
| MissingParameter | 缺少参数错误 |
| UnauthorizedOperation | 未授权操作 |
