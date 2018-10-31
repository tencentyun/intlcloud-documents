## Description

This API (Delete Archive) is used to delete an archive. If the request is successful, the x-cas-archive-id that uniquely identifies the archive as well as "204 No Content" are returned.

After the deletion of the archive, your request to retrieve the deleted archive may be successful, but the archive retrieval job will fail.

While you delete the archive, the retrieval of the corresponding archive ID may or may not be successful, depending on the following scenarios:

- If the archive is being downloaded to the output by the archive retrieval job when the request to delete the archive is received, the archive retrieval operation may fail.
- If the archive has been downloaded to the output by the archive retrieval job when the request to delete the archive is received, you can export the downloaded archive.

Cross-account operation is supported. The UID is "-" when the operation is performed in the account that owns the vault.

## Request

### Request syntax

```HTTP
DELETE /<UID>/vaults/<VaultName>/archives/<ArchiveID> HTTP 1.1
Host:cas.<Region>.myqcloud.com
Date:date
Authorization: Auth
```

### Request parameters

No additional request parameters are needed.

### Request headers

No additional request headers are needed except the headers described in "Common Request Headers".

### Request content

No request content.

## Response

### Response headers

No additional response headers are needed except the headers described in "Common Request Headers".

### Response content

No response content.
