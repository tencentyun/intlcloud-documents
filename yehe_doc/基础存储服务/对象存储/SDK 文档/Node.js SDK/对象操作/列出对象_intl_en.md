## Overview

This document provides an overview of APIs and SDK code samples related to listing objects.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |

#### Description

This API is used to query some or all the objects in a bucket.

>! In COS, if a listed object key is project/, it is an empty object to simulate the effects of a folder. For more information, please see [Folder and directory](https://intl.cloud.tencent.com/document/product/436/13324).
>

#### Sample code

Sample 1. Listing all files in the `a` directory

[//]: # (.cssg-snippet-get-bucket)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Prefix: 'a/',           /* Set a prefix to indicate that the key of the listed object starts with the prefix. Not required. */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

Response:

```json
{
    "Name": "examplebucket-1250000000",
    "Prefix": "",
    "Marker": "a/",
    "MaxKeys": "1000",
    "Delimiter": "",
    "IsTruncated": "false",
    "Contents": [{
        "Key": "a/3mb.zip",
        "LastModified": "2018-10-18T07:08:03.000Z",
        "ETag": "\"05a9a30179f3db7b63136f30aa6aacae-3\"",
        "Size": "3145728",
        "Owner": {
            "ID": "1250000000",
            "DisplayName": "1250000000"
        },
        "StorageClass": "STANDARD"
    }],
    "statusCode": 200,
    "headers": {}
}
```

Sample 2. Listing the files in the `a` directory without deep traversal

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Prefix: 'a/',           /* Set a prefix to indicate that the key of the listed object starts with the prefix. Not required. */
    Delimiter: '/',            /* Set the delimiter "/" to list objects in the current directory. To list all objects, leave this parameter empty. Not required. */
}, function(err, data) {
    console.log(err || data.CommonPrefixes);
});
```

Response:

```json
{
    "Name": "examplebucket-1250000000",
    "Prefix": "a/",
    "Marker": "",
    "MaxKeys": "1000",
    "Delimiter": "/",
    "IsTruncated": "false",
    "CommonPrefixes": [{
        "Prefix": "a/1/"
    }],
    "Contents": [{
        "Key": "a/3mb.zip",
        "LastModified": "2018-10-18T07:08:03.000Z",
        "ETag": "\"05a9a30179f3db7b63136f30aa6aacae-3\"",
        "Size": "3145728",
        "Owner": {
            "ID": "1250000000",
            "DisplayName": "1250000000"
        },
        "StorageClass": "STANDARD"
    }],
    "statusCode": 200,
    "headers": {}
}
```

Sample 3. Listing all files in the `a` directory.

```js
var listFolder = function(marker) {
    cos.getBucket({
        Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
        Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
        Prefix: 'a/',           /* Set a prefix to indicate that the key of the listed object starts with the prefix. Not required. */
        Marker:       marker,
        MaxKeys: 1000,
    }, function(err, data) {
        if (err) {
            return console.log('list error:', err);
        } else {
            console.log('list result:', data.Contents);
            if (data.IsTruncated === 'true') listFolder(data.NextMarker);
            else return console.log('list complete');
        }
    });
};
listFolder();
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Prefix | Key prefix to query objects by | String | No   |
| Delimiter | Separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String | No |
| Marker | Indicates where the object key listing begins. Entries are listed starting from the key after the `Marker` in UTF-8 lexicographical order by default. | String | No |
| MaxKeys | Maximum number of entries returned in a single response, which is `1000` (the maximum value allowed) by default | String | No |
| encoding-type | Indicates the encoding method of the returned value. Valid value: `url`, which means that the returned object keys are URL-encoded (percent-encoded) values. For example, "Tencent Cloud" will be encoded as `%E8%85%BE%E8%AE%AF%E4%BA%91`. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - headers | Headers | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - Name | Bucket name in the format of `&lt;BucketName-APPID>`, such as `examplebucket-1250000000` | string |
| - Prefix          | Key prefix by which objects are queried. Returned objects are listed according to the UTF-8 lexicographical order of their keys after the prefix.   | String      |
|  - Marker | Marker after which the returned list begins. By default, entries are listed in UTF-8 binary order. | String |
| - MaxKeys | Maximum number of entries returned in a single response | String |
| - Delimiter | Delimiter | String |
| - IsTruncated | Whether the returned list is truncated. Valid values: `true`; `false` | String |
| - NextMarker | Key of the object after which the next returned list begins if the list is truncated | String |
| - CommonPrefixes | Objects with identical paths between the specified prefix and the delimiter, which are grouped together and defined as common prefixes | ObjectArray |
| - - Prefix | A common prefix | String |
| - EncodingType | Encoding type of the returned values. This parameter is applicable to `Delimiter`, `Marker`, `Prefix`, `NextMarker`, and `Key`, | String |
| - Contents | A list of object metadata | ObjectArray |
| - - Key | Object key, i.e., object name | String |
| - - ETag | MD5 checksum of the object, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - - Size | Object size, in bytes | String |
| - - LastModified  | Last modified time of the object, in ISO 8601 format, for example, `2019-05-24T10:56:40Z` | String |
| - - Owner | Information about the object owner | Object |
| - - - ID | Complete ID of object owner in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, for example, `qcs::cam::uin/100000000001:uin/100000000001`, where `100000000001` is the uin. | String |
| - - - DisplayName | Name of the object owner | String |
| - - StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD`, `STANDARD_IA` and `ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |
