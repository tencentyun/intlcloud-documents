## Description

This API (List Parts) is used to list the uploaded data chunks.

## Request

### Request syntax

```HTTP
GET /<UID>/vaults/<VaultName>/multipart-uploads/<uploadID> HTTP/1.1
Host: cas.<Region>.myqcloud.com
Date: Date
Authorization: Auth
```

### Request parameters

| Name | Description | Type | Required |
| ------ | ----------------------------- | ------ | ---- |
| limit | The maximum number of the chunks to be returned. Both the maximum value and the default value are 1000. | A positive integer | No |
| marker | All chunks are sorted from Offset. The parameter `marker` specifies the offset value from which the uploaded chunks are listed | String | No |

### Request headers

No additional request headers are needed except the headers described in "Common Request Headers".

### Request content

No request content

## Response

### Response headers

No additional response headers are needed except the headers described in "Common Request Headers".

### Response content

| Name | Description | Type |
| ------------------ | ---------------------------------------- | ------ |
| ArchiveDescription | The archive description specified in the request to initiate the multi-part upload. NULL is returned if no description is specified. | String |
| CreationDate | The UTC time when the multi-part upload is initiated. It is in an ISO 8601 data format, for example, 2013-03-20T17:03:43.221Z | String |
| Marker | The Marker for the next page is returned if there are more results available than are currently displayed, otherwise NULL is returned. | string |
| MultipartUploadId | ID of the multi-part upload | String |
| PartSizeInBytes | Fixed size of each chunk (in bytes) | Number |
| Parts | The list of the uploaded data chunks in the multi-part upload | Array |
| RangeInBytes | The byte range of a data chunk | String |
| SHA256TreeHash | SHA256 tree hash of data chunk | String |
| VaultQCS | Resource name of vault | String |

```JSON
{
    "ArchiveDescription" : String,
    "CreationDate" : String,
    "Marker": String,
    "MultipartUploadId" : String,
    "PartSizeInBytes" : Number,
    "Parts" : 
    [ {
      "RangeInBytes" : String,
      "SHA256TreeHash" : String
      },
      ...
     ],
    "VaultQCS" : String
}
```

