
## API Description
  This API (GetAuditServiceStatus) is used to query whether CloudAudit is enabled.
Domain name for API access: `cloudaudit.api.qcloud.com`

## Request Parameters
| Parameter Name | Required | Type | Description |
|---------|---------|---------|--------|
| ownerUin |	Yes |	Number |	Primary account, which is parsed automatically by Tencent Cloud APIs. |

## Response Parameters


| Parameter Name | Type | Description |
|---------|---------|---------|
| status | Number | Audit status. 0: Disabled; 1: Enabled. |


## Example
### Request

```
{
   "ownerUin": Number
}
```
### Response

```
{
   "status":0
}
```

