## Introduction

This document provides an overview of APIs and SDK sample codes related to simple operations, multipart operations and other operations on objects.

**Simple Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/7734) | Querying object list | Queries some or all objects in a bucket |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/35521) | Querying list of current and historical versions of objects | Queries some or all objects in a bucket and their historical versions |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [HEAD Object](https://cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object (file) to the local file system |
| [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies a file to the destination path |
| [DELETE Object](https://cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object in the bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |


**Multipart Upload Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information on ongoing multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload task |
| [Upload Part](https://cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads file parts |
| [Upload Part - Copy](https://cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload task |
| [Complete Multipart Upload](https://cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload task and deletes the uploaded parts |

**Other Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [POST Object restore](https://cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://cloud.tencent.com/document/product/436/7748) | Setting the object ACL | Sets an ACL for an object (file) in the bucket |
| [GET Object acl](https://cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object (file) |



## Simple Operations

### Querying Object List

#### Feature Description

This API (List Object) is used to query all objects in a bucket.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model listObjects(array $args = array());
```

#### Sample Request

[//]: # (.cssg-snippet-get-bucket-comp)
```php
try {
    $result = $cosClient->listObjects(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Delimiter | String | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | String | No |
| EncodingType | String | Indicates the encoding method of the returned value. The value is not encoded by default. Valid value: `url`  | No |
| Marker | String | Marks the starting point of the list of returned objects. Entries are listed using UTF-8 binary order by default.  | No |
| Prefix | String | Filters the keys of objects by matching the objects prefixed with this parameter. It is left empty by default. | No |
| MaxKeys | Int  | The maximum number of returned objects. It defaults to 1000. | No |

#### Sample Response

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
#### Returned Result

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Delimiter | String | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | String | No |
| EncodingType | String | Specifies the encoding type of the returned value | No |
| Marker | Marks the starting point of the list of returned objects. Entries are listed using UTF-8 binary order by default. | string | No |
| Prefix | String | Filters the keys of objects by matching the objects prefixed with this parameter.  | No |
| MaxKeys | Int  | The maximum number of returned objects. It defaults to 1000.  | No |
| IsTruncated | Int  | Indicates whether the returned objects are truncated | No |
| Contents | Array | Returned list of objects | No |
The list containing the meta information of all objects, including 'ETag', 'StorageClass', 'Key', 'Owner', 'LastModified', 'Size', etc. |


### Query Objects and the List of Previous Versions 

#### Feature Description

Queries a part of or all objects and previous versions in a bucket

#### Method Prototype

```
public Guzzle\Service\Resource\Model listObjectVersions(array $args = array());
```
#### Sample Request

[//]: # (.cssg-snippet-list-object-versioning)
```php
try {
    $result = $cosClient->listObjectVersions(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------- | -------------------------- | ------ | ---- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Prefix  |  Filters the object key by matching the objects prefixed with this parameter. It is left empty by default.  | String  | No |
| Delimiter | String | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | String | No |
| Marker | Marks the starting point of key of the list of returned objects. Entries are listed using UTF-8 binary order by default. | String | No |
| VersionIdMarker|  Marks the starting point of VersionId of the list of returned objects. Entries are listed using UTF-8 binary order by default. | String  |  No |
| MaxKeys | The maximum number of returned objects. It defaults to 1000. | int | No |
| EncodingType | String | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url  | No |

#### Sample Response

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
#### Returned Result

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Delimiter | String | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | String | No |
| EncodingType | String | Specifies the encoding type of the returned value | No |
| KeyMarker | String  | Marks the starting point of key of the list of returned objects. Entries are listed using UTF-8 binary order by default.  | No |
| VersionIdMarker | String |  Marks the starting point of VersionId of the list of returned objects. Entries are listed using UTF-8 binary order by default.   |  No |
|| NextKeyMarker | String | Marks the starting point of the next list of returned objects if IsTruncated is true. | No |
| NextVersionIdMarker | String| Marks the starting point of VersionId of the next list of returned objects if IsTruncated is true. | No |
| Prefix | String | Filters the keys of objects by matching the objects prefixed with this parameter.  | No |
| MaxKeys | Int  | The maximum number of returned objects. It defaults to 1000.  | No |
| IsTruncated | Int  | Indicates whether the returned objects are truncated | No |
| Versions | Array| List containing metadata of all the versions of objects | No |
| Versions | Array | List containing metadata of all the versions of objects, including 'ETag'，'StorageClass'，'Key'，'VersionId'，'IsLatest'，'Owner'，'LastModified'，and 'Size' | Versions |
| CommonPrefixes | Array  | All objects starting with Prefix and ending with Delimiter are grouped into the same type | No |




### Uploading an Object Using Simple Upload

#### Feature Description

This API (PUT Object) is used to upload an object to a specified bucket. The uploaded object has a size restriction of 5GB. Please use [Multipart Upload] (#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced APIs] (#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) to upload objects greater than 5GB.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model putObject(array $args = array())
```

#### Sample Request

[//]: # (.cssg-snippet-put-object)
```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID 
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is `doc/pic.jpg`  | No |
| ACL | String| Sets ACL of object. For example `private`，`public-read`| No |
| Body | File/String | Content to be uploaded | Yes |
| CacheControl | String  | Cache policy. Sets Cache-Control  | No |
| ContentDisposition | String | File name. Sets Content-Disposition | No |
| ContentEncoding | String | Encoding format. Sets Content-Encoding  | No |
| ContentLanguage | String  | Language type. Sets Content-Language  | No |
| ContentLength | Int | Sets transmission length  | No |
| ContentType | String | Content Type. Sets Content-Type | No |
| Expires | String | Sets Content-Expires | No |
| Metadata | Array | File metadata customized by the user | No |
| StorageClass | String | Sets the object storage class; Options: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD  | No |
| ContentMD5 | String | Set MD5 of the file to be uploaded for verification | No |
| ServerSideEncryption | String | Server side encryption method | No |

#### Sample Response

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
#### Returned Result

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| ETag | String | MD5 of the uploaded file | No |
| VersionId | String | The version ID of the file when versioning is enabled. | No  |


### Querying Object Metadata

#### Feature Description

The API (HEAD Object) is used to query object metadata.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model headObject(array $args = array());
```

#### Sample Request

[//]: # (.cssg-snippet-head-object)
```php
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //Protocol header; http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->headObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
        'Key' => 'exampleobject',
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String  | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is `doc/pic.jpg` | Yes |
| VersionId | String | The version ID of the specified file when versioning is enabled. | No  |

#### Sample Response

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
#### Returned Result

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| CacheControl | String  | Cache policy. Sets Cache-Control  | No |
| ContentDisposition | String | File name. Sets Content-Disposition | No |
| ContentEncoding | String | Encoding format. Sets Content-Encoding  | No |
| ContentLanguage | String  | Language type. Sets Content-Language  | No |
| ContentLength | Int | Sets transmission length  | No |
| ContentType | String | Content Type. Sets Content-Type | No |
| Metadata | Array | File metadata customized by the user | No |
| StorageClass | String | Sets the object storage class; Options: STANDARD, STANDARD_IA, ARCHIVE  | No |
| ServerSideEncryption | String | Server side encryption method | No |
| ETag | String| MD5 of the file | No |
| Restore | String | Restoration information of an archived file | No |


### Downloading an Object

#### Feature Description

This API (Get Object) is used to download an object locally.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model getObject(array $args = array());
```

#### Sample Request

[//]: # (.cssg-snippet-get-object)
```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String  | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is `doc/pic.jpg` | Yes |
| SaveAs | String | Path of the file saved locally | No |
| VersionId | String | The version ID of the specified file when versioning is enabled. | No  |
| Range | String | Sets the range of bytes of the file to be downloaded in the format of bytes=first-last | No |
| ResponseCacheControl | String| Sets the Cache-Control in the response header  | No |
| ResponseContentDisposition | String | Sets the Content-Disposition in the response header  | No |
| ResponseContentEncoding | String | Sets the Content-Encoding in the response header | No |
| ResponseContentLanguage | String | Sets the Content-Language in the response header | No |
| ResponseContentType | String  | Sets the Content-Type in the response header | No |
| ResponseExpires | String | Sets the Content-Expires in the response header | No |


#### Sample Response

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
#### Returned Result

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| Body | File/String | Content to be downloaded    |No  |
| ETag | String| MD5 of the file | No |
| Expires | String | Content-Expires| No |
| Metadata | Array | File metadata customized by the user | No |
| StorageClass | String | Sets the object storage class; Options: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD  | No |
| ContentMD5 | String | Set MD5 of the file to be uploaded for verification | No |
| ServerSideEncryption | String | Server side encryption method | No |
| CacheControl | String  | Cache policy. Sets Cache-Control  | No |
| ContentDisposition | String | File name. Sets Content-Disposition | No |
| ContentEncoding | String | Encoding format. Sets Content-Encoding  | No |
| ContentLanguage | String  | Language type. Sets Content-Language  | No |
| ContentLength | Int | Sets transmission length  | No |
| ContentType | String | Content Type. Sets Content-Type | No |
| Metadata | Array | File metadata customized by the user | No |
| Restore | String | Restoration information of an archived file | No |

### Setting Object Replication
This API (PUT Object - Copy) is used to copy an object to the destination path.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model copyObject(array $args = array());
```

#### Sample Request

[//]: # (.cssg-snippet-copy-object)
```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject',
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String  | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is `doc/pic.jpg` | Yes |
| CopySource | String | Path of the file to be copied, includes Appid、Bucket、Key、Region，<br>For example, `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | Yes |
| MetadataDirective | String | Available values: Copy and Replaced. When it is set to Copy, ignore the configured user metadata information and copy the file directly. When it is set to Replaced, modify the metadata according to the configured meta information. If the destination path is identical to the source path, it must be set to Replaced. | Yes |

### Deleting a Single Object

#### Feature Description

This API (DELETE Object) is used to delete a specified object (file/object) in a bucket.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model deleteObject(array $args = array());
```

#### Sample Request

[//]: # (.cssg-snippet-delete-object)
```php
try {
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String  | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is `doc/pic.jpg` | Yes |
| VersionId | String | Version ID of the deleted file |  No  |


### Deleting Multiple Objects

#### Feature Description

This API (DELETE Multiple Object) is used to batch delete multiple objects from a specified bucket in a single request.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model deleteObjects(array $args = array());
```

#### Sample Request

[//]: # (.cssg-snippet-delete-multi-object)
```php
try {
    $result = $cosClient->deleteObjects(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| -------- | ------ | ------------------------------------------------------------ | ------ |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Objects   | Array | List of objects to be deleted     | Yes     |
| Objects   | Array | Objects to be deleted     | Yes     |
| Key | String  | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is `doc/pic.jpg` | Yes |
| VersionId | String | Version ID of the deleted file |  No  |

#### Sample Response

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
#### Returned Result

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| Deleted | Array | List of objects that were successfully deleted   | No |
| Errors | Array | List of objects that failed to be deleted | No |
| Key | String | Object key | Deleted/Errors |
| Code | String | Error code | Errors|
| Message | String | Error message | Errors |


## Multipart Operations

### Query multipart upload

#### Feature Description

This API (List Multipart Uploads) is used to query in-progress multipart uploads in the specified bucket.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model listMultipartUploads(array $args = array());
```

#### Sample Request

[//]: # (.cssg-snippet-list-multi-upload)
```php
try {
    $result = $cosClient->listMultipartUploads(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Delimiter | String | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | String | No |
| EncodingType | String | Indicates the encoding method of the returned value. The value is not encoded by default. Valid value: `url`  | No |
| KeyMarker | String | Marks the starting point of the list of returned parts     | No |
| UploadIdMarker | String | Marks the starting point of the list of returned parts    | No |
| Prefix | String| Filters the keys of parts by matching the objects prefixed with this parameter. It is left empty by default.  | No |
| MaxUploads | Int | The maximum number of returned parts. It defaults to 1000. | No |

#### Sample Response

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
#### Returned Result

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| IsTruncated | Int  | Indicates whether the returned objects are truncated | No |
| Uploads | Array | Returned list of parts | No |
| Upload | Array | Returned parts attributes | Uploads |
| Key | String | Object key name | Upload |
| UploadId | String | Multipart upload ID of an object | Upload |
| Initiator | String | User who initiated the multipart upload | Upload |
| Owner | String | Owner of the parts | Upload |
| StorageClass | String | Storage class of the parts | Upload |
| Initiated | String | Time the multipart upload was initiated | Upload |


### Upload an object using multipart upload

This includes the following operations:

- Uploading an object in multiple parts: initialize multipart upload, upload parts, and complete the upload of all parts.
- Resuming a multipart upload: query uploaded parts, upload parts, and complete the upload of all parts
- Deleting uploaded parts.

### <span id = "INIT_MULIT_UPLOAD">Initializing multipart upload </span>

#### Feature Description

This API (Initiate Multipart Upload) initializes a multipart upload task.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model createMultipartUpload(array $args = array());
```

#### Sample Request

[//]: # (.cssg-snippet-init-multi-upload)
```php
try {
    $result = $cosClient->createMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String  | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is `doc/pic.jpg` | Yes |
| CacheControl | String  | Cache policy. Sets Cache-Control  | No |
| ContentDisposition | String | File name. Sets Content-Disposition | No |
| ContentEncoding | String | Encoding format. Sets Content-Encoding  | No |
| ContentLanguage | String  | Language type. Sets Content-Language  | No |
| ContentLength | Int | Sets transmission length  | No |
| ContentType | String | Content Type. Sets Content-Type | No |
| Expires | String | Sets Content-Expires | No |
| Metadata | Array | File metadata customized by the user | No |
| StorageClass | String | Sets the object storage class; Options: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD  | No |
| ContentMD5 | String | Set MD5 of the file to be uploaded for verification | No |
| ServerSideEncryption | String | Server side encryption method | No |

#### Sample Response

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
#### Returned Result

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String | Object Key | No |
| UploadId | String |  ID of multipart upload  | No |

### <span id = "LIST_MULIT_UPLOAD"> Querying a Multipart Upload </span>

#### Feature Description

This API (List Parts) is used to query the uploaded parts in a specific multipart upload process.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model listParts(array $args = array());
```

#### Sample Request

[//]: # (.cssg-snippet-list-parts)
```php
try {
    $result = $cosClient->listParts(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String | Object Key | Yes |
| UploadId | String |  ID of multipart upload  | Yes |
| PartNumberMarker | Int | Marks the starting point of the list of returned parts    | No |
| MaxParts | Int | The maximum number of returned parts. It defaults to 1000. | No |

#### Sample Response

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
#### Returned Result

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String | Object Key | No |
| UploadId | String |  ID of multipart upload  | No |
| IsTruncated | Int  | Indicates whether the returned objects are truncated | No |
| PartNumberMarker | Int | Marks the starting point of the list of returned parts    | No |
| MaxParts | Int | The maximum number of returned parts. It defaults to 1000. | No |
| Initiator | String | User who initiated the multipart upload | No |
| Parts | Array | Returned list of parts | No |
| Part | Array | Returned parts attributes | Parts |
| PartNumber | Int | Part identifier | Part |
| LastModified | String | Time the parts were last uploaded | Part |
| ETag | String | MD5 of the part | Part |
| Size | String | Part size | Part |

### <span id = "MULIT_UPLOAD_PART"> Uploading Parts</span>

This API (Upload Part) is used to upload a part.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model uploadPart(array $args = array());
```

#### Sample Request

[//]: # (.cssg-snippet-upload-part)
```php
try {
    $result = $cosClient->uploadPart(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
        'Key' => 'exampleobject', 
        'Body' => 'string',
        'UploadId' => 'NWNhNDY0YzFfMmZiNTM1MGFfNTM2YV8xYjliMTg', // Multipart upload ID of an object. Returned in the response of Initiate Multipart Upload 
        'PartNumber' => integer, // Part serial number. COS merges parts according to the part serial number
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String | Object Key | Yes |
| UploadId | String |  Multipart upload ID of an object. Returned in the response of Initiate Multipart Upload | Yes |
| Body | File/String | Content to be uploaded | Yes |
| PartNumber | Int | Part serial number. COS merges parts according to the part serial number | Yes |
| ContentLength | Int | Sets transmission length  | No |
| ContentMD5 | String | Set MD5 of the file to be uploaded for verification | No |

#### Sample Response

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
#### Returned Result

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| ETag | String | MD5 of the part | No |

### <span id = "COMPLETE_MULIT_UPLOAD"> Completing a Multipart Upload </span>

#### Feature Description

This API (Complete Multipart Upload) is used to complete the entire multipart upload.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model completeMultipartUpload(array $args = array());
```

#### Sample Request

[//]: # (.cssg-snippet-complete-multi-upload)
```php
try {
    $result = $cosClient->completeMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String | Object Key | Yes |
| UploadId | String |  ID of multipart upload  | Yes |
| Parts | Array | List of parts information | Yes |
| Part | Array | Part information | Yes |
| ETag | String | MD5 of the part | No |
| PartNumber | Int  | Part number | Yes |


### <span id = "ABORT_MULIT_UPLOAD"> Aborting a Multipart Upload </span>

#### Feature Description

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model abortMultipartUpload(array $args = array());
```

#### Sample Request

[//]: # (.cssg-snippet-abort-multi-upload)
```php
try {
    $result = $cosClient->abortMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String | Object Key | Yes |
| UploadId | String |  ID of multipart upload  | Yes |


## Other Operations

### Restoring an Archived Object 

#### Feature Description

This API (POST Object restore) is used to restore an archived object.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model restoreObject(array $args = array());
```

#### Sample Request

[//]: # (.cssg-snippet-restore-object)
```php
try {
    $result = $cosClient->restoreObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String | Object Key | Yes |
| Days | String | Sets the validity period of the temporary replica in days | Yes |
| CASJobParameters | Array | Restore information | Yes |
| Tier | String | When restoring data, Tier can be specified as three types of restoration supported by CAS: Expedited, Standard, and Bulk. | Yes |

### Setting Object ACL

#### Feature Description

This API (Put Object ACL) is used to set an ACL for an object.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model putObjectAcl(array $args = array());
```

#### Sample Request

[//]: # (.cssg-snippet-put-object-acl)
```php
try {
    $result = $cosClient->putObjectAcl(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ----------- | ------ | ------------------------------------------------------------ | --------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String | Object Key | Yes |
| Grants    | Array  | ACL permissions information                                                  | No          |
| Grant       | Array  | ACL permissions information                                                  | No          |
| Grantee    | Array  | ACL permissions information                                                  | No          |
| Type        | String | Authorized user’s permission type                                | No         |
| Permission  | String | Permission type. Valid values: FULL_CONTROL, WRITE, READ | No         |
| ACL         | String | Overall permission type. Valid values: private, public-read | No              |
| Owner       | String | Bucket owner information                               | No              |
| DisplayName | String | Name of the authorized user | string |
| ID          | String | Authorized user ID                                                 | No |


### Get the object ACL

#### Feature Description

This API (Get Object ACL) is used to get the ACL of an object.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model getObjectAcl(array $args = array());
```

#### Sample Request

[//]: # (.cssg-snippet-get-object-acl)
```php
try {
    $result = $cosClient->getObjectAcl(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
        'Key' => 'exampleobject',
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample Response

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

#### Returned Result

| Parameter Name | Type | Description | Parent Node | 
| ----------- | ------ | ----------------------------------------------- | --------------- |
| Grants    | Array  | ACL permissions information                                                  | No          |
| Grant       | Array  | ACL permissions information                               | Grants          |
| Grantee    | Array  | ACL permissions information                                                  | Grant          |
| Permission  | String | Permission type. Valid values: FULL_CONTROL, WRITE, READ | Grant           |
| Owner       | String | Bucket owner information                     | No              |
| DisplayName | String | Authorized user name                         | Grantee / Owner |
| ID          | String | Authorized user ID            | Grantee/Owner |


## Advanced APIs (Recommended)
This section encapsulates advanced APIs for uploading and copying. The user only needs to set the corresponding parameters. The APIs will decide internally whether to perform simple upload/copy or multipart upload/copy based on the file size. Before using the API, make sure you have completed initialization as instructed in [Getting Started](https://intl.cloud.tencent.com/document/product/436/8629).


### Object Uploading

#### Feature Description

This API automatically selects between simple upload and multipart upload according to the file size.

#### Sample Request

[//]: # (.cssg-snippet-transfer-upload-object)
```php
try {
    $result = $cosClient->Upload(
        $bucket = 'examplebucket-1250000000', //Format：BucketName-APPID
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

### Object Replication

#### Feature Description

This API automatically selects between simple replication and multipart replication according to the file size.

#### Sample Request

[//]: # (.cssg-snippet-transfer-copy-object)
```php
try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', //Format：BucketName-APPID
        $key = 'exampleobject',
        $copySorce = array(
            'Region' => 'ap-guangzhou', 
            'Bucket' => 'examplebucket2-1250000000', 
            'Key' => 'exampleobject', 
        ),
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
