## Overview

This document provides an overview of APIs and SDK sample codes related to simple operations, multipart operations and other operations on objects.

**Simple Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/7734) | Querying object list | Queries a part of or all objects in a bucket |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/35521) | Querying list of current and historical versions of objects | Queries some or all objects in a bucket and their historical versions |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Gets object metadata | Gets the meta information of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Gets an object | Downloads an object (file) locally |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Sets object replication | Copies a file to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deletes a single object | Deletes the specified object in the bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |


**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing multipart upload | Initializes a multipart upload |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads object parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completes multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restores an archived object | Restores an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Sets the object ACL | Sets an ACL for an object (file) in the bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Gets the object ACL | Gets the ACL of an object (file) |



## Simple Operations

### Querying object list

#### Feature

This API (List Object) is used to query all objects in a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model listObjects(array $args = array());
```

#### Sample requests
##### Sample 1: Query a list of objects with specified prefix and starting object
[//]: # (.cssg-snippet-get-bucket-comp)
```php
try{
    $result = $cosClient->listObjects(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
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


#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID                         | Yes |
| Delimiter | String | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | No |
| EncodingType | String | Indicates the encoding method of the returned value. The value is not encoded by default. Valid value: `url`    | No |
| Marker | String | Marks the starting point of the list of returned objects. Entries are listed using UTF-8 binary order by default.                     | No |
| Prefix | String | Filters the keys of objects by matching the objects prefixed with this parameter. It is left empty by default.        | No |
| MaxKeys | Int | Maximum number of returned objects. It defaults to 1000. | No |

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
#### Response

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| Name | String | Bucket name. Format: BucketName-APPID                         | No |
| Delimiter | String | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders.    | No |
| EncodingType | String | Specifies the encoding type of the returned value    | No |
| Marker | String | Marks the starting point of the list of returned objects. Entries are listed using UTF-8 binary order by default.  | No |
| Prefix | String | Filters the keys of objects by matching the objects prefixed with this parameter.        | No |
| MaxKeys | Int | The maximum number of returned objects. It defaults to 1000. | No |
| IsTruncated | Int | Indicates whether the returned objects are truncated | No |
| Contents | Array | Returned list of objects | No |
| Contents | Array | Returned object attributes, containing a list of metadata of all objects, including 'ETag', 'StorageClass', 'Key', 'Owner', 'LastModified', and 'Size' | Contents |


### Querying Objects and Their Historical Versions 

#### Feature

This API (GET Bucket Object Versions) is used to query some or all objects in a bucket and their historical versions.

#### Method prototype

```
public Guzzle\Service\Resource\Model listObjectVersions(array $args = array());
```
#### Sample requests
##### Sample 1: Query a list of historical objects
[//]: # (.cssg-snippet-list-object-versioning)
```php
try{
    $result = $cosClient->listObjectVersions(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
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

#### Parameter Description

| Parameter Name     | Type      | Description                            | Required |
| ------------- | -------------------------- | ------ | ---- |
| Bucket   | String |    Bucket name. Format: BucketName-APPID     |                    Yes |
| Prefix    | String  | Filters the object keys prefixed with the value of this parameter. It is left empty by default. | No   |
| Delimiter  | String   | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders.          | No |
| KeyMarker | String      | Marks the starting object key of the list of returned objects. Entries are listed in UTF-8 binary order by default. | No   |
| VersionIdMarker | String | Marks the starting VersionId in a list of returned objects. Entries are listed in UTF-8 binary order by default. | No |
| MaxKeys        | Int   | Maximum number of objects returned. Default value: 1000. | No   |
| EncodingType      | String   | Indicates the encoding method of returned value, which is not encoded by default. Valid value: `url`. |  No |

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
#### Response

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| Name | String | Bucket name. Format: BucketName-APPID                         | No |
| Delimiter | String | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders.    | No |
| EncodingType | String | Specifies the encoding type of the returned value    | No |
| KeyMarker | String | Marks the starting point of key of the list of returned objects. Entries are listed using UTF-8 binary order by default.    | No |
| VersionIdMarker | String |  Marks the starting point of VersionId of the list of returned objects. Entries are listed using UTF-8 binary order by default.          |  No |
| NextKeyMarker | String | Marks the starting point of the next list of returned objects if IsTruncated is true.        | No |
| NextVersionIdMarker | String | Marks the starting point of VersionId of the next list of returned objects if IsTruncated is true.    | No |
| Prefix | String | Filters the keys of objects by matching the objects prefixed with this parameter.        | No |
| MaxKeys | Int | The maximum number of returned objects. It defaults to 1000. | No |
| IsTruncated | Int | Indicates whether the returned objects are truncated | No |
| Versions | Array| List containing metadata of all the versions of objects | No |
| Versions | Array | List containing metadata of all the versions of objects, including 'ETag', 'StorageClass', 'Key', 'VersionId', 'IsLatest', 'Owner', 'LastModified', and 'Size' | Versions |
| CommonPrefixes | Array | All objects starting with Prefix and ending with Delimiter are grouped into the same type | No |




### Uploading an object using simple upload

#### Feature

This API (PUT Object) is used to upload an object to a specified bucket. The uploaded object has a size restriction of 5GB. Please use [Multipart Upload] (#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced APIs] (#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) to upload objects greater than 5GB.

#### Method prototype

```php
public Guzzle\Service\Resource\Model putObject(array $args = array())
```

#### Sample requests
##### Sample 1: Upload a local file
[//]: # (.cssg-snippet-put-object)
```php
try{ 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID 
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

##### Sample 2: Upload an archived file
[//]: # (.cssg-snippet-put-object-archive)
```php
try{ 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID 
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

##### Sample 3: Upload a specified Content-type file
[//]: # (.cssg-snippet-put-object-with-content-type)
```php
try{ 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID 
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


#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String | ObjectKey, the unique identifier of an object in a bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is `doc/pic.jpg`.    | No |
| ACL | String | Sets ACL of an object, e.g. `private`, `public-read`| No |
| Body | File/String | Content to be uploaded | Yes |
| CacheControl | String  | Cache policy. Sets CacheControl  | No |
| ContentDisposition | String | File name. Sets ContentDisposition | No |
| ContentEncoding | String | Encoding format. Sets ContentEncoding  | No |
| ContentLanguage | String | Language type. Sets ContentLanguage | No |
| ContentLength | int | Sets transmission length | No |
| ContentType | String | Content type. Sets `ContentType` | No |
| Expires | string | Sets Content-Expires | No |
| Metadata | Array | File metadata customized by the user | No |
| StorageClass | String | Sets the object storage class; Options: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD | No |
| ContentMD5 | String | Set MD5 of the uploaded file for verification | No |
| ServerSideEncryption | String | Sets server-side encryption method | No |

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
            [ObjectURL] => http://lewzylucd2-1251668577.cos.ap-chengdu.myqcloud.com/123
        )

)
```
#### Response

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| ETag | String | MD5 of the uploaded file | No |
| VersionId | String | The version ID of the file when versioning is enabled. | No  |


### Querying object metadata

#### Feature

The API (HEAD Object) is used to query object metadata.

#### Method prototype

```php
public Guzzle\Service\Resource\Model headObject(array $args = array());
```

#### Sample requests

[//]: # (.cssg-snippet-head-object)
```php
try{
    $result = $cosClient->headObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
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
| Bucket | String | Bucket name. Format: BucketName-APPID                         | Yes |
| Key | String | ObjectKey, the unique identifier of an object in a bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is `doc/pic.jpg` | Yes |
| VersionId | String | The version ID of the specified file when versioning is enabled. | No  |

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
        )

)
```
#### Response

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| CacheControl | String | Cache policy. Sets CacheControl | No |
| ContentDisposition | String | File name. Sets ContentDisposition | No |
| ContentEncoding | String | Encoding format. Sets ContentEncoding | No |
| ContentLanguage | String | Language type. Sets ContentLanguage | No |
| ContentLength | Int | Sets transmission length | No |
| ContentType | String | Content Type. Sets ContentType | No | 
| Metadata | Array | File metadata customized by the user | No |
| StorageClass | String | Sets the object storage class; Options: STANDARD, STANDARD_IA, ARCHIVE | No |
| ServerSideEncryption | String | Server-side encryption method | No |
| ETag | String | MD5 of a file | No |
| Restore | String | Restoration information of an archived file | No |


### Downloading an object

#### Feature

This API (Get Object) is used to download an object locally.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getObject(array $args = array());
```

#### Sample requests
##### Sample 1: Download a file locally
[//]: # (.cssg-snippet-get-object)
```php
try{
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
        'Key' => 'exampleobject',
        'SaveAs' => 'path/to/localFile',
    )); 
    // Request succeeded
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

##### Sample 2: Multipart download
[//]: # (.cssg-snippet-get-object-range)
```php
try{
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
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

##### Sample 3: Download a file with specified version ID
[//]: # (.cssg-snippet-get-object-with-versionId)
```php
try{
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String | ObjectKey, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is `doc/pic.jpg`. | Yes |
| SaveAs | String | Local directory used to store the file | No |
| VersionId   | String | The version ID of the specified file when versioning is enabled.  | No |
| Range | String | Sets the range of bytes of the file to be downloaded in the format of bytes=first-last   | No |
| ResponseCacheControl | String| Sets the Cache-Control in the response header  | No |
| ResponseContentDisposition | String | Sets `Content-Disposition` in the response header  | No |
| ResponseContentEncoding | String | Sets Content-Encoding in the response header | No |
| ResponseContentLanguage | String | Sets `Content-Language` in the response header  | No |
| ResponseContentType | String | Sets `Content-Type` in the response header | No |
| ResponseExpires | String | Sets Content-Expires in the response header | No |


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
        )

)
```
#### Response

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| Body | File/String | Content to be downloaded    | No |
| ETag | String | MD5 of a file | No |
| Expires | String | Content-Expires| No |
| Metadata | Array | File metadata customized by the user | No |
| StorageClass | String | Sets the object storage class; Options: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD | No |
| ContentMD5 | String | Set MD5 of the file to be uploaded for verification | No |
| ServerSideEncryption | String | Server-side encryption method | No |
| CacheControl | String | Cache policy. Sets CacheControl | No |
| ContentDisposition | String | File name. Sets ContentDisposition | No |
| ContentEncoding | String | Encoding format. Sets ContentEncoding | No |
| ContentLanguage | String | Language type. Sets ContentLanguage | No |
| ContentLength | Int | Sets transmission length | No |
| ContentType | String | Content Type. Sets ContentType | No |
| Metadata | Array | File metadata customized by the user | No |
| Restore | String | Restoration information of an archived file | No |

### Setting object replication
This API (PUT Object - Copy) is used to copy an object to the destination path.

#### Method prototype

```php
public Guzzle\Service\Resource\Model copyObject(array $args = array());
```

#### Sample requests
##### Sample 1: Copy an object
[//]: # (.cssg-snippet-copy-object)
```php
try{
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.COS_REGION.myqcloud.com/sourceObject',
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

##### Sample 2: Copy an object with specified version ID
[//]: # (.cssg-snippet-copy-object-with-versionId)
```php
try{
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.COS_REGION.myqcloud.com/sourceObject?versionId=MTg0NDUxNjI3NTM0ODE2Njc0MzU',
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

##### Sample 3: Change COS class to Archive
[//]: # (.cssg-snippet-copy-object-update-storage-class)
```php
try{
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.COS_REGION.myqcloud.com/sourceObject',
        'StorageClass' => 'Archive'
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

##### Sample 4: Modifying metadata
[//]: # (.cssg-snippet-copy-object-update-metadata)
```php
try{
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.COS_REGION.myqcloud.com/sourceObject',
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String | ObjectKey, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is `doc/pic.jpg`. | Yes |
| CopySource | String | Path of the file to copy, containing Appid, Bucket, Key and Region,<br>such as `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | Yes |
| MetadataDirective | String | Valid values: Copy and Replaced. When it is set to Copy, ignore the configured user metadata information and copy the file directly. When it is set to Replaced, modify the metadata according to the configured meta information. If the destination path is identical to the source path, it must be set to Replaced. | Yes |

### Deleting a single object

#### Feature

This API (File/Object) is used to delete a specified object in a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteObject(array $args = array());
```

#### Request samples

[//]: # (.cssg-snippet-delete-object)
```php
try{
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String | ObjectKey, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is `doc/pic.jpg`. | Yes |
VersionId | String | Version ID of a deleted file | No |


### Deleting multiple objects

#### Feature

Delete multiple objects from a bucket with a single request.

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteObjects(array $args = array());
```

#### Sample requests

[//]: # (.cssg-snippet-delete-multi-object)
```php
try{
    $result = $cosClient->deleteObjects(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
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
| Objects   | Array | List of deleted objects     | Yes     |
| Object   | Array | A deleted object     | Yes     |
| Key | String | ObjectKey, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is `doc/pic.jpg`. |    Yes    |
| VersionId | String | Version ID of a deleted file |  No  |

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
#### Response

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
Deleted | Array | List of objects deleted successfully | No |
Errors | Array | List of objects failing to be deleted | No |
Key | String | Object key | Deleted/Errors |
Code | String | Failure error code | Errors |
Message | String | Failure error message | Error |


## Multipart Operations

### Query multipart uploads

#### Feature

This API (List Multipart Uploads) is used to query in-progress multipart uploads in the specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model listMultipartUploads(array $args = array());
```

#### Sample requests

[//]: # (.cssg-snippet-list-multi-upload)
```php
try{
    $result = $cosClient->listMultipartUploads(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID                         | Yes |
| Delimiter | String | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders.    | No |
| EncodingType | String | Indicates the encoding method of the returned value. The value is not encoded by default. Valid value: `url`    | No |
| KeyMarker | String | Marks the starting part in a list of returned parts | No |
| UploadIdMarker | String | Marks the starting part in a list of returned parts | No |
| Prefix | String | Filters the keys of parts by matching the objects prefixed with this parameter. It is left empty by default. | No  |
| MaxUploads | Int | Maximum number of parts returned at a time. Default value: 1000. | No |

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
#### Response

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | No |
| IsTruncated | Int | Indicates whether the returned objects are truncated | No |
| Uploads | Array | List of returned parts | No |
| Upload | Array | Attributes of a returned part | Uploads |
| Key | String | Object Key Name | Upload |
| UploadId | String | ID of a multipart upload | Upload |
| Initiator | String | Initiator of this part | Upload |
| Owner | String | Part owner | Upload |
| StorageClass | String | Storage class of the part | Upload |
| Initiated | String | Part initiation time | Upload |


### Upload an object using multipart upload

This includes the following operations:

- Uploading an object in multiple parts: Initializing multipart upload, uploading parts, and completing the upload of all parts.
- Resuming the multipart upload: querying the parts uploaded, uploading parts, and completing all multipart uploads.
- Deleting the uploaded parts.

### <span id = "INIT_MULIT_UPLOAD"> Initializing multipart upload </span>

#### Feature

Initialize a multipart upload.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMultipartUpload(array $args = array());
```

#### Request samples

[//]: # (.cssg-snippet-init-multi-upload)
```php
try{
    $result = $cosClient->createMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID                         | Yes |
| Key | String | ObjectKey, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is `doc/pic.jpg`. | Yes |
| CacheControl | String | Cache policy. Sets `Cache-Control`. | No |
| ContentDisposition | String | File name. Sets `Content-Disposition`.  | No  |
| ContentEncoding | String | Encoding format. Sets `Content-Encoding` | No |
| ContentLanguage | String | Language type. Sets Content-Language | No |
| ContentLength | Int | Sets transmission length | No |
| ContentType | String | Content type. Sets `Content-Type` | No |
| Expires | string | Sets Content-Expires | No |
| Metadata | Array | File metadata customized by the user | No |
| StorageClass | String | Sets the object storage class; Options: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD | No |
| ContentMD5 | String | Set MD5 of the uploaded file for verification | No |
| ServerSideEncryption | String | Sets server-side encryption method | No |

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
#### Response

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | No |
| Key | String | Object key | No |
| UploadId | String | ID of a multipart upload | No |

### <span id = "LIST_MULIT_UPLOAD">Query uploaded parts</span>

#### Feature

This API (List Parts) is used to query the uploaded parts in a specific multipart upload.

#### Method prototype

```php
public Guzzle\Service\Resource\Model listParts(array $args = array());
```

#### Sample requests

[//]: # (.cssg-snippet-list-parts)
```php
try{
    $result = $cosClient->listParts(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID                         | Yes |
| Key | String | Object key | Yes |
| UploadId | String | ID of the multipart upload | Yes |
| PartNumberMarker | Int | Marks the starting part in a list of returned parts | No |
| MaxParts | Int | Maximum number of returned parts. Default value: 1000. | No |

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
#### Response

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | No |
| Key | String | Object key | No |
| UploadId | ID of the multipart upload | String | No |
| IsTruncated | Int | Indicates whether the returned objects are truncated | No |
PartNumberMarker | Int | Marks the starting part in a list of parts returned | No |
MaxParts | Int | Maximum number of parts returned. Default value: 1000. | No |
| Initiator | String | Initiator of this part | No  |
| Parts | Array | Returned part list | No |
| Part | Array | Returned part attributes | Parts |
| PartNumber | Int | Part number | Part |
| LastModified | String | Last upload time of parts | Part |
| ETag | String | MD5 of the uploaded part | Part |
| Size | String | Size of the part | Part |

### <span id = "MULIT_UPLOAD_PART"> Uploading parts</span>

This API (Upload Part) is used to upload a part.

#### Method prototype

```php
public Guzzle\Service\Resource\Model uploadPart(array $args = array());
```

#### Sample requests

[//]: # (.cssg-snippet-upload-part)
```php
try{
    $result = $cosClient->uploadPart(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
        'Key' => 'exampleobject', 
        'Body' => 'string',
        'UploadId' => 'exampleUploadId', //UploadId is ID of an multipart upload, which you get from the returned parameters when initiating the multipart upload 
        'PartNumber' => 1, //PartNumber is the serial number of a part, using which COS can combine parts
    )); 
    // Request succeeded
    print_r($result);
    $this->eTag = $result['ETag'];
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID                         | Yes |
| Key | String | Object key | Yes |
| UploadId | String | ID of an multipart upload, obtained from the returned parameters when initiating the multipart upload | Yes |
| Body | File/String | Content to be uploaded | Yes |
| PartNumber | Int | Serial number of a part, using which COS can combine parts | Yes |
| ContentLength | Int | Sets transmission length | No |
| ContentMD5 | String | Set MD5 of the uploaded file for verification | No |

#### Sample response

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
#### Response

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | -------- | ---------------------------------- | ------------- |
| ETag | String | MD5 of the uploaded part | No |

### <span id = "COMPLETE_MULIT_UPLOAD"> Complete multipart upload </ span>

#### Feature

This API (Complete Multipart Upload) is used to complete the entire multipart upload.

#### Method prototype

```php
public Guzzle\Service\Resource\Model completeMultipartUpload(array $args = array());
```

#### Sample requests

[//]: # (.cssg-snippet-complete-multi-upload)
```php
try{
    $result = $cosClient->completeMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID                         | Yes |
| Key | String | Object key | Yes |
| UploadId | String | ID of the multipart upload | Yes |
| Parts | Array | List of part information | Yes |
| Part | Array | Content information on an uploaded part | Yes |
| ETag | String | MD5 of part content | Yes |
| PartNumber | Int | Number of a part | Yes |


### <span id = "ABORT_MULIT_UPLOAD"> Aborting a multipart upload </span>

#### Feature

This API (Abort Multipart Upload) is used to abort a multipart upload and delete the uploaded parts.

#### Method prototype

```php
public Guzzle\Service\Resource\Model abortMultipartUpload(array $args = array());
```

#### Sample requests

[//]: # (.cssg-snippet-abort-multi-upload)
```php
try{
    $result = $cosClient->abortMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Key | String | Object key | Yes |
| UploadId | String | ID of the multipart upload | Yes |


## Other Operations

### Restoring an archived object 

#### Feature

This API (POST Object restore) is used to restore an archived object.

#### Method prototype

```php
public Guzzle\Service\Resource\Model restoreObject(array $args = array());
```

#### Sample requests

[//]: # (.cssg-snippet-restore-object)
```php
try{
    $result = $cosClient->restoreObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID                         | Yes |
| Key | String | Object key | Yes |
| Days | String | Sets the number of days before a temporary copy expires | Yes |
| CASJobParameters | Array | Restoration Information | Yes |
| Tier | String | When restoring data, Tier can be specified as three types of restoration supported by CAS: Expedited, Standard, and Bulk. | Yes |

### Setting object ACL

#### Feature

This API (PUT Object ACL) is used to set an ACL for an object.

#### Method prototype

```php
public Guzzle\Service\Resource\Model putObjectAcl(array $args = array());
```

#### Sample requests

[//]: # (.cssg-snippet-put-object-acl)
```php
try{
    $result = $cosClient->putObjectAcl(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
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
| Key | String | Object key | Yes |
| Grants      | Array  | List of ACL permissions                                                  | No              |
| Grant       | Array  | ACL permissions information                                                  | No          |
| Grantee     | Array  | ACL permissions information                                                  | No           |
| Type        | String | Type of owner permission                                               | No         |
| Permission  | String | Permission type. Valid values: FULL_CONTROL, WRITE, READ.          | No           |
| ACL         | String | Global permission type. Valid values: private, public-read. | No              |
| Owner       | String | Bucket owner                                             | No              |
| DisplayName | String | Name of permission owner                                         | No |
| ID          | String | ID of permission owner                                                 | No |


### Getting object ACL

#### Feature

This API (Get Object ACL) is used to get the ACL of an object.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getObjectAcl(array $args = array());
```

#### Sample requests

[//]: # (.cssg-snippet-get-object-acl)
```php
try{
    $result = $cosClient->getObjectAcl(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
        'Key' => 'exampleobject',
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample response

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

#### Response

| Parameter Name | Type | Description | Parent Node | 
| ----------- | ------ | ----------------------------------------------- | --------------- |
| Grants      | Array  | List of ACL permissions                                     | No              |
| Grant       | Array  | ACL permission information                                     | Grants          |
| Grantee     | Array  | ACL permission information                                     | Grant           |
| Permission  | String | Permission type. Valid values: FULL_CONTROL, WRITE, READ | Grant           |
| Owner       | String | Bucket owner                                | No              |
| DisplayName | String | Name of permission owner                            | Grantee / Owner |
| ID          | String | ID of permission owner                                   | Grantee / Owner |


## Advanced APIs (Recommended)
This section encapsulates advanced APIs for uploading and copying. The user only needs to set the corresponding parameters. The APIs will decide internally whether to perform simple upload/copy or multipart upload/copy based on the file size. Before using the API, make sure you have completed initialization as instructed in [Getting Started] (https://intl.cloud.tencent.com/document/product/436/8629).


### Complex upload

#### Feature

This API internally calls Simple Upload for small files and Multipart Upload for large files based on the file size. For parameters, see the `PutObject` API.

#### Sample requests
##### Sample 1: Upload a local object
[//]: # (.cssg-snippet-transfer-upload-object)
```php
try{
    $result = $cosClient->Upload(
        $bucket = 'examplebucket-1250000000', //Format: BucketName-APPID
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

##### Sample 2: Upload an archived object
[//]: # (.cssg-snippet-transfer-upload-object-archive)
```php
try{
    $result = $cosClient->Upload(
        $bucket = 'examplebucket-1250000000', //Format: BucketName-APPID
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

##### Sample 3: Upload an object with metadata by specifying the size of a single part
[//]: # (.cssg-snippet-transfer-upload-object-comp)
```php
try{
    $result = $cosClient->Upload(
        $bucket = 'examplebucket-1250000000', //Format: BucketName-APPID
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

### Complex copy

#### Feature

This API internally calls Set CopyObject for small files and Multipart Copy for large files based on the file size. For parameters, see the `CopyObject` API.


#### Sample requests
##### Sample 1: Copy an object
[//]: # (.cssg-snippet-transfer-copy-object)
```php
try{
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', //格式：BucketName-APPID
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
##### Sample 2: Transition objects to a COS class
```php
try{
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', //Format: BucketName-APPID
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
##### Sample 3: Modify COS attributes
```php
try{
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', //Format: BucketName-APPID
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
