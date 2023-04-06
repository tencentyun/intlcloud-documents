## Overview

This document provides an overview of APIs and SDK code samples for querying object metadata.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [HEAD Object](https://www.tencentcloud.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |

## Querying Object Metadata

#### Feature description

This API is used to query object metadata.

#### Method prototype

```
head_object(Bucket, Key, **kwargs)
```
#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print information about the communication with the server.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = os.environ['COS_SECRET_ID']     #  User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://www.tencentcloud.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://www.tencentcloud.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.head_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
print(response)
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
    'Connection': 'keep-alive',
    'Accept-Ranges': 'bytes',
    'Server': 'tencent-cos',
    'Date': 'Wed, 28 Oct 2019 20:20:00 GMT',
    'x-cos-meta-test': 'test',
    'x-cos-version-id': 'MTg0NDUxODMzMTMwMDM2Njc1ODA',
    'x-cos-hash-crc64ecma': '1220413902487941276',
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
|  Connection | Connection method. Standard HTTP header | String |
|  Accept-Ranges | Range request flag. Standard HTTP header | String |
|  Server | Server flag. Standard HTTP header | String |
|  Date | Request date. Standard HTTP header | String |
| x-cos-meta-* | User-defined object metadata. This parameter must start with `x-cos-meta`; otherwise, it will be ignored.  | String |
|  x-cos-hash-crc64ecma | CRC64 checksum of the file | String |
| x-cos-version-id |  Version ID of the object if versioning is enabled | String |
|  x-cos-request-id | Request ID | String |
