## Description

This operation (Delete Vault) deletes a vault. Ensure that there is no archive in the vault and there have been no writes to the vault. When you delete a vault, the vault access policy attached to the vault is also deleted. If the request is successful, 204 No Content is returned.

Cross-account deletion is supported. The UID is "-" when you delete the vault from the current account.

## Request

### Request syntax

```HTTP
DELETE /<UID>/vaults/<VaultName> HTTP 1.1
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

No response content
