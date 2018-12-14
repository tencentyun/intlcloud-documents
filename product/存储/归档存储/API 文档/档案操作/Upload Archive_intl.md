## Description

This API (Upload Archive) is used to upload an archive to the specified vault. If the request is successful, the x-cas-archive-id that uniquely identifies the archive as well as "201 Created" are returned.

When uploading an archive, you can specify x-cas-archive-description to use as a comment on the archive content.

Cross-account operation is supported. The UID is "-" when the operation is performed in the account that owns the vault.

## Request

### Request syntax

```http
POST /<UID>/vaults/<VaultName>/archives HTTP/1.1
Host: cas.<Region>.myqcloud.com
Date: date
Authorization: Auth
Content-Length: length
x-cas-content-sha256: sha256
x-cas-sha256-tree-hash: sha256
x-cas-archive-description: description

[Archive]
```

### Request parameters

No additional request parameters are needed.

### Request headers

#### Required headers

| Name | Description | Type | Required |
| ---------------------- | ------------------------------ | ------ | ---- |
| x-cas-content-sha256 | The SHA256 checksum (linear hash) of the archive | String | Yes |
| Content-Length | HTTP request length defined in RFC 2616 (in bytes). | String | Yes |
| x-cas-sha256-tree-hash | The SHA256 tree-hash checksum of the archive. | String | Yes |

#### Recommended headers

| Name | Description | Type | Required |
| ------------------------- | ---------------------------- | ------ | ---- |
| x-cas-archive-description | The description of the archive. It is returned when the archive is read. | String | No    |

### Request content

Archive

## Response

### Response headers

| Name | Description | Type |
| ---------------------- | ------------------- | ------ |
| Location | The path to the archive when it is created successfully. | String |
| x-cas-archive-id | The ID of the archive. | String |
| x-cas-content-sha256 | The SHA256 checksum (linear hash) of the archive | String |
| x-cas-sha256-tree-hash | The SHA256 tree-hash checksum of the archive. | String |

### Response content

No response content

