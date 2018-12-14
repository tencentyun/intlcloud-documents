## Description

This API (List Multipart Uploads) is used to list the multi-part uploads that are in process.

## Request

### Request syntax

```HTTP
GET /<UID>/vaults/<VaultName>/multipart-uploads HTTP/1.1
Host: cas.<Region>.myqcloud.com
Date: Date
Authorization: Auth
```

### Request parameters

| Name | Description | Type | Required |
| ------ | -------------------------- | ------ | ---- |
| limit | The maximum number of the chunks to be returned. Both the maximum value and the default value are 1000. | A positive integer | No |
| marker | An opaque string used to mark a multi-part upload. All multi-part uploads are sorted in chronological order, and `marker` specifies that all multi-part uploads following the creation time of the upload should be listed | string | No |

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
| Marker | The Marker for the next page is returned if there are more results available than are currently displayed, otherwise NULL is returned. | string |
| UploadsList | The list of multi-part uploads | Array |
| ArchiveDescription | The archive description specified in the request to initialize the multi-part upload. NULL is returned if no description is specified. | String |
| CreationDate | The UTC time when the multi-part upload is initiated. It is in an ISO 8601 date format, for example, 2013-03-20T17:03:43.221Z | String |
| MultipartUploadId | ID of the multi-part upload | String |
| PartSizeInBytes | The chunk size specified in the request to initialize the multi-part upload | Number |
| VaultQCS | Resource name of vault | String |

```JSON
{
  "Marker": String,
  "UploadsList" : [ 
    {
      "ArchiveDescription": String,
      "CreationDate": String,
      "MultipartUploadId": String,
      "PartSizeInBytes": Number,
      "VaultQCS": String
    }, 
   ...
  ]
} 
```

