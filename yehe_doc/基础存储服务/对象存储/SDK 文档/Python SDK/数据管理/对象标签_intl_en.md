## Overview

This document provides an overview of APIs and SDK code samples for object tagging.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object tagging](https://www.tencentcloud.com/document/product/436/35709) | Tagging an object | Tags an existing object. |
| [GET Object tagging](https://www.tencentcloud.com/document/product/436/35710) | Querying object tags | Queries all tags of an object |
| [DELETE Object tagging](https://www.tencentcloud.com/document/product/436/35711) | Deleting object tags | Deletes all tags of an object |

## Tagging an Object

#### Feature description

This API (`PUT Object tagging`) is used to tag an existing object.

#### Method prototype

```
put_object_tagging(self, Bucket, Key, Tagging={}, **kwargs)
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

response = client.put_object_tagging(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Tagging={
        'TagSet': {
            'Tag': [
                {
                    'Key': "string",
                    'Value': 'string'
                }
            ]
        }
    }
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket   | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://www.tencentcloud.com/document/product/436/13312)  | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.tencentcos.cn/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| Tag      | A collection of tags                                                   | List   | Yes       |
| Key | Tag key. A tag key must not exceed 128 characters and can contain letters, numbers, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes. | String | Yes |
| Value | Tag value. A tag value must not exceed 256 characters and can contain letters, numbers, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes. | String | Yes |


#### Response description

This API returns `None`.

## Querying Object Tags

#### Feature description

This API (`GET Object tagging`) is used to query the existing tags of an object.

#### Method prototype

```
get_object_tagging(self, Bucket, Key, **kwargs)
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

response = client.get_object_tagging(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
print(response)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket   | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://www.tencentcloud.com/document/product/436/13312)  | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.tencentcos.cn/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |

#### Response description

The list of object tags in the `dict` type.

```
{
    'TagSet': {
        'Tag': [
            {
                'Key': 'string',
                'Value': 'string'
            }
        ]
    }
}
```

## Deleting Object Tags

#### Feature description

This API (`DELETE Object tagging`) is used to delete existing tags of an object.

#### Method prototype

```
delete_object_tagging(self, Bucket, Key, **kwargs)
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

response = client.delete_object_tagging(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket   | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://www.tencentcloud.com/document/product/436/13312)  | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.tencentcos.cn/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |

#### Response description

This API returns `None`.
