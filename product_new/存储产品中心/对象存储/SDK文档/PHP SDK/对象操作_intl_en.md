## Overview

This document provides an overview of APIs and SDK code samples related to advanced APIs, simple operations, and multipart operations of objects.

**Simple operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------------------ | ---------------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying object list | Queries some or all objects in a bucket |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying object and historical version list | Queries some or all objects in a bucket and their historical version information |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Simply uploading an object | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies a file to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting one object | Deletes a specified object in a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |
| [POST Object restore](https://intl.cloud.tencent.com/zh/document/product/436/12633) | Restoring an archived object | Retrieves an archived object for access |

**Multipart upload operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads object parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in a specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire object |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

## Simple Operations

### Querying object list

#### Feature description

This API (List Objects) is used to queries all objects in a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model listObjects(array $args = array());
```

#### Sample request

#### Sample 1. Querying object list with specified prefix and specified start object

[//]: # (.cssg-snippet-get-bucket-comp)

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
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ------------ | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Delimiter | String | Sets the delimiter; for example, set `/` to simulate a folder. This parameter is empty by default | No |
| EncodingType | String | Specifies the encoding method of the returned value. Valid value: url. No encoding is performed by default | No |
| Marker | String |Marks the starting position of the list of returned objects. By default, entries are listed in UTF-8 binary order  | No |
| Prefix | String | Filters object keys to match the objects with a specified prefix. This parameter is empty by default | No |
| MaxKeys | Int | Maximum number of returned objects. Default and maximum values: 1000 | No |

#### Sample return result

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
| Name | String | Bucket name in the format of `BucketName-APPID`                         | None |
| Delimiter | String | Sets the delimiter; for example, set `/` to simulate a folder | None |
| EncodingType | String | Specifies the encoding method of the returned value | None |
| Marker | String |Marks the starting position of the list of returned objects. By default, entries are listed in UTF-8 binary order  | None |
| Prefix | String | Filters object keys to match the objects with a specified prefix | None |
| MaxKeys | Int | Maximum number of returned objects. Default and maximum values: 1000 | None |
| IsTruncated | Int | Indicates whether the returned objects are truncated | None |
| Contents | Array | List of returned objects | None |
| Content | Array | Attributes of the returned objects including a list of metadata of all objects such as 'ETag', 'StorageClass', 'Key', 'Owner', 'LastModified', and 'Size' | Contents |

### Querying object and historical version list 

#### Feature description

This API is used to query some or all objects in a bucket and their historical version information.

#### Method prototype

```
public Guzzle\Service\Resource\Model listObjectVersions(array $args = array());
```

#### Sample request

#### Sample 1. Querying historical object list

[//]: # (.cssg-snippet-list-object-versioning)

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
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Prefix | String | Filters object keys to match the objects with a specified prefix. This parameter is empty by default | No |
| Delimiter | String | Sets the delimiter; for example, set `/` to simulate a folder. This parameter is empty by default | No |
| KeyMarker | String | Marks the starting position of the key in the list of returned objects. By default, entries are listed in UTF-8 binary order  | No |
| VersionIdMarker | String | Marks the starting position of the VersionId in the list of returned objects. By default, entries are listed in UTF-8 binary order  | No |
| MaxKeys | Int | Maximum number of returned objects. Default and maximum values: 1000 | No |
| EncodingType | String | Specifies the encoding method of the returned value. Valid value: url. No encoding is performed by default | No |

#### Sample return result

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
| Name | String | Bucket name in the format of `BucketName-APPID`                         | None |
| Delimiter | String | Sets the delimiter; for example, set `/` to simulate a folder | None |
| EncodingType | String | Specifies the encoding method of the returned value | None |
| KeyMarker | String | Marks the starting position of the key in the list of returned objects. By default, entries are listed in UTF-8 binary order  | None |
| VersionIdMarker | String | Marks the starting position of the VersionId in the list of returned objects. By default, entries are listed in UTF-8 binary order  | None |
| NextKeyMarker | String |Marks the starting position of the key in the list of objects returned next time if IsTruncated is true | None |
| NextVersionIdMarker | String | Marks the starting position of the VersionId in the list of objects returned next time if IsTruncated is true | None |
| Prefix | String | Filters object keys to match the objects with a specified prefix | None |
| MaxKeys | Int | Maximum number of returned objects. Default and maximum values: 1000 | None |
| IsTruncated | Int | Indicates whether the returned objects are truncated | None |
| Versions | Array | List of metadata of all multi-version objects | None |
| Version | Array | List of metadata of all multi-version objects, including information such as 'ETag', 'StorageClass', 'Key', 'VersionId', 'IsLatest', 'Owner', 'LastModified', and 'Size' | Versions |
| CommonPrefixes | Array | All objects starting with `Prefix` and ending in `Delimiter` are grouped into the same class | None |



### Simply uploading an object

#### Feature description

This API (PUT Object) is used to upload an object to a specified bucket. It can upload a file up to 5 GB in size. For larger files, please upload them through [multipart upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89).

#### Method prototype

```php
public Guzzle\Service\Resource\Model putObject(array $args = array())
```

#### Sample request

#### Sample 1. Uploading local file

[//]: # (.cssg-snippet-put-object)

```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID 
        'Key' => 'exampleobject', 
        'Body' => fopen('path/to/localFile', 'rb'), 
    )); 
    // Request succeeded 
    print_r($result);
    $this->versionId = $result['VersionId'];
} catch (\Exception $e) { 
    // Request failed 
    echo($e); 
}
```

#### Sample 2. Uploading file to archive storage

[//]: # (.cssg-snippet-put-object-archive)

```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID 
        'Key' => 'exampleobject', 
        'Body' => fopen('path/to/localFile', 'rb'), 
        'StorageClass' => 'Archive'
    )); 
    // Request succeeded 
    print_r($result); 
} catch (\Exception $e) { 
    // Request failed 
    echo($e); 
}
```

#### Sample 3. Uploading file with specified Content-type

[//]: # (.cssg-snippet-put-object-with-content-type)

```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID 
        'Key' => 'exampleobject', 
        'Body' => fopen('path/to/localFile', 'rb'), 
        'ContentType' => 'text/xml'
    )); 
    // Request succeeded 
    print_r($result); 
} catch (\Exception $e) { 
    // Request failed 
    echo($e); 
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key                  | String      | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg` | No |
| ACL | String | Sets the object ACL such as private and public-read | No |
| Body | File/String | Uploaded content | Yes |
| CacheControl | String | Cache policy, which sets `Cache-Control` | No |
| ContentDisposition | String | Filename, which sets `Content-Disposition` | No |
| ContentEncoding | String | Encoding format, which sets `Content-Encoding` | No |
| ContentLanguage | String | Language type, which sets `Content-Language` | No |
| ContentLength | Int | Sets transfer length | No |
| ContentType | String | Content type, which sets `Content-Type` | No |
| Expires | String | Sets Content-Expires | No |
| Metadata | Array | User-defined file metadata | No |
| StorageClass | String | File storage class. Valid values: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD | No |
| ContentMD5 | String | Sets the MD5 value of the uploaded file for verification | No |
| ServerSideEncryption | String | Server-side encryption method | No |

#### Sample return result

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
| ETag | String | MD5 value of the uploaded file | None |
| VersionId | String | File version number after versioning is enabled | None |

### Querying object metadata

#### Feature description

This API (HEAD Object) is used to query the metadata of an object.

#### Method prototype

```php
public Guzzle\Service\Resource\Model headObject(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-head-object)

```php
try {
    $result = $cosClient->headObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key                        | String | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg` | Yes       |
| VersionId | String | Specifies a file version if versioning is enabled | No |

#### Sample return result

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
| CacheControl | String | Cache policy, which sets `Cache-Control` | None |
| ContentDisposition | String | Filename, which sets `Content-Disposition` | None |
| ContentEncoding | String | Encoding format, which sets `Content-Encoding` | None |
| ContentLanguage | String | Language type, which sets `Content-Language` | None |
| ContentLength | Int | Sets transfer length | None |
| ContentType | String | Content type, which sets `Content-Type` | None |
| Metadata | Array | User-defined file metadata | None |
| StorageClass | String | File storage class. Valid values: STANDARD, STANDARD_IA, ARCHIVE | None |
| ServerSideEncryption | String | Server-side encryption method | None |
| ETag | String | MD5 value of a file | None |
| Restore | String | Restoration information of an archived file | None |

### Downloading object

#### Feature description

This API (GET Object) is used to download an object to the local file system.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getObject(array $args = array());

```

#### Sample request

#### Sample 1. Downloading file to local file system

[//]: # (.cssg-snippet-get-object)

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'SaveAs' => 'path/to/localFile',
    )); 
    // Request succeeded
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 2. Downloading file in multiple parts

[//]: # (.cssg-snippet-get-object-range)

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'Range' => 'bytes=0-10'
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 3. Downloading file on specified version

[//]: # (.cssg-snippet-get-object-with-versionId)

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'VersionId' => 'exampleVersionId'
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------------------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key                        | String | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg` | Yes       |
| SaveAs | String | Path to the file saved locally | No |
| VersionId | String | Specifies a file version if versioning is enabled | No |
| Range | String | Sets the range of file download in the format of `bytes=first-last` | No |
| ResponseCacheControl | String | Sets the response header Cache-Control | No|
| ResponseContentDisposition | String | Sets the response header Content-Disposition  | No |
| ResponseContentEncoding | String | Sets the response header Content-Encoding | No |
| ResponseContentLanguage | String | Sets the response header Content-Language  | No |
| ResponseContentType | String | Sets the response header Content-Type | No |
| ResponseExpires | String | Sets the response header Content-Expires | No |

#### Sample return result

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
| Body | File/String | Downloaded content | None |
| ETag | String | MD5 value of a file | None |
| Expires | String | Content-Expires | None |
| Metadata | Array | User-defined file metadata | None |
| StorageClass | String | File storage class. Valid values: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD | None |
| ContentMD5 | String | Sets the MD5 value of the uploaded file for verification | None |
| ServerSideEncryption | String | Server-side encryption method | None |
| CacheControl | String | Cache policy, which sets `Cache-Control` | None |
| ContentDisposition | String | Filename, which sets `Content-Disposition` | None |
| ContentEncoding | String | Encoding format, which sets `Content-Encoding` | None |
| ContentLanguage | String | Language type, which sets `Content-Language` | None |
| ContentLength | Int | Sets transfer length | None |
| ContentType | String | Content type, which sets `Content-Type` | None |
| Metadata | Array | User-defined file metadata | None |
| Restore | String | Restoration information of an archived file | None |

### Setting object replication

This API (Put Object - Copy) is used to copy an object to the destination path.

#### Method prototype

```php
public Guzzle\Service\Resource\Model copyObject(array $args = array());

```

#### Sample request

#### Sample 1. Copying object

[//]: # (.cssg-snippet-copy-object)

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 2. Copying object on specified version

[//]: # (.cssg-snippet-copy-object-with-versionId)

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject?versionId=MTg0NDUxNjI3NTM0ODE2Njc0MzU',
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 3. Changing storage class to archive storage

[//]: # (.cssg-snippet-copy-object-update-storage-class)

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'StorageClass' => 'Archive'
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 4. Modifying meta attributes

[//]: # (.cssg-snippet-copy-object-update-metadata)

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
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ----------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key                        | String | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg` | Yes       |
| CopySource | String | Describes the path to the source file to be copied, including `Appid`, `Bucket`, `Key`, and `Region`, <br>such as `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | Yes       |
| MetadataDirective | String | Valid values: Copy, Replaced. If this parameter is set to `Copy`, the configured user metadata is ignored and the copy is performed directly; if `Replaced`, the metadata is modified based on the configured metadata. If the destination path is the same as the source path, this parameter has to be set to `Replaced` | No |

### Deleting one single object

#### Feature description

This API is used to delete a specified object (file/object) in a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteObject(array $args = array());

```

#### Sample request

[//]: # (.cssg-snippet-delete-object)

```php
try {
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'VersionId' => 'exampleVersionId'
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key                        | String | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg` | Yes       |
| VersionId | String | Version number of the deleted file | No |

### Deleting multiple objects

#### Feature description

This API is used to delete objects (files/objects) in a bucket in batches.

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteObjects(array $args = array());

```

#### Sample request

[//]: # (.cssg-snippet-delete-multi-object)

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
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Objects | Array | List of deleted objects | Yes |
| Object | Array | Deleted object | Yes |
| Key                        | String | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg` | Yes       |
| VersionId | String | Version number of the deleted file | No |

#### Sample return result

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
| Errors | Array | List of objects that failed to be deleted | None |
| Key | String | Object key | Deleted/Errors |
| Code     | String | Error code for failure           | Errors         |
| Message | String | Error message | Errors |

### Restoring archived object 

#### Feature description

This API (POST Object restore) is used to retrieve an archived object for access.

#### Method prototype

```php
public Guzzle\Service\Resource\Model restoreObject(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-restore-object)

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
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ---------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| Days | String | Sets expiration time of the temporary copy in days | Yes |
| CASJobParameters | Array | Restoration information | Yes |
| Tier | String | For data restoration, Tier can specify the restoration type supported by CAS, including Expedited, Standard, and Bulk | Yes |

## Multipart Upload Operations

With multipart upload, you can do the following:

- Upload an object in parts, including initializing a multipart upload, uploading parts, and completing the multipart upload.
- Resume a multipart upload, including querying uploaded parts, uploading parts, and completing the multipart upload.
- Delete uploaded parts.

### Querying multipart upload

#### Feature description

This API (List Multipart Uploads) is used to query multipart uploads in progress in a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model listMultipartUploads(array $args = array());

```

#### Sample request

[//]: # (.cssg-snippet-list-multi-upload)

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
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Delimiter | String | Sets the delimiter; for example, set `/` to simulate a folder. This parameter is empty by default | No |
| EncodingType | String | Specifies the encoding method of the returned value. Valid value: url. No encoding is performed by default | No |
| KeyMarker | String | Marks the starting position of the list of returned parts | No |
| UploadIdMarker | String | Marks the starting position of the list of returned parts | No |
| Prefix | String | Filters object keys to match the parts with a specified prefix. This parameter is empty by default | No |
| MaxUploads | Int | Maximum number of returned parts. Default and maximum values: 1000 | No |

#### Sample return result

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
| Bucket | String | Bucket name in the format of `BucketName-APPID`                         | None |
| IsTruncated | Int | Indicates whether the returned objects are truncated | None |
| Uploads | Array | List of returned parts | None |
| Upload | Array | Attribute of returned parts | Uploads |
| Key | String | Object key name | Upload |
| UploadId | String | Multipart upload ID of an object | Upload |
| Initiator | String | The operator who initialized the multipart upload | Upload |
| Owner | String | Part owner | Upload |
| StorageClass | String | Part storage class | Upload |
| Initiated | String | Multipart upload initialization time | Upload |



### <span id = "INIT_MULIT_UPLOAD">Initializing multipart upload</span>

#### Feature description

This API (Initiate Multipart Upload) is used to initialize a multipart upload operation.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMultipartUpload(array $args = array());

```

#### Sample request

[//]: # (.cssg-snippet-init-multi-upload)

```php
try {
    $result = $cosClient->createMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
    )); 
    // Request succeeded
    print_r($result);
    $this->uploadId = $result['UploadId'];
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key                        | String | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg` | Yes       |
| CacheControl | String | Cache policy, which sets `Cache-Control` | No |
| ContentDisposition | String | Filename, which sets `Content-Disposition` | No |
| ContentEncoding | String | Encoding format, which sets `Content-Encoding` | No |
| ContentLanguage | String | Language type, which sets `Content-Language` | No |
| ContentLength | Int | Sets transfer length | No |
| ContentType | String | Content type, which sets `Content-Type` | No |
| Expires | String | Sets Content-Expires | No |
| Metadata | Array | User-defined file metadata | No |
| StorageClass | String | File storage class. Valid values: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD | No |
| ContentMD5 | String | Sets the MD5 value of the uploaded file for verification | No |
| ServerSideEncryption | String | Server-side encryption method | No |

#### Sample return result

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

| Parameter name | Type | Description | Parent Node |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | String | Bucket name in the format of `BucketName-APPID`                         | None |
| Key | String | Object key | None |
| UploadId | String | Multipart upload ID of an object | None |




### <span id = "MULIT_UPLOAD_PART">Uploading parts</span>

This API (Upload Part) is used to upload a file in parts.

#### Method prototype

```php
public Guzzle\Service\Resource\Model uploadPart(array $args = array());

```

#### Sample request

[//]: # (.cssg-snippet-upload-part)

```php
try {
    $result = $cosClient->uploadPart(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject', 
        'Body' => 'string',
        'UploadId' => 'exampleUploadId', // `UploadId` is the multipart upload ID of an object, which can be obtained from the return parameter of multipart upload initialization 
        'PartNumber' => 1, // `PartNumber` is the serial number of a part, which will be used by COS to merge parts
    )); 
    // Request succeeded
    print_r($result);
    $this->eTag = $result['ETag'];
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| UploadId      | String      | `UploadId` is the multipart upload ID of an object, which can be obtained from the return parameter of multipart upload initialization | Yes |
| Body | File/String | Uploaded content | Yes |
| PartNumber    | Int         | `PartNumber` is the serial number of a part, which will be used by COS to merge parts | Yes       |
| ContentLength | Int | Sets transfer length | No |
| ContentMD5 | String | Sets the MD5 value of the uploaded file for verification | No |

#### Sample return result

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
| ETag | String | MD5 value of a part | None |




### Copying parts

#### Feature description

This API (Upload Part - Copy) is used to copy an object as a part.

#### Method prototype

```php
public Guzzle\Service\Resource\Model uploadPartCopy(array $args = array());

```

#### Sample request

[//]: # (.cssg-snippet-upload-part-copy)

```php
try {
    $result = $cosClient->uploadPartCopy(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject', 
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'CopySourceRange' => 'bytes=0-1', // This example copies only the first two bytes
        'UploadId' => 'exampleUploadId', // `UploadId` is the multipart upload ID of an object, which can be obtained from the return parameter of multipart upload initialization 
        'PartNumber' => 1, // `PartNumber` is the serial number of a part, which will be used by COS to merge parts
    )); 
    // Request succeeded
    print_r($result);
    $this->eTag = $result['ETag'];
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| UploadId      | String      | `UploadId` is the multipart upload ID of an object, which can be obtained from the return parameter of multipart upload initialization | Yes |
| CopySource | String | Describes the path to the source file to be copied, including `Appid`, `Bucket`, `Key`, and `Region`, <br>such as `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | Yes       |
| CopySource    | String | Describes the scope of source object copying in the format of `bytes=first-last`. If this parameter is not specified, the entire source object will be copied by default | No |
| PartNumber    | Int         | `PartNumber` is the serial number of a part, which will be used by COS to merge parts | Yes       |
| ContentLength | Int | Sets transfer length | No |
| ContentMD5 | String | Sets the MD5 value of the uploaded file for verification | No |

#### Sample return result

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
| ETag | String | MD5 value of a part | None |
| LastModified | String | Returns the last modified time of the object in GMT time | No     |







### <span id = "LIST_MULIT_UPLOAD">Querying uploaded parts</span>

#### Feature description

This API (List Parts) is used to query uploaded parts in a specified multipart upload operation.

#### Method prototype

```php
public Guzzle\Service\Resource\Model listParts(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-list-parts)

```php
try {
    $result = $cosClient->listParts(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'UploadId' => 'exampleUploadId',
        'PartNumberMarker' => 1,
        'MaxParts' => 1000,
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ---------------- | ------ | --------------------------------------- | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| UploadId | String | Multipart upload ID of an object | Yes |
| PartNumberMarker | Int | Marks the starting position of the list of returned parts | No |
| MaxParts | Int | Maximum number of returned parts. Default and maximum values: 1000 | No |

#### Sample return result

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
| Bucket | String | Bucket name in the format of `BucketName-APPID`                         | None |
| Key | String | Object key | None |
| UploadId | String | Multipart upload ID of an object | None |
| IsTruncated | Int | Indicates whether the returned objects are truncated | None |
| PartNumberMarker | Int | Marks the starting position of the list of returned parts | None |
| MaxParts | Int | Maximum number of returned parts. Default and maximum values: 1000 | None |
| Initiator | String | The operator who initialized the multipart upload | None |
| Parts | Array | List of returned parts | None |
| Part | Array | Attribute of returned parts | Parts |
| PartNumber | Int | Part number | Part |
| LastModified | String | Last uploaded time of a part | Part |
| ETag | String | MD5 value of a part | Part |
| Size | String | Part size | Part |



### <span id = "COMPLETE_MULIT_UPLOAD">Completing multipart upload</span>

#### Feature description

The API (Complete Multipart Upload) is used to complete the multipart upload of the entire file.

#### Method prototype

```php
public Guzzle\Service\Resource\Model completeMultipartUpload(array $args = array());

```

#### Sample request

[//]: # (.cssg-snippet-complete-multi-upload)

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
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ---------- | ------ | ---------------------------------- | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| UploadId | String | Multipart upload ID of an object | Yes |
| Parts | Array | Part information list | Yes |
| Part | Array | Content information of an uploaded part | Yes |
| ETag | String | MD5 value of a part | Yes |
| PartNumber | Int | Part number | Yes |

### <span id = "ABORT_MULIT_UPLOAD">Aborting multipart upload</span>

#### Feature description

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts.

#### Method prototype

```php
public Guzzle\Service\Resource\Model abortMultipartUpload(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-abort-multi-upload)

```php
try {
    $result = $cosClient->abortMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject', 
        'UploadId' => 'exampleUploadId',
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------- | ------ | ---------------------------------- | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| UploadId | String | Multipart upload ID of an object | Yes |



## Advanced APIs (Recommended)

This section describes the advanced APIs provided by COS that encapsulate the upload and copy operations. You only need to set the corresponding parameters, and the APIs will decide whether to perform simple upload/copy or multipart upload/copy according to the file size. Please confirm that the initialization as described in [Getting Started](https://intl.cloud.tencent.com/document/product/436/12266) has been completed before you use these APIs.

### Composite upload

#### Feature description

Based on the file size, this API internally calls the simple upload API for small files or multipart upload API for large files. For the API parameters, please see the `PutObject` API.

#### Sample request

#### Sample 1. Uploading local object

[//]: # (.cssg-snippet-transfer-upload-object)

```php
try {
    $result = $cosClient->Upload(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject',
        $body = fopen('path/to/localFile', 'rb')
    );
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 2. Uploading object to archive storage

[//]: # (.cssg-snippet-transfer-upload-object-archive)

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
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 3. Uploading object containing meta with part size specified

[//]: # (.cssg-snippet-transfer-upload-object-comp)

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
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Composite copy

#### Feature description

Based on the file size, this API internally calls the setting object replication API for small files or multipart copy API for large files. For the API parameters, please see the `CopyObject` API.

#### Sample request

#### Sample 1. Copying object

[//]: # (.cssg-snippet-transfer-copy-object)

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
    );
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

[//]: # (.cssg-snippet-transfer-copy-object-update-storage-class)

#### Sample 2. Changing object storage class

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
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

[//]: # (.cssg-snippet-transfer-copy-object-update-metadata)

##### Sample 3. Modifying object storage attributes

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
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```
