## Overview

This document provides an overview of APIs and SDK code samples for copying and moving an object.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path. |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Copying a multipart upload | Copies a multipart upload. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart copy | Completes the multipart copy of an object. |

## Simple Operations

### Copying an object

#### Feature description

This API (`PUT Object - Copy`) is used to create a copy of an existing COS object, that is, to copy an object from the source path (object key) to the destination path (object key). During the process, object metadata and ACLs can be modified.
You can use this API to create a copy of an object, modify an object’s metadata (the source object and destination file have the same attributes), and move or rename an object (copy the object first and then call the deletion API).

>! We recommend that you use this API to copy objects of 1-5 GB. For objects larger than 5 GB, please use the advanced API [Slice Copy File](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A1).
>

#### Sample code

[//]: # (.cssg-snippet-copy-object)
```js

/* Copy a/1.jpg to b/1.jpg */
cos.putObjectCopy({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: 'b/1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    CopySource: 'examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/a/1.jpg', /* Required */
    /* If Key in CopySource contains Chinese characters, escaping is required. */
    // CopySource: `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/${encodeURIComponent('a/Chinese filename.jpg')}`,
}, function(err, data) {
    console.log(err || data);
});
```

#### Field description

| Parameter | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| CopySource | URL of the source object. You can specify a previous version using the URL parameter ?versionId=&lt;versionId>. | String | Yes |
| ACL | ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note**: If you do not need access control for the object, set this parameter to `default` or do not specify it, in which case the object will inherit the permissions of its bucket. | String | No |
| GrantRead              | Grants a user read access to the object in the format of `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| GrantWrite                  | Grants a user write access to the object in the format of `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>. <br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| GrantFullControl       | Grants a user full access in the format of `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.</br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` </li></ul> | String               | No   |
| MetadataDirective | Whether to copy the metadata. Enumerated values: `Copy` (default), `Replaced`. If it is set to `Copy`, the metadata of the source object will be copied and the user-defined metadata in the header will be ignored. If it is set to `Replaced`, the metadata of the source object will be replaced with the user-defined metadata in the header. **If the destination and source paths are the same, that is, if you want to modify the metadata, this parameter must be set to `Replaced`.** | String | No |
| CopySourceIfModifiedSince | Required modification time. The object is copied only if it has been modified after the specified time. Otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfNoneMatch`. Using it together with other conditions may cause a conflict.** | String | No |
| CopySourceIfUnmodifiedSince | Required unmodified time. The object is copied only if it hasn’t been modified since the specified time. Otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfMatch`. Using it together with other conditions may cause a conflict.** | String | No |
| CopySourceIfMatch | `ETag` that must be matched. The object is copied only if its `ETag` matches the specified value. Otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfUnmodifiedSince`. Using it together with other conditions may cause a conflict.** | String | No |
| CopySourceIfNoneMatch | `ETag` that cannot be matched. The object is copied only if its `ETag` does not match the specified value. Otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfModifiedSince`. Using it together with other conditions may cause a conflict**. | string | No |
| StorageClass | Storage class of the object, such as `STANDARD` (default) and `STANDARD_IA`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-\* | Other user-defined file headers. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Returns headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Returns headers | Object |
| - ETag | MD5 checksum of the object, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - LastModified | Last modified time of the object, for example, `2017-06-23T12:33:27.000Z` | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |

### Moving an object

#### Feature description

Object movement involves copying the source object to the target location and deleting the source object.

Since COS uses the bucket name (`Bucket`) and object key (`ObjectKey`) to identify objects, moving an object will change the object identifier. Currently, COS does not provide a standalone API to change object identifiers. However, you can still move the object with a combination of basic operations (object copy and object deletion).

#### Sample code

[//]: # (.cssg-snippet-copy-object)
```js
/* Move a/1.jpg to b/1.jpg */
/* Alternatively, you can use the advanced copy API `cos.sliceCopyFile`. */
cos.putObjectCopy({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: 'b/1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/a/1.jpg', /* Required */
}, function(err, data) {
    if (err) return console.log(err);
    /* Delete a/1.jpg */
    cos.deleteObject({
        Bucket: 'examplebucket-1250000000', /* Required */
        Region: 'COS_REGION',     /* Bucket region. Required */
        Key: 'a/1.jpg'        /* Required */
    }, function(err, data) {
        console.log(err || data);
    });
});
```
### Modifying the storage class of an object

#### Feature description

To modify the storage class of an object, you can set `StorageClass` when copying the object (the source and destination objects are the same object).

#### Sample code

[//]: # (.cssg-snippet-copy-object)
```js
/* Set the storage class of 1.jpg in the root directory to ARCHIVE */
/* Alternatively, you can use the advanced copy API `cos.sliceCopyFile`. */
cos.putObjectCopy({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/1.jpg', /* Required */
    StorageClass: 'ARCHIVE',  /* Set the storage class to ARCHIVE. */
}, function(err, data) {
    console.log(err || data);
});
```
## Multipart Operations

### Initializing a multipart copy

#### Feature description

This API is used to initialize a multipart copy. After a successful operation, an `upload ID` will be returned, which can be used in the subsequent `Upload Part - Copy` requests.

#### Sample code

[//]: # (.cssg-snippet-init-multi-upload)
```js
cos.multipartInit({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
}, function(err, data) {
    console.log(err || data);
    if (data) {
      uploadId = data.UploadId;
    }
});
```

#### Field description

| Parameter | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Content-Disposition | Filename as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expires | Cache expiration time as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ACL | ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note**: If you do not need access control for the object, set this parameter to `default` or do not specify it, in which case the object will inherit the permissions of its bucket. | String | No |
| GrantRead              | Grants a user read access to the object in the format of `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code> </li></ul> | String | No   |
| GrantFullControl       | Grants a user full access in the format of `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.</br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-\* | User-defined headers, which will be returned as the object metadata. The maximum size is 2 KB. | String | No |
| UploadAddMetaMd5 | Sets x-cos-meta-md5 as the object’s MD5 checksum in the object’s metadata during upload in the format of a 32-bit lowercase string. Example: `4d00d79b6733c9cc066584a02ed03410` | String | No   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| Bucket | Name of the destination bucket for the multipart upload. The value is formed by connecting a user-defined string and the system-generated `APPID` with a hyphen, for example, `examplebucket-1250000000`. | string |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| UploadId | Upload ID, which is required for the subsequent upload | String |

### Copying an object part

#### Feature description

This API (`Upload Part - Copy`) is used to copy a part of an object from the source path to the destination path.

> !To copy an object part, you must first initialize a multipart upload, after which a unique upload ID will be returned. This ID is required in the copy request.

#### Sample code

[//]: # (.cssg-snippet-upload-part-copy)
```js
cos.uploadPartCopy({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject', /*Required*/
    UploadId: 'exampleUploadId', /*Required*/
    PartNumber: '1', /*Required*/
}, function(err, data) {
    console.log(err || data);
    if (data) {
      eTag = data.ETag;
    }
});
```

#### Field description

| Parameter | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| CopySource | URL of the source object. You can specify a previous version using the URL parameter ?versionId=&lt;versionId>. | String | Yes |
| PartNumber | Part number | String | Yes |
| uploadId | To copy an object part, you must first initialize a multipart upload, after which a unique upload ID will be returned. This ID is required in the copy request. | String | Yes |
| CopySourceRange | Byte range of the source object. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means to copy the first 10 bytes of the source object. If this parameter is not specified, the entire object will be copied. | String | No |
| CopySourceIfMatch | `ETag` that must be matched. The part will be copied only if its `ETag` matches the specified value. Otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Unmodified-Since`. Using it together with other conditions may cause a conflict. | String | No |
| CopySourceIfNoneMatch | `ETag` that cannot be matched. The part is copied only if its `ETag` does not match the specified value. Otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Modified-Since`. Using it together with other conditions may cause a conflict. | string | No |
| CopySourceIfUnmodifiedSince | Required unmodified time. The object is copied only if it hasn’t been modified since the specified time. Otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Match`. Using it together with other conditions may cause a conflict.  | String | No |
| CopySourceIfModifiedSince | Required modification time. The object is copied only if it has been modified after the specified time. Otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-None-Match`. Using it together with other conditions may cause a conflict. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Returns headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Returns headers | Object |
| - ETag | MD5 checksum of the object, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - LastModified | Last modified time of the object, in GMT format | String |

### Completing a multipart copy

#### Feature description

This API is used to complete a multipart copy. After all parts are copied via the `Copy Parts` API, you need to call this API to complete the multipart copy. When using this API, you need to specify the `PartNumber` and `ETag` of each part in the request body for the part information to be verified.
The parts need to be reassembled after they are copied, which takes several minutes. When the assembly starts, COS will immediately return the status code `200` and will periodically return spaces during the process to keep the connection active until the assembly is completed. After that, COS will return the assembled result in the body.

- If any uploaded part is less than 1 MB in size, `400` (EntityTooSmall) will be returned when this API is called.
- If the part numbers are not continuous, "400 InvalidPart" will be returned when this API is called.
- If the part numbers in the request body are not in ascending order, "400 InvalidPartOrder" will be returned when this API is called.
- If the `uploadId` does not exist, `404` (NoSuchUpload) will be returned when this API is called.

> ! We recommend you either complete or abort a multipart copy as early as possible, as the uploaded parts of an incomplete multipart copy will take up storage capacity and incur storage fees.

#### Sample code

[//]: # (.cssg-snippet-complete-multi-upload)
```js
cos.multipartComplete({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    UploadId: 'exampleUploadId', /* Obtained during the multipart task initialization. Required. */
    Parts: [
        {PartNumber: '1', ETag: 'exampleETag'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### Field description

| Parameter | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key                                                          | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String    | Yes   |
| UploadId | ID of the upload | String | Yes |
| Parts | A list of information about the parts of the multipart upload | ObjectArray | Yes |
| - PartNumber | Part number | String | Yes |
| - ETag | MD5 checksum of each part. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`<br>**Note that double quotation marks are required at the beginning and the end.** | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - Location   | Access address of the uploaded file                                        | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | Unique ID of the file after assembly in the format of `"uuid-<part quantity>"`. </br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end.** | String |

## Advanced APIs (Recommended)

Advanced APIs are highly recommended. They encapsulate the native methods mentioned above to implement multipart copies.

### Copying an object in multiple parts

#### Feature description

This API (Slice Copy File) is used to copy an object from the source path to the destination path through multipart copy. During the copy, the object metadata and ACL can be modified. You can use this API to move, rename, and copy a file or modify its attributes.


#### Method prototype

Calling `Slice Copy File`

[//]: # (.cssg-snippet-transfer-copy-object)
```js
/* Copy a/1.jpg to b/1.jpg */
cos.sliceCopyFile({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: 'b/1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/a/1.jpg', /* Required */
    onProgress:function (progressData) {                     /* Optional */
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});
```

#### Field description

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| CopySource | URL of the source object. You can specify a previous version using the URL parameter ?versionId=<versionId>. | String | Yes |
| ChunkSize | Size (in bytes) of each part in the multipart copy. Defaults to `1048576` (1 MB). | Number | No |
| SliceSize | Specifies the minimum file size (in bytes) to use multipart copy. The default value is 5 GB. If the file size is equal to or smaller than this value, the file will be uploaded using `putObjectCopy`; otherwise, it will be uploaded using `sliceCopyFile`. | Number | No |
| onProgress | Callback for the upload progress, whose parameter is `progressData` | Function | No |
| - progressData.loaded | Size of the uploaded parts, in bytes | Number | No |
| - progressData.total | Size of the entire file, in bytes | Number | No |
| - progressData.speed | File upload speed, in bytes/s | Number | No |
| - progressData.percent | Percentage of the file upload progress, in decimal form. For example, 0.5 means 50% has been uploaded. | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - Location | Public network access endpoint of the object | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | MD5 checksum of the file after assembly. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String |
