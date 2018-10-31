## Description

This API (Initiate Multipart Upload) is used to initialize a multi-part upload. When this request is sent, an Upload ID is returned to be used for all subsequent uploads in the multi-part upload. This Upload ID is valid for 24 hours.

Each chunk to be uploaded (except for the last chunk) must have the same size, which should be the value obtained by multiplying 1 MB by 2n.

## Request

### Request syntax

```HTTP
POST /<UID>/vaults/<VaultName>/multipart-uploads HTTP/1.1
Host: cas.<Region>.myqcloud.com
Date: Date
Authorization: Auth
x-cas-archive-description: ArchiveDescription
x-cas-part-size: PartSize
```

### Request parameters

No additional request parameters are needed.

### Request headers

#### Required headers

| Name | Description | Type | Required |
| --------------- | ---------------------- | ------ | ---- |
| x-cas-part-size | The size of each chunk to be uploaded. It must be a value obtained by multiplying 1 MB by 2n, for example, 1,048,576 bytes (1 MB × 2º), 2,097,152 bytes (1 MB × 2¹) | String | Yes |

#### Recommended headers

| Name | Description | Type | Required |
| ------------------------- | --------------------- | ------ | ---- |
| x-cas-archive-description | The description of the archive that is uploaded in multiple parts. It is limited to 1024 B. | String | No |

### Request content

No request content

## Response

### Response headers

| Name | Description | Type |
| ------------------------- | ---------------------------------------- | ------ |
| Location | The relative URI path of the created multi-part upload in the format of ` /<UID>/vaults/<VaultName>/multipart-uploads/<UploadId>` | String |
| x-cas-multipart-upload-id | The ID of the multi-part upload | String |

### Response content

No response content

