## Overview

This document provides an overview of APIs and SDK code samples related to object copy and movement.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object - Copy](https://www.tencentcloud.com/document/product/436/10881) | Setting object replication | Copies an object to the destination path |

## Advanced APIs (Recommended)

### Copying an object

#### Feature description
This advanced API copies objects smaller than 5 GB by calling `copy_object`. If an object is larger than or equal to 5 GB, it calls `upload_part_copy`.

#### Method prototype

```
copy(Bucket, Key, CopySource, CopyStatus='Copy', PartSize=10, MAXThread=5, **kwargs)
```
#### Sample 1. Copying an object

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

response = client.copy(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'sourceobject', 
        'Region': 'ap-guangzhou'
    }
)
```

#### Sample 2: moving an object

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

bucket = 'examplebucket-1250000000'
srcKey = 'src_object_key'  # Path of the source object
destKey = 'dest_object_key'   # Path of the destination object

# COS does not offer an API to move objects. To move an object, you can copy it first and delete the old one.
response = client.copy(
    Bucket=bucket,
    Key=destKey,
    CopySource={
        'Bucket':bucket,
        'Key':srcKey,
        'Region':'ap-guangzhou',
    })
client.delete_object(Bucket=bucket, Key=srcKey)
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
| CopySource | Path of the source object to copy, which contains `Bucket`, `Key`, `Region`, and `VersionId` |  Dict | Yes |
| CopyStatus | Copy status. Valid values: `Copy`, `Replaced`                        | String | No |
| PartSize | Part size for multipart download. Default value: 10 MB |  Int | No |
|  MAXThread  | Maximum number of concurrent threads for a multipart download. Default value: 5 |  Int |  No |

#### Response description
If the object is smaller than 5 GB, the response of `copy_object` is returned. Otherwise, the response of `complete_multipart_upload` is returned. The format is dict.

## Simple Operations

### Copying an object

#### Feature description

This API is used to copy an existing object to a destination path.

#### Method prototype

```
copy_object(Bucket, Key, CopySource, CopyStatus='Copy', **kwargs)
```
#### Sample 1. Copying an object

If the source and destination objects are different, a new object will be generated. The metadata of the destination object will be copied from the source.

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

response = client.copy_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'sourceobject', 
        'Region': 'ap-guangzhou'
    }
)
```

#### Sample 2: moving an object

COS does not offer an API to move objects. To move an object, you can copy it first and delete the old one.

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

response = client.copy_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'sourceobject', 
        'Region': 'ap-guangzhou'
    }
)
client.delete_object(Bucket='sourcebucket-1250000000', Key='sourceobject')
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
