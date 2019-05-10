## 1. 接口描述

接口请求域名： vod.tencentcloudapi.com 。

对来源为 URL 的音视频媒体发起处理任务，功能包括：

1. 智能内容审核（鉴黄、鉴恐、鉴政）；
2. 智能内容分析（标签、分类、封面）。

默认接口请求频率限制：100次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见[公共请求参数](/document/api/266/31756)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：ProcessMediaByUrl |
| Version | 是 | String | 公共参数，本接口取值：2018-07-17 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| InputInfo | 否 | [MediaInputInfo](/document/api/266/31773#MediaInputInfo) | 输入视频信息，包括视频 URL ， 名称、视频自定义 ID。 |
| OutputInfo | 否 | [MediaOutputInfo](/document/api/266/31773#MediaOutputInfo) | 输出文件 COS 路径信息。 |
| AiContentReviewTask | 否 | [AiContentReviewTaskInput](/document/api/266/31773#AiContentReviewTaskInput) | 视频内容审核类型任务参数。 |
| AiAnalysisTask | 否 | [AiAnalysisTaskInput](/document/api/266/31773#AiAnalysisTaskInput) | 视频内容分析类型任务参数。 |
| TasksPriority | 否 | Integer | 任务流的优先级，数值越大优先级越高，取值范围是 -10 到 10，不填代表 0。 |
| TasksNotifyMode | 否 | String | 任务流状态变更通知模式，可取值有 Finish，Change 和 None，不填代表 Finish。 |
| SessionContext | 否 | String | 来源上下文，用于透传用户请求信息，任务流状态变更回调将返回该字段值，最长 250 个字符。 |
| SessionId | 否 | String | 用于去重的识别码，如果七天内曾有过相同的识别码的请求，则本次的请求会返回错误。最长 50 个字符，不带或者带空字符串表示不做去重。 |
| SubAppId | 否 | Integer | 点播[子应用](/document/product/266/14574) ID。如果要访问子应用中的资源，则将该字段填写为子应用 ID；否则无需填写该字段。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| TaskId | String | 任务 ID|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 发起内容审核任务

对 URL 为 http://www.abc.com/abc.mp4 的视频发起内容审核任务。

#### 输入示例

```
https://vod.tencentcloudapi.com/?Action=ProcessMediaByUrl
&InputInfo.Url=http://www.abc.com/abc.mp4
&InputInfo.Name=大国外交
&InputInfo.Id=872988202
&OutputInfo.Region=ap-guangzhou
&OutputInfo.Bucket=myoutputbucket-1256244234
&OutputInfo.Dir=/output/test/
&AiContentReviewTask.Definition=10
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "5ca61e3a-6b8e-4b4e-9256-fdc701190064ef0",
    "TaskId": "125xxxxxx07-procedurev2-893dc41e6fdc22dcf24aa6e9c61cp94"
  }
}
```

### 示例2 发起内容分析任务

对 URL 为 http://www.abc.com/abc.mp4 的视频发起内容分析任务。

#### 输入示例

```
https://vod.tencentcloudapi.com/?Action=ProcessMediaByUrl
&InputInfo.Url=http://www.abc.com/abc.mp4
&InputInfo.Name=大国外交
&InputInfo.Id=872988202
&OutputInfo.Region=ap-guangzhou
&OutputInfo.Bucket=myoutputbucket-1256244234
&OutputInfo.Dir=/output/test/
&AiAnalysisTask.Definition=10
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "5ca61e3a-6b8e-4b4e-9256-fdc701190064ef0",
    "TaskId": "125xxxxxx07-procedurev2-813dc41e6fdc22dcf24aa6e9c61cp92"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=ProcessMediaByUrl)

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

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见[公共错误码](/document/api/266/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| FailedOperation.TaskDuplicate | 操作失败：任务重复。 |
| InternalError | 内部错误。 |
| InternalError.GetFileInfoError | 内部错误：获取媒体文件信息错误。 |
| InvalidParameter | 参数错误。 |
| InvalidParameterValue.AiAnalysisTaskDefinition | 参数值错误：AI 分析 Definition。 |
| InvalidParameterValue.AiContentReviewTaskDefinition | 参数值错误：AI 内容审核 Definition。 |
| InvalidParameterValue.SessionContextTooLong | SessionContext 过长。 |
| InvalidParameterValue.SessionId | 去重识别码重复，请求被去重。 |
| InvalidParameterValue.SessionIdTooLong | SessionId 过长。 |
| InvalidParameterValue.SubAppId | 参数值错误：子应用 ID。 |
