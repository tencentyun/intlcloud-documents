## Description

This operation (Delete Vault Access Policy) deletes the access policy associated with the specified vault.

The access policy can only be deleted by the account that owns the vault, whose UID is "-". If the request is successful, 204 No Content is returned.

## Request

### Request syntax

```HTTP
DELETE /<UID>/vaults/<VaultName>/access-policy HTTP 1.1
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

No response content.
