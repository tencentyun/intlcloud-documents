
## API Description
The API `GetAuditServiceStatus` is used to query whether the tracking set is enabled.
Domain name for API access: `cloudaudit.api.qcloud.com`

## Request Parameters
| Parameter | Required | Type | Description |
|---------|---------|---------|--------|
| ownerUin |Yes |Number | Root account, which is parsed automatically by TencentCloud APIs. |

## Response Parameters


| Parameter | Type | Description |
|---------|---------|---------|
| status | Number | Audit status. 0: Disabled; 1: Enabled. |


## Use Cases
### Request

```
{
   "ownerUin": "Number"
}
```
### Response

```
{
   "status":0
}
```
