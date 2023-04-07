

## Feature Overview

This document provides an overview of APIs and SDK code samples related to logging.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://www.tencentcloud.com/document/product/436/17054) | Setting logging configuration | Enables logging for a source bucket |
| [GET Bucket logging](https://www.tencentcloud.com/document/product/436/17053) | Querying log management | Queries the logging configuration of a source bucket |

## Setting Logging Configuration

#### Feature description

This API is used to enable logging for a source bucket and store the access logs in a specified destination bucket.

#### Method prototype

```
put_bucket_logging(Bucket, BucketLoggingStatus={}, **kwargs):
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

response = client.put_bucket_logging(
    Bucket='examplebucket-1250000000',
    BucketLoggingStatus={
        'LoggingEnabled': {
            'TargetBucket': 'logging-bucket-1250000000',
            'TargetPrefix': 'string'
        }
    }
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | -------- |
| Bucket       | Name of the source bucket for which logging is to be enabled. The name format is `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312). | String | Yes       |
| TargetBucket | Name of the destination bucket to store logs. The name format is `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312). | String | Yes       |
| TargetPrefix | The specified path prefix used to store logs in the destination bucket                           | String | Yes       |

#### Response description

This API returns `None`.

## Querying Logging Configuration

#### Feature description

This API is used to query the logging configuration of a specified bucket.

#### Method prototype

```
get_bucket_logging(Bucket, **kwargs):
```

#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
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

response = client.get_bucket_logging(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description                      

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Destination bucket to store logs, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312). | String | Yes |

#### Response description

Bucket log management configuration in dict format.

```
{
    'LoggingEnabled': {
        'TargetBucket': 'logging-bucket-1250000000',
        'TargetPrefix': 'string'
    }
}
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| TargetBucket | Name of the destination bucket to store logs. The name format is `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312). | String |
| TargetPrefix             | The specified path prefix used to store logs in the destination bucket                                           | String      |
