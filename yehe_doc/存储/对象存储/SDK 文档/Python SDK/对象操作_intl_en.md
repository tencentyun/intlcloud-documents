## Overview

This document provides an overview of APIs and SDK sample codes related to simple operations, multipart operations, and other object operations.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Object)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying a list of objects and their version history | Queries some or all objects in a bucket and their version history |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access|
| [SELECT Object content](https://intl.cloud.tencent.com/document/product/436/32360) | Extracting object content | Extracts the content of a specified object |


**Multipart operations**

| API          | Operation                   | Description                                       |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Queries multipart uploads | Queries in-progress multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading a part | Uploads a part in a multipart upload. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Uploads a part by copying data from an existing object as data source |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts |  Queries the uploaded parts of a specific multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of an entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts |




## Simple Operations

### Querying an object list

#### API description

This API is used to query some or all objects in a bucket.

#### Method prototype

```
list_objects(Bucket, Delimiter="", Marker="", MaxKeys=1000, Prefix="", EncodingType="", **kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-get-bucket)
```python
response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='folder1'
)
```

#### Sample request with all parameters

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes | 
| Prefix  |  Filters the object keys prefixed with the value of this parameter. It is left empty by default. | String  | No | 
| Delimiter | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | String | No |
| Marker | Marks the starting point of the returned object list. Entries are listed in UTF-8 binary order by default. | String | No | 
| MaxKeys | The maximum number of returned objects. Default value: 1000. | Int | No | 
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Valid value: url | String | No |

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
| MaxKeys | The maximum number of returned objects. Default value: 1000. | String |
| Prefix   | Filters objects prefixed with the value of this parameter. It is left empty by default. | String  | 
| Delimiter | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | String |
| Marker | Specifies the object after which the listing should begin. Objects are listed in UTF-8 binary order by default. | String |
| NextMarker | Specifies the object after which the next listing should begin if `IsTruncated` is set to `true`. | String |
| Name | Bucket name in the format: `BucketName-APPID` | String | 
| IsTruncated   |  Indicates whether returned objects are truncated | String |
| EncodingType | Indicates the encoding method of the returned value. It’s left empty by default. Valid value: `url` | String |
| Contents | List of all object metadata, including 'ETag', 'StorageClass', 'Key', 'Owner', 'LastModified', 'Size' | List |
| CommonPrefixes | All objects starting with a particular prefix and ending with the delimiter are grouped into the same type | List |

### Querying objects and their version history 

#### API description

This API is used to query some or all objects in a bucket as well as their version history.

#### Method prototype

```
list_objects_versions(Bucket, Prefix="", Delimiter="", KeyMarker="", VersionIdMarker="", MaxKeys=1000, EncodingType="", **kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-list-objects-versioning)
```python
response = client.list_objects_versions(
    Bucket='examplebucket-1250000000',
    Prefix='string'
)
```

#### Sample request with all parameters

[//]: # (.cssg-snippet-list-objects-versioning-next-page)
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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes | 
| Prefix  |  Filters the object keys prefixed with the value of this parameter. It is left empty by default. | String  | No | 
| Delimiter | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | String | No |
| KeyMarker | Specifies the key after which the listing should begin. Objects are listed in UTF-8 binary order by default. | String | No |
| VersionIdMarker | Specifies the version ID after which the listing should begin. Objects are listed in UTF-8 binary order by default. | String  |  No |
| MaxKeys | The maximum number of returned objects; the default value is 1000. | Int | No | 
| EncodingType | Indicates the encoding method of the returned value. It’s left empty by default. Valid value: `url` | String | No |

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
| MaxKeys | The maximum number of returned objects. Default value: 1000. | String |
| Prefix   | Filters objects prefixed with the value of this parameter. It is left empty by default. | String  | 
| Delimiter | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | String |
| KeyMarker | Specifies the key after which the listing should begin. Objects are listed in UTF-8 binary order by default. | String |
| VersionIdMarker | Specifies the version ID after which the listing should begin. Objects are listed in UTF-8 binary order by default. | String  |  
| NextKeyMarker | Specifies the key after which the next listing should begin if `IsTruncated` is set to `true` | String |
| NextVersionIdMarker | Specifies the version ID after which the next listing should begin if `IsTruncated` is set to `true` | String |
| Name | Bucket name in the format: `BucketName-APPID` | String |  
| IsTruncated   |  Indicates whether returned objects are truncated | String |
| EncodingType | Indicates the encoding method of the returned value. It’s left empty by default. Valid value: `url` | String |
| Version | Lists the metadata of all objects with multiple versions, including 'ETag', 'StorageClass', 'Key', 'VersionId', 'IsLatest', 'Owner', 'LastModified', and 'Size' | List |
| DeleteMarker | Lists the metadata of all delete markers, including 'Key', 'VersionId', 'IsLatest', 'Owner', and 'LastModified' | List |
| CommonPrefixes | Groups all object keys starting with the `Prefix` and ending with the `Delimiter` as a common prefix | List |

### Uploading an object using simple upload

#### API description

This API is used to upload an object to a bucket.

#### Method prototype

```
put_object(Bucket, Body, Key, **kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-put-object)
```python
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes',
    Key='exampleobject',
    EnableMD5=False
)
```

#### Sample request with all parameters
[//]: # (.cssg-snippet-put-object-comp)
```python
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes'|file,
    Key='exampleobject',
    EnableMD5=False|True,
    ACL='private'|'public-read',
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
    },
    TrafficLimit='1048576'
)
```
#### Parameter description


| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
 |  Body  | Content of the object to be uploaded. It can be a file stream or a byte stream |  file/bytes | Yes |
 | Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes | 
| EnableMD5 | Specifies whether the SDK needs to calculate the Content-MD5 value. This feature is disabled by default. The upload will take longer if it is enabled | Bool | No | 
| ACL | Sets the object ACL, e.g. 'private', 'public-read' | String | No |
| GrantFullControl | Grants full permission in the format: `id="OwnerUin"` | String | No |
| GrantRead | Grants read permission in the format: `id="OwnerUin"` | String | No |
 | StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
 | Expires | Sets `Expires`. | String | No | 
 | CacheControl | Cache policy. Sets `Cache-Control` | String | No |
 | ContentType | Content type. Sets `Content-Type` | String | No |  
 | ContentDisposition | Object name. Sets `ContentDisposition` | String | No |
 | ContentEncoding | Encoding format. Sets `Content-Encoding`  | String | No |
 | ContentLanguage | Language type. Sets `Content-Language`  | String | No |
 | ContentLength | Sets the length of the request content  | String | No | 
 | ContentMD5 | Sets the MD5 checksum of the uploaded object | String | No | 
 | Metadata | User-defined object metadata. This parameter must start with `x-cos-meta`; otherwise, it will be ignored | Dict | No |
 |  TrafficLimit | Specifies the bandwidth limit for a single request in bit/s. Value range: 819200 - 838860800, i.e., 100 KB/s - 100 MB/s | String |  No |

#### Response description
The response contains the attributes of the uploaded object in dict format:

```python
{
    'ETag': 'string',
    'x-cos-version-id': 'string'
}
```


| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- |
| ETag | MD5 checksum of the uploaded object | String |
| x-cos-version-id | Version ID of the object if versioning is enabled | String  |



### Querying object metadata

#### API description

This API is used to query object metadata.

#### Method prototype

```
head_object(Bucket, Key, **kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-head-object)
```python
response = client.head_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```
#### Sample request with all parameters

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
  | Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes | 
  | Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
  | VersionId | Version ID of the object if versioning is enabled  | String  | No | 
  | IfModifiedSince | Returns the object metadata only if the object is modified after the time specified in GMT format | String | No | 

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
 | ETag | This value does not represent the MD5 checksum of the object content, but is used only to verify the uniqueness of the object as a whole during multipart upload | String |
 | Last-Modified | Time the object was last modified | String |
 | Cache-Control | Cache policy. Standard HTTP header | String | 
 | Content-Type | Content type. Standard HTTP header | String | 
 | Content-Disposition | File name. Standard HTTP header | String |
 | Content-Encoding | Encoding format. Standard HTTP header | String | 
 | Content-Language | Language type. Standard HTTP header | String | 
 | Content-Length  | Object size | String |
 | Expires | Cache expiration time. Standard HTTP header | String |
 | x-cos-meta-* | User-defined object metadata. This parameter must start with `x-cos-meta`; otherwise, it will be ignored  | String | 
 | x-cos-version-id |  Version ID of the object if versioning is enabled | String | 


### Downloading an object

#### API description

This API is used to download an object.

#### Method prototype

```
 get_object(Bucket, Key, **kwargs)
```
#### Sample request
```python
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)

response['Body'].get_stream_to_file('exampleobject')
```
#### Sample request with all parameters

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
    VersionId='string',
    TrafficLimit='819200'
)
```
#### Parameter description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes | 
 | Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes | 
 | Range | Sets the byte range of the object to be downloaded in the format: `bytes=first-last` | String | No | 
 |  IfMatch  | Returns the object only if the Etag matches the specified content |String  | No |  
 | IfModifiedSince | Returns the object only if it is modified after the time specified in GMT format | String | No |
 |  IfNoneMatch  |  Returns the object only if the Etag does not match the specified content | String  | No | 
 | IfUnmodifiedSince | Returns the object only if it is modified before or at the time specified in GMT format  | String | No |
 | ResponseCacheControl | Sets the value of `Cache-Control` in the response header | String | No | 
 | ResponseContentDisposition | Sets the value of `Content-Disposition` in the response header | String | No | 
 | ResponseContentEncoding | Sets the value of `Content-Encoding` in the response header | String | No |
 | ResponseContentLanguage | Sets the value of `Content-Language` in the response header | String | No | 
 | ResponseContentType | Sets the value of `Content-Type` in the response header | String | No |
 | ResponseExpires | Sets the value of `Expires` in the response header | String | No | 
 | VersionId | Version ID of the object to be downloaded | String | No |
 |  TrafficLimit | Specifies the bandwidth limit in bit/s for a single request (or a single thread for the advanced download API). Value range: 819200 - 838860800, i.e., 100 KB/s - 100 MB/s | String |  No |

#### Response description

The response contains the content and metadata of the downloaded object in dict format:

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
      <td>User-defined object metadata, must start with `x-cos-meta`; otherwise, it will be ignored</td>
      <td>String</td>
   </tr>
   <tr>
      <td>x-cos-version-id</td>
      <td>Specifies the version ID of the object if versioning is enabled </td>
      <td>String</td>
   </tr>
</table>



### Copying an object

#### API description

This API is used to copy an existing object to a destination path.

#### Method prototype

```
copy_object(Bucket, Key, CopySource, CopyStatus='Copy', **kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-copy-object)
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
#### Sample request with all parameters

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
 | Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
 | Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes | 
 | CopySource | Path of the source object to be copied, including `Bucket`, `Key`, `Region`, `VersionId` |  Dict | Yes |
 | CopyStatus | Valid values: 'Copy': ignore the configured metadata and copy the file directly; 'Replaced': modify the metadata according to the configured metadata. If the destination path is identical to the source path, this parameter must be set to ‘Replaced’. | String | Yes |
| ACL | Sets the object ACL, e.g. 'private', 'public-read' |String| No |
| GrantFullControl | Grants full permission in the format: `id="OwnerUin"`| String | No |
| GrantRead | Grants read access in the format: `id="OwnerUin"`| String | No |
 | StorageClass | Sets the object storage class: `STANDARD` or `STANDARD_IA`. Default value: `STANDARD` | String | No |
 | Expires | Sets `Expires` | String | No | 
 | CacheControl | Cache policy. Sets `Cache-Control` | String | No | 
 | ContentType | Content type. Sets `Content-Type` | String | No | 
 | ContentDisposition | File name. Sets `Content-Disposition` | String | No |
 | ContentEncoding | Encoding format. Sets `Content-Encoding` | String | No | 
 | ContentLanguage | Language type. Sets the value of `Content-Language` | String | No |
 |  Metadata | User-defined object metadata | Dict |  No | 
 

#### Response description
The response contains the attributes of the uploaded object in dict format:

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
| LastModified | Time the copied object was last modified | String |
| VersionId | Specifies the version ID of the copied object if versioning is enabled | String  |
| x-cos-copy-source-version-id | Version ID of the source object | String | 


### Deleting a single object

#### API description

This API is used to delete a specified object.

#### Method prototype

```
delete_object(Bucket, Key, **kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-delete-object)
```python
response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```
#### Sample request with all parameters

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
 | Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes | 
 | Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
 | VersionId | Version ID of the object if versioning is enabled | String  | No | 

#### Response description

This response contains information on the deleted object in dict format:

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

#### API description

The API is used to delete multiple objects.

#### Method prototype

```
delete_objects(Bucket, Delete={}, **kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-delete-multi-object)
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
#### Sample request with all parameters

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
 | Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes | 
 | Delete  | Describes the objects to be deleted and the way the deletion results are returned | Dict | Yes | 
 | Objects | Describes information on each object to be deleted | List | Yes | 
 | Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String |
 | VersionId | Specifies the version IDs of the objects to be deleted if versioning is enabled. | String  | No |
 | Quiet | Specifies how the deletion results are returned. Valid values: 'true', only information on failed deletions is returned; 'false', information on all deletions is returned. Default value: 'false' | String | No |

#### Response description
This response contains the deletion results in dict format:
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
 | Deleted | Information on the successfully deleted objects |  List |
 | Key | Paths to the successfully deleted objects | String |
 | VersionId | Version IDs of the successfully deleted objects | String |
 | DeleteMarker | Identifies whether the successfully deleted object is a delete marker | String |
 | DeleteMarkerVersionId | Version IDs of the delete markers of the successfully deleted objects | String |
 | Error  |  Information on the objects that failed to be deleted | List |
 | Key | Paths to the objects that failed to be deleted | string |
 | VersionId | Version IDs of the objects that failed to be deleted | String |
 | Code | Error codes for the objects that failed to be deleted | string |
 | Message | Error messages for the objects that failed to be deleted | string |


### Restoring an archived object 

#### API description

This API is used to retrieve an archived object for access.

#### Method prototype

```
restore_object(Bucket, Key, RestoreRequest={}, **kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-restore-object)
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
#### Sample request with all parameters

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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| RestoreRequest | Describes the rules of the retrieved temporary object | Dict | Yes |
| Days | Specifies the number of days before the temporary object expires | Int | Yes |
| CASJobParameters | Describes the configuration of the restoration type | Dict | No |
| Tier | Describes the object’s restoration mode. Valid values: 'Expedited', 'Standard', and 'Bulk' | String| No |

#### Response description
This method returns None.


### Extracting object content 

#### API description

This API is used to extract content from a specific object.

#### Method prototype

```
select_object_content(Bucket, Key, Expression, ExpressionType, InputSerialization, OutputSerialization, RequestProgress=None, **kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-select-object-content)
```python
response = client.select_object_content(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expression='Select * from COSObject',
    ExpressionType='SQL',
    InputSerialization={
        'CompressionType': 'NONE',
        'JSON': {
            'Type': 'LINES'
        }
    },
    OutputSerialization={
        'CSV': {
            'RecordDelimiter': '\n'
        }
    }
)
```
#### Sample request with all parameters

```python
response = client.select_object_content(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expression='Select * from COSObject',
    ExpressionType='SQL',
    InputSerialization={
        'CompressionType': 'GZIP',
        'JSON': {
            'Type': 'LINES'
        }
    },
    OutputSerialization={
        'CSV': {
            'RecordDelimiter': '\n'
        }
    },
    RequestProgress={
        'Enabled': 'FALSE'
    }
)
```
#### Parameter description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
|Expression| SQL expression, representing the extract operation you need to initiate | String| Yes |
| ExpressionType | Expression type, which is an extension. Currently, only SQL expressions and parameters are supported. | String | Yes |
|InputSerialization| Specifies the format of the object to extract. For more information, see [Sample request](https://intl.cloud.tencent.com/document/product/436/32360#.E8.AF.B7.E6.B1.82)| Dict | Yes|
|OutputSerialization| Specifies the output format of extraction results. For more information, see [Sample request](https://intl.cloud.tencent.com/document/product/436/32360#.E8.AF.B7.E6.B1.82)| Dict | Yes|
| RequestProgress | Specifies whether to return the query progress information (QueryProgress). If this parameter is used, COS Select will periodically return the query progress information. | Dict| No |

#### Response description
The response contains the content and metadata of the downloaded object in dict format.
```python
{
    'Body': EventStream(),
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


## Multipart Operations
Operations related to multipart uploads include the following:

- Uploading objects with multipart upload: initializing a multipart upload, uploading parts, and completing a multipart upload.
- Resuming a multipart upload: querying uploaded parts, uploading remaining parts, and completing a multipart upload.
- Deleting uploaded parts.

### Querying a multipart upload

#### API description

This API is used to query in-progress multipart uploads in a specified bucket.

#### Method prototype

```
list_multipart_uploads(Bucket, Prefix="", Delimiter="", KeyMarker="", UploadIdMarker="", MaxUploads=1000, EncodingType="", **kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-list-multi-upload)
```python
response = client.list_multipart_uploads(
    Bucket='examplebucket-1250000000',
    Prefix='dir'
)
```
#### Sample request with all parameters

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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Prefix | Filters multipart uploads by object key prefixed with the value of this parameter. It is left empty by default. | String | No | 
| Delimiter | A separator which is left empty by default. | String | No |
| KeyMarker | Specifies the key after which the multipart upload listing should begin. It is used together with `UploadIdMarker`. | String | No |
| UploadIdMarker | Specifies the upload ID after which the multipart upload list should begin. It is used together with `KeyMarker`. If `KeyMarker` is not specified, `UploadIdMarker` will be ignored. | String | No |
| MaxUploads | Maximum number of multipart uploads returned at a time; the default value is 1000. | Int | No | 
| EncodingType | Indicates the encoding method of the returned value. It’s left empty by default. Valid value: `url` | String | No |

#### Response description

This response contains information on the multipart uploads in dict format:

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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | 
| Prefix | Filters multipart uploads by object key prefixed with the value of this parameter. It is left empty by default. | String |
| Delimiter | A separator which is left empty by default. | String |
| KeyMarker | Specifies the key after which the multipart upload listing should begin. It is used together with `UploadIdMarker`. | Sring |
| UploadIdMarker | Specifies the upload ID after which the multipart upload listing should begin. It is used together with `KeyMarker`. If `KeyMarker` is not specified, `UploadIdMarker` will be ignored. | String |
| NextKeyMarker | Specifies the key after which the next multipart upload listing should begin if `IsTruncated` is set to `true`. | String |
| NextUploadIdMarker | Specifies the upload ID after which the next multipart upload listing should begin if `IsTruncated` is set to `true`. | String |
| MaxUploads | Maximum number of multipart uploads returned at a time; the default value is 1000. | int |
| IsTruncated | Indicates whether the returned multipart upload list is truncated | String |
| EncodingType | Indicates the encoding method of the returned value. It’s left empty by default. Valid value: `url` | String |
| Upload | Lists information on all multipart uploads, including 'UploadId', 'StorageClass', 'Key', 'Owner', 'Initiator', 'Initiated' | List |
| CommonPrefixes | Groups all keys starting with `Prefix` and ending with `Delimiter` as a common prefix | List |


### Initializing a multipart upload

#### API description

This API is used to initialize a multipart upload operation and obtain its uploadId.

#### Method prototype

```
create_multipart_upload(Bucket, Key, **kwargs):
```
#### Sample request

[//]: # (.cssg-snippet-init-multi-upload)
```python
response = client.create_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    StorageClass='STANDARD'
)
```
#### Sample request with all parameters

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
#### Parameter description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
 | Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
 | StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No | 
 | Expires | Sets `Expires`. | String | No |
 | CacheControl | Cache policy. Sets `Cache-Control` | String | No | 
 | ContentType | Content type. Sets `Content-Type` | String | No | 
 | ContentDisposition | File name. Sets `Content-Disposition` | String | No | 
 | ContentEncoding | Encoding format. Sets `Content-Encoding` | String | No | 
 | ContentLanguage | Language type. Sets `Content-Language` | String | No |
 |  Metadata | User-defined object metadata | Dict |  No |
 | ACL | Sets the object ACL, e.g. 'private', 'public-read'|String| No |
| GrantFullControl | Grants full permission in the format: `id="OwnerUin"` | String | No |
| GrantRead | Grants read permission in the format: `id="OwnerUin"` | String | No |

#### Response description

This response contains information on the initialization of the multipart upload in dict format:

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
| Bucket | Bucket name in the format: `BucketName-APPID` | String |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String |

### Uploading a part

This API is used to upload a part in a multipart upload.

#### Method prototype

```
upload_part(Bucket, Key, Body, PartNumber, UploadId, **kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-upload-part)
```python
# Note: a maximum of 10,000 parts can be uploaded in a multipart upload
response = client.upload_part(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Body=b'b'*1024*1024,
    PartNumber=1,
    UploadId='exampleUploadId'
)
```
#### Sample request with all parameters

```python
# Note: a maximum of 10,000 parts can be uploaded in a multipart upload
response = client.upload_part(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Body=b'bytes'|file,
    PartNumber=1,
    UploadId='string',
    EnableMD5=False|True,
    ContentLength='123',
    ContentMD5='string',
    TrafficLimit='1048576'
)
```
#### Parameter description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
 | Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
 | Body  | Content of the parts to be uploaded. It can be a local file stream or an input stream | file/bytes |  Yes|
 | PartNumber | Identifies the part number | int | Yes |
 | UploadId | ID of the multipart upload | string | Yes |
 | EnableMD5 | Indicates whether the SDK needs to calculate Content-MD5. This feature is disabled by default. The upload will take longer if it is enabled | Bool | No | 
 | ContentLength | Sets the length of the request content | string | No |
 | ContentMD5 | Sets the MD5 checksum of the uploaded object | String | No |
 |  TrafficLimit | Specifies the bandwidth limit for a single request in bit/s. Value range: 819200 - 838860800, i.e., 100 KB/s - 100 MB/s | String |  No |
 
#### Response description

This response contains the attributes of the uploaded parts in dict format:

```python
{
    'ETag': 'string'
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- | 
| ETag | MD5 hash of the uploaded part | String |

### Copying a part

This API is used to upload a part by copying data from an existing object as data source.

#### Method prototype

```
upload_part_copy(Bucket, Key, PartNumber, UploadId, CopySource, CopySourceRange='', **kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-upload-part-copy)
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
#### Sample request with all parameters

```python
response = client.upload_part_copy(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    PartNumber=100,
    UploadId='string',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'sourceObject', 
        'Region': 'COS_REGION', #Replace with the source bucket’s region
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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| PartNumber | Identifies the part number | Int | Yes |
| UploadId | ID of the multipart upload | String | Yes |
| CopySource  | Path of the source object to be copied, including `Bucket`, `Key`, `Region`, `VersionId` |  Dict | Yes |
| CopySourceRange | Describes the byte range of the source object to be copied in the format: `bytes=first-last`. The entire source will be copied by default if no range is specified | String | No |
| CopySourceIfMatch | Copies the source object only if its Etag matches the specified value | String | No |
| CopySourceIfModifiedSince | Copies the source object only if it is modified after the specified time | String | No |
| CopySourceIfNoneMatch | Copies the source object only if its Etag does not match the specified value | String | No |
| CopySourceIfUnmodifiedSince | Copies the source object only if it is not modified after the specified time | String | No |

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
| LastModified | Time the copied part was last modified | string |
| x-cos-copy-source-version-id | Version ID of the source object | String | 

### Querying uploaded parts

#### API description

This API is used to query the uploaded parts of a specific multipart upload operation.

#### Method prototype

```
list_parts(Bucket, Key, UploadId, MaxParts=1000, PartNumberMarker=0, EncodingType='', **kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-list-parts)
```python
response = client.list_parts(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId='exampleUploadId'
)
```
#### Sample request with all parameters

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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| UploadId | ID of the multipart upload | String | Yes |
| MaxParts | Maximum number of parts returned at a time; the default value is 1,000. | Int | No |
| PartNumberMarker | Specifies the part after which to begin listing; the default value is 0, meaning the parts are listed starting with the first part. | Int | No |
| EncodingType | Specifies the encoding method of the returned value. It is left empty by default. Valid value: `url`. | String | No |

#### Response description

This response contains information on all the uploaded parts in dict format:

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
| Bucket | Bucket name in the format: `BucketName-APPID` | String |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | 
| UploadId | ID of the multipart upload | String | 
| EncodingType | Indicates the encoding method of the returned value. It’s left empty by default. Valid value: `url` | String |
| MaxParts | Maximum number of parts returned at a time; the default value is 1000. | String |
| IsTruncated | Indicates whether the returned list is truncated | String |
| PartNumberMarker | Specifies the part after which to being listing; the default value is 0, meaning the parts are listed starting with the first part. | String |
| NextPartNumberMarker | Specifies the part after which the next part listing should begin | String |
 | StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String |
| Part | Information on the uploaded parts, including `ETag`, `PartNumber`, `Size`, `LastModified` | String |
 | Initiator | Creator of the multipart upload, including `DisplayName`, and `ID` | Dict | 
 | Owner | Information on the object owner, including `DisplayName` and `ID` | Dict | 



### Completing a multipart upload

#### API description

This API is used to complete a multipart upload.

#### Method prototype

```
complete_multipart_upload(Bucket, Key, UploadId, MultipartUpload={}, **kwargs)
```
#### Sample request

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
#### Parameter description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes | 
| Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes | 
| UploadId | ID of the multipart upload | String | Yes | 
| MultipartUpload | Information on all parts, including `ETag` and `PartNumber` | Dict | 

#### Response description

The response contains information on the merged object in dict format:

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
 | ETag | The unique tag of a merged object. This value does not represent the MD5 checksum of the object content, but is used only to verify the uniqueness of the object as a whole. To verify the object content, you can check the ETag of each part during the upload process | String | 
 | Bucket | Bucket name in the format: `BucketName-APPID` | String | 
 | Location | URL address | String | 
 | Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String |


### Aborting a multipart upload

#### API description

This API is used to abort a multipart upload and delete the uploaded parts.

#### Method prototype

```
abort_multipart_upload(Bucket, Key, UploadId, **kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-abort-multi-upload)
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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| UploadId | ID of the multipart upload | String | Yes |

#### Response description
This method returns None.





 ## Advanced APIs (recommended)

### Uploading an object (checkpoint restart)

#### API description
The advanced upload API can automatically select between simple upload and multipart upload according to the file size. It uses simple upload for files smaller than or equal to 20 MB and multipart upload for files larger than 20 MB. It also supports automatic checkpoint restart for suspended multipart uploads.

#### Method prototype

```
upload_file(Bucket, Key, LocalFilePath, PartSize=1, MAXThread=5, **kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-transfer-upload-file)
```python
response = client.upload_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    LocalFilePath='local.txt',
    EnableMD5=False
)
```

#### Sample request with all parameters
```python
response = client.upload_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    LocalFilePath='local.txt',
    PartSize=1,
    MAXThread=5,
    EnableMD5=False|True,
    ACL='private'|'public-read',
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
    },
    TrafficLimit='1048576'
)
```
#### Parameter description


| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
 | Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes | 
| LocalFilePath | Path to the local file | String | Yes |
| PartSize | Part size; the default value is 1 MB |  Int | No |
|  MAXThread  | Maximum number of threads for concurrent multipart uploads; the default value is 5 |  Int |  No |
| EnableMD5 | Specifies whether the SDK needs to calculate the Content-MD5 value. This feature is disabled by default. The upload will take longer if it is enabled | Bool | No | 
| ACL | Sets the object ACL, e.g. 'private', 'public-read' | String | No |
| GrantFullControl | Grants full permission in the format: `id="OwnerUin"` | String | No |
| GrantRead | Grants read permission in the format: `id="OwnerUin"` | String | No |
 | StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
 | Expires | Sets `Expires`. | String | No | 
 | CacheControl | Cache policy. Sets `Cache-Control` | String | No |
 | ContentType | Content type. Sets the value of `Content-Type`. | String | No |  
 | ContentDisposition | File name. Sets `Content-Disposition` | String | No |
 | ContentEncoding | Encoding format. Sets `Content-Encoding`. | String | No |
 | ContentLanguage | Language type. Sets `Content-Language`  | String | No |
 | ContentLength | Sets the length of the request content  | string | No | 
 | ContentMD5 | Sets the MD5 checksum of the uploaded object | String | No | 
 |  Metadata | User-defined object metadata | Dict |  No |
 |  TrafficLimit | Specifies the bandwidth limit in bit/s for a single request (or a single thread for the advanced APIs). Value range: 819200 - 838860800, i.e., 100 KB/s - 100 MB/s | String |  No |

#### Response description
The response contains the attributes of the uploaded object in dict format:

```python
{
    'ETag': 'string'
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- |
| ETag | This value does not represent the MD5 checksum of the object content, but is used only to verify the uniqueness of the object as a whole during multipart upload | String |


### Downloading an object (checkpoint restart)

#### Feature description
The advanced download API can automatically select between simple download and multipart download according to the file size. It uses simple download for files smaller than or equal to 20 MB and multipart upload for files larger than 20 MB. It also supports automatic checkpoint restart for suspended multipart downloads.

#### Method prototype

```
download_file(Bucket, Key, DestFilePath, PartSize=20, MAZThread=5, EnableCRC=False, **Kwargs)
```
#### Sample request

[//]: # (.cssg-snippet-transfer-upload-file)
```python
response = client.download_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    DestFilePath='local.txt'
)
```

#### Sample request with all parameters
```python
response = client.download_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    DestFilePath='local.txt',
    PartSize=1,
    MAXThread=5,
    EnableCRC=True,
    TrafficLimit='1048576'
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
 | Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes | 
 | key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes | 
 |  DestFilePath  | The destination local path to the downloaded file |  String |  Yes |
 | PartSize | Part size for multipart download; default value: 20 MB |  Int | No |
 |  MAXThread  | Maximum number of concurrent threads for a multipart download; the default value is 5 |  Int |  No |
 | EnableCRC | Indicates whether to enable CRC check for local and remote files. Default: `False` | Bool | No |
 |  TrafficLimit | Specifies the bandwidth limit in bit/s for a single request (or a single thread for the advanced APIs). Value range: 819200 - 838860800, i.e., 100 KB/s - 100 MB/s | String |  No |
 |  IfMatch  | Returns the object only if the Etag matches the specified content |String  | No |  
 | IfModifiedSince | Returns the object only if it is modified after the time specified in GMT format | String | No |
 |  IfNoneMatch  |  Returns the object only if the Etag does not match the specified content | String  | No | 
 | IfUnmodifiedSince | Returns the object only if it is modified before or at the time specified in GMT format  | String | No |
 | ResponseCacheControl | Sets the value of `Cache-Control` in the response header | String | No | 
 | ResponseContentDisposition | Sets the value of `Content-Disposition` in the response header | String | No | 
 | ResponseContentEncoding | Sets the value of `Content-Encoding` in the response header | String | No |
 | ResponseContentLanguage | Sets the value of `Content-Language` in the response header | String | No | 
 | ResponseContentType | Sets the value of `Content-Type` in the response header | String | No |
 | ResponseExpires | Sets the value of `Expires` in the response header | String | No | 
 | VersionId | Version ID of the object to be downloaded | String | No |

#### Response description
None


## Client-Side Encryption

#### Feature description

The SDK for Python allows client-side encryption that encrypts files before upload and decrypts them at the time of download. There are two types of client-side encryption: AES (symmetric) and RSA (asymmetric).
These two types are for the encryption of generated random keys. File data, however, is always encrypted symmetrically using AES256.
Client-side encryption is suitable for users who store sensitive data. As it may affect the upload speed, the SDK uses the serial method for multipart upload.

### Encryption for upload

1. Before each upload, COS generates a random symmetric key which is encrypted through the customer-provided symmetric or asymmetric key. The encryption result is then base64-encoded and stored in object metadata.
2. During the upload, the file is encrypted in memory using AES256 algorithm.

### Decryption for download

1. Get the necessary encryption information from the metadata of the file, base64-decode it, and then decrypt it using the customer managed key (CMK) to get the encryption key at upload.
2. Use the resulting key to decrypt the downloaded input stream using AES256.

#### Sample request

Example 1: using symmetric AES256 encryption for random keys generated each time.

[//]: # (.cssg-snippet-put-object-cse-c-aes)
```python
# Initialize user authentication information (SECRET_ID, SECRET_KEY)
SECRET_ID = "COS_SECRETID"
SECRET_KEY = "COS_SECRETKEY"
REGION = "COS_REGION"
conf = CosConfig(
    Region=REGION,
    SecretId=SECRET_ID,
    SecretKey=SECRET_KEY,
)

# Method 1: initializing the encryption client using the key value
aes_provider = AESProvider(aes_key='aes_key_value')

# Method 2: initializing the encryption client using the key path
aes_key_pair = AESProvider(aes_key_path='aes_key_path')

client_for_aes = CosEncryptionClient(conf, aes_provider)

# Upload an object, an operation fully compatible with non-encryption clients. For more information, see PUT Object documentation
response = client_for_aes.put_object(
                        Bucket='examplebucket-1250000000',
                        Body=b'bytes'|file,
                        Key='exampleobject',
                        EnableMD5=False)

# Download an object, an operation fully compatible with non-encryption clients. For more information, see GET Object documentation
response = client_for_aes.get_object(
                        Bucket='examplebucket-1250000000',
                        Key='exampleobject')

# Multipart upload, an operation compatible with non-encryption clients. Except for the last part, the size of each part must be an integer multiple of 16 bytes
response = client_for_aes.create_multipart_upload(
                        Bucket='examplebucket-1250000000',
                        Key='exampleobject_upload')
uploadid = response['UploadId']
client_for_aes.upload_part(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                Body=b'bytes'|file,
                PartNumber=1,
                UploadId=uploadid)
response = client_for_aes.list_parts(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                UploadId=uploadid)
client_for_aes.complete_multipart_upload(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                UploadId=uploadid,
                MultipartUpload={'Part':response['Part']})

# Upload an object with checkpoint restart. The size of each part must be an integer multiple of 16 bytes
response = client_for_aes.upload_file(
    Bucket='test04-123456789',
    LocalFilePath='local.txt',
    Key=file_name,
    PartSize=10,
    MAXThread=10
)

```

Example 2: using asymmetric RSA encryption for random keys generated each time.

[//]: # (.cssg-snippet-put-object-cse-c-rsa)
```python
# Initialize user authentication information (SECRET_ID, SECRET_KEY)
SECRET_ID = "COS_SECRETID"
SECRET_KEY = "COS_SECRETKEY"
REGION = "COS_REGION"
conf = CosConfig(
    Region=REGION,
    SecretId=SECRET_ID,
    SecretKey=SECRET_KEY,
)

# Method 1: initializing the encryption client using the key value
rsa_key_pair = RSAProvider.get_rsa_key_pair('public_key_value', 'private_key_value')

# Method 2: initializing the encryption client using the key path
rsa_key_pair = RSAProvider.get_rsa_key_pair('public_key_path', 'private_key_path')

rsa_provider = RSAProvider(key_pair_info=rsa_key_pair)
client_for_rsa = CosEncryptionClient(conf, rsa_provider)

# Upload an object, an operation fully compatible with non-encryption clients. For more information, see PUT Object documentation
response = client_for_rsa.put_object(
                        Bucket='examplebucket-1250000000',
                        Body=b'bytes'|file,
                        Key='exampleobject',
                        EnableMD5=False)

# Download an object, an operation fully compatible with non-encryption clients. For more information, see GET Object documentation
response = client_for_rsa.get_object(
                        Bucket='examplebucket-1250000000',
                        Key='exampleobject')

# Multipart upload, an operation compatible with non-encryption clients. Except for the last part, the size of each part must be an integer multiple of 16 bytes
response = client_for_rsa.create_multipart_upload(
                        Bucket='examplebucket-1250000000',
                        Key='exampleobject_upload')
uploadid = response['UploadId']
client_for_rsa.upload_part(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                Body=b'bytes'|file,
                PartNumber=1,
                UploadId=uploadid)
response = client_for_rsa.list_parts(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                UploadId=uploadid)
client_for_rsa.complete_multipart_upload(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                UploadId=uploadid,
                MultipartUpload={'Part':response['Part']})

# Upload an object with checkpoint restart. The size of each part must be an integer multiple of 16 bytes
response = client_for_rsa.upload_file(
    Bucket='test04-123456789',
    LocalFilePath='local.txt',
    Key=file_name,
    PartSize=10,
    MAXThread=10
)
```
