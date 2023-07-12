## Overview

This document provides SDK code samples for modifying object metadata.

## Modifying object metadata

If the source and destination objects are the same and `CopyStatus` is set to `Replaced`, you can modify the object metadata via the header.

#### Sample request
```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import os
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

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| CopySource | Path of the source object to copy, which contains `Bucket`, `Key`, `Region`, and `VersionId` |  Dict | Yes |
| CopyStatus | Valid values: `Copy`: ignores the configured metadata and copies the file directly; `Replaced`: modifies the metadata according to the configured metadata. If the destination path is identical to the source path, this parameter must be set to `Replaced`. | String | Yes |
| ACL  | ACL of the object, such as private or public-read                      | String | No |
| GrantFullControl | Grants full permission. Format: `id="OwnerUin"`| String | No |
| GrantRead | Grants read permission. Format: `id="OwnerUin"`| String | No |
| Expires | Expiration time | String | No |
| CacheControl | Cache policy | String | No |
| ContentType | Content type | String | No |
| ContentDisposition | Filename | String | No |
| ContentEncoding | Encoding type | String | No |
| ContentLanguage | Language type | String | No |
|  Metadata | User-defined object metadata | Dict |  No |

## Modifying the storage class of an object

If the source and destination objects are the same and `CopyStatus` is set to `Replaced`, you can use `StorageClass` to modify the storage class.

#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import os
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
| CopySource | Path of the source object to copy, which contains `Bucket`, `Key`, `Region`, and `VersionId` |  Dict | Yes |
| CopyStatus | Valid values: `Copy`: ignores the configured metadata and copies the file directly; `Replaced`: modifies the metadata according to the configured metadata. If the destination path is identical to the source path, this parameter must be set to `Replaced`. | String | Yes |
| StorageClass | Storage class of the object. Valid values: `STANDARD` (default); `STANDARD_IA`. | String | No |
