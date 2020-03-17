## AttributeKeyDetail

AttributeKey值详情

被如下接口引用：GetAttributeKey。

| 名称 | 类型 | 必选 | 描述 |
|------|------|----------|------|
| Label | String | 是 | 中文标签 |
| LabelType | String | 是 | 输入框类型 |
| Order | Integer | 是 | 展示排序 |
| Starter | String | 是 | 初始化展示 |
| Value | String | 是 | AttributeKey值 |

## AuditSummary

跟踪集概览

被如下接口引用：ListAudits。

| 名称 | 类型 | 必选 | 描述 |
|------|------|----------|------|
| AuditName | String | 否 | 跟踪集名称 |
| AuditStatus | Integer | 否 | 跟踪集状态，1：开启，0：关闭 |
| CosBucketName | String | 否 | COS存储桶名称 |
| LogFilePrefix | String | 否 | 日志前缀 |

## CmqRegionInfo

cmq地域信息

被如下接口引用：ListCmqEnableRegion。

| 名称 | 类型 | 必选 | 描述 |
|------|------|----------|------|
| CmqRegion | String | 否 | cmq地域 |
| CmqRegionName | String | 否 | 地域描述 |

## CosRegionInfo

cmq地域信息

被如下接口引用：ListCosEnableRegion。

| 名称 | 类型 | 必选 | 描述 |
|------|------|----------|------|
| CosRegion | String | 否 | cos地域 |
| CosRegionName | String | 否 | 地域描述 |

## Event

日志详情

被如下接口引用：LookUpEvents。

| 名称 | 类型 | 必选 | 描述 |
|------|------|----------|------|
| Resources | [Resource](#Resource) | 否 | 资源对 |
| AccountID | Integer | 否 | 主账号ID |
| CloudAuditEvent | String | 否 | 日志详情 |
| ErrorCode | Integer | 否 | 鉴权错误码 |
| EventId | String | 否 | 日志ID |
| EventName | String | 否 | 事件名称 |
| EventNameCn | String | 否 | 事件名称中文描述（此字段请按需使用，如果您是其他语言使用者，可以忽略该字段描述） |
| EventRegion | String | 否 | 事件地域 |
| EventSource | String | 否 | 请求来源 |
| EventTime | String | 否 | 事件时间 |
| RequestID | String | 否 | 请求ID |
| ResourceRegion | String | 否 | 资源地域 |
| ResourceTypeCn | String | 否 | 资源类型中文描述（此字段请按需使用，如果您是其他语言使用者，可以忽略该字段描述） |
| SecretId | String | 否 | 证书ID |
| SourceIPAddress | String | 否 | 源IP |
| Username | String | 否 | 用户名 |

## LookupAttribute

检索条件

被如下接口引用：LookUpEvents。

| 名称 | 类型 | 必选 | 描述 |
|------|------|----------|------|
| AttributeKey | String | 是 | AttributeKey的有效取值范围是:RequestId、EventName、ReadOnly、Username、ResourceType、ResourceName和AccessKeyId，EventId |
| AttributeValue | String | 否 | AttributeValue |

## Resource

资源类型

被如下接口引用：LookUpEvents。

| 名称 | 类型 | 必选 | 描述 |
|------|------|----------|------|
| ResourceName | String | 否 | 资源名称 |
| ResourceType | String | 否 | 资源类型 |

