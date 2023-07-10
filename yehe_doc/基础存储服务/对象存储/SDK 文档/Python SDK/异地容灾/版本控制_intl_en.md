
## Overview

This document provides an overview of APIs and SDK code samples for versioning.



| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://www.tencentcloud.com/document/product/436/19889) | Setting versioning | Sets versioning configuration for a bucket |
| [GET Bucket versioning](https://www.tencentcloud.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |



## Setting Versioning

#### Feature description

This API (`PUT Bucket versioning`) is used to set the versioning configuration for a bucket.

#### Method prototype

```
put_bucket_versioning(Bucket, Status, **kwargs)
```

#### Request example

##### Enabling versioning

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print information about the communication with the server.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = os.environ['COS_SECRET_ID']     #  User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, see https://cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.put_bucket_versioning(
    Bucket='examplebucket-1250000000',
    Status='Enabled'
)
```

##### Suspending versioning

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print information about the communication with the server.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = os.environ['COS_SECRET_ID']     #  User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, see https://cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.put_bucket_versioning(
    Bucket='examplebucket-1250000000',
    Status='Suspended'
)
```

#### Field description

| Parameter | Description | Type | Required |
| -------- | ---------------------------------------------------------- | ------ | -------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Status | Sets the versioning status of a bucket. Valid values: `Suspended`, `Enabled` | String | Yes |


#### Response description

This API returns `None`.

## Querying Versioning

#### Feature description

This API (`GET Bucket versioning`) is used to query the versioning configuration of a bucket.

#### Method prototype

```
get_bucket_versioning(Bucket, **kwargs)
```


#### Request example

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print information about the communication with the server.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = os.environ['COS_SECRET_ID']     #  User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, see https://cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.get_bucket_versioning(
    Bucket='examplebucket-1250000000',
)
```


#### Field description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |

#### Response description

This API returns the versioning configuration on a bucket in dict format.

```python
{
    'Status': 'Enabled'|'Suspended'
}
```


| Parameter | Description | Type |
| -------- | ---------------------------------------------------- | ------ |
| Status | Sets the versioning status of a bucket. Valid values: `Suspended`, `Enabled` | String |




