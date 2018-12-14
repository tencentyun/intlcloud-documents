## Description

This operation (Initiate Job) retrieves an archive or an archive inventory to the output. After that, you can read the archive or the archive inventory using the operation Get Job Output.

The time cost for archive retrieval in three modes:

| -         | Expedited | Standard | Bulk    |
| --------- | --------- | -------- | ------- |
| Time cost for archive retrieval | 1-5 minutes | 3-5 hours | 5-12 hours |

 **File size is limited to 256 MB for Expedited requests.**

The time cost for archive inventory retrieval:

| -           | Standard |
| ----------- | -------- |
|Time cost for archive inventory retrieval | 3-5 hours |

You can **import archives from CAS to COS** and **import objects from COS to CAS** under the same account using the operation Initiate Job. You need to **pre-configure the internal system permissions** in the CAS console -> Permission Management, to grant COS with the permission for all operations.

Time cost for importing archives from CAS to COS in three modes:

| -              | Expedited | Standard | Bulk    |
| -------------- | --------- | -------- | ------- |
| Time cost for importing archives to COS | 1-5 minutes | 3-5 hours | 5-12 hours |

You can directly import objects from COS to CAS without waiting.

Cross-account operation is supported for this request. The UID is "-" when the operation is performed in the account that owns the vault.

## Request

### Request syntax

```HTTP
POST /<UID>/vaults/<VaultName>/jobs HTTP 1.1
Host:cas.<Region>.myqcloud.com
Date:date
Authorization: Auth
```

### Request parameters

No additional request parameters are needed.

### Request headers

No additional request headers are needed except the headers described in "Common Request Headers".

### Request content

Retrieve an archive

| Name      | Description                          | Type        | Required   |
| ------------------ | ---------------------------------------- | ------ | ---- |
| Type | Job type. It is `archive-retrieval` for archive retrieval | String | Yes |
| ArchiveId | ID of the archive to be retrieved | string | Yes |
| CallBackUrl | The HTTP address of the callback, which must start with http:// or https:// | String | No |
| Description | Job description | String | No |
| RetrievalByteRange | The range of bytes of the retrieval archive. The format is "*StartByteValue*-*EndByteValue*". If this field is not specified, the entire archive is retrieved. If the range of bytes is specified, it must be aligned in megabytes (1 024\*1 024), which means that *StartByteValue* must be divisible by 1Mb and *EndByteValue* plus 1 must be divisible by 1Mb or equal to the end value specified as the file byte size value minus 1. If RetrievalByteRange is not aligned in megabytes, `400` is returned. | String | No    |
| Tier               | Archive retrieval type. Enumerated values: `Expedited`, `Standard`, `Bulk`. It is `Standard` by default. | String | No |

```json
{
  "Type": "archive-retrieval",
  "ArchiveId": String,
  "CallBackUrl":String,
  "Description": String,
  "RetrievalByteRange": String,
  "Tier": String 
}
```

Retrieve archive inventory

| Name | Description | Type | Required |
| ---------------------------- | ---------------------------------------- | ------ | ---- |
| Type | Job type. It is `inventory-retrieval` for archive inventory retrieval. | String | Yes |
| CallBackUrl | The HTTP address of the callback, which must start with http:// or https:// | String | No |
| Description | Job description | String | No |
| Format | Output format of archive inventory. Enumerated values: `CSV`, `JSON`. It is `JSON` by default. | String | No |
| InventoryRetrievalParameters | Configurations related to archive inventory retrieval | String | No |
| StartDate | The UTC date that archive inventory retrieval starts. Archives created on or after the date are retrieved. It is a string in ISO 8601 date format (`YYYY-MM-DDThh:mm:ssZ`, in seconds). For example, 2017-02-28T17:03:43Z | String | No |
| EndDate | The UTC date that archive inventory retrieval ends. Archives created on or before the date are retrieved. It is a string in ISO 8601 date format (`YYYY-MM-DDThh:mm:ssZ`, in seconds). For example, 2017-02-28T17:03:43Z | String | No |
| Limit                        | The maximum number of entries returned for the archive inventory request. It is 10000 by default. It should be a positive integer between 1 and 10000. | String | No |
| Marker | Read the archive inventory from Marker in lexicographical order | String | No |

```json
{
  "Type":"inventory-retrieval",
  "CallBackUrl":String,
  "Description": String,
  "Format": String,  
  "InventoryRetrievalParameters": { 
      "StartDate": String,
      "EndDate": String,
      "Limit": String,
      "Marker": String
   }   
}
```

Import an archive into COS

| Name      | Description                          | Type        | Required   |
| ------------------ | ---------------------------------------- | ------ | ---- |
| Type | Job type. It is `push-to-cos` when importing archives into COS. | String | Yes |
| ArchiveId | ID of the archive to be retrieved | string | Yes |
| CallBackUrl | The HTTP address of the callback, which must start with http:// or https:// | String | No |
| Description | Job description | String | No |
| RetrievalByteRange | The range of bytes of the retrieval archive. The format is "*StartByteValue*-*EndByteValue*". If this field is not specified, the entire archive is retrieved. If the range of bytes is specified, it must be aligned in megabytes (1 024\*1 024), which means that *StartByteValue* must be divisible by 1Mb and *EndByteValue* plus 1 must be divisible by 1Mb or equal to the end value specified as the file byte size value minus 1. If RetrievalByteRange is not aligned in megabytes, `400` is returned. | String | No    |
| Tier               | Archive retrieval type. Enumerated values: `Expedited`, `Standard`, `Bulk`. It is `Standard` by default. | String | No |
| Bucket             | Domain name of the target bucket in COS | String | Yes |
| Object             | Object address of the target bucket in COS | String | Yes |

```json
{
  "Type": "push-to-cos",
  "Description": String,
  "ArchiveId": String,
  "CallBackUrl":String,
  "RetrievalByteRange":String,
  "Tier":String,
  "Bucket":String,
  "Object":String
}
```

Pull object files from COS.

| Name | Description | Type | Required |
| ------------------ | -------------------------------------- | ------ | ---- |
| Type | Job type. It is ` pull-from-cos` when pulling object files from COS. | String | Yes |
| CallBackUrl | The HTTP address of the callback, which must start with http:// or https:// | String | No |
| Description | Job description | String | No |
| Bucket             | Domain name of the source bucket in COS | String | Yes |
| Object             | Object address of the source bucket in COS | String | Yes |
| Range | The range of source objects in COS (in bytes) | String | Yes |
| Condition | Preconditions for obtaining data from COS | Array | No |
| If-Modified-Since | The file content is returned if the file is modified after the specified time. | String | No    |
| If-Umodified-Since | The file content is returned if the file has been modified before the specified time. | String | No    |
| If-Match           | The file content is returned if its ETag is the same as specified. | String | No    |
| If-None-Match           | The file content is returned if its ETag is not the same as specified. | String | No    |
| ArchiveDescription | Archive file description | String | No |

```json
{
  "Type": "pull-from-cos",
  "CallBackUrl":String,
  "Description":String,
  "Bucket":String,
  "Object":String,
  "Range":String,
  "Condition":{
    "If-Modified-Since":String,
    "If-Umodified-Since":String,
    "If-Match":String,
    "If-None-Match":String
  },
  "ArchiveDescription":String
}
```

## Response

### Response headers

| Name | Description | Type |
| ------------ | ---------------------------------------- | ------ |
| Location | The relative URI path of the job in the format of /< UID >/vaults/< VaultName >/jobs/< JobID > | String |
| x-cas-job-id | Job ID                           | String |

### Response content

No response content

