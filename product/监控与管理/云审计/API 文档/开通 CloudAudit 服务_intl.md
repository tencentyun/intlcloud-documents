
## API Description
The API OpenAuditService is used to enable the CloudAudit service.
Domain name for API access: `cloudaudit.api.qcloud.com`


## Request Parameters
| Parameter Name | Required | Type | Description |
|---------|---------|---------|--------|
| ownerUin |	Yes |	Number |	Primary account, which is parsed automatically by Tencent Cloud APIs. |
| Uin |	Yes |	Number |	Account number, which is parsed automatically by Tencent Cloud APIs. |
| clientIp |	Yes	| String	| User IP |
| clientUa |	Yes |	String	| Client UA |
> **Note:**
> Each user can create up to 50 CloudAudits.

## Response Parameters
The response parameter is null.

## Example
### Request

```
{
   "ownerUin": 1150691759,
   "Uin": 1150691759,
   "clientIp": "127.0.0.1",
   "clientUa": "Chrome"
}
```
### Response

```
{
}
```

