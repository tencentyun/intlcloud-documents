## Description

This operation (Get Job Output) downloads the retrieved archives or archive inventory in the output. The content in the output is valid for 24 hours. If all data is successfully output, 200 OK is returned. If some of the data is output, 206 Partial Content is returned.

Cross-account operation is supported. The UID is "-" when the operation is performed in the account that owns the vault.

## Request

### Request syntax

```HTTP
GET /<UID>/vaults/<VaultName>/jobs/<JobID>/output HTTP 1.1
Host:cas.<Region>.myqcloud.com
Date:date
Authorization: Auth
Range:ByteRangeToRetrieve
```

### Request parameters

No additional request parameters are needed.

### Request headers

#### Recommended headers

| Name | Description | Type | Required |
| ----- | ------------------ | ------ | ---- |
| Range | The range of bytes of the retrieval output. All contents are downloaded by default | String | No |

### Request content

No request content.

## Response

### Response headers

| Name | Description | Type |
| ---------------------- | ---------------------------------------- | ------ |
| Content-Range          | The range of bytes of the returned content. | String |
| Content-Type | It depends on whether the job output is an archive or archive inventory. For an archive, it is `application/octet-stream`. For an archive inventory in JSON format, it is `application/json`. For an archive inventory in CSV format, it is `text/csv`. | String |
| x-cas-sha256-tree-hash | Tree-hash of the output content. This header is returned only when Job is a sub-tree of Archive and the Range of Job is also a sub-tree. | String |

### Response content

**Retrieve archive inventory (in JSON format)**

Note: "ArchiveId", "ArchiveDescription", "CreationDate" and "Size" are returned for retrieving an archive inventory in CSV format, of which the descriptions are the same as those of JSON fields.

| Name | Description | Type |
| ------------------ | ---------------------------------------- | ------ |
| VaultQCS           | QCS of the vault from which the archive is retrieved. | String |
| InventoryDate | The UTC date and time of the last inventory for the vault that was completed after changes to the vault. It is in an ISO 8601 date format, for example, `2013-03-20T17:03:43.221Z`. | String |
| ArchiveList | Archive metadata array. Each data element in the array represents the metadata of an archive in the vault. | String |
| ArchiveId | Archive ID. | String |
| ArchiveDescription | Archive description. | String |
| CreationDate | The UTC date and time when the archive was created. It is in an ISO 8601 date format, for example, `2013-03-20T17:03:43.221Z`. | String |
| Size | Size of the archive (in bytes). | Number |
| SHA256TreeHash     | Tree hash value of the archive. | String |

```JSON
{
 "VaultQCS": String,
 "InventoryDate": String,
 "ArchiveList": [
      {"ArchiveId": String,
       "ArchiveDescription": String,
       "CreationDate": String,
       "Size": Number,
       "SHA256TreeHash":String
      },
      ...
    ]
}
```

**Retrieve an archive**

Download the archive

