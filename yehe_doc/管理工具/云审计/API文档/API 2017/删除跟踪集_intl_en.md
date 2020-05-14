
## API Description
The API `DeleteAudit` is used to delete a CloudAudit tracking set.
Domain name for API access: `cloudaudit.api.qcloud.com`

## Request Parameters
The following request parameter list only provides the API request parameters.

| Parameter | Required | Type | Description |
|---------|---------|---------|--------|
| Name | Yes | String | Tracking set name |

## Response Parameters
The response parameter is `OK`.

## Use Cases
### Request
```
{
   "Name":"String"
}
```

### Response
```
{
     "ok"
}
```
