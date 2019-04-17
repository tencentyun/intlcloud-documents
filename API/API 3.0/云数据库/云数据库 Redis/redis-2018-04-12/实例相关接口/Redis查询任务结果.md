## 1. 接口描述

接口请求域名： redis.tencentcloudapi.com 。

用于查询任务结果

默认接口请求频率限制：20次/秒。

注意：本接口支持金融区地域。由于金融区和非金融区是隔离不互通的，因此当公共参数 Region 为金融区地域（例如 ap-shanghai-fsi）时，需要同时指定带金融区地域的域名，最好和 Region 的地域保持一致，例如：redis.ap-shanghai-fsi.tencentcloudapi.com 。



## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见[公共请求参数](/document/api/239/20005)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeTaskInfo |
| Version | 是 | String | 公共参数，本接口取值：2018-04-12 |
| Region | 是 | String | 公共参数，详见产品支持的[地域列表](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| TaskId | 是 | Integer | 任务ID |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| Status | String | 任务状态preparing:待执行，running：执行中，succeed：成功，failed：失败，error 执行出错|
| StartTime | String | 任务开始时间|
| TaskType | String | 任务类型|
| InstanceId | String | 实例的ID|
| TaskMessage | String | 任务信息，错误时显示错误信息。执行中与成功则为空|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 请求示例

#### 输入示例

```
https://redis.tencentcloudapi.com/?Action=DescribeTaskInfo
&TaskId=18215
&<公共请求参数>
```

#### 输出示例

```
{
    "Response": {
        "Status": "succeed",
        "StartTime": "2018-11-01 17:25:14",
        "TaskType": "redis缓存清空流程",
        "InstanceId": "crs-09u2u96z",
        "TaskMessage": "",
        "RequestId": "81120ab8-fea0-41ab-af7e-283c0348c4fc"
    }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeTaskInfo)

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

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见[公共错误码](/document/api/239/20007#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| FailedOperation.SystemError | 内部系统错误，和业务无关。 |
| InvalidParameter.InvalidParameter | 业务参数错误。 |
