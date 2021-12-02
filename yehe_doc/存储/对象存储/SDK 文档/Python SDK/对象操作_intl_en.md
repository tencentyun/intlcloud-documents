## Overview

This document provides an overview of APIs and SDK code samples related to simple operations, multipart operations, and other object operations.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Object)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying objects | Queries some or all the objects in a bucket |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying objects and their version history | Queries some or all the objects in a bucket and their version history. |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object | Uploads an object to a bucket. |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object. |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system. |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to the destination path. |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes an object from a bucket. |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket. |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access. |
| [SELECT Object content](https://intl.cloud.tencent.com/document/product/436/32360) | Extracting object content | Extracts content from a specified object. |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | Appending parts | Appends object parts to a bucket.                      |


**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads a file in parts. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying an object part | Copies a part of an object. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |




## Simple Operations

### Query objects

#### Description

This API is used to query some or all the objects in a bucket.

#### Method prototype

```
list_objects(Bucket, Delimiter="", Marker="", MaxKeys=1000, Prefix="", EncodingType="", **kwargs)
```
#### Sample 1: listing all objects in a bucket

[//]: # ".cssg-snippet-get-all-objects"
```python
response = client.list_objects(Bucket='examplebucket-1250000000')
if 'Contents' in response:
    for content in response['Contents']:
        print(content['Key'])
# Note: A maximum of 1,000 objects can be listed at a time. If there are too many objects, you need to list them in multiple responses (see sample 3).
```

#### Sample 2: listing objects with a specified prefix

[//]: # ".cssg-snippet-get-prefix-objects"
```python
# List objects prefixed with “folder”.
response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='folder' 
)

# List objects in the “folder1” directory: In COS, an object whose name ends with a slash (/) is considered a folder.
response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='folder1/' 
)
```

#### Sample 3: listing objects in multiple responses

[//]: # ".cssg-snippet-get-objects-by-page"
```python
# List objects in a bucket with multiple responses, and a maximum of 10 objects can be listed at a time.
marker = ""
while True:
    response = client.list_objects(
        Bucket='examplebucket-1250000000', Prefix='folder1/', Marker=marker, MaxKeys=10)
    if 'Contents' in response:
        for content in response['Contents']:
            print(content['Key'])

    if response['IsTruncated'] == 'false':
        break

    marker = response["NextMarker"]
```

#### Sample 4: listing objects and subdirectories in a directory

[//]: # ".cssg-snippet-get-files-and-subfolder"
```python
# List objects and subdirectories in “folder1”.
response = client.list_objects(
    Bucket='examplebucket-1250000000', Prefix='folder1/', Delimiter='/')
# Print the object list.
if 'Contents' in response:
    for content in response['Contents']:
        print(content['Key'])
# Print subdirectories.
if 'CommonPrefixes' in response:
    for folder in response['CommonPrefixes']:
        print(folder['Prefix'])
```

#### Sample request with all parameters

[//]: # ".cssg-snippet-get-bucket-with-delimiter"
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

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Prefix  |  Key prefix to query objects by, which is left empty by default | String  | No |
| Delimiter | Separator, left empty by default. For example, you can set it to `/` to indicate folders. | String | No |
| Marker | The object after which the returned list begins. Entries are listed in UTF-8 binary order by default. | String | No |
| MaxKeys | Maximum number of returned objects, which is `1000` (the maximum value allowed) by default | Int | No |
| EncodingType | Encoding method of the returned value. The value is not encoded by default. Valid value: `url` | String | No |

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

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| MaxKeys | Maximum number of returned objects, which is `1000` (the maximum value allowed) by default | String |
| Prefix   | Key prefix to filter objects by, which is left empty by default | String  | 
| Delimiter | Separator, left empty by default. For example, you can set it to `/` to indicate folders. | String |
| Marker | The object after which the returned list begins. Entries are listed in UTF-8 binary order by default. | String |
| NextMarker | The object after which the next returned list begins if `IsTruncated` is `true` | String |
| Name | Bucket name in the format of `BucketName-APPID` | String |
| IsTruncated   |  Whether the returned object list is truncated. | String |
| EncodingType | Encoding method of the returned value. The value is not encoded by default. Valid value: `url` | String | 
| Contents | List of all object metadata, including `ETag`, `StorageClass`, `Key`, `Owner`, `LastModified`, `Size` | List |
| CommonPrefixes | All objects starting with the specified prefix and ending with the specified delimiter | List |

### Querying objects and their version history 

#### Description

This API is used to query some or all the objects in a bucket and their version history.

#### Method prototype

```
list_objects_versions(Bucket, Prefix="", Delimiter="", KeyMarker="", VersionIdMarker="", MaxKeys=1000, EncodingType="", **kwargs)
```
#### Sample request

[//]: # ".cssg-snippet-list-objects-versioning"
```python
response = client.list_objects_versions(
    Bucket='examplebucket-1250000000',
    Prefix='string'
)
```

#### Sample request with all parameters

[//]: # ".cssg-snippet-list-objects-versioning-next-page"
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

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Prefix  |  Key prefix to query objects by, which is left empty by default | String  | No |
| Delimiter | Separator, left empty by default. For example, you can set it to `/` to indicate folders. | String | No |
| KeyMarker | The key of the object after which the returned list begins. Objects are listed in UTF-8 binary order by default. | String | No |
| VersionIdMarker | The version ID of the object after which the returned object list begins. Objects are listed in UTF-8 binary order by default. | String  |  No |
| MaxKeys | Maximum number of returned objects, which is `1000` (the maximum value allowed) by default | Int | No |
| EncodingType | Encoding method of the returned value. The value is not encoded by default. Valid value: `url` | String | No |

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

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| MaxKeys | Maximum number of returned objects, which is `1000` (the maximum value allowed) by default | String |
| Prefix   | Key prefix to filter objects by, which is left empty by default | String  | 
| Delimiter | Separator, left empty by default. For example, you can set it to `/` to indicate folders. | String |
| KeyMarker | The key of the object after which the returned object list begins. Objects are listed in UTF-8 binary order by default. | String |
| VersionIdMarker | The version ID of the object after which the returned object list begins. Objects are listed in UTF-8 binary order by default. | String  |
| NextKeyMarker | The key of the object after which the next returned list begins if `IsTruncated` is `true` | String |
| NextVersionIdMarker | The version ID of the object after which the next returned list begins if `IsTruncated` is `true` | String |
| Name | Bucket name in the format of `BucketName-APPID` | String |
| IsTruncated   |  Whether the returned object list is truncated. | String |
| EncodingType | Encoding method of the returned value. The value is not encoded by default. Valid value: `url` | String | 
| Version | List of the metadata of all objects with multiple versions, including `ETag`, `StorageClass`, `Key`, `VersionId`, `IsLatest`, `Owner`, `LastModified`, and `Size`  | List |
| DeleteMarker | List of the metadata of all delete markers, including `Key`, `VersionId`, `IsLatest`, `Owner`, and `LastModified` | List |
| CommonPrefixes | All objects starting with the specified prefix and ending with the specified delimiter | List |

### Uploading an object using simple upload

#### Description

This API (`PUT Object`) is used to upload an object to a bucket.

#### Method prototype

```
put_object(Bucket, Body, Key, **kwargs)
```
#### Sample 1. Simple object upload

[//]: # ".cssg-snippet-put-object"
```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos import CosServiceError
from qcloud_cos import CosClientError

import sys
import logging

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://www.qcloud.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  # Get the configured object
client = CosS3Client(config)

# Simple upload using file stream
file_name = 'test.txt'
with open('test.txt', 'rb') as fp:
    response = client.put_object(
        Bucket='examplebucket-1250000000',  # Bucket name format: BucketName-APPID
        Body=fp,
        Key=file_name,
        StorageClass='STANDARD',
        ContentType='text/html; charset=utf-8'
    )
    print(response['ETag'])

# Byte stream (upload in whole)
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'abcdefg',
    Key=file_name
)
print(response['ETag'])

# Local path (upload in whole)
response = client.put_object_from_local_file(
    Bucket='examplebucket-1250000000',
    LocalFilePath='local.txt',
    Key=file_name,
)
print(response['ETag'])

# HTTP header (upload in whole)
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'test',
    Key=file_name,
    ContentType='text/html; charset=utf-8'
)
print(response['ETag'])

# Custom header (upload in whole)
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'test',
    Key=file_name,
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    }
)
print(response['ETag'])
```
#### Sample 2: creating a directory
In COS, a directory is an object whose name ends with a slash (/). Therefore, you can call the `Put Object` API.

[//]: # ".cssg-snippet-put-object-diretory"
```python
# Create a directory.
dir_to_create='path/to/create/dir/'
response = client.put_object(
    Bucket='examplebucket-1250000000',  # Bucket name format: BucketName-APPID
    Key=dir_to_create,
    Body=b'',
)
print(response)
```
#### Sample 3: uploading an object to a specified directory

[//]: # ".cssg-snippet-put-object-comp"
```python
# When you upload an object whose name is separated with slashes, a directory that contains this object will be created automatically. To upload a new object to this COS directory, set the key prefix of the object to this directory.
dir_name = 'path/to/dir/'
file_name = 'test.txt'
object_key = dir_name + file_name
with open('test.txt', 'rb') as fp:
    response = client.put_object(
        Bucket='examplebucket-1250000000',  # Bucket name format: BucketName-APPID
        Body=fp,
        Key=object_key,
        StorageClass='STANDARD',
        ContentType='text/html; charset=utf-8'
    )
    print(response['ETag'])
```
#### Sample 4: limiting the upload speed
Use `TrafficLimit` to limit the upload speed, in bit/s. The speed range is 819200 to 838860800, that is, 100 KB/s to 100 MB/s.

[//]: # ".cssg-snippet-put-object-by-limit"
```python
with open('test.bin', 'rb') as fp:
    response = client.put_object(
        Bucket='examplebucket-1250000000',  # Bucket name format: BucketName-APPID
        Key='exampleobject',
        Body=fp,
        TrafficLimit='819200'
    )
    print(response['ETag'])
```

#### Sample request with all parameters
[//]: # ".cssg-snippet-put-object-comp"
```python
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes'|file,
    Key='exampleobject',
    EnableMD5=False|True,
    ACL='private'|'public-read', # Please note that the maximum number (1000) of ACLs allowed may be reached if you use this parameter
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


| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
|  Body  | Content of the object to be uploaded. It can be a file stream or a byte stream. |  file/bytes | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| EnableMD5 | Whether to calculate the Content-MD5 checksum, which will extend the upload time. It’s not calculated by default. | Bool | No |
| ACL | ACL of the object, such as `private` or `public-read`|String| No |
| GrantFullControl | Grants full permission. Format: `id="OwnerUin"` | String | No |
| GrantRead | Grants read permission. Format: `id="OwnerUin"` | String | No |
| StorageClass | Storage class of the object, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String     | No |
| Expires | Expiration time | String | No |
| CacheControl | Cache policy | String | No |
| ContentType | Content type | String | No |
| ContentDisposition | Object name | String | No |
| ContentEncoding | Encoding type  | String | No |
| ContentLanguage | Language type  | String | No |
| ContentLength | Length of the content  | String | No |
| ContentMD5 | MD5 checksum of the uploaded object, which is used for verification | String | No |
| Metadata | User-defined object metadata. This parameter must start with `x-cos-meta`; otherwise, it will be ignored. | Dict | No |
|  TrafficLimit | Bandwidth limit for a single request in bit/s. Value range: 819200-838860800, i.e., 100 KB/s - 100 MB/s | String |  No |

#### Response description
The response contains the attributes of the copied object in dict format:

```python
{
    'ETag': 'string',
    'x-cos-version-id': 'string'
}
```


| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| ETag | MD5 checksum of the uploaded object | String |
| x-cos-version-id | Version ID of the object if versioning is enabled | String  |



### Querying object metadata

#### Description

This API is used to query object metadata.

#### Method prototype

```
head_object(Bucket, Key, **kwargs)
```
#### Sample request

[//]: # ".cssg-snippet-head-object"
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
    IfModifiedSince='Wed, 28 Oct 2020 20:30:00 GMT',
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| VersionId | Version ID of the object if versioning is enabled  | String  | No |
| IfModifiedSince |  Required modification time. Metadata is returned only if the object has been modified after the specified time.  | String | No |

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


| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| ETag | For multipart uploads, this value does not represent the MD5 checksum of the object content, but is used only to verify the uniqueness of the object. | String |
| Last-Modified | Time when the object was last modified | String |
| Cache-Control | Cache policy. Standard HTTP header | String | 
| Content-Type | Content type. Standard HTTP header | String | 
| Content-Disposition | Filename. Standard HTTP header | String |
| Content-Encoding | Encoding type. Standard HTTP header | String | 
| Content-Language | Language type. Standard HTTP header | String | 
| Content-Length  | Object size | String |
| Expires | Cache expiration time. Standard HTTP header | String |
| x-cos-meta-* | User-defined object metadata. This parameter must start with `x-cos-meta`; otherwise, it will be ignored.  | String |
| x-cos-version-id | Version ID of the object if versioning is enabled | String  |


### Download an object

#### Description

This API (`GET Object`) is used to download an object.

#### Method prototype

```
 get_object(Bucket, Key, **kwargs)
```
#### Sample 1: downloading an object

[//]: # ".cssg-snippet-get-object"
```python
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
response['Body'].get_stream_to_file('exampleobject')
```
#### Sample 2: limiting the download speed

[//]: # ".cssg-snippet-get-object-by-limit"
```python
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    TrafficLimit='819200'
)
response['Body'].get_stream_to_file('exampleobject')
```
#### Sample 3: partially downloading an object

[//]: # ".cssg-snippet-get-object-by-range"
```python
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Range='bytes=0-100'
)
response['Body'].get_stream_to_file('exampleobject')
```
#### Sample request with all parameters

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
    VersionId='string',
    TrafficLimit='819200'
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| Range | Byte range of the object to download. Format: `bytes=first-last` | String | No |
|  IfMatch  | `ETag` that needs to be matched. The object is downloaded only if its `ETag` matches the value. | String  | No |
| IfModifiedSince |  Required modification time. The object is downloaded only if it has been modified after the specified time.  | String | No |
|  IfNoneMatch  |  `ETag` that cannot be matched. The object is downloaded only if its `ETag` does not match the value. | String  | No |
| IfUnmodifiedSince | Required unmodified time. The object is downloaded only if it has not been modified since the specified time.   | String | No |
| ResponseCacheControl | `Cache-Control` of the response header | String | No |
| ResponseContentDisposition | `Content-Disposition` of the response header | String | No |
| ResponseContentEncoding | `Content-Encoding` of the response header | String | No |
| ResponseContentLanguage | `Content-Language` of the response header | String | No |
| ResponseContentType | `Content-Type` of the response header | String | No |
| ResponseExpires | `Expires` of the response header | String | No |
| VersionId | Version ID of the object to download| String | No |
|  TrafficLimit | Bandwidth limit in bit/s for a single request (or a single thread for the advanced download API). Value range: 819200 - 838860800, i.e., 100 KB/s - 100 MB/s | String |  No |

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
      <th>Parameter Name</th>
      <th>Description</th>
      <th>Type</th>
   </tr>
   <tr>
      <td>Body</td>
      <td>Content of the downloaded object. You can use the `get_raw_stream()` method to get a file stream and the `get_stream_to_file(local_file_path)` method to download the object’s content to a specified local file.</td>
      <td>StreamBody</td>
   </tr>
   <tr>
      <td>ETag</td>
      <td>MD5 checksum of the object</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Last-Modified</td>
      <td>Time when the object was last modified</td>
      <td>String</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Accept-Ranges</td>
      <td>Range unit. HTTP standard header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Range</td>
      <td>Content range. HTTP standard header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Cache-Control</td>
      <td>Cache policy. HTTP standard header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>Content type. HTTP standard header</td>
      <td>String</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Content-Disposition</td>
      <td>Filename. HTTP standard header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Encoding</td>
      <td>Encoding format. HTTP standard header</td>
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
      <td>User-defined object metadata. It must start with `x-cos-meta`; otherwise, it will be ignored.</td>
      <td>String</td>
   </tr>
   <tr>
      <td>x-cos-version-id</td>
      <td>Version ID of the object if versioning is enabled</td>
      <td>String</td>
   </tr>
</table>



### Copying an object

#### Description

This API is used to copy an existing object to a destination path.

#### Method prototype

```
copy_object(Bucket, Key, CopySource, CopyStatus='Copy', **kwargs)
```
#### Sample 1: copying an object
If the source and destination objects are different, a new object will be generated. The metadata of the destination object will be copied from the source.

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
#### Sample 2: modifying object metadata
If the source and destination objects are the same and `CopyStatus` is set to `Replaced`, you can modify the object metadata via the header.

[//]: # ".cssg-snippet-copy-object-metadata"
```python
response = client.copy_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou'
    },
    CopyStatus='Replaced', 
    ContentType='text/plain', # Modify object ContentType.
    Metadata={'x-cos-meta-key1': 'value1', 'x-cos-meta-key2': 'value2'} # Modify custom metadata.
)
```
#### Sample 3: modifying storage class
If the source and destination objects are the same and `CopyStatus` is set to `Replaced`, you can use `StorageClass` to modify the storage class.

[//]: # ".cssg-snippet-copy-object-storage-class"
```python
response = client.copy_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    CopySource={
        'Bucket': 'examplebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou'
    },
    CopyStatus='Replaced', 
    StorageClass='STANDARD_IA' # Modify the storage class to STANDARD_IA.
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
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| CopySource  | Path of the source object to copy, which contains `Bucket`, `Key`, `Region`, and `VersionId` |  Dict | Yes |
| CopyStatus | Valid values: `Copy`: ignores the configured metadata and copies the file directly; `Replaced`: modifies the metadata according to the configured metadata. If the destination path is identical to the source path, this parameter must be set to `Replaced`. | String | Yes |
| ACL  | ACL of the object, such as private or public-read                      | String | No |
| GrantFullControl | Grants full permission. Format: `id="OwnerUin"`| String | No |
| GrantRead | Grants read permission. Format: `id="OwnerUin"`| String | No |
| StorageClass | Storage class of the object. Valid values: `STANDARD` (default); `STANDARD_IA`. | String | No |
| Expires | Expiration time | String | No |
| CacheControl | Cache policy | String | No |
| ContentType | Content type | String | No |
| ContentDisposition | Filename | String | No |
| ContentEncoding | Encoding type | String | No |
| ContentLanguage | Language type | String | No |
|  Metadata | User-defined object metadata | Dict |  No |


#### Response description
The response contains the attributes of the copied object in dict format:

```python
{
    'ETag': 'string',
    'LastModified': 'string',
    'VersionId': 'string',
    'x-cos-copy-source-version-id': 'string'
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| ETag | MD5 checksum of the copied object | String |
| LastModified | Time when the copied object was last modified | String |
| versionId | Specifies the version ID of the copied object if versioning is enabled | String |
| x-cos-copy-source-version-id | Version ID of the source object | String |


### Deleting an object

#### Description

This API (`DELETE Object`) is used to delete a specified object.

#### Method prototype

```
delete_object(Bucket, Key, **kwargs)
```
#### Sample 1. Deleting an object

[//]: # ".cssg-snippet-delete-object"
```python
response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### Sample 2. Deleting a directory

In COS, a directory is an object whose path ends with a slash (/). Therefore, you can call the `Delete Object` API to delete a directory.

[//]: # ".cssg-snippet-delete-object"
```python
try:
    to_delete_dir='path/to/delete/dir/'
    response = client.delete_object(
        Bucket='examplebucket-1250000000',
        Key=to_delete_dir,
    )
    print(response)
except CosServiceError as e:
    print(e.get_status_code())
```

#### Sample 3: Deleting objects with a specified prefix

[//]: # ".cssg-snippet-delete-multi-object"
```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos import CosServiceError
from qcloud_cos import CosClientError

import sys
import os
import logging

# Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://www.qcloud.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  # Get the configured object
client = CosS3Client(config)

# Delete objects with the specified prefix.
bucket = 'examplebucket-1250000000'
is_over = False
marker = ''
prefix = 'root/logs'
while not is_over:
    try:
        response = client.list_objects(Bucket=bucket, Prefix=prefix, Marker=marker)
        if response['Contents']:
            for content in response['Contents']:
                print("delete object: ", content['Key'])
                client.delete_object(Bucket=bucket, Key=content['Key'])

            if response['IsTruncated'] == 'false':
                is_over = True
                marker = response['Marker']
    except CosServiceError as e:
        print(e.get_origin_msg())
        print(e.get_digest_msg())
        print(e.get_status_code())
        print(e.get_error_code())
        print(e.get_error_msg())
        print(e.get_resource_location())
        print(e.get_trace_id())
        print(e.get_request_id())
        break
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

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| VersionId | Version ID of the object if versioning is enabled  | String  | No |

#### Response description

This response contains information on the deleted object in dict format:

```python
{
    'x-cos-version-id': 'string',
    'x-cos-delete-marker': 'true'|'false',
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| x-cos-version-id    | Version ID of the deleted object  | String |
| x-cos-delete-marker | Whether the deleted object is a delete marker | String |



### Deleting multiple objects

#### Description

The API (DELETE Multiple Objects) is used to delete multiple objects.

#### Method prototype

```
delete_objects(Bucket, Delete={}, **kwargs)
```
#### Sample request

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

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Delete  | Response method and target objects to delete  | Dict | Yes |
| Objects | Information of each object to delete | List | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String |No |
| VersionId | Version ID of the target object if versioning is enabled | String  | No |
| Quiet | Response method. Valid values: `true`: returns only the failed results; `false` (default): returns all results. | String | No |

#### Response description
The response contains the deletion results in dict format:
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

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| Deleted | Information on the successfully deleted objects |  List |
| Key | Paths to the successfully deleted objects | String |
| VersionId | Version IDs of the successfully deleted objects | String |
| DeleteMarker | Whether a successfully deleted object is a delete marker | String |
| DeleteMarkerVersionId | Version IDs of the delete markers of the successfully deleted objects | String |
| Error  |  Information on the objects that failed to be deleted | List |
| Key | Paths to the objects that failed to be deleted | String |
| VersionId | Version IDs of the objects that failed to be deleted | String |
| Code | Error codes for the deletion failures | String |
| Message | Error messages for the deletion failures | String |



### Restoring an archived object 

#### Description

This API (`POST Object restore`) is used to restore an archived object for access.

#### Method prototype

```
restore_object(Bucket, Key, RestoreRequest={}, **kwargs)
```
#### Sample request

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

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| RestoreRequest | Rules for restoration | Dict | Yes |
| Days | Number of days before the temporary object expires | Int | Yes |
| CASJobParameters | Configuration of the restoration mode | Dict | No |
| Tier  | Object restoration mode. For ARCHIVE objects, valid values are `Expedited`, `Standard`, and `Bulk`. For DEEP ARCHIVE objects, valid values are `Standard` and `Bulk` | String | No |

#### Response description
This API returns None.


### Searching for object content 

#### Description

This API is used to extract content from a specific object.

#### Method prototype

```
select_object_content(Bucket, Key, Expression, ExpressionType, InputSerialization, OutputSerialization, RequestProgress=None, **kwargs)
```
#### Sample request

[//]: # ".cssg-snippet-select-object-content"
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

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
|Expression| SQL statement, which represents the extract operation you want to perform | String| Yes |
| ExpressionType | Statement type, which is an extension. Currently, only SQL statements and parameters are supported. | String | Yes |
|InputSerialization| Format of the object to extract. For more information, see [Sample request](https://intl.cloud.tencent.com/document/product/436/32360#.E8.AF.B7.E6.B1.82)| Dict | Yes|
|OutputSerialization| Output format of the extraction results. For more information, see [Sample request](https://intl.cloud.tencent.com/document/product/436/32360#.E8.AF.B7.E6.B1.82)| Dict | Yes|
| RequestProgress | Whether to return the query progress (QueryProgress). If this feature is enabled, COS Select will return the query progress periodically. | Dict| No |

#### Response description
The response contains the content and metadata of the object in dict format.
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

### Appending parts 

#### Description

This API (`APPEND Object`) is used to append object parts to a bucket.

#### Method prototype

```
append_object(Bucket, Key, Position, Data, **kwargs)
```
#### Sample request

[//]: # ".cssg-snippet-append-object"
```python
response = client.append_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Position=0,
    Data=b'b'*1024*1024
)
```
#### Sample request with all parameters

```python
response = client.append_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Position=0,
    Data=b'bytes'|file
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| Position | Starting point for the append operation (in bytes). For the first append, the value of this parameter is 0. For subsequent appends, the value is the `Content-Length` of the current object. | Int | Yes |
|Data|Content of the parts to upload, which may be a file stream or byte stream | file/bytes|Yes|

#### Response description
The response contains the attributes of the object in dict format after the append operation.
```python
{
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'x-cos-next-append-position': '12',
    'x-cos-request-id': 'NjEwN2Q0ZGZfMWNhZjU4NjRfMzM1M19hNzQzYjc2'
}
```

## Multipart Operations
Multipart operations include:

- Uploading an object in parts: initializing a multipart upload, uploading parts, and completing a multipart upload
- Resuming a multipart upload: querying uploaded parts, uploading remaining parts, and completing a multipart upload
- Deleting uploaded parts

### Querying multipart uploads

#### Description

This API is used to query in-progress multipart uploads in a specified bucket.

#### Method prototype

```
list_multipart_uploads(Bucket, Prefix="", Delimiter="", KeyMarker="", UploadIdMarker="", MaxUploads=1000, EncodingType="", **kwargs)
```
#### Sample request

[//]: # ".cssg-snippet-list-multi-upload"
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

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Prefix | Object key prefix to filter multipart uploads by. It is left empty by default. | String | No |
| Delimiter | Separator, left empty by default | String | No |
| KeyMarker | The key of the object after which the returned list begins. It is used together with `UploadIdMarker`. | String | No |
| UploadIdMarker | The upload ID of the object after which the returned list begins. It is used together with `KeyMarker`. If `KeyMarker` is not specified, `UploadIdMarker` will be ignored. | String | No |
| MaxUploads | Maximum number of multipart uploads returned at a time, which is `1000` (the maximum value allowed) by default | Int | No |
| EncodingType | Encoding method of the returned value. The value is not encoded by default. Valid value: `url` | String | No |

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

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String |
| Prefix | Object prefix key by which multipart uploads are queried. It is left empty by default. | String |
| Delimiter | Separator, which is left empty by default. | String |
| KeyMarker | The key of the object after which the returned list begins. It is used together with `UploadIdMarker`. | String |
| UploadIdMarker | The upload ID of the object after which the returned list begins. If `KeyMarker` is not specified, `UploadIdMarker` will be ignored. | String |
| NextKeyMarker | The key of the object after which the next returned list begins if `IsTruncated` is `true` | String |
| NextUploadIdMarker | The upload ID of the object after which the next returned list begins if `IsTruncated` is `true` | String |
| MaxUploads | Maximum number of multipart uploads returned at a time, which is `1000` (the maximum value allowed) by default  | Int |
| IsTruncated | Whether the returned multipart upload list is truncated | String |
| EncodingType | Encoding type of the returned value. The returned value is not encoded by default. Valid value: `url` | String |
| Upload | List of information on all the returned multipart uploads, including `UploadId`, `StorageClass`, `Key`, `Owner`, `Initiator`, and `Initiated` | List |
| CommonPrefixes | All keys starting with the specified prefix and ending with the specified delimiter | List |


### Initializing a multipart upload

#### Description

This API (`Initiate Multipart Upload`) is used to initialize a multipart upload and obtain its `uploadId`.

#### Method prototype

```
create_multipart_upload(Bucket, Key, **kwargs):
```
#### Sample request

[//]: # ".cssg-snippet-init-multi-upload"
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
# Obtain UploadId for subsequent API calls
uploadid = response['UploadId']
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| StorageClass | Storage class of the object, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String     | No |
| Expires | Expiration time | String | No |
| CacheControl | Cache policy | String | No |
| ContentType | Content type | String | No |
| ContentDisposition | Filename | String | No |
| ContentEncoding | Encoding type | String | No |
| ContentLanguage | Language type | String | No |
|  Metadata | User-defined object metadata | Dict |  No |
| ACL | ACL of the object, such as `private` or `public-read`|String| No |
| GrantFullControl | Grants full permission. Format: `id="OwnerUin"` | String | No |
| GrantRead | Grants read permission. Format: `id="OwnerUin"` | String | No |

#### Response description

This response contains information on the initialization of the multipart upload in dict format:

```python
{
    'UploadId': '150219101333cecfd6718d0caea1e2738401f93aa531a4be7a2afee0f8828416f3278e5570',
    'Bucket': 'examplebucket-1250000000', 
    'Key': 'exampleobject' 
}

```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| UploadId | ID of the multipart upload | String |
| Bucket | Bucket name in the format of `BucketName-APPID` | String |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String |

### Uploading parts

This API (`Upload Part`) is used to upload an object in parts.

#### Method prototype

```
upload_part(Bucket, Key, Body, PartNumber, UploadId, **kwargs)
```
#### Sample request

[//]: # ".cssg-snippet-upload-part"
```python
# Note: You can upload at most 10,000 parts at a time.
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
# Note: You can upload at most 10,000 parts at a time.
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

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| Body  | Content of the parts to upload. It can be a local file stream or a byte stream | file/bytes |  Yes|
| PartNumber | Part number | Int | Yes |
| UploadId | ID of the multipart upload | String | Yes |
| EnableMD5 | Whether to calculate the Content-MD5 checksum, which will extend the upload time. It’s not calculated by default. | Bool | No |
| ContentLength | Length of the content  | String | No |
| ContentMD5 | MD5 checksum of the uploaded object, which is used for verification | String | No |
|  TrafficLimit | Bandwidth limit for a single request in bit/s. Value range: 819200-838860800, i.e., 100 KB/s - 100 MB/s | String |  No |

#### Response description

This response contains the attributes of the uploaded parts in dict format:

```python
{
    'ETag': 'string'
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| ETag | MD5 checksum of the uploaded parts | String |

### Copying an object part

This API (`Upload Part - Copy`) is used to copy a part of an object.

#### Method prototype

```
upload_part_copy(Bucket, Key, PartNumber, UploadId, CopySource, CopySourceRange='', **kwargs)
```
#### Sample request

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
        'Region': 'COS_REGION', #Replace it with the source bucket’s region
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

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| PartNumber | Part number | Int | Yes |
| UploadId | ID of the multipart upload | String | Yes |
| CopySource  | Path of the source object to copy, which contains `Bucket`, `Key`, `Region`, and `VersionId` |  Dict | Yes |
| CopySourceRange | Byte range of the source object to copy in the format of `bytes=first-last`. The entire source will be copied by default if no range is specified. | String | No |
| CopySourceIfMatch | `ETag` that must be matched. The object is copied only if its `ETag` matches the value. | String | No |
| CopySourceIfModifiedSince | Required modification time. The object is copied only if it has been modified since the specified time. | String | No |
| CopySourceIfNoneMatch | `ETag` that cannot be matched. The object is copied only if its `ETag` does not match the specified value. | String | No |
| CopySourceIfUnmodifiedSince | Required unmodified time. The object is copied only if it hasn’t been modified since the specified time. | String | No |

#### Response description

This response contains the attributes of the copied parts in dict format:
```python
{
    'ETag': 'string',
    'LastModified': 'string',
    'x-cos-copy-source-version-id': 'string',
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| ETag | MD5 checksum of the copied parts | String |
| LastModified | Time when the copied parts were last modified | String |
| x-cos-copy-source-version-id | Version ID of the source object | String |

### Querying uploaded parts

#### Description

This API (`List Parts`) is used to query the uploaded parts of a multipart upload.

#### Method prototype

```
list_parts(Bucket, Key, UploadId, MaxParts=1000, PartNumberMarker=0, EncodingType='', **kwargs)
```
#### Sample request

[//]: # ".cssg-snippet-list-parts"
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

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| UploadId | ID of the multipart upload | String | Yes |
| MaxParts | Maximum number of parts returned at a time, which is `1000` (the maximum value allowed) by default | Int | No |
| PartNumberMarker | The number of the part after which the list begins. The value of this parameter is `0` by default, which means the list begins from the first part. | Int | No |
| EncodingType | Encoding method of the returned value. The value is not encoded by default. Valid value: `url`  | String | No |

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

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String |
| UploadId | ID of the multipart upload | String |
| EncodingType | Encoding type of the returned value. The returned value is not encoded by default. Valid value: `url` | String |
| MaxParts | Maximum number of parts returned at a time, which is `1000` (the maximum value allowed) by default  | String |
| IsTruncated | Whether the returned part list is truncated | String |
| PartNumberMarker | The number of the part after which the list begins. The value of this parameter is `0` by default, which means the list begins from the first part. | String |
| NextPartNumberMarker | The number of the part after which the next returned list begins | String |
| StorageClass | Storage class of the object, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |
| Part | Information on the uploaded parts, including `ETag`, `PartNumber`, `Size`, and `LastModified` | String |
| Initiator | Initiator of the multipart upload, including `DisplayName` and `ID` | Dict |
| Owner | Information on the object owner, including `DisplayName` and `ID` | Dict |



### Completing a multipart upload

#### Description

This API (`Complete Multipart Upload`) is used to complete a multipart upload.

#### Method prototype

```
complete_multipart_upload(Bucket, Key, UploadId, MultipartUpload={}, **kwargs)
```
#### Sample request

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

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| UploadId | ID of the multipart upload | String | Yes |
| MultipartUpload | Information on all parts, including `ETag` and `PartNumber` | Dict |Yes |

#### Response description

The response contains information on the object assembled from the uploaded parts in dict format:

```python
{
    'ETag': '"3f866d0050f044750423e0a4104fa8cf-2"', 
    'Bucket': 'examplebucket-1250000000', 
    'Location': 'examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject', 
    'Key': 'exampleobject'
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| ETag | The unique tag of the assembled object. This value is not necessarily the MD5 checksum of the object. It is used to verify the uniqueness of the object. To verify the object content, you can check the `ETag` of each part during the upload process. | String |
| Bucket | Bucket name in the format of `BucketName-APPID` | String |
| Location | URL address | String |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String |


### Aborting a multipart upload

#### Description

This API (`Abort Multipart Upload`) is used to abort a multipart upload and delete the uploaded parts.

#### Method prototype

```
abort_multipart_upload(Bucket, Key, UploadId, **kwargs)
```
#### Sample request

[//]: # ".cssg-snippet-abort-multi-upload"
```python
response = client.abort_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId='exampleUploadId'
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| UploadId | ID of the multipart upload | String | Yes |

#### Response description
This API returns None.





 ## Advanced APIs (Recommended)

### Uploading an object (checkpoint restart)

#### Description
This advanced upload API can automatically select between the `PUT Object` API and the `Upload Part` API according to the file size. It uses the former for files smaller than or equal to 20 MB and the latter for files larger than 20 MB. It also supports automatic checkpoint restart for suspended multipart uploads.
You can use the `progress_callback` function to query the multipart upload progress.

#### Method prototype

```
upload_file(Bucket, Key, LocalFilePath, PartSize=1, MAXThread=5, EnableMD5=False, progress_callback=None, **kwargs)
```
#### Sample request

[//]: # ".cssg-snippet-transfer-upload-file"
```python


response = client.upload_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    LocalFilePath='local.txt',
    EnableMD5=False,
    progress_callback=None
)
```

#### Sample request with all parameters
```python

def upload_percentage(consumed_bytes, total_bytes):
    """Callback function that calculates the upload progress (in percentage)

    :param consumed_bytes: uploaded data amount
    :param total_bytes: total data amount
    """
    if total_bytes:
        rate = int(100 * (float(consumed_bytes) / float(total_bytes)))
        print('\r{0}% '.format(rate))
        sys.stdout.flush()
        

response = client.upload_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    LocalFilePath='local.txt',
    PartSize=1,
    MAXThread=5,
    progress_callback=upload_percentage,
    EnableMD5=False|True,
    ACL='private'|'public-read', # Please note that the maximum number (1000) of ACLs allowed may be reached if you use this parameter
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


| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| LocalFilePath | Path to the local file | String | Yes |
| PartSize | Part size. Default value: 1 MB |  Int | No |
|  MAXThread  | Maximum number of threads for concurrent multipart uploads. Default value: 5 |  Int |  No |
| progress_callback | Callback function for the upload progress. You can customize this function to query the upload progress. | Func | No |
| EnableMD5 | Whether to calculate the Content-MD5 checksum, which will extend the upload time. It’s not calculated by default. | Bool | No |
| ACL  | ACL of the object, such as private or public-read                      | String | No |
| GrantFullControl | Grants full permission. Format: `id="OwnerUin"` | String | No |
| GrantRead | Grants read permission. Format: `id="OwnerUin"` | String | No |
| StorageClass | Storage class of the object, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |   No |
| Expires | Expiration time | String | No |
| CacheControl | Cache policy | String | No |
| ContentType | Content type | String | No |
| ContentDisposition | Filename | String | No |
| ContentEncoding | Encoding type  | String | No |
| ContentLanguage | Language type  | String | No |
| ContentLength | Length of the content  | String | No |
| ContentMD5 | MD5 checksum of the uploaded object, which is used for verification | String | No |
|  Metadata | User-defined object metadata | Dict |  No |
|  TrafficLimit | Bandwidth limit in bit/s for a single request (or a single thread for the advanced download API). Value range: 819200 - 838860800, i.e., 100 KB/s - 100 MB/s | String |  No |

#### Response description
The response contains the attributes of the copied object in dict format:

```python
{
    'ETag': 'string'
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| ETag | This value is not necessarily the MD5 checksum of the object. It is used to verify the uniqueness of the multipart uploaded object. | String |


### Downloading an object (checkpoint restart)

#### Description
This advanced download API can determine whether to download a file in whole or in parts based on the file size. It downloads files smaller than or equal to 20 MB in whole and files larger than 20 MB in parts. It also supports automatic checkpoint restart for suspended multipart downloads.

#### Method prototype

```
download_file(Bucket, Key, DestFilePath, PartSize=20, MAXThread=5, EnableCRC=False, **Kwargs)
```
#### Sample request

[//]: # ".cssg-snippet-transfer-upload-file"
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


| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
|  DestFilePath  | Local path to save the downloaded file |  String |  Yes |
| PartSize | Part size for multipart download. Default value: 20 MB |  Int | No |
|  MAXThread  | Maximum number of concurrent threads for a multipart download. Default value: 5 |  Int |  No |
| EnableCRC | Whether to enable CRC for local and remote files. Default: `False` | Bool | No |
|  TrafficLimit | Bandwidth limit in bit/s for a single request (or a single thread for the advanced download API). Value range: 819200 - 838860800, i.e., 100 KB/s - 100 MB/s | String |  No |
|  IfMatch  | `ETag` that needs to be matched. The object is downloaded only if its `ETag` matches the value. | String  | No |
| IfModifiedSince |  Required modification time. The object is downloaded only if it has been modified after the specified time.  | String | No |
|  IfNoneMatch  |  `ETag` that cannot be matched. The object is downloaded only if its `ETag` does not match the value. | String  | No |
| IfUnmodifiedSince | Required unmodified time. The object is downloaded only if it has not been modified since the specified time.   | String | No |
| ResponseCacheControl | `Cache-Control` of the response header | String | No |
| ResponseContentDisposition | `Content-Disposition` of the response header | String | No |
| ResponseContentEncoding | `Content-Encoding` of the response header | String | No |
| ResponseContentLanguage | `Content-Language` of the response header | String | No |
| ResponseContentType | `Content-Type` of the response header | String | No |
| ResponseExpires | `Expires` of the response header | String | No |
| VersionId | Version ID of the object to download| String | No |

#### Response description
None



### Copying objects

#### Description
This advanced API copies objects smaller than 5 GB by calling `copy_object`. If an object is larger than or equal to 5 GB, it calls `upload_part_copy`.

#### Method prototype

```
copy(Bucket, Key, CopySource, CopyStatus='Copy', PartSize=10, MAXThread=5, **kwargs)
```

#### Sample 1. Copying an object

[//]: # ".cssg-snippet-transfer-copy"
```python
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos import CosServiceError
from qcloud_cos import CosClientError

import sys
import os
import logging

# Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  # Get the configured object
client = CosS3Client(config)

response = client.copy(
    Bucket='test',
    Key='copy_10G.txt',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou'
    }
)
```

#### Sample 2: moving an object

[//]: # ".cssg-snippet-transfer-copy-move"
```python
bucket = 'examplebucket-1250000000'
srcKey = 'src_object_key'  # Path of the source object
destKey = 'dest_object_key'   # Path of the destination object

# COS does not offer an API to move objects. To move an object, you can copy it first and delete the old one.
try:
    response = client.copy(
        Bucket=bucket,
        Key=destKey,
        CopySource={
            'Bucket':bucket,
            'Key':srcKey,
            'Region':'ap-guangzhou',
        })
    client.delete_object(Bucket=bucket, Key=srcKey)
except CosException as e:
    print(e.get_error_msg())
```

#### Sample request with all parameters

```python
response = client.copy(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou'
    }
    CopyStatus='Copy'|'Replaced',
    PartSize=20,
    MAXThread=10
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| CopySource  | Path of the source object to copy, which contains `Bucket`, `Key`, `Region`, and `VersionId` |  Dict | Yes |
 | CopyStatus | Copy status. Valid values: `Copy`, `Replaced`                        | String | No |
 | PartSize | Part size for multipart download. Default value: 10 MB |  Int | No |
 |  MAXThread  | Maximum number of concurrent threads for a multipart download. Default value: 5 |  Int |  No |

#### Response description
If the object is smaller than 5 GB, the response of `copy_object` is returned. Otherwise, the response of `complete_multipart_upload` is returned. The format is dict.


### Batch uploading files (uploading a local folder)

#### Description
The following example shows how to use the SDK’s basic APIs to upload a local folder to COS.

#### Sample request

[//]: # ".cssg-snippet-transfer-upload-file"
```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos import CosServiceError
from qcloud_cos import CosClientError
from qcloud_cos.cos_threadpool import SimpleThreadPool

import sys
import os
import logging

# Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://www.qcloud.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  # Get the configured object
client = CosS3Client(config)

uploadDir = '/root/logs'
bucket = 'examplebucket-125000000'
g = os.walk(uploadDir)
# Create a thread pool for the upload.
pool = SimpleThreadPool()
for path, dir_list, file_list in g:
    for file_name in file_list:
        srcKey = os.path.join(path, file_name)
        cosObjectKey = srcKey.strip('/')
        # Determine whether the object exists in COS.
        exists = False
        try:
            response = client.head_object(Bucket=bucket, Key=cosObjectKey)
            exists = True
        except CosServiceError as e:
            if e.get_status_code() == 404:
                exists = False
            else:
                print("Error happened, reupload it.")
        if not exists:
            print("File %s not exists in cos, upload it", srcKey)
            pool.add_task(client.upload_file, bucket, cosObjectKey, srcKey)


pool.wait_completion()
result = pool.get_result()
if not result['success_all']:
    print("Not all files upload sucessed. you should retry")
```

### Batch downloading files (downloading a COS directory)

#### Description
The following example shows how to use the SDK’s basic APIs to download a COS directory to local storage.

#### Sample request

[//]: # ".cssg-snippet-transfer-upload-file"
```python
# -*- coding=utf-8
import logging
import sys
import json
import os

from qcloud_cos import CosConfig, CosServiceError
from qcloud_cos import CosS3Client
from qcloud_cos.cos_threadpool import SimpleThreadPool

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://www.qcloud.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048
scheme = 'http'            # Specify whether to use HTTP or HTTPS protocol to access COS. This is optional and is https by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)  # Obtain the object to configure.
client = CosS3Client(config)

# Bucket information
test_bucket = 'examplebucket-1250000000'
start_prefix = 'data/'
# COS uses slashes (/) to indicate folders.
# The delimiter parameter is left empty by default, which lists all subdirectories under the directories to achieve the recursive effect of a local folder.
# If the delimiter parameter is set to "/", you need to handle subdirectories recursively in the SDK.
delimiter = ''


# List and return information about all subdirectories under the current directory.
def listCurrentDir(prefix):
    file_infos = []
    sub_dirs = []
    marker = ""
    count = 1
    while True:
        response = client.list_objects(test_bucket, prefix, delimiter, marker)
        # Debug the output.
        # json_object = json.dumps(response, indent=4)
        # print(count, " =======================================")
        # print(json_object)
        count += 1

        if "CommonPrefixes" in response:
            common_prefixes = response.get("CommonPrefixes")
            sub_dirs.extend(common_prefixes)

        if "Contents" in response:
            contents = response.get("Contents")
            file_infos.extend(contents)

        if "NextMarker" in response.keys():
            marker = response["NextMarker"]
        else:
            break

    print("=======================================================")

    # If the delimiter parameter is set to "/", you need to handle subdirectories recursively.
    # sorted(sub_dirs, key=lambda sub_dir: sub_dir["Prefix"])
    # for sub_dir in sub_dirs:
    #     print(sub_dir)
    #     sub_dir_files = listCurrentDir(sub_dir["Prefix"])
    #     file_infos.extend(sub_dir_files)

    print("=======================================================")

    sorted(file_infos, key=lambda file_info: file_info["Key"])
    for file in file_infos:
        print(file)
    return file_infos


# Download files to a local directory. Local files with the same name (if any) will be overwritten.
# If the directory structure does not exist, a directory structure will be created according to that in COS.
def downLoadFiles(file_infos):
    localDir = "./download/"

    pool = SimpleThreadPool()
    for file in file_infos:
        # Download files to local.
        file_cos_key = file["Key"]
        localName = localDir + file_cos_key

        # If the local directory does not exist, create it recursively.
        if not os.path.exists(os.path.dirname(localName)):
            os.makedirs(os.path.dirname(localName))

        # skip dir, no need to download it
        if str(localName).endswith("/"):
            continue

        # Download files
        # Use a thread pool.
        pool.add_task(client.download_file, test_bucket, file_cos_key, localName)

        # Download in whole
        # response = client.get_object(
        #     Bucket=test_bucket,
        #     Key=file_cos_key,
        # )
        # response['Body'].get_stream_to_file(localName)

    pool.wait_completion()
    return None


# Encapsulate the feature. Download a COS directory to local.
def downLoadDirFromCos(prefix):
    global file_infos

    try:
        file_infos = listCurrentDir(prefix)

    except CosServiceError as e:
        print(e.get_origin_msg())
        print(e.get_digest_msg())
        print(e.get_status_code())
        print(e.get_error_code())
        print(e.get_error_msg())
        print(e.get_resource_location())
        print(e.get_trace_id())
        print(e.get_request_id())

    downLoadFiles(file_infos)
    return None


if __name__ == "__main__":
    downLoadDirFromCos(start_prefix)
```


### Deleting multiple objects (deleting a directory)

#### Description
COS does not have the concept of directories, but you can use slashes (/) as the delimiter to stimulate directories.

In COS, deleting a directory and the objects contained actually means deleting objects that have the same specified prefix. Currently, COS’s Python SDK does not provide a standalone API to perform this operation. However, you can still do so with a combination of basic operations (query object list + batch delete objects).

#### Sample request
```python
import logging
import sys
import os

from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos.cos_threadpool import SimpleThreadPool

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048
scheme = 'http'            # Specify whether to use HTTP or HTTPS protocol to access COS. This is optional and is https by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)  # Obtain the object to configure.
client = CosS3Client(config)

bucket = 'examplebucket-1250000000'
folder = 'folder/' # A directory to delete (an object name ending with a slash (/) is a directory)

def delete_cos_dir():
    pool = SimpleThreadPool()
    marker = ""
    while True:
        file_infos = []

        # List 100 objects in a response.
        response = client.list_objects(Bucket=bucket, Prefix=folder, Marker=marker, MaxKeys=100)

        if "Contents" in response:
            contents = response.get("Contents")
            file_infos.extend(contents)
            pool.add_task(delete_files, file_infos)

        # Quit after the listing.
        if response['IsTruncated'] == 'false':
            break
        
        # Get the next response.
        marker = response["NextMarker"]

    pool.wait_completion()
    return None   

def delete_files(file_infos):

    # Construct the batch delete request.
    delete_list = []
    for file in file_infos:
        delete_list.append({"Key": file['Key']})

    response = client.delete_objects(Bucket=bucket, Delete={"Object": delete_list})
    print(response)

if __name__ == "__main__":
    delete_cos_dir()
```


## Client-Side Encryption

#### Description

The SDK for Python allows client-side encryption, which encrypts files before upload and decrypts them at the time of download. There are two types of client-side encryption: AES (symmetric) and RSA (asymmetric).
They are only used for the encryption of the random keys generated. File data is always encrypted using the symmetric method AES256.
Client-side encryption is suitable for users who store sensitive data and may affect the upload speed. The SDK uses the serial method for multipart upload.

### Encryption for upload

1. Before each upload, COS randomly generates a symmetric key which is encrypted through the customer-provided symmetric or asymmetric key. The encryption result is then Base64-encoded and stored in object metadata.
2. During the upload, the file is encrypted in memory using the AES256 algorithm.

### Decryption for download

1. Get the necessary encryption information from the metadata of the file, Base64-decode it, and then decrypt it using the customer managed key (CMK) to get the encryption key at upload.
2. Use the resulting key to decrypt the downloaded input stream using AES256.

#### Sample request

Sample 1. Using symmetric AES256 encryption for randomly generated keys

[//]: # ".cssg-snippet-put-object-cse-c-aes"
```python
# Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://www.qcloud.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048

conf = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)

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

# Upload an object in parts, an operation compatible with non-encryption clients. Except for the last part, the size of each part must be an integer multiple of 16 bytes.
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

# Upload an object with checkpoint restart. The size of each part must be an integer multiple of 16 bytes.
response = client_for_aes.upload_file(
    Bucket='test04-123456789',
    LocalFilePath='local.txt',
    Key=file_name,
    PartSize=10,
    MAXThread=10
)

```

Sample 2. Using asymmetric RSA encryption for randomly generated keys

[//]: # ".cssg-snippet-put-object-cse-c-rsa"
```python
# Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://www.qcloud.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048

conf = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)

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

# Upload an object in parts, an operation compatible with non-encryption clients. Except for the last part, the size of each part must be an integer multiple of 16 bytes.
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

# Upload an object with checkpoint restart. The size of each part must be an integer multiple of 16 bytes.
response = client_for_rsa.upload_file(
    Bucket='test04-123456789',
    LocalFilePath='local.txt',
    Key=file_name,
    PartSize=10,
    MAXThread=10
)
```
