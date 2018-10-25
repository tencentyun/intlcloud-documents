## Description

This API (Complete Multipart Upload) is used to complete a multipart upload operation to form an archive. The tree hash value of the entire archive is required when you initiate this request. The server will compare the uploaded tree hash value with the tree hash value obtained by using the uploaded chunks. The request is successful in case of consistency, and fails in case of inconsistency.

## Request

### Request syntax

```HTTP
POST /<UID>/vaults/<VaultName>/multipart-uploads/<uploadID> HTTP/1.1
Host: cas.<Region>.myqcloud.com
Date: date
Authorization: Auth
x-cas-sha256-tree-hash: SHA256 tree hash of the archive
x-cas-archive-size: ArchiveSize in bytes
```

### Request parameters

No additional request parameters are needed.

### Request headers

#### Required headers

| Name | Description | Type | Required |
| ---------------------- | ---------------------------------------- | ------ | ---- |
| x-cas-archive-size | The total size of the archive (in bytes). This value is the sum of sizes of all uploaded chunks. | String | Yes |
| x-cas-sha256-tree-hash | The SHA256 tree-hash checksum of the entire archive. The server will compare the uploaded tree hash value with the tree hash value obtained by using the uploaded file chunks. The request is successful in case of consistency, and fails in case of inconsistency. | String | Yes |

### Request content

No request content

## Response

### Response headers

| Name | Description | Type |
| ---------------- | --------------- | ------ |
| Location | The relative URI path of a new archive | String |
| x-cas-archive-id | The ID of the archive | String |

### Response content

No response content

