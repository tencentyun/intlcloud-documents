## AttributeKeyDetail

Details of AttributeKey value

Referenced by: GetAttributeKey.

| Name | Type | Required | Description |
|------|------|----------|------|
| Label | String | Yes | Label |
| LabelType | String | Yes | Input box type |
| Order | Integer | Yes | Display sort order |
| Starter | String | Yes | Initial display |
| Value | String | Yes | AttributeKey value |

## AuditSummary

Tracking set overview

Referenced by: ListAudits.

| Name | Type | Required | Description |
|------|------|----------|------|
| AuditName | String | No | Tracking set name |
| AuditStatus | Integer | No | Tracking set status. 1: enabled, 0: disabled |
| CosBucketName | String | No | COS bucket name |
| LogFilePrefix | String | No | Log prefix |

## CmqRegionInfo

CMQ region information

Referenced by: ListCmqEnableRegion.

| Name | Type | Required | Description |
|------|------|----------|------|
| CmqRegion | String | No | CMQ region |
| CmqRegionName | String | No | Region description |

## CosRegionInfo

CMQ region information

Referenced by: ListCosEnableRegion.

| Name | Type | Required | Description |
|------|------|----------|------|
| CosRegion | String | No | COS region |
| CosRegionName | String | No | Region description |

## Event

Log details

Referenced by: LookUpEvents.

| Name | Type | Required | Description |
|------|------|----------|------|
| Resources | [Resource](#Resource) | No | Resource pair |
| AccountID | Integer | No | Root account ID |
| CloudAuditEvent | String | No | Log details |
| ErrorCode | Integer | No | Authentication error code |
| EventId | String | No | Log ID |
| EventName | String | No | Event name |
| EventNameCn | String | No | Chinese description of the event name (please use this field as required; if you are using other languages, you can ignore this field) |
| EventRegion | String | No | Event region |
| EventSource | String | No | Request source |
| EventTime | String | No | Event time |
| RequestID | String | No | Request ID |
| ResourceRegion | String | No | Resource region |
| ResourceTypeCn | String | No | Chinese description of the resource type (please use this field as required; if you are using other languages, you can ignore this field) |
| SecretId | String | No | Certificate ID |
| SourceIPAddress | String | No | Source IP |
| Username | String | No | Username |

## LookupAttribute

Search criteria

Referenced by: LookUpEvents.

| Name | Type | Required | Description |
|------|------|----------|------|
| AttributeKey | String | Yes | Valid values of AttributeKey: RequestIdEventName, ReadOnly, Username, ResourceType, ResourceName, AccessKeyId, EventId |
| AttributeValue | String | No | AttributeValue |

## Resource

Resource type

Referenced by: LookUpEvents.

| Name | Type | Required | Description |
|------|------|----------|------|
| ResourceName | String | No | Resource name |
| ResourceType | String | No | Resource type |

