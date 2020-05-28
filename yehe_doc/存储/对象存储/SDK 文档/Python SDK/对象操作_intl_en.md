## Overview

This document provides an overview of APIs and SDK sample codes related to simple, multipart, and other operations on objects.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/7734) | Querying object list | Queries some or all objects in a bucket |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying a list of current and noncurrent (previous) versions of an object | Queries all or a subnet of objects in a bucket and their versions |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading on object using simple upload | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies a file to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |


**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Queries multipart uploads | Queries in-progress multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload job |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads file parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |




## Simple Operations

### Querying object list

#### Feature

This API (GET Bucket (List Object)) is used to query some or all objects in a bucket.

#### Method prototype

```
list_objects(Bucket, Delimiter="", Marker="", MaxKeys=1000, Prefix="", EncodingType="", **kwargs)
```
#### Request samples

[//]: # ".cssg-snippet-get-bucket"
```python
response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='folder1'
)
```

#### Sample request for all parameters

[//]: # ".cssg-snippet-get-bucket-comp"
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
#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| Prefix  |  Filters the object keys prefixed with the value of this parameter. It is left empty by default. | String  | No |
| Delimiter | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | String | No |
| Marker | Marks the starting point of returned objects. Entries are listed in UTF-8 binary order by default. | String | No |
| MaxKeys | The maximum number of returned objects. It defaults to 1000. | int | No |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | String | No |

#### Response description 

The response contains object metadata in dict format:

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
| MaxKeys   | Maximum number of returned objects. Default value: 1,000.  | String |
| Prefix   | Filters objects prefixed with the value of this parameter. It is left empty by default. | String  | 
| Delimiter | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | String |
| Marker | Marks the starting object of returned objects list. Entries are listed in UTF-8 binary order by default. | String |
| NextMarker | Marks the starting object of the next list of returned objects if `IsTruncated` is set to `true`. | String |
| Name | Bucket name. Format: BucketName-APPID | String |
| IsTruncated   |  Indicates whether returned objects are truncated | String|
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Valid value: url | String | No |
| Contents | List of object metadata, including 'ETag', 'StorageClass', 'Key', 'Owner', 'LastModified', 'Size' | List |
| CommonPrefixes | All objects starting with a particular prefix and ending with the delimiter are grouped into the same type | List |

### Querying objects and their version history 

#### Feature

This API (GET Bucket Object Versions) is used to query some or all objects in a bucket and their version history.

#### Method prototype

```
list_objects_versions(Bucket, Prefix="", Delimiter="", KeyMarker="", VersionIdMarker="", MaxKeys=1000, EncodingType="", **kwargs)
```
#### Request samples

[//]: # ".cssg-snippet-list-object-versioning"
```python
response = client.list_objects_versions(
    Bucket='examplebucket-1250000000',
    Prefix='string'
)
```

#### Sample request for all parameters

[//]: # ".cssg-snippet-list-object-versioning-comp"
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
#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| Prefix  |  Filters the object keys prefixed with the value of this parameter. It is left empty by default. | String  | No |
| Delimiter | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | String | No |
| Marker | Marks the starting object key of the list of returned objects. Entries are listed in UTF-8 binary order by default. | String | No |
| VersionIdMarker|  Marks the starting VersionId of the list of returned objects. Entries are listed in UTF-8 binary order by default. | String  |  No |
| MaxKeys | The maximum number of returned objects. It defaults to 1000. | int | No |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | String | No |

#### Response description 

The response contains object metadata in dict format:

```python
{
    'MaxKeys': '1000', 
    'Prefix': 'string',
    'Delimiter': 'string',
    'KeyMarker': 'string',
    'VersionIdMarker': 'string',
    'NextKeyMarker': 'string',
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
| MaxKeys   | Maximum number of returned objects. Default value: 1000.  | String |
| Prefix   | Filters objects prefixed with the value of this parameter. It is left empty by default. | String  | 
| Delimiter | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | String |
| KeyMarker | Marks the starting object key of the list of returned objects. Entries are listed in UTF-8 binary order by default. | String |
| VersionIdMarker|  Marks the starting VersionId of the list of returned objects. Entries are listed in UTF-8 binary order by default. | String  |  
| NextKeyMarker | Marks the starting object key of the next list of returned objects if `IsTruncated` is set to `true`. | String |
| NextVersionIdMarker | Marks the starting VersionId of the next list of returned objects if `IsTruncated` is set to `true`. | String |
| Name | Bucket name. Format: BucketName-APPID | String | 
| IsTruncated   |  Indicates whether returned objects are truncated | String|
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Valid value: url | String | No |
| Version | A List of metadata on all the versions of each object, including 'ETag', 'StorageClass', 'Key', 'VersionId', 'IsLatest', 'Owner', 'LastModified', and 'Size' | List |
| DeleteMarker | A list of metadata on all object delete markers, including 'Key', 'VersionId', 'IsLatest', 'Owner', and 'LastModified' | List |
| CommonPrefixes | All objects starting with a particular prefix and ending with the delimiter are grouped into the same type | List |

### Uploading an object usng simple upload

#### Feature

This API (Put Object) is used to upload an object to a bucket.

#### Method prototype

```
put_object(Bucket, Body, Key, **kwargs)
```
#### Request samples

[//]: # ".cssg-snippet-put-object"
```python
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes',
    Key='exampleobject',
    EnableMD5=False
)
```

#### Sample request for all parameters
[//]: # ".cssg-snippet-put-object-comp"
```python
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes'|file,
    Key='exampleobject',
    EnableMD5=False|True,
    ACL='private'|'public-read',  # Please be aware that by using this parameter, the maximum of 1000 ACLs may be reached
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
#### Parameter description


| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
|  Body  | Content of the object to be uploaded. It can be a file stream or a byte stream|  file/bytes | Yes |
| Key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`，the ObjectKey is doc/pic.jpg | String | Yes |
| EnableMD5 | Whether the SDK needs to calculate Content-MD5. This feature is disabled by default. The upload will take longer if it is enabled |Bool | No |
| ACL | Sets the object ACL, e.g. 'private'，'public-read' |String| No |
| GrantFullControl | Grants full permission in the format: `id="OwnerUin"` | String | No |
| GrantRead | Grants the grantee Read access in the format of `id="OwnerUin"` | String | No |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| Expires | Sets `Expires`. | String | No |
| CacheControl | Cache policy. Sets `Cache-Control`. | String | No |
| ContentType | Content type. Sets `Content-Type` | String | No |
| ContentDisposition | File name. Sets `Content-Disposition` | String | No |
| ContentEncoding | Encoding format. Sets `Content-Encoding` | String | No |
| ContentLanguage | Language type. Sets `Content-Language` | String | No |
| ContentLength | Sets the length of the request content | string | No |
| ContentMD5 | Sets the MD5 hash of the object to be uploaded for verification | String | No |
|  Metadata | User-defined object metadata. It must start with `x-cos-meta`; otherwise, it will be ignored | Dict | No |

#### Response description 
This response contains attributes of the uploaded object. The type is dict:

```python
{
    'ETag': 'string',
    'x-cos-version-id': 'string'
}
```


| Parameter Name | Description | Type |
| -------------- | -------------- |---------- |
|  ETag   |  MD5 hash of the uploaded object | String |
|  x-cos-version-id   |  Version ID of the object if versioning is enabled | String  |



### Querying object metadata

#### Feature

The API (HEAD Object) is used to query object metadata.

#### Method prototype

```
head_object(Bucket, Key, **kwargs)
```
#### Request samples

[//]: # ".cssg-snippet-head-object"
```python
response = client.head_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```
#### Request sample for all parameters

```python
response = client.head_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    VersionId='string',
    IfModifiedSince='Wed, 28 Oct 2014 20:30:00 GMT',
)
```
#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| key | Object key, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| VersionId   | Specifies the object version ID if versioning is enabled  | String  | No |
| IfModifiedSince | The object metadata is returned only if the object is modified after the specified time in GMT format | String | No |

#### Response description 

The response contains object metadata in dict format:

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
| ETag  |  MD5 hash of the object | String |
| Last-Modified | Last modified time of the object | String |
| CacheControl | Caching policy. HTTP standard header. | String | 
| ContentType | Content type. HTTP standard header. | String | 
| ContentDisposition | File name. HTTP standard header | String |
| ContentEncoding | Encoding format. HTTP standard header. | String | 
| ContentLanguage | Language type. HTTP standard header. | String | 
|  Content-Length  | Object size | String |
|  Expires | Cache expiration time. HTTP standard header. | String |
|  x-cos-meta-* | User-defined object metadata. It must start with `x-cos-meta`; otherwise, it will be ignored  | String |
|  x-cos-version-id   |  Version ID of the object if versioning is enabled | String  |


### Downloading an object

#### Feature

This API (Get Object) is used to download an object.

#### Method prototype

```
 get_object(Bucket, Key, **kwargs)
```
#### Request samples
```python
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)

response['Body'].get_stream_to_file('exampleobject')
```
#### Sample request for all parameters

[//]: # ".cssg-snippet-get-object"
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
#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| key | Object key, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| Range | Sets the range of bytes of the object to be downloaded in the format of `bytes=first-last` | String | No |
|  IfMatch  | The object is returned only if Etag matches the specified content |String  | No |
| IfModifiedSince | The object is returned only if the object is modified after the specified time in GMT format | String | No |
|  IfNoneMatch  |  The object is returned only if Etag does not match the specified content | String  | No |
| IfUnmodifiedSince | The object is returned only if the object is modified before or at the specified time in GMT format  | String | No |
| ResponseCacheControl | Sets the `Cache-Control` in the response header | String | No |
| ResponseContentDisposition | Sets the `Content-Disposition` in the response header | String | No |
| ResponseContentEncoding | Sets the `Content-Encoding` in the response header | String | No |
| ResponseContentLanguage | Sets the `Content-Language` in the response header | String | No |
| ResponseContentType | Sets the `Content-Type` in the response header | String | No |
| Response-expires | Sets the `Expires` in the response header | String | No |
| VersionId | Specifies the version ID of the object to be downloaded | String | No |

#### Response description 

The response contains the body and the metadata of the downloaded object in dict format:

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
      <td>Content of the downloaded object. The get_raw_stream() method gets a file stream; the get_stream_to_file(local_file_path) method downloads the object content to a specified local file</td>
      <td>StreamBody</td>
   </tr>
   <tr>
      <td>ETag</td>
      <td>MD5 hash of the object</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Last-Modified</td>
      <td>Last modified time of the object</td>
      <td>String</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Accept-Ranges</td>
      <td>Range. HTTP standard header.</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Range</td>
      <td>Content range. HTTP standard header.</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Cache-Control</td>
      <td>Cache policy. HTTP standard header.</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>Content type. HTTP standard header.</td>
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
      <td>User-defined object metadata. It must start with `x-cos-meta`; otherwise, it will be ignored</td>
      <td>String</td>
   </tr>
   <tr>
      <td>x-cos-version-id</td>
      <td>Version ID of the object if versioning is enabled </td>
      <td>String</td>
   </tr>
</table>



### Setting object replication

#### Feature

This API (PUT Object - Copy) is used to copy a file to a destination path.

#### Method prototype

```
copy_object(Bucket, Key, CopySource, CopyStatus='Copy', **kwargs)
```
#### Request samples

[//]: # ".cssg-snippet-copy-object"
```python
response = client.copy_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou'
    }
)
```
#### Sample request for all parameters

```python
response = client.copy_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou',
        'VesionId': 'string'
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
#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| Key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | string | Yes |
|  CopySource  | Describes the path to the source object, including `Bucket`, `Key`, `Region`, `VersionId` |  Dict | Yes |
| CopyStatus | Valid values: 'Copy': ignore the configured metadata and copy the file directly; 'Replaced': modify the metadata according to the configured metadata. If the destination path is identical to the source path, this parameter must be set to ‘Replaced’. | String | Yes |
| ACL | Sets the ACL of the object, e.g. 'private', 'public-read' |String| No |
| GrantFullControl | Grants the grantee full permission in the format of `id="OwnerUin"`| String | No |
|GrantRead | Grants the grantee Read access in the format of `id="OwnerUin"`| String | No |
| StorageClass | Sets the object storage class: `STANDARD` or `STANDARD_IA`. Default value: `STANDARD` | String | No |
| Expires | Sets `Expires`. | String | No |
| CacheControl | Caching policy. Sets `Cache-Control`. | String | No |
| ContentType | Content type. Sets `Content-Type`. | String | No |
| ContentDisposition | File name. Sets `Content-Disposition`. | String | No |
| ContentEncoding | Encoding format. Sets `Content-Encoding`. | String | No |
| ContentLanguage | Language type. Sets `Content-Language` | String | No |
|  Metadata | User-defined object metadata | Dict |  No |


#### Response description 
This response contains attributes of the uploaded object in dict format:

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
| ETag | MD5 hash of the copied object | String |
| LastModified | Last modified time of the copied object | String |
| VersionId | Version ID of the copied object if versioning is enabled | String  |
| x-cos-copy-source-version-id | Version ID of the source object | String |


### Deleting a single object

#### Feature

This API (Delete Object) is used to delete a specified object.

#### Method prototype

```
delete_object(Bucket, Key, **kwargs)
```
#### Request samples

[//]: # ".cssg-snippet-delete-object"
```python
response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```
#### Sample request for all parameters

```python
response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    VersionId='string',
)
```
#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| VersionId |Specifies the object version ID if versioning is enabled | String  | No |

#### Response description 

This response contains the information on the deleted object in Dict format:

```python
{
    'x-cos-version-id': 'string',
    'x-cos-delete-marker': 'true'|'false',
}
```

| Parameter Name | Description | Type |
| -------------- | -------------- |---------- |
| x-cos-version-id | Version ID of the deleted object | String |
| x-cos-delete-marker | Identifies whether the deleted object is a delete marker | String |

### Deleting multiple objects

#### Feature

The API（DELETE Multiple Objects）is used to delete multiple objects.

#### Method prototype

```
delete_objects(Bucket, Delete={}, **kwargs)
```
#### Request samples

[//]: # ".cssg-snippet-delete-multi-object"
```python
response = client.delete_objects(
    Bucket='examplebucket-1250000000',
    Delete={
        'Object': [
            {
                'Key': 'exampleobject1'
            },
            {
                'Key': 'exampleobject2'
            }
        ]
    }
)
```
#### Sample request for all parameters

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

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| Delete  | Describes the objects to be deleted and the way the deletion results are returned | Dict | Yes |
| Objects | Information on the objects to be deleted | List | Yes |
| Key | Object key is the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String |
| VersionId | Version IDs of the objects to be deleted if versioning is enabled. | String  | No |
| Quiet | Specifies how the deletion results are returned. Valid values: 'true', only information on failed deletions is returned; 'false', information on all deletions is returned. Default value: 'false' | String | No |

#### Response description 
This response contains the result of the object deletions in dict format:
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
| Deleted  |  Information on the objects successfully deleted |  List |
| Key | Path to the objects successfully deleted | String |
| VersionId     | Version IDs of the objects successfully deleted | String|
| DeleteMarker     | Whether the object deleted successfully is delete marker| String|
| DeleteMarkerVersionId | Version IDs of the delete markers of the objects successfully deleted | String|
| Error  |  Information on the objects that failed to be deleted| List |
| Key | Paths to the objects that failed to be deleted | string |
| VersionId     | Version IDs of the objects that failed to be deleted| String|
| Code | Error codes for the objects that failed to be deleted | string |
| Message | Error messages for the objects that failed to be deleted | string |


### Restoring an archived object 

#### Feature

This API (POST Object restore) is used to restore an archived object.

#### Method prototype

```
restore_object(Bucket, Key, RestoreRequest={}, **kwargs)
```
#### Request samples

[//]: # ".cssg-snippet-restore-object"
```python
response = client.restore_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    RestoreRequest={
        'Days': 100,
        'CASJobParameters': {
            'Tier': 'Standard'
        }
    }
)
```
#### Sample request for all parameters

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
#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
|RestoreRequest| Describes the rules of the restored temporary object| Dict| Yes |
|Days| Describes the expiration time of the temporary object | Int| Yes |
|CASJobParameters| Describes the configuration of the restoration type| Dict| No |
|Tier| Describes the object restoration mode. Valid values: 'Expedited', 'Standard', and 'Bulk' | String| No |

#### Response description 
This method returns None.



## Multipart Operations
Operations related to multipart uploads include the following:

- Multipart upload of objects: initializing multipart upload, uploading parts, and completing multipart upload
- Resuming a multipart upload: querying uploaded parts, uploading parts, and completing a multipart upload
- Deleting uploaded parts

### Querying multipart upload

#### Feature

This API (List Multipart Uploads) is used to query ongoing multipart uploads in a specified bucket.

#### Method prototype

```
list_multipart_uploads(Bucket, Prefix="", Delimiter="", KeyMarker="", UploadIdMarker="", MaxUploads=1000, EncodingType="", **kwargs)
```
#### Request samples

[//]: # ".cssg-snippet-list-multi-upload"
```python
response = client.list_multipart_uploads(
    Bucket='examplebucket-1250000000',
    Prefix='dir'
)
```
#### Sample request for all parameters

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
#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| Prefix | Filters the multipart upload keys prefixed with the value of this parameter. It is left empty by default. | String | No |
| Delimiter | A separator which is left empty by default. | String | No |
| KeyMarker | Specifies the starting key of the multipart upload list. It is used together with `UploadIdMarker`. | String | No |
| UploadIdMarker | Specifies the starting `UploadId` of the multipart upload list. It is used together with `KeyMarker`. If `KeyMarker` is not specified, `UploadIdMarker` will be ignored. | String | No |
| MaxUploads | Maximum number of multipart uploads returned at a time. Default value: 1000. | Int | No |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | String | No |

#### Response description 

This response contains information on the multipart uploads obtained in dict format:

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
| Prefix | Filters the multipart upload keys prefixed with the value of this parameter. It is left empty by default. | String |
| Delimiter | A separator which is left empty by default. | String |
| KeyMarker | Specifies the starting key of the multipart upload list. It is used together with `UploadIdMarker`. | Sring |
| UploadIdMarker | Specifies the starting `UploadId` of the multipart upload list. It is used together with `KeyMarker`. If `KeyMarker` is not specified, `UploadIdMarker` will be ignored. | String |
| NextKeyMarker | Specifies the starting key of the next multipart upload list if `IsTruncated` is `true`. | String |
| NextUploadIDMarker | Specifies the starting `UploadId` of the next multipart upload list if `IsTruncated` is `true`. | String |
| MaxUploads | Maximum number of multipart uploads returned at a time. Default value: 1000. | int |
| IsTruncated | Indicates whether the returned multipart upload list is truncated | String |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Valid value: `url` | String |
| Upload | List of information on the returned multipart uploads, including 'UploadId', 'StorageClass', 'Key', 'Owner', 'Initiator', 'Initiated', etc. | List |
| CommonPrefixes | The identical paths between `Prefix` and `Delimiter` are grouped and defined as a common prefix | List |


### Initializing a multipart upload

#### Feature

This API (Initiate Multipart Upload) is used to initialize a multipart upload and obtain the corresponding uploadId.

#### Method prototype

```
create_multipart_upload(Bucket, Key, **kwargs):
```
#### Request samples

[//]: # ".cssg-snippet-init-multi-upload"
```python
response = client.create_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    StorageClass='STANDARD'
)
```
#### Sample request for all parameters

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
# Obtain UploadId for use by other APIs
uploadid = response['UploadId']
```
#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| Expires | Sets `Expires`. | String | No |
| CacheControl | Caching policy. Sets `Cache-Control`. | String | No |
| ContentType | Content type. Sets `Content-Type`. | String | No |
| ContentDisposition | File name. Sets `Content-Disposition`. | String | No |
| ContentEncoding | Encoding format. Sets `Content-Encoding`. | String | No |
| ContentLanguage | Language type. Sets `Content-Language` | String | No |
|  Metadata | User-defined object metadata | Dict |  No |
| ACL | Sets the object ACL, e.g. 'private'，'public-read'|String| No |
| GrantFullControl | Grants full permission in the format: `id="OwnerUin"` | String | No |
| GrantRead | Grants the grantee Read access in the format of `id="OwnerUin"` | String | No |

#### Response description 

This response contains the initialization information of the multipart upload in dict format:

```python
{
    'UploadId': '150219101333cecfd6718d0caea1e2738401f93aa531a4be7a2afee0f8828416f3278e5570',
    'Bucket': 'examplebucket-1250000000', 
    'Key': 'exampleobject' 
}

```

| Parameter Name | Description | Type |
| -------------- | -------------- |---------- |
| UploadId | ID of the multipart upload | String |
| Bucket | Bucket name. Format: BucketName-APPID | String |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String |

### Uploading parts

This API (Upload Part) is used to upload parts.

#### Method prototype

```
upload_part(Bucket, Key, Body, PartNumber, UploadId, **kwargs)
```
#### Request samples

[//]: # ".cssg-snippet-upload-part"
```python
# Note: The maximum number of parts to be uploaded is 10,000.
response = client.upload_part(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Body=b'b'*1024*1024,
    PartNumber=1,
    UploadId='exampleUploadId'
)
```
#### Sample request for all parameters

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
#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| Body  | Content of the parts to be uploaded. It can be a local file stream or an input stream.| file/bytes |  Yes|
| PartNumber | Identifies the part number | int | Yes |
| UploadId | ID of the multipart upload | string | Yes |
| EnableMD5 | Whether the SDK needs to calculate Content-MD5. This feature is disabled by default. The upload will take longer if it is enabled|Bool | No |
| ContentLength | Sets the length of the request content | string | No |
| ContentMD5 | Sets the MD5 hash of the object to be uploaded for verification | String | No |

#### Response description 

This response contains attributes of the uploaded parts. The type is dict:

```python
{
    'ETag': 'string'
}
```

| Parameter Name | Description | Type |
| -------------- | -------------- |---------- |
| ETag | MD5 hash of the uploaded part | String |

### Copying parts

This API (Upload Part - Copy) is used to copy an object as a part.

#### Method prototype

```
upload_part_copy(Bucket, Key, PartNumber, UploadId, CopySource, CopySourceRange='', **kwargs)
```
#### Request samples

[//]: # ".cssg-snippet-upload-part-copy"
```python
response = client.upload_part_copy(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    PartNumber=1,
    UploadId='exampleUploadId',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou'
    }
)
```
#### Sample request for all parameters

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

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| Key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg. | string | Yes |
| PartNumber | Identifies the part number | int | Yes |
| UploadId | ID of the multipart upload | string | Yes |
|  CopySource  | Describes the path to the source object, including `Bucket`, `Key`, `Region`, `VersionId` |  Dict | Yes |
|CopySourceRange| Describes the range of the source object to be copied in the format of `bytes=first-last`. The entire source will be copied by default if no range is specified|String| No |
|CopySourceIfMatch| The source object is copied only if the Etag of the source object matches the specified value|String| No |
|CopySourceIfModifiedSince| The source object is copied only if it is modified after the specified time |String| No |
|CopySourceIfNoneMatch| The source object is copied only if the Etag of the source object does not match the specified value |String| No |
|CopySourceIfUnmodifiedSince| The source object is copied only if it is not modified after the specified time|String| No |

#### Response description 

This response contains the attributes of the copied part in dict format:
```python
{
    'ETag': 'string',
    'LastModified': 'string',
    'x-cos-copy-source-version-id': 'string',
}
```

| Parameter Name | Description | Type |
| -------------- | -------------- |---------- |
| ETag | MD5 hash of the copied part | String |
| LastModified | Last modified time of the copied part | String |
| x-cos-copy-source-version-id | Version ID of the source object | String |

### Querying uploaded parts

#### Feature

This API (List Parts) is used to query the uploaded parts in a specific multipart upload.

#### Method prototype

```
list_parts(Bucket, Key, UploadId, MaxParts=1000, PartNumberMarker=0, EncodingType='', **kwargs)
```
#### Request samples

[//]: # ".cssg-snippet-list-parts"
```python
response = client.list_parts(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId='exampleUploadId'
)
```
#### Sample request for all parameters

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
#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| UploadId | ID of the multipart upload | String | Yes |
| MaxParts | Maximum number of parts returned at a time. Default value: 1,000. | Int | No |
| PartNumberMarker | The parts are listed starting from the one following `PartNumberMarker`. Default value: 0, which means the parts are listed from the first one. | int | No |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Valid value: `url` | String | No |

#### Response description 

This response contains information on the uploaded parts obtained. The type is dict:

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
| Key | Object key, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String |
| UploadId | ID of the multipart upload | String |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Valid value: `url` | String |
| MaxParts | Maximum number of parts returned at a time. Default value: 1000. | String |
| IsTruncated | Indicates whether the returned list is truncated | String |
| PartNumberMarker | The parts are listed starting from the one following `PartNumberMarker`. Default value: 0, which means the parts are listed from the first one. | String |
| NextPartNumberMarker | Marks the starting part of the next part list | String |
| StorageClass | Sets the object storage class; Valid values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String |
| Part | Information on the uploaded parts, including `ETag`, `PartNumber`, `Size`, `LastModified` | String |
| Initiator | Creator of the multipart upload, including `DisplayName`, and `ID` | Dict |
| Owner | Information on the object owner, including `DisplayName` and `ID` | Dict |



### Completing a multipart upload

#### Feature

This API (Complete Multipart Upload) is used to complete a multipart upload.

#### Method prototype

```
complete_multipart_upload(Bucket, Key, UploadId, MultipartUpload={}, **kwargs)
```
#### Request samples

[//]: # ".cssg-snippet-complete-multi-upload"
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
#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| UploadId | ID of the multipart upload | String | Yes |
| MultipartUpload | Information on all parts, including `ETag` and `PartNumber` | Dict |

#### Response description 

This response contains information on the merged object. The type is dict:

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
| ETag | The unique tag of the merged object. It is not the MD5 checksum of the object content; it is only used to check the uniqueness of the object. To verify the object content, you can check the ETag of each part during the upload process. | string |
| Bucket | Bucket name. Format: BucketName-APPID | String |
| Location | URL address | String |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String |


### Aborting a multipart upload

#### Feature

This API (Abort Multipart Upload) is used to abort a multipart upload and delete the uploaded parts.

#### Method prototype

```
abort_multipart_upload(Bucket, Key, UploadId, **kwargs)
```
#### Request samples

[//]: # ".cssg-snippet-abort-multi-upload"
```python
response = client.abort_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId='exampleUploadId'
)
```
#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| UploadId | ID of the multipart upload | String | Yes |

#### Response description 
This method returns None.





 ## Advanced APIs (recommended)

### Uploading objects (checkpoint restart)

#### Feature
This API can automatically select between simple upload and multipart upload according to the file size. It uses simple upload for files smaller than or equal to 20 MB and multipart upload for files larger than 20 MB. It also supports automatic checkpoint restart for incomplete multipart uploads.

#### Method prototype

```
upload_file(Bucket, Key, LocalFilePath, PartSize=1, MAXThread=5, **kwargs)
```
#### Request samples

[//]: # ".cssg-snippet-transfer-upload-object"
```python
response = client.upload_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    LocalFilePath='local.txt',
    EnableMD5=False
)
```

#### Sample request for all parameters
```python
response = client.upload_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    LocalFilePath='local.txt',
    PartSize=1,
    MAXThread=5,
    EnableMD5=False|True,
    ACL='private'|'public-read', # Please be aware that by using this parameter, the maximum of 1000 ACLs may be reached
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
#### Parameter description


| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| Key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`，the ObjectKey is doc/pic.jpg | String | Yes |
|  LocalFilePath  | Path to the local file |  String | Yes |
|  PartSize  | Part size. Default value: 1 MB |  Int |  No |
|  MAXThread  | Maximum number of concurrent multipart upload tasks. Default value: 5 |  Int |  No |
| EnableMD5 | Whether the SDK needs to calculate Content-MD5. This feature is disabled by default. The upload will take longer if it is enabled| Bool | No |
| ACL | Sets the object ACL, e.g. 'private'，'public-read'|String| No |
| GrantFullControl | Grants full permission in the format: `id="OwnerUin"` | String | No |
| GrantRead | Grants the grantee Read access in the format of `id="OwnerUin"` | String | No |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| Expires | Sets `Expires`. | String | No |
| CacheControl | Cache policy. Sets `Cache-Control`. | String | No |
| ContentType | Content type. Sets `Content-Type`. | String | No |
| ContentDisposition | File name. Sets `Content-Disposition`. | String | No |
| ContentEncoding | Encoding format. Sets `Content-Encoding`. | String | No |
| ContentLanguage | Language type. Sets `Content-Language` | String | No |
| ContentLength | Sets the length of the request content | string | No |
| ContentMD5 | Sets the MD5 hash of the object to be uploaded for verification | String | No |
|  Metadata | User-defined object metadata | Dict |  No |

#### Response description 
This response contains attributes of the uploaded object in dict format:

```python
{
    'ETag': 'string'
}
```

| Parameter Name | Description | Type |
| -------------- | -------------- |---------- |
| ETag | MD5 hash of the uploaded object | String |
