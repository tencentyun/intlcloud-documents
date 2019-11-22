## Overview

This document provides an overview of APIs related to simple object operations, multipart upload, and other operations and corresponding SDK sample code.

**Simple operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/30614) | Querying object list 	| Queries some or all objects in a bucket |
[GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying object and historical version list | Queries some or all objects in a bucket and their historical version information |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Simply uploading an object | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) |	 Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies an object to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes the specified object in a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes specified objects in a bucket in batches |

**Multipart upload operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload |	 Initializes a multipart upload task |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads file parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Retrieves an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of the specified object in a bucket |

## Simple Operations

### Querying Object List

#### Feature Description

This API is used to query some or all objects in a bucket.

#### Method Prototype

```
list_objects(Bucket, Delimiter="", Marker="", MaxKeys=1000, Prefix="", EncodingType="", **kwargs)
```
#### Sample Request

```python
response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='string'
)
```

#### Request Example with All Parameters

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
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes | 
| Prefix | Filters object keys to match the objects with the specified prefix. This parameter is blank by default | String | No | 
| Delimiter | Sets the delimiter; for example, set `/` to simulate a folder. This parameter is blank by default | String | No |
| Marker | Marks the starting position of the list of returned objects. By default, entries are listed in UTF-8 binary order  | String | No | 
| MaxKeys | Maximum number of returned objects; default and maximum value: 1,000 | Int | No | 
| EncodingType | Specifies the encoding method of the return value; value range: url; no encoding is performed by default | String | No |

#### Return Result Descriptions

Object metadata in dict type.

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
| MaxKeys | Maximum number of returned objects; default and maximum value: 1,000 | String |
| Prefix | Matches the objects with the specified prefix. This parameter is blank by default | String |
| Delimiter | Sets the delimiter; for example, set `/` to simulate a folder. This parameter is blank by default | String |
| Marker | Marks the starting position of the list of returned objects. By default, entries are listed in UTF-8 binary order  | String |
| NextMarker | String | Marks the starting position of the list of objects returned next time if IsTruncated is true | None |
| Name | Bucket name in the format of BucketName-APPID | String | 
| IsTruncated | Indicates whether the returned objects are truncated | String |
| EncodingType | Specifies the encoding method of the return value; value range: url; no encoding is performed by default | String | No |
| Contents | List of metadata of all objects, including information such as 'ETag', 'StorageClass', 'Key', 'Owner', 'LastModified', and 'Size' | List |
|CommonPrefixes | Array | All objects starting with Prefix and ending in Delimiter are grouped into the same class | List |

### Querying Object and Historical Version List 

#### Feature Description

This API is used to query some or all objects in a bucket and their historical version information.

#### Method Prototype

```
list_objects_versions(Bucket, Prefix="", Delimiter="", KeyMarker="", VersionIdMarker="", MaxKeys=1000, EncodingType="", **kwargs)
```
#### Sample Request

```python
response = client.list_objects_versions(
    Bucket='examplebucket-1250000000',
    Prefix='string'
)
```

#### Request Example with All Parameters

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
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes | 
| Prefix | Filters object keys to match the objects with the specified prefix. This parameter is blank by default | String | No | 
| Delimiter | Sets the delimiter; for example, set `/` to simulate a folder. This parameter is blank by default | String | No |
| KeyMarker | Marks the starting position of the key in the list of returned objects. By default, entries are listed in UTF-8 binary order  | String | No |
| VersionIdMarker| String | Marks the starting position of the VersionId in the list of returned objects. By default, entries are listed in UTF-8 binary order  | String  |  No |
| MaxKeys | Maximum number of returned objects; default and maximum value: 1,000 | Int | No | 
| EncodingType | Specifies the encoding method of the return value; value range: url; no encoding is performed by default | String | No |

#### Return Result Descriptions

Object metadata in dict type.

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
| MaxKeys | Maximum number of returned objects; default and maximum value: 1,000 | String |
| Prefix | Matches the objects with the specified prefix. This parameter is blank by default | String |
| Delimiter | Sets the delimiter; for example, set `/` to simulate a folder. This parameter is blank by default | String |
| KeyMarker | Marks the starting position of the key in the list of returned objects. By default, entries are listed in UTF-8 binary order  | String |
| VersionIdMarker| String | Marks the starting position of the VersionId in the list of returned objects. By default, entries are listed in UTF-8 binary order  | String  |
| NextMarker | String | Marks the starting position of the key in the list of objects returned next time if IsTruncated is true | String |
| NextVersionIdMarker | Marks the starting position of the VersionId in the list of objects returned next time if IsTruncated is true | String |
| Name | Bucket name in the format of BucketName-APPID | String | 
| IsTruncated | Indicates whether the returned objects are truncated | String |
| EncodingType | Specifies the encoding method of the return value; value range: url; no encoding is performed by default | String | No |
| Version | List of metadata of all multi-version objects, including information such as 'ETag', 'StorageClass', 'Key', 'VersionId', 'IsLatest', 'Owner', 'LastModified', and 'Size' | List |
|DeleteMarker| List of metadata of all objects with a delete marker, including information such as 'Key', 'VersionId', 'IsLatest', 'Owner', and 'LastModified'  | List |
|CommonPrefixes | Array | All objects starting with Prefix and ending in Delimiter are grouped into the same class | List |

### Simply Uploading an Object

#### Feature Description

This API (PUT Object) is used to upload an object to a bucket.

#### Method Prototype

```
put_object(Bucket, Body, Key, **kwargs)
```
#### Sample Request

```python
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes'|file,
    Key='exampleobject',
    EnableMD5=False
)
```
#### Request Example with All Parameters
```python
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes'|file,
    Key='exampleobject',
    EnableMD5=False|True,
    ACL='private'|'public-read',  # Please use this parameter with caution; otherwise, the upper limit of 1,000 ACL entries will be reached
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
#### Parameter Descriptions


| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
 | Body  | Content of an uploaded object, which can be a file stream or byte stream | file/bytes | Yes |
 | Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes | 
| EnableMD5 | Whether the SDK is required to calculate the Content-MD5. This is disabled by default, and enabling this will increase the upload time | Bool | No | 
| ACL | Sets the object ACL such as 'private' and 'public-read' | String | No |
| GrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | String | No |
| GrantRead | Grants the grantee read permission in the format of id="[OwnerUin]" | String | No |
 | StorageClass | Sets the object storage class; value range: STANDARD, STANDARD_IA, ARCHIVE; default value: STANDARD | String | No |
 | Expires | Sets Expires | String | No | 
 | CacheControl | Cache policy, which sets Cache-Control | String | No |
 | ContentType | Content type, which sets Content-Type | String | No |  
 | ContentDisposition | Object name, which sets Content-Disposition | String | No |
 | ContentEncoding | Encoding format, which sets Content-Encoding | String | No |
 | ContentLanguage | Language type, which sets Content-Language | String | No |
 | ContentLength | Sets transfer length | String | No | 
 | ContentMD5 | Sets the MD5 value of the uploaded object for verification | String | No | 
 |  Metadata | User-defined object metadata, which must start with x-cos-meta; otherwise, it will be ignored | Dict | No |

#### Return Result Descriptions
Attributes of the uploaded object in dict type:

```python
{
    'ETag': 'string',
    'x-cos-version-id': 'string'
}
```


| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- |
| ETag | MD5 value of the uploaded object | String |
|  x-cos-version-id | Object version number after versioning is enabled | String |



### Querying Object Metadata

#### Feature Description

This API (HEAD Object) is used to query object metadata.

#### Method Prototype

```
head_object(Bucket, Key, **kwargs)
```
#### Sample Request

```python
response = client.head_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    VersionId='string',
    IfModifiedSince='string',
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
  | Bucket | Bucket name in the format of BucketName-APPID | String | Yes | 
  | Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
  | VersionId | Specifies an object version if versioning is enabled | String | No | 
  | IfModifiedSince | Returned only if modified after the specified time | String | No | 

#### Return Result Descriptions

Object metadata in dict type.

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
 | ETag | MD5 value of the object | String |
 | Last-Modified | Last modified time of the object | String |
 | Cache-Control | Cache policy, which is a standard HTTP header | String |
 | Content-Type | Content Type, which is a standard HTTP header | String |
 | Content-Disposition | Filename, which is a standard HTTP header | String |
 | ContentEncoding | Encoding format, which is a standard HTTP header | String |
 | Content-Language | Language type, which is a standard HTTP header | String |
 | Content-Length | Object size | String |
 | Expires | Cache expiration time, which is a standard HTTP header | String |
 |  x-cos-meta-* | User-defined object metadata, which must start with x-cos-meta; otherwise, it will be ignored | String | 
 |  x-cos-version-id | Object version number after versioning is enabled | String | 


### Downloading an Object

#### Feature Description

This API (GET Object) is used to download an object to the local file system.

#### Method Prototype

```
 get_object(Bucket, Key, **kwargs)
```
#### Sample Request

```python
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Range='string',
    IfMatch='string',
    IfModifiedSince='string',
    IfNoneMatch='string',
    IfUnmodifiedSince='string',
    ResponseCacheControl='string',
    ResponseContentDisposition='string',
    ResponseContentEncoding='string',
    ResponseContentLanguage='string',
    ResponseContentType='string',
    ResponseExpires='string',
    VersionId='string'
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format of BucketName-APPID | String | Yes | 
 | Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes | 
 | Range | Sets the range of object download in the format of bytes=first-last | String | No | 
 | IfMatch | Returned only if ETag matches the specified content | String | No |  
 | IfModifiedSince | Returned only if modified after the specified time | String | No |
 | IfNoneMatch | Returned only if ETag does not match the specified content | String | No | 
 | IfModifiedSince | Returned only if the object is modified before or at the specified time | String | No |
 | ResponseCacheControl | Sets the response header Cache-Control | String | No | 
 | ResponseContentDisposition | Sets the response header Content-Disposition  | String | No | 
 | ResponseContentEncoding | Sets the response header Content-Encoding | String | No |
 | ResponseContentLanguage | Sets the response header Content-Language  | String | No | 
 | ResponseContentType | Sets the response header Content-Type | String | No |
 | ResponseExpires | Sets the response header Expires | String |  No | 
 | VersionId | Specifies the downloaded object version | String | No | 

#### Return Result Descriptions

Body and metadata of the download object in dict type:

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
      <th>Parameter Name</th>
      <th>Description</th>
      <th>Type</th>
   </tr>
   <tr>
      <td>Body</td>
      <td>Content of the downloaded object. The get_raw_stream method can get a file stream, while the get_stream_to_file method can download the object content to the specified local file</td>
      <td>StreamBody</td>
   </tr>
   <tr>
      <td>ETag</td>
      <td>MD5 value of the object</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Last-Modified</td>
      <td>Last modified time of the object</td>
      <td>String</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Accept-Ranges</td>
      <td>Range unit, which is a standard HTTP header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Range</td>
      <td>Content range, which is a standard HTTP header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Cache-Control</td>
      <td>Cache policy, which is a standard HTTP header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>Content type, which is a standard HTTP header</td>
      <td>String</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Content-Disposition</td>
      <td>Filename, which is a standard HTTP header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Encoding</td>
      <td>Encoding format, which is a standard HTTP header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Language</td>
      <td>Language type, which is a standard HTTP header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Length</td>
      <td>Object size</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Expires</td>
      <td>Cache expiration time, which is a standard HTTP header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>x-cos-meta-*</td>
      <td>User-defined object metadata, which must start with x-cos-meta; otherwise, it will be ignored</td>
      <td>String</td>
   </tr>
   <tr>
      <td>x-cos-version-id</td>
      <td>Object version number after versioning is enabled</td>
      <td>String</td>
   </tr>
</table>



### Setting Object Replication

#### Feature Description

This API (PUT Object - Copy) is used to copy a file to the destination path.

#### Method Prototype

```
copy_object(Bucket, Key, CopySource, CopyStatus='Copy', **kwargs)
```
#### Sample Request

```python
response = client.copy_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    CopySource={
        'Bucket': 'examplebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou',
        'VesionId': 'string'
    },
    CopyStatus='Copy'|'Replaced',
    ACL='private'|'public-read',
    GrantFullControl='string',
    GrantRead='string',
    StorageClass='STANDARD'|'STANDARD_IA',
    Expires='string'
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
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
 | Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes | 
 | CopySource | String | Describes the path to the source object to be copied, including Bucket, Key, Region, and VersionId | Dict | Yes |
 | CopyStatus | Value range: 'Copy', 'Replaced'. If this parameter is set to 'Copy', the configured user metadata is ignored and the copy is performed directly; if 'Replaced', the metadata is modified based on the configured metadata. If the destination path is the same as the source path, this parameter has to be set to Replaced | String | Yes |
| ACL | Sets the object ACL such as 'private' and 'public-read' | String | No |
| GrantFullControl | Grants the specified account full permission to the object in the format of `id="[OwnerUin]"` | String | No |
|GrantRead | Grants the specified account read permission to the object in the format of `id="[OwnerUin]"` | String | No |
 | StorageClass | Sets the object storage class; value range: STANDARD, STANDARD_IA; default value: STANDARD | String | No |
 | Expires | Sets Expires | String | No | 
 | CacheControl | Cache policy, which sets Cache-Control | String | No | 
 | ContentType | Content type, which sets Content-Type | String | No | 
 | ContentDisposition | Filename, which sets Content-Disposition | String | No |
 | ContentEncoding | Encoding format, which sets Content-Encoding | String | No | 
 | ContentLanguage | Language type, which sets Content-Language | String | No |
 |  Metadata | User-defined object metadata | Dict | No | 
 

#### Return Result Descriptions
Attributes of the uploaded object in dict type:

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
| ETag | MD5 value of the copied object | String |
| LastModified | Last modified time of the copied object | String |
|  VersionId | Destination object version number after versioning is enabled | String |
| x-cos-copy-source-version-id | Source object version number | String | 


### Deleting a Single Object

#### Feature Description

This API (DELETE Object) is used to delete the specified object.

#### Method Prototype

```
delete_object(Bucket, Key, **kwargs)
```
#### Sample Request

```python
response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    VersionId='string',
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format of BucketName-APPID | String | Yes | 
 | Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
 | VersionId | Specifies an object version if versioning is enabled | String | No | 

#### Return Result Descriptions
Information of the deleted object in dict type.

```python
{
    'x-cos-version-id': 'string',
    'x-cos-delete-marker': 'true'|'false',
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- | 
|  x-cos-version-id | Deleted object version number | String |
| x-cos-delete-marker | Identifies whether the deleted object is the delete marker | String | 

### Deleting Multiple Objects

#### Feature Description

This API (DELETE Multiple Objects) is used to delete multiple specified objects.

#### Method Prototype

```
delete_objects(Bucket, Delete={}, **kwargs)
```
#### Sample Request

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

#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format of BucketName-APPID | String | Yes | 
 | Delete | Indicates the return result mode and target objects of this deletion | Dict | Yes | 
 | Object  | Describes the information of each target object to be deleted | List | Yes | 
 | Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | No |
 |  VersionId | Destination object version number after versioning is enabled | String |
 | Quiet | Specifies the return result mode of the deletion. Value range: 'true', 'false'; default value: 'false'. If this is set to 'true', only the error information of failures will be returned; if 'false', all information of successes and failures will be returned | String | No |

#### Return Result Descriptions
Result of batch deletion of objects in dict type:
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
 | Deleted  | Information of the successfully deleted object |  List |
 | Key | Path to the successfully deleted object | string |
 | VersionId | Version number of the successfully deleted object | String |
 | DeleteMarker  | Whether the successfully deleted object is the delete marker | String |
 | DeleteMarkerVersionId | Version number of the delete marker of the successfully deleted object | String |
 | Error | Information of the object that failed to be deleted | List |
 | Key | Path to the object that failed to be deleted | string |
 | VersionId | Version number of the object that failed to be deleted | String |
 | Code | Error code corresponding to the object that failed to be deleted | String |
 | Message | Error message corresponding to the object that failed to be deleted | String |

## Multipart Upload Operations
With multipart upload, you can do the following:

- Upload an object in parts, including initializing a multipart upload, uploading parts, and completing the upload of all parts.
- Resume a multipart upload, including querying uploaded parts, uploading parts, and completing the upload of all parts.
- Delete uploaded parts.

### Querying a Multipart Upload

#### Feature Description

This API (List Multipart Uploads) is used to query multipart uploads in progress in the specified bucket.

#### Method Prototype

```
list_multipart_uploads(Bucket, Prefix="", Delimiter="", KeyMarker="", UploadIdMarker="", MaxUploads=1000, EncodingType="", **kwargs)
```
#### Sample Request

```python
response = client.list_multipart_uploads(
    Bucket='examplebucket-1250000000',
    Prefix='string',
    Delimiter='string',
    KeyMarker='string',
    UploadIdMarker='string'
    MaxUploads=100,
    EncodingType='url'
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
| Prefix | Filters multipart upload keys to match the multipart uploads with the specified prefix. This parameter is blank by default | String | No | 
| Delimiter | Sets the delimiter. This parameter is blank by default | String | No |
| KeyMarker | Used with UploadIdMarker to indicate the starting position of the multipart upload | String | No |
| UploadIdMarker | Used with KeyMarker to indicate the starting position of the multipart upload. If KeyMarker is not specified, UploadIdMarker will be ignored | String | No |
| MaxUploads | Maximum number of returned multipart uploads; default and maximum value: 1,000 | Int | No | 
| EncodingType | Specifies the encoding method of the return value; value range: url; no encoding is performed by default | String | No |

#### Return Result Descriptions

Information of multipart uploads obtained in dict type:

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
| Bucket | Bucket name in the format of BucketName-APPID | String | 
| Prefix | Filters multipart upload keys to match the multipart uploads with the specified prefix. This parameter is blank by default | String |
| Delimiter | Sets the delimiter. This parameter is blank by default | String |
| KeyMarker | Used with UploadIdMarker to indicate the starting key position of the multipart upload | String |
| UploadIdMarker | Used with KeyMarker to indicate the starting uploadid position of the multipart upload. If KeyMarker is not specified, UploadIdMarker will be ignored | String |
| NextKeyMarker | Indicates the starting key position of the next multipart upload if IsTruncated is true | String |
| NextUploadIdMarker | Indicates the starting uploadid position of the next multipart upload if IsTruncated is true | String |
| MaxUploads | Maximum number of returned multipart uploads; default and maximum value: 1,000 | Int |
| IsTruncated | Indicates whether the returned multipart uploads are truncated | String |
| EncodingType | Specifies the encoding method of the return value; value range: url; no encoding is performed by default | String |
|Upload | List of all multipart uploads, including information such as 'UploadId', 'StorageClass', 'Key', 'Owner', 'Initiator', and 'Initiated'  | List |
|CommonPrefixes | Array | All keys starting with Prefix and ending in Delimiter are grouped into the same class | List |


### Initializing a Multipart Upload

#### Feature Description

This API (Initiate Multipart Upload) is used to initialize a multipart upload and get the corresponding uploadId.

#### Method Prototype

```
create_multipart_upload(Bucket, Key, **kwargs):
```
#### Sample Request

```python
response = client.create_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='multipart.txt',
    StorageClass='STANDARD'|'STANDARD_IA'|'ARCHIVE',
    Expires='string'
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
# Get UploadId for use by subsequent APIs
uploadid = response['UploadId']
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
 | Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
 | StorageClass | Sets the object storage class; value range: STANDARD, STANDARD_IA, ARCHIVE; default value: STANDARD | String | No | 
 | Expires | Sets Expires | String | No |
 | CacheControl | Cache policy, which sets Cache-Control | String | No | 
 | ContentType | Content type, which sets Content-Type | String | No | 
 | ContentDisposition | Filename, which sets Content-Disposition | String | No | 
 | ContentEncoding | Encoding format, which sets Content-Encoding | String | No | 
 | ContentLanguage | Language type, which sets Content-Language | String | No |
 |  Metadata | User-defined object metadata | Dict | No |
 | ACL | Sets the object ACL such as 'private' and 'public-read' | String | No |
| GrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | String | No |
| GrantRead | Grants the grantee read permission in the format of id="[OwnerUin]" | String | No |

#### Return Result Descriptions

Initialization information of multipart uploads obtained in dict type:

```python
{
    'UploadId': '150219101333cecfd6718d0caea1e2738401f93aa531a4be7a2afee0f8828416f3278e5570',
    'Bucket': 'examplebucket-1250000000', 
    'Key': 'exampleobject' 
}

```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- |
|UploadId | Identifies the ID of the multipart upload | String |
| Bucket | Bucket name in the format of BucketName-APPID | String |
|Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String |

### Uploading Parts

This API (Upload Part) is used to upload an object in parts.

#### Method Prototype

```
upload_part(Bucket, Key, Body, PartNumber, UploadId, **kwargs)
```
#### Sample Request

```python
# Note that the number of parts in a multipart upload cannot exceed 10,000
response = client.upload_part(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Body=b'bytes'|file,
    PartNumber=1,
    UploadId='string',
    EnableMD5=False|True,
    ContentLength=123,
    ContentMD5='string'
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
 | Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
 | Body  | Content of an uploaded part, which can be a local file or input stream | file/bytes | Yes |
 | PartNumber | Uploaded part number | Int | Yes |
 | UploadId | Identifies the ID of the multipart upload | String | Yes |
 | EnableMD5 | Whether the SDK is required to calculate the Content-MD5. This is disabled by default, and enabling this will increase the upload time | Bool | No | 
 | ContentLength | Sets transfer length | Int | No |
 | ContentMD5 | Sets the MD5 value of the uploaded object for verification | String | No |
 
#### Return Result Descriptions

Attributes of the uploaded part in dict type:

```python
{
    'ETag': 'string'
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- | 
| ETag | MD5 value of the uploaded part | String |

### Copying Parts

This API (Upload Part - Copy) is used to copy an object as a part.

#### Method Prototype

```
upload_part_copy(Bucket, Key, PartNumber, UploadId, CopySource, CopySourceRange='', **kwargs)
```

#### Sample Request

```python
response = client.upload_part_copy(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    PartNumber=100,
    UploadId='string',
    CopySource={
        'Bucket': 'examplebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou',
        'VersionId': 'string'
    },
    CopySourceRange='string',
    CopySourceIfMatch='string',
    CopySourceIfModifiedSince='string',
    CopySourceIfNoneMatch='string',
    CopySourceIfUnmodifiedSince='string'
)
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
| PartNumber | Uploaded part number | Int | Yes |
| UploadId | Identifies the ID of the multipart upload | String | Yes |
| CopySource | String | Describes the path to the source object to be copied, including Bucket, Key, Region, and VersionId | Dict | Yes |
| CopySourceRange | Describes the scope of source object copying in the format of bytes=first-last. If this parameter is not specified, the entire source object will be copied by default | String | No |
| CopySourceIfMatch | Copied only if the Etag of the source object is the same as the specified value | String | No |
| CopySourceIfModifiedSince | Copied only if the source object is modified after the specified time | String | No |
|CopySourceIfNoneMatch | Copied only if the Etag of the source object is different from the specified value | String | No |
| CopySourceIfUnmodifiedSince | Copied only if the source object is not modified after the specified time | String | No |

#### Return Result Descriptions

Attributes of the copied part in dict type:
```python
{
    'ETag': 'string',
    'LastModified': 'string',
    'x-cos-copy-source-version-id': 'string',
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- | 
| ETag | MD5 value of the copied part | String |
| LastModified | Last modified time of the copied part | String |
| x-cos-copy-source-version-id | Source object version number | String | 

### Querying Uploaded Parts

#### Feature Description

This API (List Parts) is used to query uploaded parts in the specified multipart upload operation.

#### Method Prototype

```
list_parts(Bucket, Key, UploadId, MaxParts=1000, PartNumberMarker=0, EncodingType='', **kwargs)
```
#### Sample Request

```python
response = client.list_parts(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId=uploadid,
    MaxParts=1000,
    PartNumberMarker=100,
    EncodingType='url'
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
|Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
|UploadId | Identifies the ID of the multipart upload | String | Yes |
|MaxParts | Maximum number of returned parts; default and maximum value: 1,000 | Int | No |
|PartNumberMarker | The part list starts from PartNumberMarker, which is 0 by default, i.e., listing parts from the first one | Int | No |
| EncodingType | Specifies the encoding method of the return value; value range: url; no encoding is performed by default | String | No |

#### Return Result Descriptions

Information of all uploaded parts in dict type:

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
| Bucket | Bucket name in the format of BucketName-APPID | String |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | 
| UploadId | Identifies the ID of the multipart upload | String | 
| EncodingType | Specifies the encoding method of the return value; value range: url; no encoding is performed by default | String |
| MaxParts | Maximum number of returned parts; default and maximum value: 1,000 | String |
| IsTruncated | Indicates whether the returned parts are truncated | String |
| PartNumberMarker | The part list starts from PartNumberMarker, which is 0 by default, i.e., listing parts from the first one | String |
| NextPartNumberMarker | Indicates the starting position of the next part list | String |
 | StorageClass | Object storage class; value range: STANDARD, STANDARD_IA, ARCHIVE; default value: STANDARD | String |
| Part | Information of an uploaded part, including ETag, PartNumber, Size, and LastModified | String |
 | Initiator | Information of the multipart upload initiator, including DisplayName, and ID | Dict | 
 | Owner | Object owner information, including DisplayName and ID | Dict | 



### Completing a Multipart Upload

#### Feature Description

The API (Complete Multipart Upload) is used to complete the multipart upload of the entire object.

#### Method Prototype

```
complete_multipart_upload(Bucket, Key, UploadId, MultipartUpload={}, **kwargs)
```
#### Sample Request

```python
response = client.complete_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId=uploadid,
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
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes | 
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes | 
| UploadId | Identifies the ID of the multipart upload | String | Yes | 
| MultipartUpload | ETag and PartNumber information of all parts | Dict | Yes | 

#### Return Result Descriptions

Information of the assembled object in dict type.

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
 | ETag |	 The unique tag value of the merged object, which is not the MD5 checksum of the object's content and can only be used to check the object's uniqueness. To verify the content of the object, check the ETag values of individual parts during the upload process | String | 
 | Bucket | Bucket name in the format of BucketName-APPID | String | 
 | Location | URL address | String | 
 | Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String |


### Aborting a Multipart Upload

#### Feature Description

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts.

#### Method Prototype

```
abort_multipart_upload(Bucket, Key, UploadId, **kwargs)
```
#### Sample Request

```python
response = client.abort_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId=uploadid
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
|Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
|UploadId | Identifies the ID of the multipart upload | String | Yes |

#### Return Result Descriptions
The return value of this method is None.

## Other Operations

### Restoring an Archived Object 

#### Feature Description

This API (POST Object restore) is used to retrieve an archived object for access.

#### Method Prototype

```
restore_object(Bucket, Key, RestoreRequest={}, **kwargs)
```
#### Sample Request

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
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
|Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
|RestoreRequest| Describes the rule of the temporary object retrieved | Dict | Yes |
| Days | Describes the expiration time of the temporary object | Int | Yes |
|CASJobParameters| Describes the configuration information of the restoration type | Dict | No |
| Tier | Describes the mode in which the temporary object is retrieved. Value range: Expedited (for expedited mode), Standard (for standard mode), Bulk (for slow mode) | String | No |

#### Return Result Descriptions
The return value of this method is None.


### Setting Object ACL

#### Feature Description

This API (PUT Object acl) is used to set the ACL for the specified object in a bucket.

#### Method Prototype

```
put_object_acl(Bucket, Key, AccessControlPolicy={}, **kwargs)
```
#### Sample Request

```python
response = client.put_object_acl(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    ACL='private'|'public-read',
    GrantFullControl='string',
    GrantRead='string',
    AccessControlPolicy={
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
        ],
        'Owner': {
            'DisplayName': 'string',
            'ID': 'string'
        }
    }
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes | 
| ACL | Sets the object ACL such as 'private' and 'public-read' | String | No | 
| GrantFullControl | Grants the specified account full permission to the object in the format of `id="[OwnerUin]"` | String | No |
|GrantRead | Grants the specified account read permission to the object in the format of `id="[OwnerUin]"` | String | No |
| AccessControlPolicy | Grants the specified account access to the object. For detailed format, see the return result descriptions of GET Object acl | Dict | No | 


#### Return Result Descriptions

The return value of this method is None.

### Querying Object ACL

#### Feature Description

This API (Get Object acl) is used to query the ACL of an object.

#### Method Prototype

```
get_object_acl(Bucket, Key, **kwargs)
```
#### Sample Request

```python
response = client.get_object_acl(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
|Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |


#### Return Result Descriptions

Bucket ACL information in Dict type:
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
 | Owner | Object owner information, including DisplayName and ID | Dict | 
 | Grant | Object permission grantee information, including Grantee and Permission  | List | 
 | Grantee | Object permission grantee information, including DisplayName, Type, ID, and URI | Dict | 
 | DisplayName | Permission grantee name | String |
 | Type              | Permission grantee type; CanonicalUser or Group            | String |
 | ID | If Type is CanonicalUser, this parameter corresponds to the ID of the permission grantee | String | 
 | URI | If Type is Group, this parameter corresponds to the URI of the permission grantee | String | 
 | Permission | Permission to the object owned by the grantee. Value range: FULL_CONTROL (for full permission), WRITE (for write permission), READ (for read permission) | string |


 ## Advanced API (Recommended)

### Upload Resumption

#### Feature Description
This advanced API automatically selects simple upload or multipart upload based on the file length. For files below 20 MB, it calls a simple upload. For files above 20 MB, it calls a multipart upload that can be automatically resumed if paused before completion.

#### Method Prototype

```
upload_file(Bucket, Key, LocalFilePath, PartSize=1, MAXThread=5, **kwargs)
```
#### Sample Request

```python
response = client.upload_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    LocalFilePath='local.txt',
    EnableMD5=False
)
```

#### Request Example with All Parameters
```python
response = client.upload_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    LocalFilePath='local.txt',
    PartSize=1,
    MAXThread=5,
    EnableMD5=False|True,
    ACL='private'|'public-read',  # Please use this parameter with caution; otherwise, the upper limit of 1,000 ACL entries will be reached
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
#### Parameter Descriptions


| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
 | Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes | 
| LocalFilePath | Path to the local file | String | Yes |
| PartSize | Part size in the multipart upload; default value: 1 MB | Int | No |
| MAXThread | Number of concurrent threads of the multipart upload; default value: 5 | Int | No |
| EnableMD5 | Whether the SDK is required to calculate the Content-MD5. This is disabled by default, and enabling this will increase the upload time | Bool | No | 
| ACL | Sets the object ACL such as 'private' and 'public-read' | String | No |
| GrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | String | No |
| GrantRead | Grants the grantee read permission in the format of id="[OwnerUin]" | String | No |
 | StorageClass | Sets the object storage class; value range: STANDARD, STANDARD_IA, ARCHIVE; default value: STANDARD | String | No |
 | Expires | Sets Expires | String | No | 
 | CacheControl | Cache policy, which sets Cache-Control | String | No |
 | ContentType | Content type, which sets Content-Type | String | No |  
 | ContentDisposition | Filename, which sets Content-Disposition | String | No |
 | ContentEncoding | Encoding format, which sets Content-Encoding | String | No |
 | ContentLanguage | Language type, which sets Content-Language | String | No |
 | ContentLength | Sets transfer length | String | No | 
 | ContentMD5 | Sets the MD5 value of the uploaded object for verification | String | No | 
 |  Metadata | User-defined object metadata | Dict | No |

#### Return Result Descriptions
Attributes of the uploaded object in dict type:

```python
{
    'ETag': 'string'
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- |
| ETag | MD5 value of the uploaded object | String |
