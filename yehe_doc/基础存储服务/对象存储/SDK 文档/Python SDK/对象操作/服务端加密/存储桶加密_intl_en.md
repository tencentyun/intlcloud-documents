## Overview
This document provides an overview of APIs and SDK code samples related to bucket encryption.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket encryption](https://www.tencentcloud.com/document/product/436/33459) | Setting bucket encryption | Sets the default encryption configuration for a bucket |
| [GET Bucket encryption](https://www.tencentcloud.com/document/product/436/33460) | Querying bucket encryption configuration | Queries the default encryption configuration of a bucket |
| [DELETE Bucket encryption](https://www.tencentcloud.com/document/product/436/33461) | Deleting bucket encryption configuration | Deletes the default encryption configuration of a bucket |

## Setting Bucket Encryption

#### Feature description

This API is used to set the default server-side encryption configuration for a bucket. To call this API, you must have the `PutBucketEncryption` permission. By default, the bucket owner has permission to use this API and can grant such permission to other users.

#### Method prototype

```
put_bucket_encryption(Bucket, ServerSideEncryptionConfiguration={}, **kwargs)
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

config_dict = {
    'Rule': [
        {
            'ApplySideEncryptionConfiguration': {
                'SSEAlgorithm': 'AES256',
            }
        },
    ]
}
client.put_bucket_encryption(Bucket='examplebucket-1250000000', ServerSideEncryptionConfiguration=config_dict)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| ServerSideEncryptionConfiguration | Server-side encryption configuration | Dict | Yes |

`ServerSideEncryptionConfiguration` is described as follows:

| Parameter | Description | Type | Required |
| -------------- | ----------------------------------------------- | ------ | ---- |
| Rule | Server-side encryption rule list. Currently, only one rule is supported. | List | Yes |
| ApplySideEncryptionConfiguration | Description of the server-side encryption configuration | Dict | Yes |
|SSEAlgorithm| Server-side encryption algorithm. Currently, bucket encryption supports only the SSE-COS type and uses the AES-256 encryption algorithm. | String | Yes |

#### Response description

This API returns `None`.

## Querying Bucket Encryption Configuration

#### Feature description

This API is used to query the default server-side encryption configuration for a bucket. To call this API, you must have the `GetBucketEncryption` permission. By default, the bucket owner has permission to use this API and can grant such permission to other users.

#### Method prototype

```
get_bucket_encryption(Bucket, **kwargs)
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

response = client.get_bucket_encryption(Bucket='examplebucket-1250000000')
sse_algorithm = response['Rule'][0]['ApplyServerSideEncryptionByDefault']['SSEAlgorithm']
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |

#### Response description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| ServerSideEncryptionConfiguration | Server-side encryption configuration | Dict | Yes |

`ServerSideEncryptionConfiguration` is described as follows:

| Parameter | Description | Type | Required |
| -------------- | ----------------------------------------------- | ------ | ---- |
| Rule | Server-side encryption rule list. Currently, only one rule is supported. | List | Yes |
| ApplySideEncryptionConfiguration | Description of the server-side encryption configuration | Dict | Yes |
|SSEAlgorithm| Server-side encryption algorithm. Currently, bucket encryption supports only the SSE-COS type and uses the AES-256 encryption algorithm. | String | Yes |

## Deleting Bucket Encryption Configuration

#### Feature description

This API is used to delete the default encryption configuration for a bucket. To call this API, you must have the `DeleteBucketEncryption` permission. By default, the bucket owner has permission to use this API and can grant such permission to other users.

#### Method prototype

```
delete_bucket_encryption(Bucket, **kwargs)
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

response = client.delete_bucket_encryption(Bucket='examplebucket-1250000000')
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |

#### Response description

This API returns `None`.
