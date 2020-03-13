## Introduction

This document provides an overview of APIs and SDK sample codes related to simple operations, multipart operations and other operations on objects.

**Simple Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/7734) | Querying object list | Queries a part of or all objects in a bucket |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/35521) | Querying list of current and historical versions of objects | Queries some or all objects in a bucket and their historical versions |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies an object to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
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
| [PUT Object acl](https://cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple Operations

### Querying Object List

#### Feature Description

This API (GET Bucket (List Object)) is used to query some or all objects in a bucket.

#### Method Prototype

```
list_objects(Bucket, Delimiter="", Marker="", MaxKeys=1000, Prefix="", EncodingType="", **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-get-bucket)
```python
response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='folder1'
)
```

#### Request Example for All Parameters

[//]: # (.cssg-snippet-get-bucket-comp)
```python
response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='string',
    Delimiter='/',
    Marker='string',
    MaxKeys=100,
    EncodingType='url'
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes | 
| Prefix  |  Filters the object key by matching the objects prefixed with this parameter. It is left empty by default.  | String  | No | 
| Delimiter | Sets a delimiter ("/") to simulate a folder. It is left empty by default. | String | No |
| Marker | Marks the starting point of the list of returned objects. Entries are listed using UTF-8 binary order by default. | String | No | 
| MaxKeys | The maximum number of returned objects. It defaults to 1000. | int | No | 
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | String | No |

#### Returned Result

The meta information of the object obtained. Type is dict:

```python
{
    'MaxKeys': '1000', 
    'Prefix': 'string',
    'Delimiter': 'string',
    'Marker': 'string',
    'NextMarker': 'string',
    'Name': 'examplebucket-1250000000',  
    'IsTruncated': 'false'|'true',
    'EncodingType': 'url',
    'Contents':[
        {
            'ETag': '"a5b2e1cfb08d10f6523f7e6fbf3643d5"', 
            'StorageClass': 'STANDARD', 
            'Key': 'exampleobject',
            'Owner': {
                'DisplayName': '1250000000',
                'ID': '1250000000'
            }, 
            'LastModified': '2017-08-08T09:43:35.000Z', 
            'Size': '23'
        },
    ],
    'CommonPrefixes':[
        {
            'Prefix': 'string'
        },
    ],
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- |
| MaxKeys   | The maximum number of returned objects. It defaults to 1000.  | String |
| Prefix   | Matches the objects prefixed with this parameter. It is left empty by default. | String  | 
| Delimiter | Sets a delimiter ("/") to simulate a folder. It is left empty by default. | String |
| Marker | Marks the starting point of the list of returned objects. Entries are listed using UTF-8 binary order by default. | string |
| NextMarker | Marks the starting point of the next list of returned objects if IsTruncated is true. | string |
| Name | Bucket name. Format: BucketName-APPID | String | 
| IsTruncated   |  Indicates whether the returned object is truncated | String|
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | String | No |
| Contents | The list containing the meta information of all objects, including 'ETag', 'StorageClass', 'Key', 'Owner', 'LastModified', 'Size' | List |
| CommonPrefixes | All objects starting with Prefix and ending with Delimiter are grouped into the same type | List |

### Query Objects and the List of Previous Versions 

#### Feature Description

Queries a part of or all objects and previous versions in a bucket

#### Method Prototype

```
list_objects_versions(Bucket, Prefix="", Delimiter="", KeyMarker="", VersionIdMarker="", MaxKeys=1000, EncodingType="", **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-list-object-versioning)
```python
response = client.list_objects_versions(
    Bucket='examplebucket-1250000000',
    Prefix='string'
)
```

#### Request Example for All Parameters

[//]: # (.cssg-snippet-list-object-versioning-comp)
```python
response = client.list_objects_versions(
    Bucket='examplebucket-1250000000',
    Prefix='string',
    Delimiter='/',
    KeyMarker='string',
    VersionIdMarker='string',
    MaxKeys=100,
    EncodingType='url'
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes | 
| Prefix  |  Filters the object key by matching the objects prefixed with this parameter. It is left empty by default.  | String  | No | 
| Delimiter | Sets a delimiter ("/") to simulate a folder. It is left empty by default. | String | No |
| Marker | Marks the starting point of key of the list of returned objects. Entries are listed using UTF-8 binary order by default. | String | No |
| VersionIdMarker|  Marks the starting point of VersionId of the list of returned objects. Entries are listed using UTF-8 binary order by default. | String  |  No |
| MaxKeys | The maximum number of returned objects. It defaults to 1000. | int | No | 
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | String | No |

#### Returned Result

The meta information of the object obtained. Type is dict:

```python
{
    'MaxKeys': '1000', 
    'Prefix': 'string',
    'Delimiter': 'string',
    'KeyMarker': 'string',
    'VersionIdMarker': 'string',
    'NextMarker': 'string',
    'NextVersionIdMarker': 'string',
    'Name': 'examplebucket-1250000000',  
    'IsTruncated': 'false'|'true',
    'EncodingType': 'url',
    'Version':[
        {
            'ETag': '"a5b2e1cfb08d10f6523f7e6fbf3643d5"', 
            'StorageClass': 'STANDARD', 
            'Key': 'exampleobject',
            'VersionId': 'string',
            'IsLatest': 'true'|'false',
            'Owner': {
                'DisplayName': '1250000000',
                'ID': '1250000000'
            }, 
            'LastModified': '2017-08-08T09:43:35.000Z', 
            'Size': '23'
        },
    ],
    'DeleteMarker': [
        {
            'Key': 'exampleobject',
            'VersionId': 'string',
            'IsLatest': 'true'|'false',
            'Owner': {
                'DisplayName': '1250000000',
                'ID': '1250000000'
            },
            'LastModified': '2017-08-08T09:43:35.000Z'
        },
    ],
    'CommonPrefixes':[
        {
            'Prefix': 'string'
        },
    ],
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- |
| MaxKeys   | The maximum number of returned objects. It defaults to 1000.  | String |
| Prefix   | Matches the objects prefixed with this parameter. It is left empty by default. | String  | 
| Delimiter | Sets a delimiter ("/") to simulate a folder. It is left empty by default. | String |
| Marker | Marks the starting point of the list of returned objects. Entries are listed using UTF-8 binary order by default. | String |
| VersionIdMarker|  Marks the starting point of VersionId of the list of returned objects. Entries are listed using UTF-8 binary order by default. | String  |  
| NextMarker | Marks the starting point of the next list of returned objects if IsTruncated is true. | String |
| NextMarker | Marks the starting point of VersionId of the next list of returned objects if IsTruncated is true. | String |
| Name | Bucket name. Format: BucketName-APPID | String | 
| IsTruncated   |  Indicates whether the returned object is truncated | String|
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | String | No |
| Version | The list containing all the meta information of multiple versions of objects, including 'ETag'，'StorageClass'，'Key'，'VersionId'，'IsLatest'，'Owner'，'LastModified'，and 'Size' | List |
| DeleteMarker | The list containing all the meta information of delete marker objects, including 'Key'，'VersionId'，'IsLatest'，'Owner'，and 'LastModified' | List |
| CommonPrefixes | All objects starting with Prefix and ending with Delimiter are grouped into the same type | List |

### Uploading an Object Using Simple Upload

#### Feature Description

This API (Put Object) is used to upload an object to the specified bucket.

#### Method Prototype

```
put_object(Bucket, Body, Key, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-put-object)
```python
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes'|file,
    Key='exampleobject',
    EnableMD5=False
)
```

#### Request Example for All Parameters
[//]: # (.cssg-snippet-put-object-comp)
```python
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes'|file,
    Key='exampleobject',
    EnableMD5=False|True,
    ACL='private'|'public-read',  # Please use this parameter carefully, or the maximum of 1000 ACLs will be reached.
    GrantFullControl='string',
    GrantRead='string',
    StorageClass='STANDARD'|'STANDARD_IA'|'ARCHIVE',
    Expires='string',
    CacheControl='string',
    ContentType='string',
    ContentDisposition='string',
    ContentEncoding='string',
    ContentLanguage='string',
    ContentLength='123',
    ContentMD5='string',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    }
)
```
#### Parameter Description


| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
 |  Body  | The body of uploaded objects can be FileStream or ByteStream.|  file/bytes | Yes |
 | Key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | String | Yes | 
| EnableMD5 | Whether SDK is used to calculate Content-MD5, which is off by default. When it is turned on, the uploading time will increase. |Bool | No | 
| ACL | Sets ACL of objects. For example 'private'，'public-read' |String| No |
| GrantFullControl | Grants the grantee full permission in the format of `id="OwnerUin"` | String | No |
| GrantRead | Grants the grantee Read access in the format of `id="OwnerUin"` | String | No |
 | StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
 | Expires | Sets Expires. | String | No | 
 | CacheControl | Cache policy. Sets Cache-Control. | String | No |
 | ContentType | Content Type. Sets Content-Type. | String | No |  
 | ContentDisposition | File name. Sets Content-Disposition. | String | No |
 | ContentEncoding | Encoding format. Sets Content-Encoding. | String | No |
 | ContentLanguage | Language type. Sets Content-Language | String | No |
 | ContentLength | Sets transmission length | string | No | 
 | ContentMD5 | Sets MD5 of the uploaded object for verification | String | No | 
 |  Metadata | The meta information of objects customized by users must start with x-cos-meta. Otherwise it will be ignored. | Dict | No |

#### Returned Result
Attributes of the uploaded object. Type is dict:

```python
{
    'ETag': 'string',
    'x-cos-version-id': 'string'
}
```


| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- |
|  ETag   |  MD5 of the upload object | String |
|  x-cos-version-id   |  The version id of objects when the version control is enabled. | String  |



### Querying Object Metadata

#### Feature Description

The API (HEAD Object) is used to query the meta information of objects.

#### Method Prototype

```
head_object(Bucket, Key, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-head-object)
```python
response = client.head_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    VersionId='string',
    IfModifiedSince='Wed, 28 Oct 2014 20:30:00 GMT',
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
  | Bucket | Bucket name. Format: bucketname-appid. | String | Yes | 
  | Key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | String | Yes |
  | VersionId   | Specifies the version id of objects when the version control is enabled.  | String  | No | 
  | IfModifiedSince | The file is returned after it has been modified since the specified time. The time type is GMT. | String | No | 

#### Returned Result

The meta information of the object obtained. Type is dict:

```python
{
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'Cache-Control': 'max-age=1000000',
    'Content-Type': 'application/octet-stream',
    'Content-Disposition': 'attachment; filename="filename.jpg"',
    'Content-Encoding': 'gzip',
    'Content-Language': 'zh-cn',
    'Content-Length': '16807',
    'Expires': 'Wed, 28 Oct 2019 20:30:00 GMT',
    'x-cos-meta-test': 'test',
    'x-cos-version-id': 'MTg0NDUxODMzMTMwMDM2Njc1ODA',
    'x-cos-request-id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```


| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- | 
 | ETag  |  MD5 of the object | String |
 | Last-Modified | The last modification time of object. | String |
 | CacheControl | Cache policy. HTTP standard header. | String | 
 | ContentType | Content Type. HTTP standard header. | String | 
 | ContentDisposition | File name. HTTP standard header | String |
 | ContentEncoding | Encoding format. HTTP standard header. | String | 
 | ContentLanguage | Language type. HTTP standard header. | String | 
 |  Content-Length  | Object size | String |
 |  Expires | Cache expiration time. HTTP standard header. | String |
 |  x-cos-meta-* | The meta information of objects customized by users must start with x-cos-meta. Otherwise it will be ignored.  | String | 
 |  x-cos-version-id   |  The version id of objects when the version control is enabled. | String  | 


### Downloading an Object

#### Feature Description

This API (Get Object) is used to download an object.

#### Method Prototype

```
 get_object(Bucket, Key, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-get-object)
```python
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Range='string',
    IfMatch='"9a4802d5c99dafe1c04da0a8e7e166bf"',
    IfModifiedSince='Wed, 28 Oct 2014 20:30:00 GMT',
    IfNoneMatch='"9a4802d5c99dafe1c04da0a8e7e166bf"',
    IfUnmodifiedSince='Wed, 28 Oct 2014 20:30:00 GMT',
    ResponseCacheControl='string',
    ResponseContentDisposition='string',
    ResponseContentEncoding='string',
    ResponseContentLanguage='string',
    ResponseContentType='string',
    ResponseExpires='string',
    VersionId='string'
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name. Format: BucketName-APPID | String | Yes | 
 | key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | String | Yes | 
 | Range | Sets the range of bytes of the object  to be downloaded in the format of bytes=first-last | String | No | 
 |  IfMatch  | The file is returned when Etag matches with the specified content. |String  | No |  
 | IfModifiedSince | The file is returned after it has been modified since the specified time. The time type is GMT. | String | No |
 |  IfNoneMatch  |  The file is returned when Etag does not match with the specified content. | String  | No | 
 | IfUnmodifiedSince | The file is returned if it has been modified at or before the specified time. The time type is GMT.  | String | No |
 | ResponseCacheControl | Sets the Cache-Control in the response header | String | No | 
 | ResponseContentDisposition | Sets the Content-Disposition in the response header | String | No | 
 | ResponseContentEncoding | Sets the Content-Encoding in the response header | String | No |
 | ResponseContentLanguage | Sets the Content-Language in the response header | String | No | 
 | ResponseContentType | Sets the Content-Type in the response header | String | No |
 | Response-expires | Sets the `Expires` in the response header | String | No | 
 | VersionId | Specifies the Version ID of the object to be downloaded | String | No | 

#### Returned Result

Body and meta information of the download object. Type is dict:

```python
{
    'Body': StreamBody(),
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'Accept-Ranges': 'bytes',
    'Content-Range': 'bytes 0-16086/16087',
    'Cache-Control': 'max-age=1000000',
    'Content-Type': 'application/octet-stream',
    'Content-Disposition': 'attachment; filename="filename.jpg"',
    'Content-Encoding': 'gzip',
    'Content-Language': 'zh-cn',
    'Content-Length': '16807',
    'Expires': 'Wed, 28 Oct 2019 20:30:00 GMT',
    'x-cos-meta-test': 'test',
    'x-cos-version-id': 'MTg0NDUxODMzMTMwMDM2Njc1ODA',
    'x-cos-request-id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

<table>
   <tr>
      <th>Parameter Name</td>
      <th>Description</th>
      <th>Type</th>
   </tr>
   <tr>
      <td>Body</td>
      <td>downloads the object body. The method of get_raw_stream() gets a file stream, and the method of  get_stream_to_file(local_file_path) downloads the object body into the specified local file.</td>
      <td>StreamBody</td>
   </tr>
   <tr>
      <td>ETag</td>
      <td>MD5 of the object</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Last-Modified</td>
      <td>Last modified time of the object</td>
      <td>String</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Accept-Ranges</td>
      <td>Units of range. HTTP standard header.</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Range</td>
      <td>Content Range. HTTP standard header.</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Cache-Control</td>
      <td>Cache policy. HTTP standard header.</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>Content Type. HTTP standard header.</td>
      <td>String</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Content-Disposition</td>
      <td>File name. HTTP standard header.</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Encoding</td>
      <td>Encoding format. HTTP standard header.</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Language</td>
      <td>Language type. HTTP standard header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Length</td>
      <td>Object size</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Expires</td>
      <td>Cache expiration time. HTTP standard header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>x-cos-meta-*</td>
      <td>The meta information of objects customized by users must start with x-cos-meta. Otherwise it will be ignored.</td>
      <td>String</td>
   </tr>
   <tr>
      <td>x-cos-version-id</td>
      <td>The version id of objects when the version control is enabled. </td>
      <td>String</td>
   </tr>
</table>



### Setting Object Replication

#### Feature Description

This API(PUT Object - Copy) is used to copy files to the destination path.

#### Method Prototype

```
copy_object(Bucket, Key, CopySource, CopyStatus='Copy', **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-copy-object)
```python
response = client.copy_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'sourceObject', 
        'Region': 'COS_REGION', #replace with source bucket’s Region
        'VersionId': 'string'
    },
    CopyStatus='Copy'|'Replaced',
    ACL='private'|'public-read',
    GrantFullControl='string',
    GrantRead='string',
    StorageClass='STANDARD'|'STANDARD_IA',
    Expires='string',
    CacheControl='string',
    ContentType='string',
    ContentDisposition='string',
    ContentEncoding='string',
    ContentLanguage='string',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    }
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
 | key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | string | Yes | 
 |  CopySource  | Path of the object to be copied, includes Bucket、Key、Region、VersionId |  Dict | Yes |
 | XCosMetadataDirective | Available values: 'Copy' and 'Replaced'. When it is set to ‘Copy’, ignore the configured user metadata information and copy the file directly. When it is set to ‘Replaced’, modify the metadata according to the configured meta information. If the destination path is identical to the source path, it must be set to ‘Replaced’. | String | Yes |
| ACL | Sets ACL of objects, such as 'private'，'public-read' |String| No |
| GrantFullControl | Grants the grantee full permission in the format of `id="OwnerUin"` | String | No |
|GrantRead | Grants the grantee Read access in the format of `id="OwnerUin"`| String | No |
 | XCosStorageClass | Sets object storage type: STANDARD and STANDARD_IA. Default value: STANDARD | String | No |
 | Expires | Sets Expires. | String | No | 
 | CacheControl | Cache policy. Sets Cache-Control. | String | No | 
 | ContentType | Content Type. Sets Content-Type. | String | No | 
 | ContentDisposition | File name. Sets Content-Disposition. | String | No |
 | ContentEncoding | Encoding format. Sets Content-Encoding. | String | No | 
 | ContentLanguage | Language type. Sets Content-Language | String | No |
 |  Metadata | Metadata of objects customized by users. | Dict |  No | 
 

#### Returned Result
Attributes of the uploaded object. Type is dict:

```python
{
    'ETag': 'string',
    'LastModified': 'string',
    'VersionId': 'string',
    'x-cos-copy-source-version-id': 'string'
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- | 
| ETag | MD5 of the copied object | String |
| LastModified | The time when the copied file was last modified | String |
| VersionId | The version id of objects when the version control is enabled. | String  |
| x-cos-copy-source-version-id | Version ID of the source object | String | 


### Deleting a Single Object

#### Feature Description

This API (Delete Object) is used to delete the specified object.

#### Method Prototype

```
delete_object(Bucket, Key, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-delete-object)
```python
response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    VersionId='string',
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name. Format: BucketName-APPID | String | Yes | 
 | key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | String | Yes |
 | VersionId |The version id of objects when the version control is enabled. | String  | No | 

#### Returned Result
Delete the information of object. Type is dict.

```python
{
    'x-cos-version-id': 'string',
    'x-cos-delete-marker': 'true'|'false',
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- | 
| x-cos-version-id | Deletes object version ID | String |
| x-cos-delete-marker | Marks whether the deleted object is delete marker | String | 

### Deleting Multiple Objects

#### Feature Description

The API（DELETE Multiple Objects）is used to delete multiple specified objects.

#### Method Prototype

```
delete_objects(Bucket, Delete={}, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-delete-multi-object)
```python
response = client.delete_objects(
    Bucket='examplebucket-1250000000',
    Delete={
        'Object': [
            {
                'Key': 'exampleobject1',
                'VersionId': 'string'
            },
            {
                'Key': 'exampleobject2',
                'VersionId': 'string'
            },
        ],
        'Quiet': 'true'|'false'
    }
)
```

#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name. Format: BucketName-APPID | String | Yes | 
 | Delete  | Provides the way and target object of returned results for this deletion  | Dict | Yes | 
 | Objects | Provides the information of each target object to be deleted | List | Yes | 
 | key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | String | No |
 | VersionId | The version id of objects when the version control is enabled. | String  | No |
 | Quiet | Indicates the method by which the result is returned for the deletion. Available values: ‘true ‘and ‘false’. Defaults to ‘false’. If it is set to ‘true’, only error message for failed deletion is returned. If it is set to ‘false’, messages indicating successful and failed deletion are returned. | String | No |

#### Returned Result
Delete the result of object in a single request. Type is dict：
```python
{
    'Deleted': [
        {
            'Key': 'string',
            'VersionId': 'string',
            'DeleteMarker': 'true'|'false',
            'DeleteMarkerVersionId': 'string'
        },
        {
            'Key': 'string',
        },
    ],
    'Error': [
        {
            'Key': 'string',
            'VersionId': 'string',
            'Code': 'string',
            'Message': 'string'
        },
    ]
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- |
 | Deleted  |  The information of the object deleted successfully|  List |
 | Key | The path of the object deleted successfully | String |
 | VersionId     | The version ID of the object deleted successfully | String|
 | DeleteMarker     | Whether the object deleted successfully is delete marker| String|
 | DeleteMarkerVersionId | The delete maker version id of the object deleted successfully | String|
 | Error  |  The information of the object that failed to be deleted| List |
 | Key | The path of the object that failed to be deleted | string |
 | VersionId     | The version ID of the object that failed to be deleted| String|
 | Code | The error code for the object that failed to be deleted | string |
 | Message | The error message for the object that failed to be deleted | string |

## Multipart Operations
This includes the following operations:

- Multipart upload objects: Initializing multipart upload, uploading parts, and completing all multipart uploads
- Resuming the multipart upload: Querying the parts uploaded, uploading parts, and completing all multipart uploads
- Delete the part uploaded

### Querying Multipart Upload

#### Feature Description

This API (List Multipart Uploads) is used to query in-progress multipart uploads in the specified bucket.

#### Method Prototype

```
list_multipart_uploads(Bucket, Prefix="", Delimiter="", KeyMarker="", UploadIdMarker="", MaxUploads=1000, EncodingType="", **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-list-multi-upload)
```python
response = client.list_multipart_uploads(
    Bucket='examplebucket-1250000000',
    Prefix='string',
    Delimiter='string',
    KeyMarker='string',
    UploadIdMarker='string',
    MaxUploads=100,
    EncodingType='url'
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| Prefix | Filters the keys of multipart uploads by matching the multipart uploads prefixed with this parameter. It is left empty by default. | String | No | 
| Delimiter | Sets a delimiter. It is left empty by default. | String | No |
| KeyMarker | Marks the starting point of a multipart upload task. It is used with UploadIdMarker. | String | No |
| UploadIdMarker | Marks the starting point of a multipart upload task. It is used with KeyMarker. If KeyMarker is not specified, UploadIdMarker will be ignored. | String | No |
| MaxUploads | The maximum number of returned multipart uploads. It defaults to 1000. | Int | No | 
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | String | No |

#### Returned Result

The information of the multipart upload task obtained. Type is dict:

```python
{
    'Bucket': 'examplebucket-1250000000',
    'Prefix': 'string',
    'Delimiter': 'string',
    'KeyMarker': 'string',
    'UploadIdMarker': 'string',
    'NextKeyMarker': 'string',
    'NextUploadIdMarker': 'string',
    'MaxUploads': '1000',
    'IsTruncated': 'true'|'false',,
    'EncodingType': 'url',
    'Upload':[
        {
            'UploadId': 'string',
            'Key': 'string',
            'Initiated': 'string',
            'StorageClass': 'STANDARD',
            'Owner': {
                'DisplayName': 'string',
                'ID': 'string'
            },
            'Initiator': {
                'ID': 'string',
                'DisplayName': 'string'
            }
        },
    ],
    'CommonPrefixes':[
        {
            'Prefix': 'string'
        },
    ],
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | 
| Prefix | Filters the keys of multipart uploads by matching the multipart uploads prefixed with this parameter. It is left empty by default. | String |
| Delimiter | Sets a delimiter. It is left empty by default. | String |
| KeyMarker | Marks the starting point of the list of keys for multipart uploads. It is used with UploadIdMarker. | Sring |
| UploadIdMarker | Marks the starting point of the list of uploadids for multipart uploads. It is used with KeyMarker. If KeyMarker is not specified, UploadIdMarker will be ignored. | String |
| NextKeyMarker | Marks the starting point of the next list of keys for multipart uploads if IsTruncated is true. | String |
| NextUploadIDMarker | Marks the starting point of the next list of uploadids for multipart uploads if IsTruncated is true. | String |
| MaxUploads | The maximum number of returned multipart uploads. It defaults to 1000. | int |
| IsTruncated | Indicates whether the returned multipart upload is truncated | String |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | String |
| Upload | The list containing information of all multipart uploads, including UploadId, StorageClass, Key, Owner, Initiator, and Initiated. | List |
| CommonPrefixes | All keys starting with Prefix and ending with Delimiter are grouped into the same type | List |


### Initialize multipart upload

#### Feature Description

This API (Initiate Multipart Upload) is used to initialize multipart upload and obtain the corresponding uploadId.

#### Method Prototype

```
create_multipart_upload(Bucket, Key, **kwargs):
```
#### Sample Request

[//]: # (.cssg-snippet-init-multi-upload)
```python
response = client.create_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='multipart.txt',
    StorageClass='STANDARD'|'STANDARD_IA'|'ARCHIVE',
    Expires='string',
    CacheControl='string',
    ContentType='string',
    ContentDisposition='string',
    ContentEncoding='string',
    ContentLanguage='string',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    },
    ACL='private'|'public-read',
    GrantFullControl='string',
    GrantRead='string'
)
# Obtain UploadId for use by subsequent APIs
uploadid = response['UploadId']
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
 | key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | String | Yes |
 | StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No | 
 | Expires | Sets Expires. | String | No |
 | CacheControl | Cache policy. Sets Cache-Control. | String | No | 
 | ContentType | Content Type. Sets Content-Type. | String | No | 
 | ContentDisposition | File name. Sets Content-Disposition. | String | No | 
 | ContentEncoding | Encoding format. Sets Content-Encoding. | String | No | 
 | ContentLanguage | Language type. Set Content-Language | String | No |
 |  Metadata | Metadata of objects customized by users. | Dict |  No |
 | ACL | Sets ACL of object. For example 'private'，'public-read'|String| No |
| GrantFullControl | Grants the grantee full permission in the format of `id="OwnerUin"` | String | No |
| GrantRead | Grants the grantee Read access in the format of `id="OwnerUin"` | String | No |

#### Returned Result

The initialization information of the multipart upload task obtained. Type is dict:

```python
{
    'UploadId': '150219101333cecfd6718d0caea1e2738401f93aa531a4be7a2afee0f8828416f3278e5570',
    'Bucket': 'examplebucket-1250000000', 
    'Key': 'exampleobject' 
}

```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- |
| UploadId | Indicate the ID of multipart upload. | String |
| Bucket | Bucket name. Format: BucketName-APPID | String |
| Key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | string |

### Upload Parts

This API (Upload Part) is used to upload a part.

#### Method Prototype

```
upload_part(Bucket, Key, Body, PartNumber, UploadId, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-upload-part)
```python
# Note: The maximum number of parts to be uploaded is 10,000.
response = client.upload_part(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Body=b'bytes'|file,
    PartNumber=1,
    UploadId='string',
    EnableMD5=False|True,
    ContentLength='123',
    ContentMD5='string'
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
 | key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | String | Yes |
 | Body  | The body of uploaded objects can be local filestream or inputstream.| file/bytes |  Yes|
 | PartNumber | Indicates the number of the uploaded part | int | Yes |
 | UploadId | Indicates the ID of multipart upload | string | Yes |
 | EnableMD5 | Whether SDK is used to calculate Content-MD5, which is off by default. When it is turned on, the uploading time will increase.|Bool | No | 
 | ContentLength | Sets transmission length | string | No |
 | ContentMD5 | Sets MD5 of the uploaded object for verification | String | No |
 
#### Returned Result

Attributes of the uploaded part. Type is dict:

```python
{
    'ETag': 'string'
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- | 
| ETag | MD5 of the uploaded part | String |

### Copy Parts

Copy other objects as an upload part.

#### Method Prototype

```
upload_part_copy(Bucket, Key, PartNumber, UploadId, CopySource, CopySourceRange='', **kwargs)
```

#### Sample Request

[//]: # (.cssg-snippet-upload-part-copy)
```python
response = client.upload_part_copy(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    PartNumber=100,
    UploadId='string',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'sourceObject', 
        'Region': 'COS_REGION', #replace with source bucket’s Region
        'VersionId': 'string'
    },
    CopySourceRange='string',
    CopySourceIfMatch='string',
    CopySourceIfModifiedSince='string',
    CopySourceIfNoneMatch='string',
    CopySourceIfUnmodifiedSince='string'
)
```

#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | string | Yes |
| PartNumber | Indicates the index of the part uploaded | int | Yes |
| UploadId | Indicates the ID of multipart upload | string | Yes |
|  CopySource  | Path of the object to be copied, includes Bucket、Key、Region、VersionId |  Dict | Yes |
|CopySourceRange| Describes the range of the source in the format of bytes=first-last. The entire source will be copied by default if the range is not specified.|String| No |
|CopySourceIfMatch| Copies source only if the Etag of source object is the same as the specified values|String| No |
|CopySourceIfModifiedSince| Copies source only if source object is modified after the specified time. |String| No |
|CopySourceIfNoneMatch| Copies source only if the Etag of source object is different from the specified value. |String| No |
|CopySourceIfUnmodifiedSince| Copies source only if source object is not modified after the specified time.|String| No |

#### Returned Result

Attributes of the uploaded part. Type is dict:
```python
{
    'ETag': 'string',
    'LastModified': 'string',
    'x-cos-copy-source-version-id': 'string',
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- | 
| ETag | MD5 of the copied file | string |
| LastModified | The time when the copied file was last modified | string |
| x-cos-copy-source-version-id | Version ID of the source object | String | 

### Query Uploaded Parts

#### Feature Description

This API (List Parts) is used to query the uploaded parts in a specific multipart upload process.

#### Method Prototype

```
list_parts(Bucket, Key, UploadId, MaxParts=1000, PartNumberMarker=0, EncodingType='', **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-list-parts)
```python
response = client.list_parts(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId='exampleUploadId',
    MaxParts=1000,
    PartNumberMarker=100,
    EncodingType='url'
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | string | Yes |
| UploadId | Indicates the ID of multipart upload. | String | Yes |
| MaxParts | The maximum number of returned parts. Default is 1,000. | Int | No |
| PartNumberMarker | Indicates that the parts are listed from the one following PartNumberMarker. It defaults to 0, which means the parts are listed from the first one. | int | No |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | String | No |

#### Returned Result

Information of all uploaded parts. Type is dict:

```python
{
    'Bucket': 'examplebucket-1250000000', 
    'Key': 'exampleobject', 
    'UploadId': '1502192444bdb382add546a35b2eeab81e06ed84086ca0bb75ea45ca7fa073fa9cf74ec4f2', 
    'EncodingType': None, 
    'MaxParts': '1000',
    'IsTruncated': 'true',
    'PartNumberMarker': '0', 
    'NextPartNumberMarker': '1000', 
    'StorageClass': 'Standard',
    'Part': [
        {
            'LastModified': '2017-08-08T11:40:48.000Z',
            'PartNumber': '1',
            'ETag': '"8b8378787c0925f42ccb829f6cc2fb97"',
            'Size': '10485760'
        },
    ], 
    'Initiator': {
        'DisplayName': '3333333333', 
        'ID': 'qcs::cam::uin/3333333333:uin/3333333333'
    }, 
    'Owner': {
        'DisplayName': '124564654654',
        'ID': '124564654654'
    }
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- | 
| Bucket | Bucket name. Format: BucketName-APPID | String |
| Key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | string | 
| UploadId | Indicates the ID of multipart upload | String | 
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | String |
| MaxParts | The maximum number of returned parts. It defaults to 1000. | String |
| IsTruncated | Indicates whether the returned part is truncated | String |
| PartNumberMarker | Indicates that the parts are listed from the one following PartNumberMarker. It defaults to 0, which means the parts are listed from the first one. | String |
| NextPartNumberMarker | Marks the starting point of the next list of parts | String |
 | StorageClass | Sets the object storage class; Available values: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD | String |
| Part | Information of the uploaded part, including ETag, PartNumber, Size, LastModified | String |
 | Initiator | Creator of the multipart upload, including DisplayName, and ID | Dict | 
 | Owner | Information of the object owner, including DisplayName and ID | Dict | 



### Complet Multipart Upload

#### Feature Description

This API (Complete Multipart Upload) is used to complete the entire multipart upload.

#### Method Prototype

```
complete_multipart_upload(Bucket, Key, UploadId, MultipartUpload={}, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-complete-multi-upload)
```python
response = client.complete_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId='exampleUploadId',
    MultipartUpload={
        'Part': [
            {
                'ETag': 'string',
                'PartNumber': 1
            },
            {
                'ETag': 'string',
                'PartNumber': 2
            },
        ]
    },
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes | 
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | String | Yes | 
| UploadId | Indicates the ID of multipart upload | String | Yes | 
| MultipartUpload | ETag and PartNumber information for all parts. | Dict | 

#### Returned Result

Information about the constructed file. Type is dict:

```python
{
    'ETag': '"3f866d0050f044750423e0a4104fa8cf-2"', 
    'Bucket': 'examplebucket-1250000000', 
    'Location': 'examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject', 
    'Key': 'exampleobject'
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- | 
 | ETag | The unique tag of the resulting object. It is not the MD5 check value for the object content, but is only used to check the uniqueness of the object. To verify the object content, you can check the ETag of each part during the process of upload. | string | 
 | Bucket | Bucket name. Format: BucketName-APPID | String | 
 | Location | URL address | String | 
 | Key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | String |


### Terminate Multipart Upload

#### Feature Description

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts.

#### Method Prototype

```
abort_multipart_upload(Bucket, Key, UploadId, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-abort-multi-upload)
```python
response = client.abort_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId='exampleUploadId'
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | string | Yes |
| UploadId | Indicates the ID of multipart upload. | String | Yes |

#### Returned Result
The returned value for this method is None.

## Other Operations

### Restoring an Archived Object 

#### Feature Description

This API (POST Object restore) is used to restore an archived object.

#### Method Prototype

```
restore_object(Bucket, Key, RestoreRequest={}, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-restore-object)
```python
response = client.restore_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    RestoreRequest={
        'Days': 100,
        'CASJobParameters': {
            'Tier': 'Expedited'|'Standard'|'Bulk'
        }
    }
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | string | Yes |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | string | Yes |
|RestoreRequest| Describes the rules of restoring the temporary object| Dict| Yes |
|Days| Describes the expiration time of the temporary object. | Int| Yes |
|CASJobParameters| Describes the configuration information of restoration type| Dict| No |
|Tier| Describes the mode of getting the temporary object. Options are 'Expedited'(fast mode)，Standard'(standard mode)，and 'Bulk'(slow mode). | String| No |

#### Returned Result
The returned value for this method is None.


### Setting Object ACL

#### Feature Description

The API(Put object acl) is used to set some object ACL in a bucket. The parameters of AccessControlPolicy and other permissions are mutually exclusive and they cannot be specified at the same time.

#### Method Prototype

```
put_object_acl(Bucket, Key, AccessControlPolicy={}, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-put-object-acl)
```python
response = client.put_object_acl(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    ACL='private'|'public-read',
    GrantFullControl='string',
    GrantRead='string',
    AccessControlPolicy={
        'AccessControlList': {
            'Grant': [
                {
                    'Grantee': {
                        'DisplayName': 'string',
                        'Type': 'CanonicalUser'|'Group',
                        'ID': 'string',
                        'URI': 'string'
                    },
                    'Permission': 'FULL_CONTROL'|'WRITE'|'READ'
                },
            ]
        },
        'Owner': {
            'DisplayName': 'string',
            'ID': 'string'
        }
    }
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | string | Yes | 
| ACL | Sets ACL of object. For example 'private'，'public-read'|String| No | 
| GrantFullControl | Grants the grantee full permission in the format of `id="OwnerUin"` | String | No |
|GrantRead |Grants the grantee Read access in the format of `id="OwnerUin"` | String | No |
| AccessControlPolicy   | Grants the grantee access permission, For the format, please see the Returned result of GET Object acl | Dict  | No  | 


#### Returned Result

The returned value for this method is None.

### Querying Object ACL

#### Feature Description

The API(GET Object acl) is used to get object acl.

#### Method Prototype

```
get_object_acl(Bucket, Key, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-get-object-acl)
```python
response = client.get_object_acl(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | string | Yes |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`中，the ObjectKey is doc/pic.jpgg. | String | Yes |


#### Returned Result

Bucket ACL information. Type is dict.
```python
{
    'Owner': {
        'DisplayName': 'string',
        'ID': 'string'
    },
    'Grant': [
        {
            'Grantee': {
                'DisplayName': 'string',
                'Type': 'CanonicalUser'|'Group',
                'ID': 'string',
                'URI': 'string'
            },
            'Permission': 'FULL_CONTROL'|'WRITE'|'READ'
        },
    ]
}
```

| Parameter Name | Description | Type |
| -------------- | -------------- |---------- | 
 | Owner | Information of the object owner, including DisplayName and ID | Dict | 
 | Grant | Information of a user granted the object permissions, including Grantee and Permission | List | 
 | Grantee | Information of grantee, including DisplayName, Type, ID and URI | Dict | 
 | DisplayName | Name of grantee | string |
 | Type | Type of grantee: CanonicalUser or Group | string |
 | ID | ID of grantee when Type is CanonicalUser | string | 
 | URI | URI of grantee when Type is Group | String | 
 | Permission | Object permissions of grantee. Available values: FULL_CONTROL (read and write permissions), WRITE (write permission), and READ (read permission) | string |


 ## Advanced APIs (Recommended)

### Uploading Objects (Checkpoint Restart)

#### Feature Description
This API for file upload selects easy upload or multi-part upload according to the file length. Easy upload is used for files smaller than or equal to 20 MB. Multi-part upload is used for files larger than 20 MB. If the upload of a part is not completed, you can resume the upload from the breakpoint.

#### Method Prototype

```
upload_file(Bucket, Key, LocalFilePath, PartSize=1, MAXThread=5, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-transfer-upload-object)
```python
response = client.upload_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    LocalFilePath='local.txt',
    EnableMD5=False
)
```

#### Request Example for All Parameters
```python
response = client.upload_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    LocalFilePath='local.txt',
    PartSize=1,
    MAXThread=5,
    EnableMD5=False|True,
    ACL='private'|'public-read', # Please use this parameter carefully, or the maximum of 1000 ACLs will be reached.
    GrantFullControl='string',
    GrantRead='string',
    StorageClass='STANDARD'|'STANDARD_IA'|'ARCHIVE',
    Expires='string',
    CacheControl='string',
    ContentType='string',
    ContentDisposition='string',
    ContentEncoding='string',
    ContentLanguage='string',
    ContentLength='123',
    ContentMD5='string',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    }
)
```
#### Parameter Description


| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
 | key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`，the ObjectKey is doc/pic.jpg | String | Yes | 
|  LocalFilePath  | File Path of Local File |  String | Yes |
|  PartSize  | Size of part uploaded. Default value:1MB |  Int |  No |
|  MAXThread  | MAXThread of parts uploaded parallelly. Default value: 5 MAXThread parts |  Int |  No |
| EnableMD5 | Whether SDK is used to calculate Content-MD5, which is off by default. When it is turned on, the uploading time will increase. | Bool | No | 
| ACL | Sets ACL of object. For example 'private'，'public-read'|String| No |
| GrantFullControl | Grants the grantee full permission in the format of `id="OwnerUin"` | String | No |
| GrantRead | Grants the grantee Read access in the format of `id="OwnerUin"` | String | No |
 | StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
 | Expires | Sets Expires. | String | No | 
 | CacheControl | Cache policy. Sets Cache-Control. | String | No |
 | ContentType | Content Type. Sets Content-Type. | String | No |  
 | ContentDisposition | File name. Sets Content-Disposition. | String | No |
 | ContentEncoding | Encoding format. Sets Content-Encoding. | String | No |
 | ContentLanguage | Language type. Sets Content-Language | String | No |
 | ContentLength | Sets transmission length | string | No | 
 | ContentMD5 | Sets MD5 of the uploaded object for verification | String | No | 
 |  Metadata | Metadata of objects customized by users. | Dict |  No |

#### Returned Result
Attributes of the uploaded object. Type is dict:

```python
{
    'ETag': 'string'
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- |
| ETag | MD5 of the upload Object | String |
