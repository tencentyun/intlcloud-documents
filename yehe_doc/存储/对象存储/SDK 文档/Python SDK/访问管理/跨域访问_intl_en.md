## Overview

This document provides an overview of APIs and SDK sample codes for cross-origin resource sharing (CORS).



| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://www.tencentcloud.com/document/product/436/8279) | Setting cross-origin access configuration | Sets cross-origin access permissions for a bucket |
| [GET Bucket cors](https://www.tencentcloud.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://www.tencentcloud.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration of a bucket |




## Setting CORS Configuration

#### Feature description

This API is used to set the CORS configuration of a specified bucket.

#### Method prototype

```
put_bucket_cors(Bucket, CORSConfiguration={}, **kwargs)
```

#### Request example

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
secret_id = os.environ['COS_SECRET_ID']     #  User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, see https://cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.put_bucket_cors(
    Bucket='examplebucket-1250000000',
    CORSConfiguration={
        'CORSRule': [
            {
                'ID': 'string',
                'MaxAgeSeconds': 100,
                'AllowedOrigin': [
                    'string',
                ],
                'AllowedMethod': [
                    'string',
                ],
                'AllowedHeader': [
                    'string',
                ],
                'ExposeHeader': [
                    'string',
                ]
            }
        ]
    },
)
```

#### Field description

| Parameter | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket  | Bucket name in the format of `BucketName-APPID`  | String | Yes  |
| CORSRule | Specifies the cross-origin access rule, including ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, and ExposeHeader | List | Yes|
| ID | Rule ID | string | No |
| MaxAgeSeconds | Validity period of the `OPTIONS` request result | int | No |
| AllowedOrigin | Sets allowed access sources, e.g. `"http://cloud.tencent.com"`. The wildcard "*" is supported. | Dict | Yes |
| AllowedMethod | Sets allowed methods, including GET, PUT, HEAD, POST, DELETE | Dict | Yes |
| AllowedHeader | Sets custom HTTP request headers that can be included in a request. The wildcard "*" is supported. | Dict | No |
| ExposeHeader | Configures custom headers that can be received by the browser from the server. | Dict | No |

#### Response description

This API returns `None`.

## Querying CORS Configuration

#### Feature description

This API is used to query the CORS configuration of a bucket.

#### Method prototype


```
get_bucket_cors(Bucket, **kwargs)
```


#### Request example

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
secret_id = os.environ['COS_SECRET_ID']     #  User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, see https://cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.get_bucket_cors(
    Bucket='examplebucket-1250000000',
)
```


#### Field description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |


#### Response description


This API returns the cross-origin access configuration on a bucket in dict format.


```python
{
    'CORSRule': [
        {
            'ID': 'string',
            'MaxAgeSeconds': 100,
            'AllowedOrigin': [
                'string',
            ],
            'AllowedMethod': [
                'string',
            ],
            'AllowedHeader': [
                'string',
            ],
            'ExposeHeader': [
                'string',
            ],
        }
    ]
}
```

| Parameter | Description | Type |
| ------------- | ------------------------------------------------------------ | ------ |
| CORSRule | Specifies the cross-origin access rule, including ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, and ExposeHeader | List |
| - - ID | Configures the rule ID | String |
| MaxAgeSeconds | Sets the validity period of the OPTIONS request result | String |
| AllowedOrigin | Allowed access sources, e.g. `"http://cloud.tencent.com"`. The wildcard "*" is supported. | Dict |
| AllowedMethod | Allowed methods, including GET, PUT, HEAD, POST, DELETE | Dict |
| AllowedHeader | Sets custom HTTP request headers that can be included in a request. The wildcard "*" is supported. | Dict |
| ExposeHeader | Configures custom headers that can be received by the browser from the server. | Dict |


## Deleting CORS Configuration

#### Feature description

This API is used to delete the CORS configuration of a bucket.

#### Method prototype

```
delete_bucket_cors(Bucket, **kwargs)
```

#### Request example

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
secret_id = os.environ['COS_SECRET_ID']     #  User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, see https://cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.delete_bucket_cors(
    Bucket='examplebucket-1250000000',
)
```


#### Field description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |

#### Response description

This API returns `None`.



