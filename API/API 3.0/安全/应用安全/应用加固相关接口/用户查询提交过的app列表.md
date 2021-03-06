## 1. 接口描述

接口请求域名： ms.tencentcloudapi.com 。

本接口用于查看app列表。
可以通过指定任务唯一标识ItemId来查询指定app的详细信息，或通过设定过滤器来查询满足过滤条件的app的详细信息。 指定偏移(Offset)和限制(Limit)来选择结果中的一部分，默认返回满足条件的前20个app信息。


默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见[公共请求参数](https://cloud.tencent.com/document/api/283/17745)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeShieldInstances |
| Version | 是 | String | 公共参数，本接口取值：2018-04-08 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| Filters.N | 否 | Array of [Filter](https://cloud.tencent.com/document/api/283/17759#Filter) | 支持通过app名称，app包名，加固的服务版本，提交的渠道进行筛选。 |
| Offset | 否 | Integer | 偏移量，默认为0。 |
| Limit | 否 | Integer | 数量限制，默认为20，最大值为100。 |
| ItemIds.N | 否 | Array of String | 可以提供ItemId数组来查询一个或者多个结果。注意不可以同时指定ItemIds和Filters。 |
| OrderField | 否 | String | 按某个字段排序，目前仅支持TaskTime排序。 |
| OrderDirection | 否 | String | 升序（asc）还是降序（desc），默认：desc。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| TotalCount | Integer | 符合要求的app数量|
| AppSet | Array of [AppSetInfo](https://cloud.tencent.com/document/api/283/17759#AppSetInfo) | 一个关于app详细信息的结构体，主要包括app的基本信息和加固信息。|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询加固实例列表

#### 输入示例

```
https://ms.tencentcloudapi.com/?Action=DescribeShieldInstances
&Filters.0.Name=AppName
&Filters.0.Value=wechat
&Filters.1.Name=AppPkgName
&Filters.1.Value=com.tencent.mm
&Offset=0
&Limit=20
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "TotalCount": 10,
    "RequestId": "5e93a212-ca01-0fdc-eedd-5a1fce5e83e6",
    "AppSet": [
      {
        "ItemId": "1234-xcse-ddw1",
        "AppMd5": "der2331ds",
        "AppUrl": "https://www.example.com/a.apk",
        "ShieldMd5": "ae5df985a27b07f56d8c670fef70d7c9",
        "ShieldSize": 1193311,
        "AppName": "微信",
        "ShieldCode": 0,
        "ServiceEdition": "basic",
        "AppVersion": "6.5",
        "TaskStatus": 1,
        "TaskTime": 1524744997,
        "AppSize": 123454,
        "AppPkgName": "com.tencent.mm",
        "AppIconUrl": "https://wwww.example.com/12334"
      }
    ]
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=ms&Version=2018-04-08&Action=DescribeShieldInstances)

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

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见[公共错误码](https://cloud.tencent.com/document/api/283/17747#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| InternalError.ServerError | 服务端无法响应。 |
| InvalidParameterValue.InvalidCoexistItemIdsFilters | 不能同时指定ItemIds和Filters。 |
| InvalidParameterValue.InvalidFilter | 无效的过滤器。 |
| InvalidParameterValue.InvalidItemIds | ItemIds不合法。 |
| InvalidParameterValue.InvalidLimit | Limit不是有效的数字。 |
| InvalidParameterValue.InvalidOffset | Offset不是有效的数字。 |
| InvalidParameterValue.InvalidOrderDirection | OrderDirection参数。 |
| InvalidParameterValue.InvalidOrderField | OrderField取值不合法。 |
