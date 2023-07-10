## Overview

This document provides an overview of advanced APIs and APIs for simple object operations and multipart upload operations, as well as their SDK code samples.

**Simple operations**

| API                                                          | Operation                   | Description                                       |
| ------------------------------------------------------------ | ------------------------ | ---------------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying objects | Queries some or all the objects in a bucket. |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying objects and their version history | Queries some or all the objects in a bucket and their version history. |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object in whole | Uploads an object in whole to a bucket. |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | Appending parts | Appends object parts to a bucket.                      |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object. |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system. |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies a file to the destination path. |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes a specified object from a bucket. |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket. |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access. |


**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads an object in multiple parts. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying an object part | Copies a part of an object. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of an object. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |

## Simple Operations

### Query objects

#### Description

This API (`List Objects`) is used to query all the objects in a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model listObjects(array $args = array());
```

#### Sample request

#### Sample 1. Querying a list of objects with the specified prefix starting from a specified object

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
| Delimiter | String | Separator, left empty by default. For example, you can set it to `/` to indicate folders. | No |
| EncodingType | String | Encoding method of the returned value. The value is not encoded by default. Valid value: `url`  | No |
| Marker | String | The object after which the returned list begins. Objects are listed in UTF-8 binary order by default.  | No |
| Prefix | String | Key prefix to query objects by, left empty by default | No |
| MaxKeys | Int | The maximum number of returned objects, which is `1000` (the maximum value allowed) by default | No |

#### Sample response

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

#### Response description

| Parameter | Type | Description | Parent Node | 
| ------------ | ------ | ------------------------------------------------------------ | -------- |
| Name | String | Bucket name in the format of `BucketName-APPID`                         | None |
| Delimiter | String | Separator, left empty by default. For example, you can set it to `/` to indicate folders. | None |
| EncodingType| String | Encoding method of the returned value | None |
| Marker | String | The object after which the returned list begins. Objects are listed in UTF-8 binary order by default.  | None |
| Prefix | String | Key prefix by which objects are queried       | None |
| MaxKeys | Int | The maximum number of returned objects, which is `1000` (the maximum value allowed) by default | None |
| IsTruncated | Int    | Whether the returned objects are truncated | None |
| Contents     | Array  | Returned object list                                              | None       |
| Content | Array | List of the metadata (attributes) of all returned objects, including 'ETag', 'StorageClass', 'Key', 'Owner', 'LastModified', and 'Size' | Contents |

### Querying objects and their version history 

#### Description

This API is used to query some or all the objects in a bucket and their version history.

#### Method prototype

```
public Guzzle\Service\Resource\Model listObjectVersions(array $args = array());
```

#### Sample request

#### Sample 1. Querying objects and their version history

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
| Bucket   | String | Bucket name in the format of `BucketName-APPID`     | Yes |
| Prefix | String  | Key prefix to query objects by, which is left empty by default | No |
| Delimiter | String | Separator, left empty by default. For example, you can set it to `/` to indicate folders. | No |
| KeyMarker | String      | The key of the object after which the returned object list begins. Entries are listed in UTF-8 binary order by default. | No   |
| VersionIdMarker | String  | The version ID of the object after which the returned object list begins. Entries are listed in UTF-8 binary order by default. | No |
| MaxKeys | Int  | The maximum number of returned objects, which is `1000` (the maximum value allowed) by default | No |
| EncodingType | String | Encoding method of the returned value. The value is not encoded by default. Valid value: `url`  | No |

#### Sample response

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
                                    [UID] => 1250000000
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
                                    [UID] => 1250000000
                                )
                        )
                    )
            [RequestId] => NWQwOGVkZGRfMjViMjU4NjRfODNjN18xMTE5YWI4
        )

)
```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | ------ | ------------------------------------------------------------ | -------- |
| Name | String | Bucket name in the format of `BucketName-APPID`                         | None |
| Delimiter | String | Separator, left empty by default. For example, you can set it to `/` to indicate folders. | None |
| EncodingType |String | Encoding method of the returned value | None |
| KeyMarker | String  | The key of the object after which the returned object list begins. Entries are listed in UTF-8 binary order by default.  | None |
| VersionIdMarker | String |  The version ID of the object after which the returned object list begins. Entries are listed in UTF-8 binary order by default.   |  None |
| NextKeyMarker | String | The key of the object after which the next returned list begins if `IsTruncated` is `true` | None |
| NextVersionIdMarker | String | The version ID of the object after which the next returned list begins if `IsTruncated` is `true` | None |
| Prefix | String | Key prefix by which objects are queried       | None |
| MaxKeys | Int | The maximum number of returned objects, which is `1000` (the maximum value allowed) by default | None |
| IsTruncated | Int    | Whether the returned objects are truncated | None |
| Versions            | Array  | List of the metadata of all objects with multiple versions                            | None       |
| Version | Array | List of the metadata of all objects with multiple versions, including `ETag`, `StorageClass`, `Key`, `VersionId`, `IsLatest`, `Owner`, `LastModified`, and `Size` | Versions |
| CommonPrefixes | Array  | All objects starting with the specified prefix and ending with the specified delimiter | None |



### Uploading an object in whole

#### Description

This API (`PUT Object`) is used to upload an object of up to 5 GB to a specified bucket. To upload objects larger than 5 GB, please use [multipart upload APIs](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89).

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
    // Request succeeded 
    print_r($result);
} catch (\Exception $e) { 
    // Request failed 
    echo($e); 
}
```

#### Sample 2. Uploading a file to ARCHIVE

[//]: # ".cssg-snippet-put-object-archive"

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
    // Request succeeded 
    print_r($result); 
} catch (\Exception $e) { 
    // Request failed 
    echo($e); 
}
```

#### Sample 4. Creating an empty virtual directory

[//]: # ".cssg-snippet-put-object-with-new-foler"

```php
try {
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'folder/',
        'Body' => "",
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

```

#### Sample 5. Uploading a ContentMD5-verified local file

```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID 
        'Key' => 'exampleobject', 
        'Body' => fopen('path/to/localFile', 'rb'), 
        'ContentMD5' => true, 
    )); 
    // Request succeeded 
    print_r($result);
} catch (\Exception $e) { 
    // Request failed 
    echo($e); 
}
```

#### Sample 6. Uploading an object (limiting single-URL speed)
>? For more information about the speed limits on object uploads, please see [Single-URL Speed Limits](https://intl.cloud.tencent.com/document/product/436/34072).

```php
try {
$result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-125000000', //Format: BucketName-APPID
        'Key' => 'exampleobject',
        'Body' => fopen($local_path, 'rb'),
        'TrafficLimit' => 8 * 1024 * 1024 // Limit the speed to 1 MB/s.
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```
#### Parameter description

| Parameter | Type | Description | Required |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`.  | No |
| ACL | String | ACL of the object, such as private or public-read | No |
| Body                 | Stream/String | Uploaded content                                                   | Yes       |
| CacheControl | String | Cache policy | No |
| ContentDisposition | String | File name | No |
| ContentEncoding | String | Encoding format | No |
| ContentLanguage | String | Language type | No |
| ContentLength | Int | Length of the content | No |
| ContentType | String | Content type | No |
| Expires | String | `Content-Expires` | No |
| Metadata             | Array       | User-defined file metadata                                       | No       |
| StorageClass | String | Storage class of the object, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | No |
| ContentMD5           | Boolean      | Whether to upload the MD5 checksum of the file for verification                                  | No       |
| ServerSideEncryption | String | Server-side encryption method | No |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "698d51a19d8a121ce581499d7b701668"
            [VersionId] => MTg0NDUxODMyMTE2ODY0OTExOTk
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ObjectURL] => http://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/123
            [CRC] => 16749565679157681890
        )

)

```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| --------- | ------ | -------------------------- | ------ |
| ETag | String | MD5 checksum of the uploaded file  | None |
| VersionId | String | Version ID of the file if versioning is enabled. | None  |
| CRC     | String | CRC64 for [Data Verification](https://intl.cloud.tencent.com/document/product/436/34078) | No |

### Appending parts

#### Description

This API (`APPEND Object`) is used to append object parts to a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model appendObject(array $args = array());
```

#### Sample request

#### Sample 1. Appending input stream
```php
try {
    $result = $cosClient->appendObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'Position' => 0,
        'Body' => "hello,world",
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 2. Appending local file stream
```php
try {
    $result = $cosClient->appendObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'Position' => 0,
        'Body' => fopen('path/to/localFile', 'rb'),
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 3. Appending multiple data

```php
try {
    $result = $cosClient->appendObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'Position' => 0, // Position to append the object
        'Body' => fopen('path/to/localFile', 'rb'),// Read the file content.
    ));
    
    $result = $cosClient->appendObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'Position' => (integer)$result['Position'], // Append to the position of the last append.
        'Body' => "hello, world", 
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | Yes |
| Position | Integer | Starting point for the append operation. For the first append, the value of this parameter is 0. For subsequent appends, the value is the `content-length` of the current object. | Yes |
| Body | File/String | Content of the uploaded part, which can be file stream or byte stream     | Yes |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [ETag] => "9a74ded332531da4c295934ba5a9cf8b"
    [Position] => 4
    [RequestId] => NjExNWU4NTlfZDIyZjJjMGJfM2Q2ZV8xMzJjZThhZg==
    [Key] => exampleobject
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject
)
```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| -------------------- | ------ | -------------------------------------------------- | ------ |
| ETag | String | MD5 checksum of the file | None |
| Position              | Integer | Starting point of the append operation | None  |

### Querying object metadata

#### Description

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
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | Yes |
| VersionId | String | Version ID of the specified file if versioning is enabled | No  |

#### Sample response

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
            [CRC] => 16749565679157681890
        )

)
```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| -------------------- | ------ | -------------------------------------------------- | ------ |
| CacheControl | String | Cache policy | None |
| ContentDisposition | String | File name | None |
| ContentEncoding | String | Encoding format | None |
| ContentLanguage | String | Language type | None |
| ContentLength | Int | Length of the uploaded content | None |
| ContentType | String | Content type | None |
| Metadata | Array | User-defined file metadata | None | 
| StorageClass | String | Storage class of the object, such as `STANDARD`, `STANDARD_IA`, and `ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | None |
| ServerSideEncryption | String | Server-side encryption method | None |
| ETag | String | MD5 checksum of the file | None |
| Restore | String | Restoration information of the archived file | None |
| CRC     | String | CRC64 for [Data Verification](https://intl.cloud.tencent.com/document/product/436/34078) | No |

### Download an object

#### Description

This API (`GET Object`) is used to download an object.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getObject(array $args = array());
```

#### Sample request

#### Sample 1. Downloading a file

[//]: # ".cssg-snippet-get-object"

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

#### Sample 2. Getting file content within a certain byte range

[//]: # ".cssg-snippet-get-object-range"

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

#### Sample 3. Downloading a specified version of a file

[//]: # ".cssg-snippet-get-object-with-versionId"

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

#### Sample 4. Downloading an object (limiting single-URL speed)
>?For more information about the speed limits on object downloads, please see [Single-URL Speed Limits](https://intl.cloud.tencent.com/document/product/436/34072).

```php
try {
   $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-125000000', //Format: BucketName-APPID
        'Key' => 'exampleobject',
        'SaveAs' => '/data/exampleobject',
        'TrafficLimit' => 8 * 1024 * 1024 // Limit the speed to 1 MB/s.
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
| Key | String | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | Yes |
| SaveAs                     | String | Local path to save the file                                     | No       |
| VersionId                  | String | Version ID of the specified file if versioning is enabled                             | No       |
| Range | String | Byte range of the file to download. Format: `bytes=first-last` | No |
| ResponseCacheControl | String  | `Cache-Control` of the response header | No |
| ResponseContentDisposition | String | `Content-Disposition` of the response header | No |
| ResponseContentEncoding | String | `Content-Encoding` of the response header | No |
| ResponseContentLanguage  | String | `Content-Language` of the response header | No |
| ResponseContentType  | String | `Content-Type` of the response header | No |
| ResponseExpires  | String | `Content-Expires` of the response header | No |

#### Sample response

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
            [CRC] => 16749565679157681890
        )

)
```

#### Response description

| Parameter Name | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------------------ | ------ |
| Body | File/String | Downloaded content                                                   | None |
| ETag | String | MD5 checksum of the file | None |
| Expires | String | Content-Expires | None |
| Metadata | Array | User-defined file metadata | None |
| StorageClass | String | Storage class of the object, such as `STANDARD (default)`, `STANDARD_IA`, and `ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | None |
| ContentMD5 | String | MD5 checksum of the file | None |
| ServerSideEncryption | String | Server-side encryption method | None |
| CacheControl | String | Cache policy | None |
| ContentDisposition | String | File name | None |
| ContentEncoding | String | Encoding format | None |
| ContentLanguage | String | Language type                              | None |
| ContentLength | Int | Length of the content | None |
| ContentType | String | Content type | None |
| Metadata | Array | User-defined file metadata | None |
| Restore | String | Restoration information of the archived file | None |
| CRC     | String | CRC64 for [Data Verification](https://intl.cloud.tencent.com/document/product/436/34078) | No |

### Copying an object

This API (`PUT Object - Copy`) is used to copy an object to the destination path.

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
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 2. Copying a specified version of an object

[//]: # ".cssg-snippet-copy-object-with-versionId"

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
    // Request succeeded
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
| Key | String | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | Yes |
| CopySource | String | Path of the source object, which contains `APPID`, `Bucket`, `Key`, and `Region`, <br>for example, `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | Yes |
| MetadataDirective | String | Valid values: `Copy`: ignores the configured metadata and copies the file directly; `Replaced`: modifies the metadata according to the configured metadata. If the destination path is identical to the source path, this parameter must be set to `Replaced`. | No |

### Deleting an object

#### Description

This API is used to delete a specified object (file) from a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteObject(array $args = array());
```

#### Sample request

[//]: # ".cssg-snippet-delete-object"

#### Sample 1. Deleting an object
```php
try {
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject'
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```
#### Sample 2. Deleting an object with a version ID
```php
try {
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'VersionId' => 'exampleVersionId' // Do not carry this parameter if versioning is not enabled for the bucket.
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```


#### Parameter description

| Parameter | Type | Description | Required |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | Yes |
| VersionId | String | Version ID of the file to delete                                             | No       |

### Deleting multiple objects

#### Description

This API is used to delete multiple objects (files) from a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteObjects(array $args = array());
```

#### Sample request

#### Sample 1. Deleting multiple objects
```php
try {
    $result = $cosClient->deleteObjects(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Objects' => array(
            array(
                'Key' => 'exampleobject',
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

#### Sample 2. Deleting multiple objects with version IDs


[//]: # ".cssg-snippet-delete-multi-object"

```php
try {
    $result = $cosClient->deleteObjects(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Objects' => array(
            array(
                'Key' => 'exampleobject',
                'VersionId' => 'string' // Do not carry this parameter if versioning is not enabled for the bucket.
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


#### Sample 3. Deleting objects with a specified prefix

[//]: # ".cssg-snippet-delete-prefix"

```php
$cos_prefix = "cos/folder";
$nextMarker = '';
$isTruncated = true;
while ( $isTruncated ) {
    try {
        $result = $cosClient->listObjects(
            ['Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
            'Delimiter' => '',
            'EncodingType' => 'url',
            'Marker' => $nextMarker,
            'Prefix' => $cos_prefix,
            'MaxKeys' => 1000]
        );    
        $isTruncated = $result['IsTruncated'];
        $nextMarker = $result['NextMarker'];
        foreach ( $result['Contents'] as $content ) {
            $cos_file_path = $content['Key'];
            $local_file_path = $content['Key'];
            // Splice a download path as needed
            try {
                $cosClient->deleteObject(array(
                    'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
                    'Key' => $cos_file_path,
                ));
                echo ( $cos_file_path . "\n" );
            } catch ( \Exception $e ) {
                echo( $e );
            }
        }
    } catch ( \Exception $e ) {
        echo( $e );
    }
}
```


#### Parameter description

| Parameter | Type | Description | Required |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Objects   | Array  | List of objects to delete                                                 | Yes       |
| Object   | Array  | Objects to delete                                                 | Yes       |
| Key | String | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | Yes |
| VersionId | String | Version ID of the file to delete                                             | No       |

#### Sample response

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

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| -------- | ------ | -------------------- | -------------- |
| Deleted | Array | List of successfully deleted objects | None |
| Errors   | Array  | List of objects that failed to be deleted | None |
| Key      | String | Object key | Deleted/Errors |
| Code     | String | Error code for failed operations | Errors |
| Message  | String | Error message for failed operations | Errors |



### Restoring an archived object 

#### Description

This API (`POST Object restore`) is used to restore an archived object for access.

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
| Days | String | Number of days before the temporary copy expires | Yes |
| CASJobParameters | Array  | Restoration information | Yes |
| Tier | String | Restoration mode. For data in the ARCHIVE storage class, `Tier` can be set to `Expedited`, `Standard`, or `Bulk`. For data in DEEP ARCHIVE, `Tier` can be set to `Standard` or `Bulk`. | Yes |

## Multipart Operations

Multipart operations include:

- Uploading an object in parts: initializing a multipart upload, uploading parts, and completing a multipart upload
- Resuming a multipart upload: querying uploaded parts, uploading remaining parts, and completing a multipart upload
- Deleting uploaded parts

### Querying multipart uploads

#### Description

This API (`List Multipart Uploads`) is used to query in-progress multipart uploads in a specified bucket.

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
| Delimiter | String | Separator, left empty by default. For example, you can set it to `/` to indicate folders. | No |
| EncodingType | String | Encoding method of the returned value. The value is not encoded by default. Valid value: `url`  | No |
| KeyMarker | String | The key of the object after which the returned part list begins | No |
| UploadIdMarker | String | The upload ID of the object after which the returned part list begins                            | No |
| Prefix | String | Key prefix to query parts by, left empty by default   | No |
| MaxUploads  | Int | Maximum number of returned parts, which is `1000` (the maximum value allowed) by default | No |

#### Sample response

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

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| ------------ | ------ | ---------------------------------- | ------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| IsTruncated | Int    | Whether the returned objects are truncated | None |
| Uploads | Array  | List of returned parts                     | None |
| Upload | Array  | Attributes of the returned parts | Uploads |
| Key | String | Object key | Upload  |
| UploadId | String | ID of the multipart upload                 | Upload  |
| Initiator    | String | Initiator of the multipart upload | Upload  |
| Owner        | String | Owner of the parts | Upload  |
| StorageClass | String | Storage class of the parts | Upload  |
| Initiated    | String | Initiation time of the multipart upload | Upload  |



### Initializing a multipart upload

#### Description

This API (`Initiate Multipart Upload`) is used to initialize a multipart upload.

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
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | Yes |
| CacheControl | String | Cache policy | No |
| ContentDisposition | String | File name | No |
| ContentEncoding | String | Encoding format | No |
| ContentLanguage | String | Language type | No |
| ContentLength | Int | Length of the content | No |
| ContentType | String | Content type | No |
| Expires | String | `Content-Expires` | No |
| Metadata | Array | User-defined file metadata | No |
| StorageClass | String | Storage class of the object, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | No |
| ContentMD5           | Boolean | Whether to upload the MD5 checksum of the file for verification                           | No       |
| ServerSideEncryption | String | Server-side encryption method | No |

#### Sample response

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

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Key  | String | Object key | None |
| UploadId  | String | ID of the multipart upload | None |




### Uploading parts

This API (`Upload Part`) is used to upload an object in parts.

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
        'UploadId' => 'exampleUploadId', // UploadId is the ID of the multipart upload, which you can get in the response returned after multipart upload initialization 
        'PartNumber' => 1, // PartNumber is the sequential number of a part, which COS uses to reassemble parts
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
| ------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| UploadId | String | ID of the multipart upload, which can be found in the response returned after the initialization of the multipart upload | Yes |
| Body | File/String | Uploaded content | Yes |
| PartNumber | Int | Sequential number of a part, which COS uses to reassemble parts | Yes |
| ContentLength | Int | Length of the content | No |
| ContentMD5           | Boolean      | Whether to upload the MD5 checksum of the file for verification                                  | No       |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "96e79218965eb72c92a549dd5a330112"
            [RequestId] => NWNhNDdjYWFfNjNhYjM1MGFfMjk2NF8xY2ViMWM=
            [CRC] => 16749565679157681890
        )

)
```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| -------- | ------ | ------------- | ------ |
| ETag | String | MD5 checksum of the part | None |
| CRC     | String | CRC64 for [Data Verification](https://intl.cloud.tencent.com/document/product/436/34078) | No |




### Copying an object part

#### Description

This API (`Upload Part - Copy`) is used to copy a part of an object.

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
        'CopySourceRange' => 'bytes=0-1', // Copy only the first 2 bytes.
        'UploadId' => 'exampleUploadId', // UploadId is the ID of the multipart upload, which you can get in the response returned after multipart upload initialization 
        'PartNumber' => 1, // PartNumber is the sequential number of a part, which COS uses to reassemble parts
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
| ------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| UploadId | String | ID of the multipart upload, which can be found in the response returned after the initialization of the multipart upload | Yes |
| CopySource | String | Path to the source object, which contains `APPID`, `Bucket`, `Key`, and `Region`, <br>for example, `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | Yes |
| CopySourceRange | String | Byte range of the source object to copy in the format of `bytes=first-last`. If no range is specified, the entire source object will be copied. | No |
| PartNumber | Int | Sequential number of a part, which COS uses to reassemble parts | Yes |
| ContentLength | Int | Length of the content | No |
| ContentMD5           | Boolean | Whether to upload the MD5 checksum of the file for verification                           | No       |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "96e79218965eb72c92a549dd5a330112"
            [LastModified] => "2017-09-04T04:45:45"
            [RequestId] => NWNhNDdjYWFfNjNhYjM1MGFfMjk2NF8xY2ViMWM=
            [CRC] => 16749565679157681890
        )

)
```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| ------------ | ------ | ------------------------------ | ------ |
| ETag | String | MD5 checksum of the part | None |
| LastModified | String | Time when the object was last modified, in GMT format | None |
| CRC     | String | CRC64 for [Data Verification](https://intl.cloud.tencent.com/document/product/436/34078) | No |


### Querying uploaded parts

#### Description

This API (`List Parts`) is used to query the uploaded parts of a multipart upload.

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
| UploadId  | String | ID of the multipart upload | Yes |
| PartNumberMarker | Int | The number of the part after which the returned list begins | No |
| MaxParts | Int | Maximum number of returned parts, which is `1000` (the maximum value allowed) by default | No |

#### Sample response

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

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| ---------------- | ------ | --------------------------------------- | ------ |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Key | String | Object key | None |
| UploadId  | String | ID of the multipart upload | None |
| IsTruncated | Int    | Whether the returned objects are truncated | None |
| PartNumberMarker | Int | The number of the part after which the returned list begins | None |
| MaxParts | Int | Maximum number of returned parts, which is `1000` (the maximum value allowed) by default | None |
| Initiator | String | Initiator of the multipart upload | None  |
| Parts | Array  | List of returned parts | None |
| Part | Array  | Attributes of the returned parts                          | Parts |
| PartNumber | Int | Part number  | Part |
| LastModified | String | Time when the part was last modified | Part |
| ETag | String | MD5 checksum of the part | Part |
| Size | String | Size of the part | Part |



###  Completing a multipart upload

#### Description

This API (`Complete Multipart Upload`) is used to complete the multipart upload of a file.

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
| UploadId  | String | ID of the multipart upload | Yes |
| Parts | Array  | List of parts | Yes |
| Part | Array | Information of the uploaded parts | Yes |
| ETag | String | MD5 checksum of the part | Yes |
| PartNumber | Int | Part number | Yes |

###  Aborting a multipart upload

#### Description

This API (`Abort Multipart Upload`) is used to abort a multipart upload and delete the uploaded parts.

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
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| -------- | ------ | ---------------------------------- | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key      | String | Object key                             | Yes       |
| UploadId  | String | ID of the multipart upload | Yes |



## Advanced APIs (Recommended)

This section is about the advanced upload and copy APIs COS provides. Pass in the parameters required, and the APIs will determine whether to upload (copy) an object in whole or in parts based on the file size. Before using the APIs, make sure you have completed the initialization step in [Getting Started](https://intl.cloud.tencent.com/document/product/436/12266).

### Uploading an object

#### Method prototype

```php
public Qcloud\Cos\Client upload(string $bucket, string $key, $body, array $options = array());
```
#### Description

This API is used to upload an object. It calls the `PUT Object` API for small files, and the `Upload Part` API for large files. For the parameters required, please see those of the `PUT Object` and `Upload Part` APIs.

#### Parameter description

| Parameter | Type | Description | Required |
| -------- | ------ | ---------------------------------- | -------- |
| bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| key      | String | Object key                             | Yes       |
| body                 | Stream/String | Content to upload                                                   | Yes       |
| options     | Array | Additional configuration items            | No       |



| options Parameter | Type   | Description | Required |
| -------- | ------ | ---------------------------------- | -------- |
| Progress         | Function      | Progress callback. `$totalSize` indicates the total size, and `$uploadedSize` indicates the uploaded size. | No       |
| PartSize         | Int      | Minimum part size. Default value: 5 MB | No       |
| Concurrency         | Int      | Concurrency. Default value: 10 | No       |
| ACL | String | ACL of the object, such as private or public-read | No |
| CacheControl | String | Cache policy | No |
| ContentDisposition | String | File name | No |
| ContentEncoding | String | Encoding format | No |
| ContentLanguage | String | Language type | No |
| ContentLength | Int | Length of the content | No |
| ContentType | String | Content type | No |
| Expires | String | `Content-Expires` | No |
| Metadata             | Array       | User-defined file metadata                                       | No       |
| StorageClass | String | Storage class of the object, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | No |
| ContentMD5           | Boolean      | Whether to upload the MD5 checksum of the file for verification                                  | No       |
| ServerSideEncryption | String | Server-side encryption method | No |

#### Sample request

#### Sample 1. Uploading a local object

[//]: # ".cssg-snippet-transfer-upload-file"

```php
try {
    $result = $cosClient->upload(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject', // Object key
        $body = fopen('path/to/localFile', 'rb')
    );
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 2. Uploading an object to ARCHIVE

[//]: # ".cssg-snippet-transfer-upload-file-archive"

```php
try {
    $result = $cosClient->upload(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject', // Object key
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

#### Sample 3. Uploading an object with specified part size and metadata

[//]: # ".cssg-snippet-transfer-upload-file-with-meta"

```php
try {
    $result = $cosClient->upload(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject', // Object key
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

### Batch uploading files (uploading a local folder)

#### Description

This API is used to upload all files in a local folder to COS.

#### Sample request

[//]: # ".cssg-snippet-transfer-upload-folder"

```php
<?php

require dirname( __FILE__ ) . '/../vendor/autoload.php';

$secretId = 'SECRETID';
// Cloud API key SecretId
$secretKey = 'SECRETKEY';
// Cloud API key SecretKey
$region = 'ap-beijing';
// Set a default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey
        )
    )
);

function uploadfiles( $path, $cosClient ) {
    foreach ( scandir( $path ) as $afile ) {
        if ( $afile == '.' || $afile == '..' ) continue;
        if ( is_dir( $path.'/'.$afile ) ) {
            uploadfiles( $path.'/'.$afile, $cosClient );
        } else {
            $local_file_path = $path.'/'.$afile;
            $cos_file_path = $local_file_path;
            // Splice an upload path as needed
            try {
                $cosClient->upload(
                    $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
                    $key = $cos_file_path,
                    $body = fopen( $cos_file_path, 'rb' )
                );
            } catch ( \Exception $e ) {
                echo( $e );
            }
        }
    }
}

$local_path = '/data/home/folder';
uploadfiles( $local_path, $cosClient );
```

### Downloading an object (according to `Range`)

#### Description

This API is used to download an object. It calls the `GET Object` API to download a small file in whole and a large file by byte range. For the parameters required, please see those of the `GET Object` API.

#### Method prototype

```php
public Qcloud\Cos\Client download(string $bucket, string $key, string $saveAs, array $options = array());
```

| Parameter | Type | Description | Required |
| -------- | ------ | ---------------------------------- | -------- |
| bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| key      | String | Object key                             | Yes       |
| saveAs     | String | Local path to save the file   | Yes       |
| options     | Array | Additional configuration items            | No       |



| options Parameter | Type   | Description | Required |
| -------- | ------ | ---------------------------------- | -------- |
| Progress         | Function      | Progress callback. `$totalSize` indicates the total size, and `$downloadedSize` indicates the downloaded size. | No       |
| PartSize         | Int      | Minimum part size. Default value: 5 MB | No       |
| Concurrency         | Int      | Concurrency. Default value: 10 | No       |
| ResumableDownload         | Bool      | Whether to enable checkpoint restart. Default value: `False` | No       |
| ResumableTaskFile         | Int      | Checkpoint file path. Default value: `&lt;saveAs.cosresumabletask>` | No       |


#### Sample request

[//]: # ".cssg-snippet-download-object"

```php
$printbar = function($totalSize, $downloadedSize) {
    printf("downloaded [%d/%d]\n", $downloadedSize, $totalSize);
};

try {
    $result = $cosClient->download(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject',
        $saveAs = $local_path,
        $options=['Progress' => $printbar, // Specify the progress.
                  'PartSize' => 10 * 1024 * 1024, //Part size
                  'Concurrency' => 5, //Number of concurrent parts
                  'ResumableDownload' => true, //Whether to enable checkpoint restart. It’s disabled by default.
                  'ResumableTaskFile' => 'tmp.cosresumabletask' //Breakpoint file path. Default value: <localpath>.cosresumabletask
                ]
    );
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Batch downloading files (downloading a COS directory)

#### Description

This API is used to download a COS directory and the files in it to the local disk.

#### Sample request

[//]: # ".cssg-snippet-download-folder"

```php
$cos_path = 'cos/folder';
$nextMarker = '';
$isTruncated = true;

while ( $isTruncated ) {
    try {
        $result = $cosClient->listObjects(
            ['Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
            'Delimiter' => '',
            'EncodingType' => 'url',
            'Marker' => $nextMarker,
            'Prefix' => $cos_path,
            'MaxKeys' => 1000]
        );
    } catch ( \Exception $e ) {
        echo( $e );
    }
    $isTruncated = $result['IsTruncated'];
    $nextMarker = $result['NextMarker'];
    foreach ( $result['Contents'] as $content ) {
        $cos_file_path = $content['Key'];
        $local_file_path = $content['Key'];
        // Splice a download path as needed
        try {
            $result = $cosClient->download(
                $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
                $key = $cos_file_path,
                $saveAs = $local_file_path
            );
            echo ( $cos_file_path . "\n" );
        } catch ( \Exception $e ) {
            echo( $e );
        }
    }
}
```

### Copying objects

#### Description

This API is used to copy an object. It calls the `PUT Object - Copy` API for small files, and the `Upload Part - Copy` API for large files. This API is usually used to modify object attributes. For the parameters required, please see those of the `PUT Object - Copy` and `Upload Part - Copy` APIs.

#### Sample request

#### Sample 1. Copying an object

[//]: # ".cssg-snippet-transfer-copy-object"

```php
try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject', // Object key
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'sourcebucket-1250000000', 
            'Key' => 'sourceobject', 
        )
    );
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

[//]: # ".cssg-snippet-transfer-copy-object-update-storage-class"

#### Sample 2. Changing the object storage class

```php
try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject', // Object key
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

[//]: # ".cssg-snippet-transfer-copy-object-update-metadata"

#### Sample 3. Modifying object storage attributes

```php
try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject', // Object key
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
