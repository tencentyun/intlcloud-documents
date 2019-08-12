## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

本接口（BindListenerRealServers）用于TCP/UDP监听器绑定解绑源站。
注意：本接口会解绑之前绑定的源站，绑定本次调用所选择的源站。例如：原来绑定的源站为A，B，C，本次调用的选择绑定的源站为C，D，E，那么调用后所绑定的源站为C，D，E。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：BindListenerRealServers |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| ListenerId | 是 | String | 监听器ID |
| RealServerBindSet.N | 否 | Array of [RealServerBindSetReq](/document/api/608/37023#RealServerBindSetReq) | 待绑定源站列表 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 监听器绑定源站

监听器绑定源站

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=BindListenerRealServers
&ListenerId=listener-pbsgn7ej
&RealServerBindSet.0.RealServerId=rs-04v3s12t
&RealServerBindSet.0.RealServerIP=119.28.69.101
&RealServerBindSet.0.RealServerPort=80
&RealServerBindSet.0.RealServerWeight=1
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "1f1e794d-a35e-41d2-8f40-fe32a2077329"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=BindListenerRealServers)

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
| FailedOperation.GroupStatusNotInRuning | 通道组状态为非运行状态，无法操作。 |
| FailedOperation.InstanceStatusNotInRuning | 通道状态为非运行状态，无法操作。 |
| FailedOperation.LimitRealServerNum | 绑定源站数量超过限制。 |
| InternalError | 内部错误 |
| InvalidParameter | 参数错误 |
| InvalidParameterValue | 参数取值错误 |
| InvalidParameterValue.RealServerNotBelong | 源站不属于该用户。 |
| MissingParameter | 缺少参数错误 |
| ResourceNotFound | 资源不存在 |
| UnauthorizedOperation | 未授权操作 |
