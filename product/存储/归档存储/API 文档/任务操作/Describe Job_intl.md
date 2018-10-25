## Description

This operation (Describe Job) returns the job information of a vault.

Cross-account operation is supported. The UID is "-" when the operation is performed in the account that owns the vault.

## Request

### Request syntax

```HTTP
GET /<UID>/vaults/<VaultName>/jobs/<JobID> HTTP 1.1
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

**Retrieve an archive**

| Name | Description | Type |
| --------------------- | ---------------------------------------- | -------- |
| Action | Job type. It is `ArchiveRetrieval` for archive retrieval jobs | String |
| JobId | Job ID | String |
| JobDescription | Job description | String |
| CallBackUrl | HTTP address of callback | String |
| CreationDate | The UTC time that the job was created. It is in an ISO 8601 date format, for example, `2013-03-20T17:03:43.221Z`. | ISO 8601 |
| CompletionDate | The UTC time that the job was completed. It is in an ISO 8601 date format, for example, `2013-03-20T17:03:43.221Z`. | ISO 8601 |
| Completed | It is `true` if the job is completed. Otherwise, it is `false` | Boolean |
| StatusCode                             | Job status code. Enumerated values: `Succeeded`, `Failed` or `InProgress` | String |
| StatusMessage | Job status message | String |
| VaultQCS                               | Vault QCS of the job                           | String |
| ArchiveId | The archive ID requested for an archive retrieval job | string |
| ArchiveSizeInBytes | Size of the archive retrieved in the request | Number |
| ArchiveSHA256TreeHash | The SHA256 tree hash of the entire archive for an archive retrieval job                 | String   |
| RetrievalByteRange    | The retrieved byte range for archive retrieval jobs in the form "*StartByteValue*-*EndByteValue*". If you don't specify a range in the archive retrieval, then the whole archive is retrieved; also StartByteValue equals 0, and EndByteValue equals the size of the archive minus 1. | String |
| SHA256TreeHash     | The SHA256 tree hash value for the requested range of an archive. This field is null in the following situations: Archive retrieval jobs that specify a range that is not tree-hash aligned; archival jobs that specify a range that is not equal to the whole archive and the job status is InProgress. If a job is completed, this field returns a value. | String |
| Tier               | Archive retrieval type. Enumerated values: `Expedited`, `Standard`, `Bulk` | String   |

```JSON
{     
  "Action": String,
  "JobId": String,
  "JobDescription": String,
  "CallBackUrl":String,
  "CreationDate": String,
  "CompletionDate": String,
  "Completed": Boolean,
  "StatusCode": String,
  "StatusMessage": String,
  "VaultQCS": String,
  "ArchiveId": String,
  "ArchiveSizeInBytes": Number,
  "ArchiveSHA256TreeHash": String,
  "RetrievalByteRange": String,
  "SHA256TreeHash": String,
  "Tier": String
}
```

**Retrieve archive inventory**

| Name | Description | Type |
| ---------------------------- | ---------------------------------------- | -------- |
| Action | Job type. It is `ArchiveRetrieval` for archive retrieval jobs | String |
| JobId | Job ID | String |
| JobDescription | Job description | String |
| CallBackUrl | HTTP address of callback | String |
| CreationDate | The UTC time that the job was created. It is in an ISO 8601 date format, for example, `2013-03-20T17:03:43.221Z`. | ISO 8601 |
| CompletionDate | The UTC time that the job was completed. It is in an ISO 8601 date format, for example, `2013-03-20T17:03:43.221Z`. | ISO 8601 |
| Completed | It is `true` if the job is completed. Otherwise, it is `false` | Boolean |
| StatusCode                             | Job status code. Enumerated values: `Succeeded`, `Failed` or `InProgress` | String |
| StatusMessage | Job status message | String |
| VaultQCS                               | Vault QCS of the job                           | String |
| InventorySizeInBytes | Size (in bytes) of the inventory associated with the request of archive inventory retrieval jobs | Number |
| Format | Output format of archive inventory. Enumerated values: `CSV`, `JSON`. | String |
| StatDate                     | The UTC date that the vault inventory starts. It is in an ISO 8601 date format, for example, `2013-03-20T17:03:43.221Z`. | ISO 8601 |
| EndDate                     | The UTC date that the vault inventory ends. It is in an ISO 8601 date format, for example, `2013-03-20T17:03:43.221Z`. | ISO 8601 |
| Limit | The maximum number of items returned for each vault inventory request. It should be a positive integer | String |
| InventorySizeInBytes. Marker | Read the archive inventory from Marker in lexicographical order | String |

```JSON
{
  "Action": String,
  "JobId": String,
  "JobDescription": String,
  "CallBackUrl":String,
  "CreationDate": String,
  "CompletionDate": String,
  "Completed": Boolean,
  "StatusCode": String,
  "StatusMessage": String,
  "VaultQCS": String,
  "InventorySizeInBytes": String,
  "InventoryRetrievalParameters": { 
    "Format": String,
    "StartDate": String,
    "EndDate": String,
    "Limit": String,
    "Marker": String
  }
}
```

**Import an archive into COS**

| Name | Description | Type |
| ------------------ | ---------------------------------------- | -------- |
| Action             | Job type. It is `PushToCOS` for importing an archive into COS. | String   |
| JobId | Job ID | String |
| JobDescription | Job description | String |
| CallBackUrl | HTTP address of callback | String |
| CreationDate | The UTC time that the job was created. It is in an ISO 8601 date format, for example, `2013-03-20T17:03:43.221Z`. | ISO 8601 |
| CompletionDate | The UTC time that the job was completed. It is in an ISO 8601 date format, for example, `2013-03-20T17:03:43.221Z`. | ISO 8601 |
| Completed | It is `true` if the job is completed. Otherwise, it is `false` | Boolean |
| StatusCode                             | Job status code. Enumerated values: `Succeeded`, `Failed` or `InProgress` | String |
| StatusMessage | Job status message | String |
| VaultQCS                               | Vault QCS of the job                           | String |
| Marker | If the returned Joblist (in lexicographical order) is truncated, marker represents the starting point of the next read. | String |
| ArchiveId | The archive ID requested for an archive retrieval job | string |
| ArchiveSizeInBytes | Size of the archive retrieved in the request | Number |
| RetrievalByteRange    | The retrieved byte range for archive retrieval jobs in the form "*StartByteValue*-*EndByteValue*". If you don't specify a range in the archive retrieval, then the whole archive is retrieved; also StartByteValue equals 0, and EndByteValue equals the size of the archive minus 1. | String |
| Bucket             | Domain name of the target bucket in COS | String |
| Object             | Object address of the target bucket in COS | String |
| Tier               | Archive retrieval type. Enumerated values: `Expedited`, `Standard`, `Bulk` | String   |

```JSON
{
  "Action": String,
  "JobId": String,
  "JobDescription": String,
  "CallBackUrl":String,
  "CreationDate": String,
  "CompletionDate": String,
  "Completed": Boolean,
  "StatusCode": String,
  "StatusMessage": String,
  "VaultQCS": String,
  "ArchiveId": String,
  "ArchiveSizeInBytes": Number,
  "RetrievalByteRange":String,
  "Bucket":String,
  "Object":String,
  "Tier":String 
}
```

**Pull objects from COS**

| Name | Description | Type |
| ------------------ | ---------------------------------------- | -------- |
| Action             | Job type. It is `PullFromCOS` for pulling objects from COS | String   |
| JobId | Job ID | String |
| JobDescription | Job description | String |
| CallBackUrl | HTTP address of callback | String |
| CreationDate | The UTC time that the job was created. It is in an ISO 8601 date format, for example, `2013-03-20T17:03:43.221Z`. | ISO 8601 |
| CompletionDate | The UTC time that the job was completed. It is in an ISO 8601 date format, for example, `2013-03-20T17:03:43.221Z`. | ISO 8601 |
| Completed | It is `true` if the job is completed. Otherwise, it is `false` | Boolean |
| StatusCode                             | Job status code. Enumerated values: `Succeeded`, `Failed` or `InProgress` | String |
| StatusMessage | Job status message | String |
| VaultQCS                               | Vault QCS of the job                           | String |
| Marker | If the returned Joblist (in lexicographical order) is truncated, marker represents the starting point of the next read. | String |
| ArchiveId | Archive ID | String   |
| ArchiveSizeInBytes | Archive size | Number |
| Bucket             | Domain name of the source bucket in COS | String |
| Object             | Object address of the source bucket in COS | String |
| Range | The range of source objects in COS (in bytes) | String |
| Condition | Preconditions for obtaining data from COS | Array |
| If-Modified-Since | The file content is returned if the file is modified after the specified time. | String |
| If-Umodified-Since | The file content is returned if the file has been modified before the specified time. | String |
| If-Match           | The file content is returned if its ETag is the same as specified. | String |
| If-None-Match           | The file content is returned if its ETag is not the same as specified. | String |
| ArchiveDescription | Archive file description | String |
```JSON
{
  "Action": String,
  "JobId": String,
  "JobDescription": String,
  "CallBackUrl":String,
  "CreationDate": String,
  "CompletionDate": String,
  "Completed": Boolean,
  "StatusCode": String,
  "StatusMessage": String,
  "VaultQCS": String,
  "ArchiveId": String,
  "ArchiveSizeInBytes": Number,
  "Bucket":String,
  "Object":String,
  "Condition":{
     "If-Modified-Since":String,
     "If-Umodified-Since":String,
     "If-Match":String,
     "If-None-Match":String
  },
  "ArchiveDescription":String 
}
```


