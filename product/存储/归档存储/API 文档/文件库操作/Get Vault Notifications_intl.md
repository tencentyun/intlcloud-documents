## Description

This operation (Get Vault Notifications) retrieves the notification-configuration subresource set on the vault.

## Request

### Request syntax

```HTTP
GET /<UID>/vaults/<VaultName>/notification-configuration HTTP 1.1
Host:cas.<Region>.myqcloud.com
Date:date
Authorization: Auth
```

### Request parameters

No additional request parameters are needed.

### Request headers

No additional request headers are needed except the headers described in "Common Request Headers".

### Request content

No request content

## Response

### Response headers

No additional response headers are needed except the headers described in "Common Request Headers".

### Response content

| Name | Description | Type |
| ----------- | ---------------------------------------- | ------ |
| CallBackUrl | HTTP address of callback | String |
| Event | Events triggered by callback. Enumerated values: `ArchiveRetrievalCompleted`, `InventoryRetrievalCompleted`, `PushToCOSCompleted` and `PullFromCOSCompleted` | String |

```JSON
{
   "CallBackUrl": String,
   "Events":[String, ...] 
}
```


