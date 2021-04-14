## 1. 接口描述

接口请求域名： gme.tencentcloudapi.com 。

本接口(CreateApp)用于创建一个GME应用

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](https://cloud.tencent.com/document/api/607/35367)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：CreateApp |
| Version | 是 | String | 公共参数，本接口取值：2018-07-11 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| AppName | 是 | String | 应用名称 |
| ProjectId | 否 | Integer | 腾讯云项目id，默认为0，表示默认项目 |
| EngineList.N | 否 | Array of String | 需要支持的引擎列表，取值android, ios, uinty, cocos, unreal, windows。默认全选。 |
| RegionList.N | 否 | Array of String | 服务区域列表, 默认为空数组. 取值: mainland(美), sa(南美), eu(欧洲), oc(澳洲), me(中东)。默认全选 |
| RealtimeSpeechConf | 否 | [RealtimeSpeechConf](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/607/35375#RealtimeSpeechConf) | 实时语音服务配置数据 |
| VoiceMessageConf | 否 | [VoiceMessageConf](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/607/35375#VoiceMessageConf) | 离线语音服务配置数据 |
| VoiceFilterConf | 否 | [VoiceFilterConf](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/607/35375#VoiceFilterConf) | 语音过滤服务配置数据 |
| Tags.N | 否 | Array of [Tag](https://cloud.tencent.com/document/api/607/35375#Tag) | 需要添加的标签列表 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| BizId | Integer | 应用id，由后台自动生成。|
| AppName | String | 应用名称，透传输入参数的AppName|
| ProjectId | Integer | 项目id，透传输入的ProjectId|
| SecretKey | String | 应用密钥，GME SDK初始化时使用|
| CreateTime | Integer | 服务创建时间戳|
| RealtimeSpeechConf | [RealtimeSpeechConf](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/607/35375#RealtimeSpeechConf) | 实时语音服务配置数据|
| VoiceMessageConf | [VoiceMessageConf](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/607/35375#VoiceMessageConf) | 语音消息服务配置数据|
| VoiceFilterConf | [VoiceFilterConf](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/607/35375#VoiceFilterConf) | 语音过滤服务配置数据|

## 4. 示例

### 示例1 使用默认配置创建一个GME应用

最简单的创建一个GME应用

#### 输入示例

```
https://gme.tencentcloudapi.com/?Action=CreateApplication
&AppName=simple_gme_application
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "Data": {
      "AppName": "simple_gme_application",
      "CreateTime": 1568945078,
      "ProjectId": 0,
      "BizId": 140000001,
      "SecretKey": "abcdefghijklmnop",
      "RealtimeSpeechConf": {
        "Status": "open",
        "quality": "ordinary"
      },
      "VoiceMessageConf": {
        "Status": "close",
        "language": "cnen"
      },
      "VoiceFilterConf": {
        "Status": "close"
      }
    },
    "RequestId": "e2900289-f21e-43a8-a3bf-0b439cdbbbb8"
  }
}
```

### 示例2 使用自定义配置，创建一个GME应用

使用项目10000，开启实时语音服务，使用高音质；关闭离线语音服务； 开启语音过滤服务

#### 输入示例

```
https://gme.tencentcloudapi.com/?Action=CreateApplication
&AppName=simple_gme_application
&ProjectId=10000，
&RealtimeSpeechConf.Status=open
&RealtimeSpecchConf.Quality=high
&VoiceMessageConf.Status=close
&VoiceFilterConf.Status=open
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "Data": {
      "AppName": "simple_gme_application",
      "CreateTime": 1568945078,
      "ProjectId": 10000,
      "BizId": 140000002,
      "SecretKey": "abcdefghijklmnop",
      "RealtimeSpeechConf": {
        "Status": "open",
        "Quality": "high"
      },
      "VoiceMessageConf": {
        "Status": "open",
        "Language": "cnen"
      },
      "VoiceFilterConf": {
        "Status": "open"
      }
    },
    "RequestId": "d61be8ca-f010-11e9-af81-fa163ee00eb7"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gme&Version=2018-07-11&Action=CreateApp)

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

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](https://cloud.tencent.com/document/api/607/35370#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| FailedOperation | 操作失败。 |
| FailedOperation.UserFeeNegative | 欠费不可操作。 |
| InternalError | 内部错误 |
| InvalidParameter | 参数错误 |
| InvalidParameter.TagKey | 标签不合法。 |
| UnauthorizedOperation | 未授权操作。 |
| UnauthorizedOperation.CreateAppDenied | 创建应用不被授权。 |
| UnknownParameter | 未知参数错误。 |
| UnsupportedOperation | 操作不支持 |
