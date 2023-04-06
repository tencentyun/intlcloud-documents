## Overview

This document provides an overview of APIs and SDK code samples for restoring an archived object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [POST Object restore](https://www.tencentcloud.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |


## Restoring an Archived Object

#### Feature description

This API (`POST Object restore`) is used to restore an archived object for access.

#### Method prototype

```
restore_object(Bucket, Key, RestoreRequest={}, **kwargs)
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
This API returns `None`.
