## Overview

This document provides an overview of APIs and SDK code samples related to bucket referer allowlist or blocklist.

>! The COS PYTHON SDK version should not be earlier than v5.1.9.7.
>

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://www.tencentcloud.com/document/product/436/31423) | Setting a bucket referer | Sets a bucket referer allowlist or blocklist |
| [GET Bucket referer](https://www.tencentcloud.com/document/product/436/30615) | Querying a bucket referer | Queries a bucket referer allowlist or blocklist |

## Setting Bucket Referer Configuration

#### Feature description

This API (PUT Bucket referer) is used to set a referer allowlist/blocklist for a bucket.

#### Method prototype

```python
put_bucket_referer(Bucket, RefererConfiguration, **kwargs)
```

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

referer_config = {
    'Status': 'Enabled',
    'RefererType': 'White-List',
    'EmptyReferConfiguration': 'Allow',
    'DomainList': {
        'Domain': [
            '*.qq.com',
            '*.qcloud.com'
        ]
    }
}
response = client.put_bucket_referer(
    Bucket='examplebucket-1250000000',
    RefererConfiguration=referer_config
)
```

#### Parameter description

| Parameter  | Description | Type |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://www.tencentcloud.com/document/product/436/13312) | String |
| RefererConfiguration | Referer configuration of the bucket                      | Dict |

Description of `RefererConfiguration`:

| Parameter | Description | Type | Required |
| -------------- | ----------------------------------------------- | ------ | ---- |
| Status         | Whether to enable hotlink protection. Enumerated values: `Enabled`, `Disabled`  | String | Yes   |
| RefererType    | Hotlink protection type. Enumerated values: `Black-List`, `White-List`          | String | Yes   |
| DomainList         | Domain list    | Dict | Yes  |
| Domain         | Domains, which can include ports, IPs, or asterisks (\*). You can set multiple domains. | List | Yes  |
| EmptyReferConfiguration |  Whether to allow access with an empty referer. Enumerated values: `Allow`, `Deny` | String | No  |

#### Response description
This API returns `None`.

## Querying Bucket Referer Configuration

#### Feature description

This API (GET Bucket referer) is used to query the referer allowlist/blocklist of a bucket.

#### Method prototype

```python
get_bucket_referer(Bucket, **kwargs)
```

#### Sample request

```python
response = client.get_bucket_referer(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description

| Parameter | Description | Type |
| ----------- | -------- | ---- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://www.tencentcloud.com/document/product/436/13312) | String |

#### Response description
The bucket referer configuration is returned. For more information, please see the description of `RefererConfiguration`.

## Deleting a Bucket Referer

#### Feature description

This API (`DELETE Bucket referer`) is used to delete the referer allowlist/blocklist set for a bucket.

#### Method prototype

```python
delete_bucket_referer(Bucket, **kwargs)
```

#### Sample request

```python
response = client.delete_bucket_referer(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description

| Parameter | Description | Type |
| ----------- | -------- | ---- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://www.tencentcloud.com/document/product/436/13312) | String |

#### Response description
This API returns `None`.
