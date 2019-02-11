
## API Description
ListAudits is used to fetch the CloudAudit list.
Domain name for API access: `cloudaudit.api.qcloud.com`

## Response Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| auditLists | Array | The list of tracking sets |

The parameter auditLists is as follows:

| Parameter Name | Type | Description |
|---------|---------|---------|
| Name | String | CloudAudit name |
| bucketName | String | COS bucket name |
| prefix | String | Log prefix |
| status | Number | Audit status. 0: Disabled; 1: Enabled. |
| IsMultiRegionAudit | Number | Indicates whether to enable multi-region collection. 0: No; 1: Yes. |

## Example
### Request

```
{
}
```
### Response

```
{
    "auditLists": [
        {
            "name": "xxx-1",
            "bucketName":"xxx",
            "prefix":"xxx",
            "status":1,
            "IsMultiRegionAudit":0
        },
        {
            "name": "xxx-1",
            "bucketName":"xxx",
            "prefix":"xxx",
            "status":1
            "IsMultiRegionAudit":0
        }
    ]
}
```

