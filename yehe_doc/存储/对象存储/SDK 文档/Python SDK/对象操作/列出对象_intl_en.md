## Overview

This document provides an overview of APIs and SDK code samples for object listing.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/30614) | Querying object list | Queries some or all objects in a bucket |
| [GET Bucket Object Versions](https://www.tencentcloud.com/document/product/436/31551) | Querying list of current and historical versions of objects | Queries some or all objects in a bucket and their historical versions |

## Querying an Object List

#### Feature description

This API is used to query some or all the objects in a bucket.

#### Method prototype

```
list_objects(Bucket, Delimiter="", Marker="", MaxKeys=1000, Prefix="", EncodingType="", **kwargs)
```
#### Sample 1: listing all objects in a bucket

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

response = client.list_objects(Bucket='examplebucket-1250000000')
if 'Contents' in response:
    for content in response['Contents']:
        print(content['Key'])
# Note: A maximum of 1,000 objects can be listed at a time. If there are too many objects, you need to list them in multiple responses (see sample 3).
```

#### Sample 2: listing objects with a specified prefix

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

# List objects prefixed with "folder".
response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='folder' 
)

# List objects in the "folder1" directory: In COS, an object whose name ends with a slash (/) is considered a folder.
response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='folder1/' 
)
```

#### Sample 3: listing objects in multiple responses

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

# List objects and subdirectories in "folder1".
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

## Querying objects and their version history 

#### Feature description

This API is used to query some or all the objects in a bucket and their version history.

#### Method prototype

```
list_objects_versions(Bucket, Prefix="", Delimiter="", KeyMarker="", VersionIdMarker="", MaxKeys=1000, EncodingType="", **kwargs)
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

response = client.list_objects_versions(
    Bucket='examplebucket-1250000000',
    Prefix='string'
)
```

#### Sample request with all parameters

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
