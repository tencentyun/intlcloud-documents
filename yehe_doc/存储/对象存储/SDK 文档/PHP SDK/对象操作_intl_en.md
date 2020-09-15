## Overview

This document provides an overview of APIs and SDK sample codes related to simple operations, multipart operations, and advanced APIs.

**Simple operations**

| API                                                          | Operation                   | Description                                       |
| ------------------------------------------------------------ | ------------------------ | ---------------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying a list objects and their version history | Queries some or all objects in a bucket and their version history |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploads an object using simple upload | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies a file to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |

**Multipart upload operations**

| API          | Operation                   | Description                                       |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart upload operations | Queries in-progress multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload task |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads object parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire object |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts |

## Simple Operations

### Querying object list

#### API description

This API is used to query all the objects in a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model listObjects(array $args = array());
```

#### Sample request

#### Sample 1. Querying a list of objects with the specified prefix and starting object

[//]: # ".cssg-snippet-get-bucket-comp"

```php
try {
    $result = $cosClient->listObjects(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Delimiter' => '',
        'EncodingType' => 'url',
        'Marker' => 'doc/picture.jpg',
        'Prefix' => 'doc',
        'MaxKeys' => 1000,
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ------------ | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | Yes |
| Delimiter | String | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | No |
| EncodingType | String | Indicates the encoding method of the returned value. The value is not encoded by default. Valid value: `url`  | No |
| Marker | String | Marks the starting point of the returned object list. Entries are listed using UTF-8 binary order by default.  | No |
| Prefix | String | Filters the object keys prefixed with the value of this parameter. It is left empty by default. | No |
| MaxKeys | Int | Maximum number of returned objects; the default value is 1,000. | No |

#### Sample returned result

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Name] => examplebucket-1250000000
            [Prefix] => doc
            [Marker] => doc/picture.jpg
            [MaxKeys] => 10
            [IsTruncated] => 1
            [NextMarker] => doc/exampleobject
            [Contents] => Array
                (
                    [0] => Array
                        (
                            [Key] => doc/exampleobject
                            [LastModified] => 2019-02-14T12:20:40.000Z
                            [ETag] => "e37b429559d82e852af0b2f5b4d078ab72b90208"
                            [Size] => 6532594
                            [Owner] => Array
                                (
                                    [ID] => 100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                        )

                    [1] => Array
                        (
                            [Key] => doc/exampleobject2
                            [LastModified] => 2019-03-04T06:34:43.000Z
                            [ETag] => "988f9f28e68eba9b8c1f5f98ccce0a3c"
                            [Size] => 28
                            [Owner] => Array
                                (
                                    [ID] => 100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                        )
                )
            [RequestId] => NWNhMzM0MmZfOWUxYzBiMDlfOTk2YV83ZWE3ODE=
        )

)
```

#### Returned result description

| Parameter Name | Type | Description | Parent Node |
| ------------ | ------ | ------------------------------------------------------------ | -------- |
| Name | String | Bucket name in the format: `BucketName-APPID`                         | None |
| Delimiter | String | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | None |
| EncodingType | String | Specifies the encoding type of the returned value | None |
| Marker | String | Marks the starting point of the returned object list. Entries are listed using UTF-8 binary order by default.  | None |
| Prefix | String | Filters the object keys prefixed with the value of this parameter.       | None |
| MaxKeys | Int | Maximum number of returned objects; the default value is 1,000. | None |
| IsTruncated | Int    | Indicates whether the returned objects are truncated | None |
| Contents     | Array  | Returned object list                                              | None       |
| Content | Array | Returned object attributes, contains a list of the metadata of all objects, including 'ETag', 'StorageClass', 'Key', 'Owner', 'LastModified', and 'Size' | Contents |

### Querying objects and their version history 

#### API description

This API is used to query some or all objects in a bucket as well as their version history.

#### Method prototype

```
public Guzzle\Service\Resource\Model listObjectVersions(array $args = array());
```

#### Sample request

#### Sample 1. Querying a list of past object versions

[//]: # ".cssg-snippet-list-object-versioning"

```php
try {
    $result = $cosClient->listObjectVersions(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Delimiter' => '',
        'EncodingType' => 'url',
        'KeyMarker' => 'doc/picture.jpg',
        'VersionIdMarker' => 'MTg0NDUxODMyMTE2ODY0OTExOTk3W',
        'Prefix' => 'doc',
        'MaxKeys' => 1000,
    )); 
    print_r($result);
} catch (\Exception $e) {
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| --------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket   | String | Bucket name in the format: `BucketName-APPID`     | Yes |
| Prefix | String  | Filters the object keys prefixed with the value of this parameter. It is left empty by default. | No |
| Delimiter | String | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | No |
| KeyMarker | String      | Marks the starting key of the returned object list. Entries are listed in UTF-8 binary order by default. | No   |
| VersionIdMarker | String  | Marks the starting VersionId of the returned object list. Entries are listed in UTF-8 binary order by default. | No |
| MaxKeys | Int  | Maximum number of returned objects; the default value is 1,000. | No |
| EncodingType | String | Indicates the encoding method of the returned value. The value is not encoded by default. Valid value: `url`  | No |

#### Sample returned result

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Name] => examplebucket-1250000000
            [Prefix] => doc
            [KeyMarker] => string
            [VersionIdMarker] => string
            [MaxKeys] => 10
            [IsTruncated] => 1
            [NextKeyMarker] => string
            [NextVersionIdMarker] => string
            [Versions] => Array
                (
                    [0] => Array
                        (
                            [Key] => doc/exampleobject1
                            [VersionId] => null
                            [IsLatest] => 1
                            [LastModified] => 2019-06-13T09:24:52.000Z
                            [ETag] => "96e79218965eb72c92a549dd5a330112"
                            [Size] => 6
                            [StorageClass] => STANDARD
                            [Owner] => Array
                                (
                                    [UID] => 1251668577
                                )
                        )

                    [1] => Array
                        (
                            [Key] => doc/exampleobject2
                            [VersionId] => MTg0NDUxODMyMTE2ODY0OTExOTk
                            [IsLatest] => 1
                            [LastModified] => 2019-06-18T12:47:03.000Z
                            [ETag] => "698d51a19d8a121ce581499d7b701668"
                            [Size] => 3
                            [StorageClass] => STANDARD
                            [Owner] => Array
                                (
                                    [UID] => 1251668577
                                )
                        )
                    )
            [RequestId] => NWQwOGVkZGRfMjViMjU4NjRfODNjN18xMTE5YWI4
        )

)
```

#### Returned result description

| Parameter Name | Type | Description | Parent Node |
| ------------------- | ------ | ------------------------------------------------------------ | -------- |
| Name | String | Bucket name in the format: `BucketName-APPID`                         | None |
| Delimiter | String | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | None |
| EncodingType        | String | Specifies the encoding type of the returned value | None |
| KeyMarker | String  | Marks the starting key of the returned object list. Entries are listed using UTF-8 binary order by default.  | None |
| VersionIdMarker | String |  Marks the starting VersionId of the returned object list. Entries are listed using UTF-8 binary order by default.   |  None |
| NextKeyMarker | String | Marks the starting key of the next list of returned objects if IsTruncated is true. | None |
| NextVersionIdMarker | String | Marks the starting VersionId of the next list of returned objects if `IsTruncated` is set to `true`. | None |
| Prefix | String | Filters the object keys prefixed with the value of this parameter.       | None |
| MaxKeys | Int | Maximum number of returned objects; the default value is 1,000. | None |
| IsTruncated | Int    | Indicates whether the returned objects are truncated | None |
| Versions            | Array  | An array of metadata on all the versions of each object                            | None       |
| Version | Array | List of the metadata of objects with multiple versions, including 'ETag', 'StorageClass', 'Key', 'VersionId', 'IsLatest', 'Owner', 'LastModified', and 'Size' | Versions |
| CommonPrefixes | Array  | All objects starting with a particular prefix and ending with the delimiter are grouped as a common prefix | None |



### Uploading an object by using simple upload

#### API description

This API is used to upload an object to a specified bucket. You can upload objects up to 5 GB in size. Please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) to upload objects greater than 5 GB.

#### Method prototype

```php
public Guzzle\Service\Resource\Model putObject(array $args = array())
```

#### Sample request

#### Sample 1. Uploading a local file

[//]: # ".cssg-snippet-put-object"

```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID 
        'Key' => 'exampleobject', 
        'Body' => fopen('path/to/localFile', 'rb'), 
    )); 
    // Request successful 
    print_r($result);
} catch (\Exception $e) { 
    // Request failed 
    echo($e); 
}
```

#### Sample 2. Upload a file to ARCHIVE

[//]: # ".cssg-snippet-put-object-archive"

```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID 
        'Key' => 'exampleobject', 
        'Body' => fopen('path/to/localFile', 'rb'), 
        'StorageClass' => 'Archive'
    )); 
    // Request successful 
    print_r($result); 
} catch (\Exception $e) { 
    // Request failed 
    echo($e); 
}
```

#### Sample 3. Uploading a file with a specified `Content-type`

[//]: # ".cssg-snippet-put-object-with-content-type"

```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID 
        'Key' => 'exampleobject', 
        'Body' => fopen('path/to/localFile', 'rb'), 
        'ContentType' => 'text/xml'
    )); 
    // Request successful 
    print_r($result); 
} catch (\Exception $e) { 
    // Request failed 
    echo($e); 
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | Yes |
| Key | String | Object key is the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg`  | No |
| ACL | String | Sets the object ACL, e.g. 'private', 'public-read' | No |
| Body | File/String | Uploaded content                                                   | Yes |
| CacheControl | String | Cache policy. Sets `Cache-Control`. | No |
| ContentDisposition | String | File name. Sets `Content-Disposition`. | No |
| ContentEncoding | String | Encoding format. Sets `Content-Encoding` | No |
| ContentLanguage | String | Language type. Sets `Content-Language` | No |
| ContentLength | Int | Sets the length of the request content | No |
| ContentType | String | Content type. Sets `Content-Type`. | No |
| Expires | String | Sets `Content-Expires`. | No |
| Metadata             | Array       | User-defined file metadata                                       | No       |
| StorageClass | String | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD`  | No |
| ContentMD5 | String | Sets the MD5 checksum of the uploaded file | No |
| ServerSideEncryption | String | Server-side encryption method | No |

#### Sample returned result

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "698d51a19d8a121ce581499d7b701668"
            [VersionId] => MTg0NDUxODMyMTE2ODY0OTExOTk
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ObjectURL] => http://lewzylucd2-1251668577.cos.ap-chengdu.myqcloud.com/123
        )

)

```

#### Returned result description

| Parameter Name | Type | Description | Parent Node |
| --------- | ------ | -------------------------- | ------ |
| ETag | String | MD5 checksum of the uploaded file  | None |
| VersionId | String | Version ID of the file if versioning is enabled. | None  |

### Querying object metadata

#### API description

The API is used to query object metadata.

#### Method prototype

```php
public Guzzle\Service\Resource\Model headObject(array $args = array());
```

#### Sample request

[//]: # ".cssg-snippet-head-object"

```php
try {
    $result = $cosClient->headObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | Yes |
| Key | String | Object key is the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, <br>the object key is `doc/pic.jpg` | Yes |
| VersionId | String | Version ID of the specified file if versioning is enabled. | No  |

#### Sample returned result

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [DeleteMarker] => 
            [AcceptRanges] => 
            [Expiration] => 
            [Restore] => 
            [LastModified] => Tue, 02 Apr 2019 12:38:09 GMT
            [ContentLength] => 238186
            [ETag] => "af9f3b8eaf64473278909183abba1e31"
            [MissingMeta] => 
            [VersionId] => 
            [CacheControl] => 
            [ContentDisposition] => 
            [ContentEncoding] => 
            [ContentLanguage] => 
            [ContentType] => text/plain; charset=utf-8
            [Expires] => 
            [ServerSideEncryption] => 
            [Metadata] => Array
                (
                    [md5] => af9f3b8eaf64473278909183abba1e31
                )
            [SSECustomerAlgorithm] => 
            [SSECustomerKeyMD5] => 
            [SSEKMSKeyId] => 
            [StorageClass] => 
            [RequestCharged] => 
            [ReplicationStatus] => 
            [RequestId] => NWNhMzU3Y2ZfMzFhYzM1MGFfODdhMF8xOTExM2U=
        )

)
```

#### Returned result description

| Parameter Name | Type | Description | Parent Node |
| -------------------- | ------ | -------------------------------------------------- | ------ |
| CacheControl | String | Cache policy. Sets `Cache-Control`. | None |
| ContentDisposition | String | File name. Sets `Content-Disposition` | None |
| ContentEncoding | String | Encoding format. Sets `Content-Encoding` | None |
| ContentLanguage | String | Language type. Sets `Content-Language` | None |
| ContentLength | Int | Sets the length of the request content | None |
| ContentType | String | Content type. Sets `Content-Type`. | None |
| Metadata | Array | User-defined file metadata | None |
| StorageClass | String | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`  | None |
| ServerSideEncryption | String | Server-side encryption method | None |
| ETag | String | MD5 checksum of the file | None |
| Restore | String | Restoration information of the archived file | None |

### Downloading an object

#### API description

This API is used to download an object.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getObject(array $args = array());
```

#### Sample request

#### Sample 1. Download a file

[//]: # ".cssg-snippet-get-object"

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'SaveAs' => 'path/to/localFile',
    )); 
    // Request successful
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 2. Getting file content within a certain byte range

[//]: # ".cssg-snippet-get-object-range"

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'Range' => 'bytes=0-10'
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 3. Downloading a file with a specified version ID

[//]: # ".cssg-snippet-get-object-with-versionId"

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'VersionId' => 'exampleVersionId'
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------------------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | Yes |
| Key | String | Object key is the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, <br>the object key is `doc/pic.jpg` | Yes |
| SaveAs                     | String | Local path for saving the file                                     | No       |
| VersionId                  | String | Version ID of the specified file if versioning is enabled                             | No       |
| Range | String | Sets the byte range of the file to be downloaded in the format: `bytes=first-last` | No |
| ResponseCacheControl | String  | Sets the `Cache-Control` in the response header | No |
| ResponseContentDisposition | String | Sets the `Content-Disposition` in the response header | No |
| ResponseContentEncoding | String | Sets the `Content-Encoding` in the response header | No |
| ResponseContentLanguage  | String | Sets the `Content-Language` in the response header | No |
| ResponseContentType  | String | Sets the `Content-Type` in the response header | No |
| ResponseExpires  | String | Sets the `Content-Expires` in the response header | No |

#### Sample returned result

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Body] => 
            [DeleteMarker] => 
            [AcceptRanges] => bytes
            [Expiration] => 
            [Restore] => 
            [LastModified] => Tue, 02 Apr 2019 20:38:09 GMT
            [ContentLength] => 238186
            [ETag] => "af9f3b8eaf64473278909183abba1e31"
            [MissingMeta] => 
            [VersionId] => 
            [CacheControl] => 
            [ContentDisposition] => 
            [ContentEncoding] => 
            [ContentLanguage] => 
            [ContentRange] => 
            [ContentType] => text/plain; charset=utf-8
            [Expires] => 
            [WebsiteRedirectLocation] => 
            [ServerSideEncryption] => 
            [Metadata] => Array
                (
                    [md5] => af9f3b8eaf64473278909183abba1e31
                )

            [SSECustomerAlgorithm] => 
            [SSECustomerKeyMD5] => 
            [SSEKMSKeyId] => 
            [StorageClass] => 
            [RequestCharged] => 
            [ReplicationStatus] => 
            [RequestId] => NWNhNDBmYzBfNmNhYjM1MGFfMmUzYzFfMWIzMDYz
        )

)
```

#### Returned result description

| Parameter Name | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------------------ | ------ |
| Body | File/String | Downloaded content                                                   | None |
| ETag | String | MD5 checksum of the file | None |
| Expires | String | Content-Expires | None |
| Metadata | Array | User-defined file metadata | None |
| StorageClass | String | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD`  | None |
| ContentMD5 | String | Sets the MD5 checksum of the uploaded file | None |
| ServerSideEncryption | String | Server-side encryption method | None |
| CacheControl | String | Cache policy. Sets `Cache-Control`. | None |
| ContentDisposition | String | File name. Sets `Content-Disposition` | None |
| ContentEncoding | String | Encoding format. Sets `Content-Encoding` | None |
| ContentLanguage | String | Language type. Sets `Content-Language`                              | None |
| ContentLength | Int | Sets the length of the request content | None |
| ContentType | String | Content type. Sets `Content-Type`. | None |
| Metadata | Array | User-defined file metadata | None |
| Restore | String | Restoration information of the archived file | None |

### Copying an object

This API is used to copy an object to the destination path.

#### Method prototype

```php
public Guzzle\Service\Resource\Model copyObject(array $args = array());
```

#### Sample request

#### Sample 1. Copying an object

[//]: # ".cssg-snippet-copy-object"

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 2. Copying an object with specified version ID

[//]: # ".cssg-snippet-copy-object-with-versionId"

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject?versionId=MTg0NDUxNjI3NTM0ODE2Njc0MzU',
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 3. Changing the storage class to `ARCHIVE`

[//]: # ".cssg-snippet-copy-object-update-storage-class"

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'StorageClass' => 'Archive'
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 4. Modifying metadata

[//]: # ".cssg-snippet-copy-object-update-metadata"

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'MetadataDirective' => 'Replaced',
        'Metadata' => array(
            'key1' => 'value1',
            'key2' => 'value2',
        )
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ----------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | Yes |
| Key | String | Object key is the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, <br>the object key is `doc/pic.jpg` | Yes |
| CopySource | String | Describes the path to the source object, including `Appid`, `Bucket`, `Key`, and `Region`, <br>for example, `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | Yes |
| MetadataDirective | String | Valid values: 'Copy': ignore the configured metadata and copy the file directly; 'Replaced': modify the metadata according to the configured metadata. If the destination path is identical to the source path, this parameter must be set to ‘Replaced’. | No |

### Deleting one single object

#### API description

This API is used to delete a specified object (file/object) from a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteObject(array $args = array());
```

#### Sample request

[//]: # ".cssg-snippet-delete-object"

```php
try {
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'VersionId' => 'exampleVersionId'
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | Yes |
| Key | String | Object key is the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, <br>the object key is `doc/pic.jpg` | Yes |
| VersionId | String | Version ID of the deleted file                                             | No       |

### Deleting multiple objects

#### API description

This API is used delete multiple objects from a specified bucket in a single request.

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteObjects(array $args = array());
```

#### Sample request

[//]: # ".cssg-snippet-delete-multi-object"

```php
try {
    $result = $cosClient->deleteObjects(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Objects' => array(
            array(
                'Key' => 'exampleobject',
                'VersionId' => 'string'
            ),  
            // ... repeated
        ),  
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | Yes |
| Objects   | Array  | List of deleted objects                                                 | Yes       |
| Object   | Array  | Deleted object                                                 | Yes       |
| Key | String | Object key is the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, <br>the object key is `doc/pic.jpg` | Yes |
| VersionId | String | Version ID of the deleted file                                             | No       |

#### Sample returned result

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Deleted] => Array
                (
                    [0] => Array
                        (
                            [Key] => exampleobject1
                        )
                )
            [Errors] => Array
                (
                    [0] => Array
                        (
                            [Key] => exampleobject2
                            [Code] => 
                            [Message] => 
                        )
                )
            [RequestId] => NWNhZWYzYWNfMTlhYTk0MGFfNGRjX2MzZTVhOQ==
        )
）
```

#### Returned result description

| Parameter Name | Type | Description | Parent Node |
| -------- | ------ | -------------------- | -------------- |
| Deleted | Array | List of successfully deleted objects | None |
| Errors   | Array  | List of objects that failed to be deleted | None |
| Key      | String | Object key | Deleted/Errors |
| Code     | String | Error code for failed operations | Errors |
| Message  | String | Error message for failed operations | Errors |

### Restoring an archived object 

#### API description

This API is used to retrieve an archived object for access.

#### Method prototype

```php
public Guzzle\Service\Resource\Model restoreObject(array $args = array());
```

#### Sample request

[//]: # ".cssg-snippet-restore-object"

```php
try {
    $result = $cosClient->restoreObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'Days' => 10,
        'CASJobParameters' => array(
            'Tier' =>'Expedited'
        )    
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ---------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| Days | String | Sets the number of days before the temporary copy expires | Yes |
| CASJobParameters | Array  | Restoration information | Yes |
| Tier | String | When restoring data, you can use `Tier` to specify one of the three restoration types supported by CAS: `Expedited`, `Standard`, and `Bulk`. | Yes |

## Multipart Operations

Operations related to multipart upload include the following:

- Uploading objects with multipart upload: initializing a multipart upload, uploading parts, and completing a multipart upload.
- Resuming a multipart upload: querying uploaded parts, uploading remaining parts, and completing a multipart upload.
- Deleting uploaded parts.

### Querying a multipart upload

#### API description

This API is used to query in-progress multipart uploads in a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model listMultipartUploads(array $args = array());
```

#### Sample request

[//]: # ".cssg-snippet-list-multi-upload"

```php
try {
    $result = $cosClient->listMultipartUploads(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Delimiter' => '/',
        'EncodingType' => 'url',
        'KeyMarker' => 'prfixKeyMarker',
        'UploadIdMarker' => 'string',
        'Prefix' => 'prfix',
        'MaxUploads' => 1000,
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | Yes |
| Delimiter | String | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | No |
| EncodingType | String | Indicates the encoding method of the returned value. The value is not encoded by default. Valid value: `url`  | No |
| KeyMarker | String | Marks the starting key of the list of returned parts | No |
| UploadIdMarker | String | Marks the starting upload ID of the list of returned parts                            | No |
| Prefix | String | Filters the object keys prefixed with the value of this parameter. It is left empty by default.  | No |
| MaxUploads  | Int | The maximum number of returned parts; the default value is 1,000. | No |

#### Sample returned result

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Bucket] => examplebucket-1250000000
            [EncodingType] => 
            [KeyMarker] => 
            [UploadIdMarker] => 
            [MaxUploads] => 1000
            [Prefix] => 
            [IsTruncated] => 
            [Uploads] => Array
                (
                    [0] => Array
                        (
                            [Key] => exampleobject
                            [UploadId] => 1551693693b1e6d0e00eec30c534059865ec89c9393028b60bfaf167e9420524b25eeb2940
                            [Initiator] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [Owner] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                            [Initiated] => 2019-03-04T10:01:33.000Z
                        )

                    [1] => Array
                        (
                            [Key] => exampleobject
                            [UploadId] => 155374001100563fe0e9d37964d53077e54e9d392bce78f630359cd3288e62acee2b719534
                            [Initiator] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [Owner] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                            [Initiated] => 2019-03-28T02:26:51.000Z
                        )

                )

            [RequestId] => NWNhNDJmNzBfZWFhZDM1MGFfMjYyM2FfMWIyNzhh
        )

)
```

#### Returned result description

| Parameter Name | Type | Description | Parent Node |
| ------------ | ------ | ---------------------------------- | ------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | None |
| IsTruncated | Int    | Indicates whether the returned objects are truncated | None |
| Uploads | Array  | List of returned parts                     | None |
| Upload | Array  | Attributes of the returned parts | Uploads |
| Key | String | Object key | Upload  |
| UploadId | String | ID of the multipart upload                 | Upload  |
| Initiator    | String | Initiator of the multipart upload | Upload  |
| Owner        | String | Owner of the multipart upload | Upload  |
| StorageClass | String | Storage class of the multipart upload | Upload  |
| Initiated    | String | Time the multipart upload was initiated | Upload  |



### <span id = "INIT_MULIT_UPLOAD">Initializing a multipart upload</span>

#### API description

This API is used to initialize a multipart upload.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMultipartUpload(array $args = array());
```

#### Sample request

[//]: # ".cssg-snippet-init-multi-upload"

```php
try {
    $result = $cosClient->createMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | Yes |
| Key | String | Object key is the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, <br>the object key is `doc/pic.jpg` | Yes |
| CacheControl | String | Cache policy. Sets `Cache-Control`. | No |
| ContentDisposition | String | File name. Sets `Content-Disposition`. | No |
| ContentEncoding | String | Encoding format. Sets `Content-Encoding` | No |
| ContentLanguage | String | Language type. Sets `Content-Language` | No |
| ContentLength | Int | Sets the length of the request content | No |
| ContentType | String | Content type. Sets `Content-Type`. | No |
| Expires | String | Sets `Content-Expires`. | No |
| Metadata | Array | User-defined file metadata | No |
| StorageClass | String | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD`  | No |
| ContentMD5 | String | Sets the MD5 checksum of the uploaded file | No |
| ServerSideEncryption | String | Server-side encryption method | No |

#### Sample returned result

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Bucket] => examplebucket-1250000000
            [Key] => exampleobject
            [UploadId] => 1554277569b3e83df05c730104c325eb7b56000449fb7d51300b0728aacde02a6ea7f6c033
            [RequestId] => NWNhNDY0YzFfMmZiNTM1MGFfNTM2YV8xYjliMTg=
        )

)
```

#### Returned result description

| Parameter Name | Type | Description | Parent Node |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | None |
| Key  | String | Object key | None |
| UploadId  | String | ID of the multipart upload | None |




### <span id = "MULIT_UPLOAD_PART"> Uploading parts</span>

This API is used to upload parts.

#### Method prototype

```php
public Guzzle\Service\Resource\Model uploadPart(array $args = array());
```

#### Sample request

[//]: # ".cssg-snippet-upload-part"

```php
try {
    $result = $cosClient->uploadPart(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject', 
        'Body' => 'string',
        'UploadId' => 'exampleUploadId', // UploadId is the ID of the multipart upload, which you can get in the response of the initialization of the multipart upload 
        'PartNumber' => 1, // Part number; COS will merge parts based on part number
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| UploadId | String | ID of the multipart upload. This value is returned in the response of the initialization of the multipart Upload | Yes |
| Body | File/String | Uploaded content | Yes |
| PartNumber | Int | Part number; COS will merge parts based on part number | Yes |
| ContentLength | Int | Sets the length of the request content | No |
| ContentMD5 | String | Sets the MD5 checksum of the uploaded file | No |

#### Sample returned result

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "96e79218965eb72c92a549dd5a330112"
            [RequestId] => NWNhNDdjYWFfNjNhYjM1MGFfMjk2NF8xY2ViMWM=
        )

)
```

#### Returned result description

| Parameter Name | Type | Description | Parent Node |
| -------- | ------ | ------------- | ------ |
| ETag | String | MD5 checksum of the part | None |




### Copying parts

#### API description

This API is used to copy an object as a part.

#### Method prototype

```php
public Guzzle\Service\Resource\Model uploadPartCopy(array $args = array());
```

#### Sample request

[//]: # ".cssg-snippet-upload-part-copy"

```php
try {
    $result = $cosClient->uploadPartCopy(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject', 
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'CopySourceRange' => 'bytes=0-1', // For example, copy only the first 2 bytes.
        'UploadId' => 'exampleUploadId', // UploadId is the ID of the multipart upload, which you can get in the response of the initialization of the multipart upload 
        'PartNumber' => 1, // Part number; COS will merge parts based on part number
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| UploadId | String | ID of the multipart upload. This value is returned in the response of the initialization of the multipart Upload | Yes |
| CopySource | String | Describes the path to the source object, including `APPID`, `Bucket`, `Key`, and `Region`, <br>for example, `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | Yes |
| CopySourceRange | String | Describes the byte range of the source object to be copied in the format: `bytes=first-last`. The entire source object will be copied by default if no range is specified. | No |
| PartNumber | Int | Part number; COS will merge parts based on part number | Yes |
| ContentLength | Int | Sets the length of the request content | No |
| ContentMD5 | String | Sets the MD5 checksum of the uploaded file | No |

#### Sample returned result

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "96e79218965eb72c92a549dd5a330112"
            [LastModified] => "2017-09-04T04:45:45"
            [RequestId] => NWNhNDdjYWFfNjNhYjM1MGFfMjk2NF8xY2ViMWM=
        )

)
```

#### Returned result description

| Parameter Name | Type | Description | Parent Node |
| ------------ | ------ | ------------------------------ | ------ |
| ETag | String | MD5 checksum of the part | None |
| LastModified | String | Returns the date/time the object was last modified in GMT format | None |


### <span id = "LIST_MULIT_UPLOAD"> Querying uploaded parts </span>

#### API description

This API is used to query the uploaded parts of a specific multipart upload operation.

#### Method prototype

```php
public Guzzle\Service\Resource\Model listParts(array $args = array());
```

#### Sample request

[//]: # ".cssg-snippet-list-parts"

```php
try {
    $result = $cosClient->listParts(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'UploadId' => 'exampleUploadId',
        'PartNumberMarker' => 1,
        'MaxParts' => 1000,
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ---------------- | ------ | --------------------------------------- | -------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| UploadId  | String | ID of the multipart upload | Yes |
| PartNumberMarker | Int | Marks the starting part of the list of returned parts | No |
| MaxParts | Int | The maximum number of returned parts; the default value is 1,000. | No |

#### Sample returned result

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Bucket] => examplebucket-1250000000
            [Key] => exampleobject
            [UploadId] => 1554279643cf19d71bb5fb0d29613e5541131f3a96387d9e168cd939c23a3d608c9eb94707
            [Owner] => Array
                (
                    [ID] => 1250000000
                    [DisplayName] => 1250000000
                )
            [PartNumberMarker] => 1
            [Initiator] => Array
                (
                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                    [DisplayName] => 100000000001
                )
            [StorageClass] => Standard
            [MaxParts] => 1000
            [IsTruncated] => 
            [Parts] => Array
                (
                    [0] => Array
                        (
                            [PartNumber] => 2
                            [LastModified] => 2019-04-03T08:21:28.000Z
                            [ETag] => "b948e77469189ac94b98e09755a6dba9"
                            [Size] => 1048576
                        )
                    [1] => Array
                        (
                            [PartNumber] => 3
                            [LastModified] => 2019-04-03T08:21:22.000Z
                            [ETag] => "9e5060e2994ec8463bfbebd442fdff16"
                            [Size] => 1048576
                        )                       
                )
            [RequestId] => NWNhNDZkNTJfOGNiMjM1MGFfMTRlYl8xYmJiOTU=
        )

)
```

#### Returned result description

| Parameter Name | Type | Description | Parent Node |
| ---------------- | ------ | --------------------------------------- | ------ |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | None |
| Key | String | Object key | None |
| UploadId  | String | ID of the multipart upload | None |
| IsTruncated | Int    | Indicates whether the returned objects are truncated | None |
| PartNumberMarker | Int | Marks the starting part of the list of returned parts | None |
| MaxParts | Int | The maximum number of returned parts; the default value is 1,000. | None |
| Initiator | String | Initiator of the multipart upload | None  |
| Parts | Array  | List of returned parts | None |
| Part | Array  | Attributes of the returned parts                          | Parts |
| PartNumber | Int | Part number which serves to identify the part  | Part |
| LastModified | String | Date/time the part was last modified/time | Part |
| ETag | String | MD5 checksum of the part | Part |
| Size | String | Size of the part | Part |



### <span id = "COMPLETE_MULIT_UPLOAD"> Completing a multipart upload </span>

#### API description

This API is used to complete the multipart upload of the entire file.

#### Method prototype

```php
public Guzzle\Service\Resource\Model completeMultipartUpload(array $args = array());

```

#### Sample request

[//]: # ".cssg-snippet-complete-multi-upload"

```php
try {
    $result = $cosClient->completeMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject', 
        'UploadId' => 'exampleUploadId',
        'Parts' => array(
            array(
                'ETag' => 'exampleETag',
                'PartNumber' => 1,
            )), 
            // ... repeated
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ---------- | ------ | ---------------------------------- | -------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| UploadId  | String | ID of the multipart upload | Yes |
| Parts | Array  | List of parts | Yes |
| Part | Array | Information on the uploaded parts | Yes |
| ETag | String | MD5 checksum of the part | Yes |
| PartNumber | Int | Part number which serves to identify the part | Yes |

### <span id = "ABORT_MULIT_UPLOAD"> Aborting a multipart upload </span>

#### API description

This API is used to abort a multipart upload and delete the uploaded parts.

#### Method prototype

```php
public Guzzle\Service\Resource\Model abortMultipartUpload(array $args = array());
```

#### Sample request

[//]: # ".cssg-snippet-abort-multi-upload"

```php
try {
    $result = $cosClient->abortMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject', 
        'UploadId' => 'exampleUploadId',
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------- | ------ | ---------------------------------- | -------- |
| Bucket | String | Bucket name in the format: `BucketName-APPID` | Yes |
| Key      | String | Object key                             | Yes       |
| UploadId  | String | ID of the multipart upload | Yes |



## Advanced APIs (Recommended)

This section encapsulates advanced APIs of COS for uploading and copying. You only need to set the corresponding parameters. The APIs will decide internally whether to perform simple upload/copy or multipart upload/copy based on the file size. Before using the APIs, make sure you have completed the initialization as instructed in [Getting Started](https://intl.cloud.tencent.com/document/product/436/12266).

### Uploading an object

#### API description

This API is used to call a simple upload API operation for small files and a multipart upload API operation for large files based on the file size. Its parameters are the same as those of the `PUT Object` and `Upload Part` APIs.

#### Sample request

#### Sample 1. Uploading an object

[//]: # ".cssg-snippet-transfer-upload-file"

```php
try {
    $result = $cosClient->Upload(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject',
        $body = fopen('path/to/localFile', 'rb')
    );
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 2. Uploading an archived object

[//]: # ".cssg-snippet-transfer-upload-file-archive"

```php
try {
    $result = $cosClient->Upload(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject',
        $body = fopen('path/to/localFile', 'rb'),
        $options = array(
            'StorageClass' => 'Archive'
        )
    );
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 3. Uploading an object with metadata by specifying the size of a single part

[//]: # ".cssg-snippet-transfer-upload-file-with-meta"

```php
try {
    $result = $cosClient->Upload(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject',
        $body = fopen('path/to/localFile', 'rb'),
        $options = array(
            'Metadata' => array(
                'string' => 'string',
            ),
            'PartSize' => 10 * 1024 * 1024
        )
    );
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Object replication

#### API description

This API calls the `CopyObject` API operation for small files and the multipart copy API operation for large files based on the file size. Its parameters are the same as those of the `PUT Object - Copy` and `Upload Part - Copy` APIs.

#### Sample request

#### Sample 1. Copying an object

[//]: # ".cssg-snippet-transfer-copy-object"

```php
try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject',
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'sourcebucket-1250000000', 
            'Key' => 'sourceObject', 
        )
    );
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

[//]: # ".cssg-snippet-transfer-copy-object-update-storage-class"

#### Sample 2. Transitioning an object between COS storage classes

```php
try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject',
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'examplebucket-1250000000', 
            'Key' => 'exampleobject', 
        ),
        $options = array(
            'StorageClass' => 'Archive'
        )
    );
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

[//]: # ".cssg-snippet-transfer-copy-object-update-metadata"

##### Sample 3. Modify object storage attributes

```php
try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject',
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'sourcebucket-1250000000', 
            'Key' => 'sourceObject', 
        ),
        $options = array(
            'MetadataDirective' => 'Replaced',
            'Metadata' => array(
                'string' => 'string',
            ),
        )
    );
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```
