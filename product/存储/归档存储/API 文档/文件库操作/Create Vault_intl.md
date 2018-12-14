## Description

This operation (Create Vault) creates a vault. You can create a maximum of 1,000 vaults per account. If the request is successful, 201 Created is returned.

Cross-account creation is supported. The UID is "-" when you create a vault under the current account.
## Request

### Request syntax

```HTTP
PUT /<UID>/vaults/<VaultName> HTTP 1.1
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

| Name | Description | Type |
| -------- | --------------- | ------ |
| Location | The relative URI path of the vault that was created. | String |

### Response content

No response content

