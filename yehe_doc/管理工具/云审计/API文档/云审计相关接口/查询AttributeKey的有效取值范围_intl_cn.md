## 1. 接口描述

接口请求域名： cloudaudit.tencentcloudapi.com 。

查询AttributeKey的有效取值范围

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](https://intl.cloud.tencent.com/document/api/1021/34192)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：GetAttributeKey。 |
| Version | 是 | String | 公共参数，本接口取值：2019-03-19。 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](https://intl.cloud.tencent.com/document/api/1021/34192#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| WebsiteType | 否 | String | 网站类型，取值范围是zh和en。如果不传值默认zh |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| AttributeKeyDetails | Array of [AttributeKeyDetail](https://intl.cloud.tencent.com/document/api/1021/34209#AttributeKeyDetail) | AttributeKey的有效取值范围|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询AttributeKey的有效取值范围

查询AttributeKey的有效取值范围

#### 输入示例

```
https://cloudaudit.tencentcloudapi.com/?Action=GetAttributeKey
&WebsiteType=zh
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "6d833833-bbc6-4463-9a8f-6cc62d3a2afd",
    "AttributeKeyDetails": [
      {
        "Label": "只读",
        "Value": "ReadOnly",
        "Starter": "选择只读值",
        "LabelType": "select",
        "Order": 1
      },
      {
        "Label": "访问密钥",
        "Value": "AccessKeyId",
        "Starter": "输入访问密钥",
        "LabelType": "text",
        "Order": 2
      },
      {
        "Label": "请求ID",
        "Value": "RequestId",
        "Starter": "输入请求ID",
        "LabelType": "text",
        "Order": 3
      },
      {
        "Label": "事件名称",
        "Value": "EventName",
        "Starter": "选择事件名称",
        "LabelType": "select",
        "Order": 4
      },
      {
        "Label": "资源名称",
        "Value": "ResourceName",
        "Starter": "输入资源名称",
        "LabelType": "text",
        "Order": 5
      },
      {
        "Label": "资源类型",
        "Value": "ResourceType",
        "Starter": "选择资源类型",
        "LabelType": "select",
        "Order": 6
      },
      {
        "Label": "用户名称",
        "Value": "Username",
        "Starter": "选择用户名称",
        "LabelType": "select",
        "Order": 7
      }
    ]
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cloudaudit&Version=2019-03-19&Action=GetAttributeKey)

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
| InternalError.SearchError | 内部错误，请联系开发人员 |
