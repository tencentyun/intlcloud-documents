## Description

This API (Upload Part) is used to upload a data chunk of an archive. Uploading data chunks out of order and overwriting uploaded data chunks are supported. The byte range of this data chunk in the archive needs to be indicated in the request. In addition, uploading data chunks in parallel is supported. A maximum of 10000 chunks can be uploaded.

If x-cas-sha256-tree-hash or x-cas-content-sha256 does not match the checksum of the actual archive in the request body, an error is returned.

If Content-Length does not match the size of the actual archive in the request body, an error is returned.

The Content-Range must be exactly aligned with the chunk size specified during the initialization of multi-part upload. For example, if 4,194,304 bytes (4 MB) is specified as the chunk size, then 0-4,194,303 bytes (4 MB-1) and 4,194,304 (4 MB)-8,388,607 (8 MB-1) are valid chunk ranges, and 2,097,152 (2 MB)-6,291,456 (6MB-1) is an invalid chunk range. 

When the chunk is uploaded successfully, `204 No Content` is returned. 

## Request

### Request syntax

```HTTP
PUT /<UID>/vaults/<VaultName>/multipart-uploads/<uploadID> HTTP/1.1
Host: cas.<Region>.myqcloud.com
Date: Date
Authorization: Auth
Content-Range: ContentRange
Content-Length: PayloadSize
Content-Type: application/octet-stream
x-cas-sha256-tree-hash: Checksum of the part
x-cas-content-sha256: Checksum of the entire payload
```

### Request parameters

No additional request parameters are needed.

### Request headers

#### Required headers

| Name | Description | Type | Required |
| ---------------------- | ---------------------------------------- | ------ | ---- |
| Content-Range | The byte range of the data chunk to be uploaded. It cannot be greater than the chunk size you specified when initiating the multi-part upload. For example, Content-Range:bytes 0-4194303/* | String | Yes |
| x-cas-content-sha256 | The SHA256 checksum (linear hash) of the data chunk to be uploaded | String | Yes |
| x-cas-sha256-tree-hash | The SHA256 tree-hash of the data chunk to be uploaded | String | Yes |

#### Recommended headers

| Name | Description | Type | Required |
| -------------- | ------------- | ------ | ---- |
| Content-Length | The length of the data chunk (in bytes) | String | No |

### Request content

`Data chunk`

## Response

### Response headers

| Name | Description | Type |
| ---------------------- | ---------------- | ------ |
| x-cas-sha256-tree-hash | The SHA256 tree-hash of the data chunk | String |

### Response content

No response content

