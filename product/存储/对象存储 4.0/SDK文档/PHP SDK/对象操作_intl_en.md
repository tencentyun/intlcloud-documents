## Overview

This document provides an overview of APIs related to simple object operations, multipart upload, and other operations and corresponding SDK sample code.

**Simple operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Object)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying object list | Queries some or all objects in a bucket |
[GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying object and historical version list | Queries some or all objects in a bucket and their historical version information |
[PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Simply uploading an object | Upload an object (file/object) to a bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using a form | Uploads an object using format request |
[HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries object metadata |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object (file/object) to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies a file to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes the specified object (file/object) in a bucket |
| [DELETE Multiple Object](https://intl.cloud.tencent.com/document/product/436/8289) 	| Deleting multiple objects 	| Deletes objects (files/objects) in a bucket in batches |


**Multipart upload operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads object parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire object |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Retrieves an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object (file/object) in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object (file/object) |



## Simple Operations

### Querying Object List

#### Feature Description

This API (List Object) is used to queries all objects in the specified bucket.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model listObjects(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->listObjects(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'Delimiter' => '/',
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

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Delimiter | String | Sets the delimiter; for example, set `/` to simulate a folder. This parameter is blank by default | No |
| EncodingType | String | Specifies the encoding method of the return value; value range: url; no encoding is performed by default | No |
| Marker | String |	Marks the starting position of the list of returned objects. By default, entries are listed in UTF-8 binary order  | No |
| Prefix | String | Filters object keys to match the objects with the specified prefix. This parameter is blank by default | No |
| MaxKeys | Int | Maximum number of returned objects; default and maximum value: 1,000 | No |

#### Return Result Example

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
#### Return Result Descriptions

| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Name | String | Bucket name in the format of BucketName-APPID                         | None |
| Delimiter | String | Sets the delimiter; for example, set `/` to simulate a folder | None |
| EncodingType | String | Specifies the encoding method of the return value | None |
| Marker | String |	Marks the starting position of the list of returned objects. By default, entries are listed in UTF-8 binary order  | None |
| Prefix | String | Filters object keys to match the objects with the specified prefix | None |
| MaxKeys | Int | Maximum number of returned objects; default and maximum value: 1,000 | None |
| IsTruncated | Int | Indicates whether the returned objects are truncated | None |
| Contents | Array | List of returned objects | None |
| Content | Array | Attributes of the returned objects including a list of metadata of all objects such as 'ETag', 'StorageClass', 'Key', 'Owner', 'LastModified', and 'Size' | Contents |


### Querying Object and Historical Version List 

#### Feature Description

This API is used to query some or all objects in a bucket and their historical version information.

#### Method Prototype

```
public Guzzle\Service\Resource\Model listObjectVersions(array $args = array());
```
#### Sample Request

```php
try {
    $result = $cosClient->listObjectVersions(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'Delimiter' => '/',
        'EncodingType' => 'url',
        'KeyMarker' => 'string',
        'VersionIdMarker' => 'string',
        'Prefix' => 'doc',
        'MaxKeys' => 1000,
    )); 
    print_r($result);
} catch (\Exception $e) {
    echo($e);
}
```

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ------------- | -------------------------- | ------ | ---- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Prefix | String | Filters object keys to match the objects with the specified prefix. This parameter is blank by default | No |
| Delimiter | String | Sets the delimiter; for example, set `/` to simulate a folder. This parameter is blank by default | No |
| KeyMarker | String | Marks the starting position of the key in the list of returned objects. By default, entries are listed in UTF-8 binary order  | No |
| VersionIdMarker | String | Marks the starting position of the VersionId in the list of returned objects. By default, entries are listed in UTF-8 binary order  | No |
| MaxKeys | Int | Maximum number of returned objects; default and maximum value: 1,000 | No |
| EncodingType | String | Specifies the encoding method of the return value; value range: url; no encoding is performed by default | No |

#### Return Result Example

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
#### Return Result Descriptions

| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Name | String | Bucket name in the format of BucketName-APPID                         | None |
| Delimiter | String | Sets the delimiter; for example, set `/` to simulate a folder | None |
| EncodingType | String | Specifies the encoding method of the return value | None |
| KeyMarker | String | Marks the starting position of the key in the list of returned objects. By default, entries are listed in UTF-8 binary order  | None |
| VersionIdMarker | String |	 Marks the starting position of the VersionId in the list of returned objects. By default, entries are listed in UTF-8 binary order  | None |
| NextKeyMarker | String |	Marks the starting position of the key in the list of objects returned next time if IsTruncated is true | None |
| NextVersionIdMarker | String | Marks the starting position of the VersionId in the list of objects returned next time if IsTruncated is true | None |
| Prefix | String | Filters object keys to match the objects with the specified prefix | None |
| MaxKeys | Int | Maximum number of returned objects; default and maximum value: 1,000 | None |
| IsTruncated | Int | Indicates whether the returned objects are truncated | None |
| Versions | Array | List of metadata of all multi-version objects | None |
| Version | Array | List of metadata of all multi-version objects, including information such as 'ETag', 'StorageClass', 'Key', 'VersionId', 'IsLatest', 'Owner', 'LastModified', and 'Size' | Versions |
| CommonPrefixes | Array | All objects starting with Prefix and ending in Delimiter are grouped into the same class | None |




### Simply Uploading an Object

#### Feature Description

This API (PUT Object) is used to upload an object to the specified bucket. It supports files of up to 5 GB in size. If you need to upload larger files, you are recommended to use the advanced composite upload API.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model putObject(array $args = array())
```

#### Sample Request

```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID 
        'Key' => 'exampleobject', 
        'Body' => fopen('/data/exampleobject', 'rb'), 
        /*
        'ACL' => 'string',
        'CacheControl' => 'string',
        'ContentDisposition' => 'string',
        'ContentEncoding' => 'string',
        'ContentLanguage' => 'string',
        'ContentLength' => integer,
        'ContentType' => 'string',
        'Expires' => 'string',
        'GrantFullControl' => 'string',
        'GrantRead' => 'string',
        'GrantWrite' => 'string',
        'Metadata' => array(
        'string' => 'string',
        ),
        'ContentMD5' => 'string',
        'ServerSideEncryption' => 'string',
        'StorageClass' => 'string'
        */
    )); 
    // Request succeeded 
    print_r($result); 
} catch (\Exception $e) { 
    // Request failed 
    echo($e); 
}

```

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Key | String | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg | No |
| ACL | String | Sets the object ACL such as private and public-read | No |
| Body | File/String | Uploaded content | Yes |
| CacheControl | String |	 Cache policy, which sets Cache-Control | No |
| ContentDisposition | String | Filename, which sets Content-Disposition | No |
| ContentEncoding | String | Encoding format, which sets Content-Encoding | No |
| ContentLanguage | String | Language type, which sets Content-Language | No |
| ContentLength | Int | Sets transfer length | No |
| ContentType | String |	 Content type, which sets Content-Type | No |
| Expires | String | Sets Content-Expires | No |
| Metadata | Array | User-defined file metadata | No |
| StorageClass | String | File storage class; value range: STANDARD, STANDARD_IA, ARCHIVE; default value: STANDARD | No |
| ContentMD5 | String | Sets the MD5 value of the uploaded file for verification | No |
| ServerSideEncryption | String | Server-side encryption method | No |

#### Return Result Example

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
#### Return Result Descriptions

| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| ETag | String | 	MD5 value of the uploaded file | None |
| VersionId | String | File version number after versioning is enabled | None |


### Querying Object Metadata

#### Feature Description

This API (HEAD Object) is used to query the metadata of an object.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model headObject(array $args = array());
```

#### Sample Request

```php
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header; http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->headObject(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'Key' => 'exampleobject',
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Key | String | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name <br>examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg | Yes |
| VersionId | String | Specifies a file version if versioning is enabled | No |

#### Return Result Example

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
#### Return Result Descriptions

| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| CacheControl | String |	 Cache policy, which sets Cache-Control | None |
| ContentDisposition | String | Filename, which sets Content-Disposition | None |
| ContentEncoding | String | Encoding format, which sets Content-Encoding | None |
| ContentLanguage | String | Language type, which sets Content-Language | None |
| ContentLength | Int | Sets transfer length | None |
| ContentType | String |	 Content type, which sets Content-Type | None |
| Metadata | Array | User-defined file metadata | None |
| StorageClass | String | File storage class; value range: STANDARD, STANDARD_IA, ARCHIVE | None |
| ServerSideEncryption | String | Server-side encryption method | None |
| ETag | String | MD5 value of a file | None |
| Restore | String | Restoration information of an archived file | None |


### Downloading an Object

#### Feature Description

This API (GET Object) is used to download an object to the local file system.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model getObject(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'SaveAs' => '/data/exampleobject',
        /*
        'Range' => 'bytes=0-10',
        'VersionId' => 'string',
        'ResponseCacheControl' => 'string',
        'ResponseContentDisposition' => 'string',
        'ResponseContentEncoding' => 'string',
        'ResponseContentLanguage' => 'string',
        'ResponseContentType' => 'string',
        'ResponseExpires' => 'string',
        */
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Key | String | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name <br>examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg | Yes |
| SaveAs | String | Path to the file saved locally | No |
| VersionId | String | Specifies a file version if versioning is enabled | No |
| Range | String | Sets the range of file download in the format of bytes=first-last | No |
| ResponseCacheControl | String |	 Sets the response header Cache-Control | No|
| ResponseContentDisposition | String | Sets the response header Content-Disposition  | No |
| ResponseContentEncoding | String | 	Sets the response header Content-Encoding | No |
| ResponseContentLanguage | String | Sets the response header Content-Language  | No |
| ResponseContentType | String |	 Sets the response header Content-Type | No |
| ResponseExpires | String | Sets the response header Content-Expires | No |


#### Return Result Example

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
#### Return Result Descriptions

| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Body | File/String | Downloaded content | None |
| ETag | String | MD5 value of a file | None |
| Expires | String | Content-Expires | None |
| Metadata | Array | User-defined file metadata | None |
| StorageClass | String | File storage class; value range: STANDARD, STANDARD_IA, ARCHIVE; default value: STANDARD | None |
| ContentMD5 | String | Sets the MD5 value of the uploaded file for verification | None |
| ServerSideEncryption | String | Server-side encryption method | None |
| CacheControl | String |	 Cache policy, which sets Cache-Control | None |
| ContentDisposition | String | Filename, which sets Content-Disposition | None |
| ContentEncoding | String | Encoding format, which sets Content-Encoding | None |
| ContentLanguage | String | Language type, which sets Content-Language | None |
| ContentLength | Int | Sets transfer length | None |
| ContentType | String |	 Content type, which sets Content-Type | None |
| Metadata | Array | User-defined file metadata | None |
| Restore | String | Restoration information of an archived file | None |

### Setting Object Replication
This API (Put Object - Copy) is used to copy an object to the destination path.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model copyObject(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject',
        /*
        'MetadataDirective' => 'string',
        'ACL' => 'string',
        'CacheControl' => 'string',
        'ContentDisposition' => 'string',
        'ContentEncoding' => 'string',
        'ContentLanguage' => 'string',
        'ContentLength' => integer,
        'ContentType' => 'string',
        'Expires' => 'string',
        'GrantFullControl' => 'string',
        'GrantRead' => 'string',
        'GrantWrite' => 'string',
        'Metadata' => array(
        'string' => 'string',
        ),
        'ContentMD5' => 'string',
        'ServerSideEncryption' => 'string',
        'StorageClass' => 'string'
        */
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

```

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Key | String | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name <br>examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg | Yes |
| CopySource | String | Describes the path to the source file to be copied, including Appid, Bucket, Key, and Region, <br>examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg | Yes |
| MetadataDirective | String | Value range: Copy, Replaced. If this parameter is set to Copy, the configured user metadata is ignored and the copy is performed directly; if Replaced, the metadata is modified based on the configured metadata. If the destination path is the same as the source path, this parameter has to be set to Replaced | No |

### Deleting a Single Object

#### Feature Description

This API is used to delete the specified object (file/object) in a bucket.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model deleteObject(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'VersionId' => 'string'
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Key | String | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name <br>examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg | Yes |
| VersionId | String | Version number of the deleted file | No |


### Deleting Multiple Objects

#### Feature Description

This API is used to delete objects (files/objects) in a bucket in batches.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model deleteObjects(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->deleteObjects(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
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

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| -------- | ------ | ------------------------------------------------------------ | ------ |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Objects | Array | List of deleted objects | Yes |
| Object | Array | Deleted object | Yes |
| Key | String | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name <br>examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg | Yes |
| VersionId | String | Version number of the deleted file | No |

#### Return Result Example

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
#### Return Result Descriptions

| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Deleted | Array | List of successfully deleted objects | None |
| Errors | Array | List of objects that failed to be deleted | None |
| Key | String | Object key | Deleted/Errors |
| Code | String | Error code of the failure | Errors |
| Message | String | Error message | Errors |


## Multipart Upload Operations

### Querying a Multipart Upload

#### Feature Description

This API (List Multipart Uploads) is used to query multipart uploads in progress in the specified bucket.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model listMultipartUploads(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->listMultipartUploads(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'Delimiter' => '/',
        'EncodingType' => 'url',
        'KeyMarker' => 'string',
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

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Delimiter | String | Sets the delimiter; for example, set `/` to simulate a folder. This parameter is blank by default | No |
| EncodingType | String | Specifies the encoding method of the return value; value range: url; no encoding is performed by default | No |
| KeyMarker | String |	 Marks the starting position of the list of returned parts | No |
| UploadIdMarker | String |	 Marks the starting position of the list of returned parts | No |
| Prefix | String | Filters object keys to match the parts with the specified prefix. This parameter is blank by default | No |
| MaxUploads | Int | Maximum number of returned parts; default and maximum value: 1,000 | No |

#### Return Result Example

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
#### Return Result Descriptions

| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID                         | None |
| IsTruncated | Int | Indicates whether the returned objects are truncated | None |
| Uploads | Array | List of returned parts | None |
| Upload | Array | Attribute of returned parts | Uploads |
| Key | String | Object key name | Upload |
| UploadId | String | Multipart upload ID of an object | Upload |
| Initiator | String | The operator who initialized the multipart upload | Upload |
| Owner | String | Part owner | Upload |
| StorageClass | String | Part storage class | Upload |
| Initiated | String | Multipart upload initialization time | Upload |


### Uploading an Object in Parts

With multipart upload, you can do the following:

- Upload an object in parts, including initializing a multipart upload, uploading parts, and completing the multipart upload.
- Resume a multipart upload, including querying uploaded parts, uploading parts, and completing the multipart upload.
- Delete uploaded parts.

### <span id = "INIT_MULIT_UPLOAD">Initializing a Multipart Upload</span>

#### Feature Description

This API (Initiate Multipart Upload) is used to initialize a multipart upload operation.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model createMultipartUpload(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->createMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'Key' => 'exampleobject',
        /*  
        'CacheControl' => 'string',
        'ContentDisposition' => 'string',
        'ContentEncoding' => 'string',
        'ContentLanguage' => 'string',
        'ContentLength' => integer,
        'ContentType' => 'string',
        'Expires' => 'string',
        'Metadata' => array(
            'string' => 'string',
        ),
        'StorageClass' => 'string'
        */
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Key | String | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name <br>examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg | Yes |
| CacheControl | String |	 Cache policy, which sets Cache-Control | No |
| ContentDisposition | String | Filename, which sets Content-Disposition | No |
| ContentEncoding | String | Encoding format, which sets Content-Encoding | No |
| ContentLanguage | String | Language type, which sets Content-Language | No |
| ContentLength | Int | Sets transfer length | No |
| ContentType | String |	 Content type, which sets Content-Type | No |
| Expires | String | Sets Content-Expires | No |
| Metadata | Array | User-defined file metadata | No |
| StorageClass | String | File storage class; value range: STANDARD, STANDARD_IA, ARCHIVE; default value: STANDARD | No |
| ContentMD5 | String | Sets the MD5 value of the uploaded file for verification | No |
| ServerSideEncryption | String | Server-side encryption method | No |

#### Return Result Example

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
#### Return Result Descriptions

| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID                         | None |
| Key | String | Object key | None |
| UploadId | String | Multipart upload ID of an object | None |

### <span id = "LIST_MULIT_UPLOAD">Querying Uploaded Parts</span>

#### Feature Description

This API (List Parts) is used to query uploaded parts in the specified multipart upload operation.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model listParts(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->listParts(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'UploadId' => 'NWNhNDY0YzFfMmZiNTM1MGFfNTM2YV8xYjliMTg',
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

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Key | String | Object key | Yes |
| UploadId | String | Multipart upload ID of an object | Yes |
| PartNumberMarker | Int | Marks the starting position of the list of returned parts | No |
| MaxParts | Int | Maximum number of returned parts; default and maximum value: 1,000 | No |

#### Return Result Example

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
#### Return Result Descriptions

| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID                         | None |
| Key | String | Object key | None |
| UploadId | String | Multipart upload ID of an object | None |
| IsTruncated | Int | Indicates whether the returned objects are truncated | None |
| PartNumberMarker | Int | Marks the starting position of the list of returned parts | None |
| MaxParts | Int | Maximum number of returned parts; default and maximum value: 1,000 | None |
| Initiator | String | The operator who initialized the multipart upload | None |
| Parts | Array | List of returned parts | None |
| Part | Array | Attribute of returned parts | Parts |
| PartNumber | Int | Part number | Part |
| LastModified | String | Last uploaded time of a part | Part |
| ETag | String | MD5 value of a part | Part |
| Size | String | Part size | Part |

### <span id = "MULIT_UPLOAD_PART">Uploading Parts</span>

This API (Upload Part) is used to upload a file in parts.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model uploadPart(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->uploadPart(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'Key' => 'exampleobject', 
        'Body' => 'string',
        'UploadId' => 'NWNhNDY0YzFfMmZiNTM1MGFfNTM2YV8xYjliMTg',
        'PartNumber' => integer,
        /*
        'ContentMD5' => 'string',
        'ContentLength' => integer,
        */
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

```

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Key | String | Object key | Yes |
| UploadId | String | Multipart upload ID of an object | Yes |
| Body | File/String | Uploaded content | Yes |
| PartNumber | Int | Uploaded part number | Yes |
| ContentLength | Int | Sets transfer length | No |
| ContentMD5 | String | Sets the MD5 value of the uploaded file for verification | No |

#### Return Result Example

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
#### Return Result Descriptions

| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| ETag | String | MD5 value of a part | None |

### <span id = "COMPLETE_MULIT_UPLOAD">Completing a Multipart Upload</span>

#### Feature Description

The API (Complete Multipart Upload) is used to complete the multipart upload of the entire file.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model completeMultipartUpload(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->completeMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'Key' => 'exampleobject', 
        'UploadId' => 'string',
        'Parts' => array(
            array(
                'ETag' => 'string',
                'PartNumber' => integer,
            ),  
            array(
                'ETag' => 'string',
                'PartNumber' => integer,
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

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Key | String | Object key | Yes |
| UploadId | String | Multipart upload ID of an object | Yes |
| Parts | Array | Part information list | Yes |
| Part | Array | Content information of an uploaded part | Yes |
| ETag | String | MD5 value of a part | Yes |
| PartNumber | Int | Part number | Yes |


### <span id = "ABORT_MULIT_UPLOAD">Aborting a Multipart Upload</span>

#### Feature Description

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model abortMultipartUpload(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->abortMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'Key' => 'exampleobject', 
        'UploadId' => 'string',
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Key | String | Object key | Yes |
| UploadId | String | Multipart upload ID of an object | Yes |


## Other Operations

### Restoring an Archived Object 

#### Feature Description

This API (POST Object restore) is used to retrieve an archived object for access.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model restoreObject(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'Days' => integer,
        'CASJobParameters' => array(
            'Tier' =>'string'
        )    
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Key | String | Object key | Yes |
| Days | String | Sets expiration time of the temporary copy in days | Yes |
| CASJobParameters | Array | Restoration information | Yes |
| Tier | String | For data restoration, Tier can specify the restoration type supported by CAS, including Expedited, Standard, and Bulk | Yes |

### Setting Object ACL

#### Feature Description

This API (PUT Object acl) is used to set the access control list (ACL) for the specified object.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model putObjectAcl(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->putObjectAcl(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'Key' => 'exampleobject',
        'ACL' => 'private',
        'Grants' => array(
            array(
                'Grantee' => array(
                    'DisplayName' => 'qcs::cam::uin/100000000001:uin/100000000001',
                    'ID' => 'qcs::cam::uin/100000000001:uin/100000000001',
                    'Type' => 'CanonicalUser',
                ),  
                'Permission' => 'FULL_CONTROL',
            ),  
            // ... repeated
        ),  
        'Owner' => array(
            'DisplayName' => 'qcs::cam::uin/100000000001:uin/100000000001',
            'ID' => 'qcs::cam::uin/100000000001:uin/100000000001',
        )));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ----------- | ------ | ------------------------------------------------------------ | --------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Key | String | Object key | Yes |
| Grants | Array | ACL permission list | No |
| Grant | Array | ACL permission information | No |
| Grantee | Array | ACL permission information | No |
| Type | String | Owner permission type        | No  |
| Permission | String | Permission type. Value range: FULL_CONTROL, WRITE, READ | No  |
| ACL | String | Overall permission type. Value range: private, public-read | No |
| Owner | String | Bucket owner information        | No |
| DisplayName | String | Permission owner name      | No |
| ID | String | Permission owner ID | No |


### Getting Object ACL

#### Feature Description

This API (GET Object acl) is used to get the access control list (ACL) of the specified object.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model getObjectAcl(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->getObjectAcl(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'Key' => 'exampleobject',
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Return Result Example

```php
Array
(
    [data:protected] => Array
        (
            [Owner] => Array
                (
                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                    [DisplayName] => qcs::cam::uin/100000000001:uin/100000000001
                )

            [Grants] => Array
                (
                    [0] => Array
                        (
                            [Grantee] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => qcs::cam::uin/100000000001:uin/100000000001
                                )

                            [Permission] => FULL_CONTROL
                        )

                )

            [RequestId] => NWE3YzhjMTRfYzdhMzNiMGFfYjdiOF8yYzZmMzU=
        )
)
```

#### Return Result Descriptions

| Parameter name | Type | Description | Parent Node |
| ----------- | ------ | ----------------------------------------------- | --------------- |
| Grants | Array | ACL permissions list | None |
| Grant | Array | ACL permission information | Grants |
| Grantee | Array | ACL permission information | Grant |
| Permission | String | Permission type. Value range: FULL_CONTROL, WRITE, READ | Grant  |
| Owner | String | Bucket owner information        | None |
| DisplayName | String | Permission owner name      | Grantee / Owner |
| ID | String | Permission owner ID | Grantee / Owner |


## Advanced API (Recommended)
This section describes the advanced API provided by COS that encapsulate the upload and copy operations. You only need to set the corresponding parameters, and the API will decide whether to perform simple upload/copy or multipart upload/copy according to the file size. Please confirm that the initialization as described in [Getting Started](https://intl.cloud.tencent.com/document/product/436/12266) has been completed before you use this API.


### Composite Upload

#### Feature Description

Based on the file size, this API internally calls the simple upload API for small files or multipart upload API for large files.

#### Sample Request

```php
try {
    $result = $cosClient->Upload(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject',
        $body = fopen('/data/exampleobject', 'rb')
        /*
        $options = array(
            'ACL' => 'string',
            'CacheControl' => 'string',
            'ContentDisposition' => 'string',
            'ContentEncoding' => 'string',
            'ContentLanguage' => 'string',
            'ContentLength' => integer,
            'ContentType' => 'string',
            'Expires' => 'string',
            'GrantFullControl' => 'string',
            'GrantRead' => 'string',
            'GrantWrite' => 'string',
            'Metadata' => array(
                'string' => 'string',
            ),
            'ContentMD5' => 'string',
            'ServerSideEncryption' => 'string',
            'StorageClass' => 'string'
        )
        */
    );
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Composite Copy

#### Feature Description

Based on the file size, this API internally calls the setting object replication API for small files or multipart copy API for large files.

#### Sample Request

```php
try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', // Format: BucketName-APPID
        $key = 'exampleobject',
        $copysource = 'examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject'
        /*
        $options = array(
            'ACL' => 'string',
            'MetadataDirective' => 'string',
            'CacheControl' => 'string',
            'ContentDisposition' => 'string',
            'ContentEncoding' => 'string',
            'ContentLanguage' => 'string',
            'ContentLength' => integer,
            'ContentType' => 'string',
            'Expires' => 'string',
            'GrantFullControl' => 'string',
            'GrantRead' => 'string',
            'GrantWrite' => 'string',
            'Metadata' => array(
                'string' => 'string',
            ),
            'ContentMD5' => 'string',
            'ServerSideEncryption' => 'string',
            'StorageClass' => 'string'
        )
        */
    );
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```
