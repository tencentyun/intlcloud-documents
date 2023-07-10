

## Overview

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tags | Sets tags for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tags | Deletes the tags of a bucket |

## Setting Bucket Tags

#### Description

This API is used to set tags for an existing bucket.

#### Method prototype

```
put_bucket_tagging(Bucket, Tagging={}, **kwargs)
```

#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import os
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = os.environ['COS_SECRET_ID']     # User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675

region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.put_bucket_tagging(
    Bucket='examplebucket-1250000000',
    Tagging={
        'TagSet': {
            'Tag': [
                {
                    'Key': 'string',
                    'Value': 'string'
                },
            ]
        }
    }
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for tag setting, in the format of `BucketName-APPID`. For more information, see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| Tag      | A collection of tags                                                   | List   | Yes       |
| Key | Tag key. A tag key must not exceed 128 characters and can contain letters, numbers, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes. | String | Yes |
| Value | Tag value. A tag value must not exceed 256 characters and can contain letters, numbers, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes. | String | Yes |

#### Response description

This API returns `None`.

## Querying Bucket Tags

#### Description

This API is used to query the existing tags of a specified bucket.

#### Method prototype

```
get_bucket_tagging(Bucket, **kwargs)
```

#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import os
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = os.environ['COS_SECRET_ID']     # User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675


region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.get_bucket_tagging(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description                        |

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for tag query, in the format of `BucketName-APPID`. For more information, see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |

#### Response description

Bucket tag management list in dict format.

```
{
    'TagSet': {
        'Tag': [
            {
                'Key': 'string',
                'Value': 'string'
            },
        ]
    }
}
```

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Tag      | A collection of tags                                                   | List   |
| Key | Tag key. A tag key must not exceed 128 characters and can contain letters, numbers, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes. | String |
| Value | Tag value. A tag value must not exceed 256 characters and can contain letters, numbers, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes. | String |

## Deleting Bucket Tags

#### Description

This API is used to delete the existing tags from a bucket.

#### Method prototype

```
delete_bucket_tagging(Bucket, **kwargs)
```

#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import os
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = os.environ['COS_SECRET_ID']     # User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675


region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.delete_bucket_tagging(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for tag deletion, in the format of `BucketName-APPID`. For more information, see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |

#### Response description

This API returns `None`.
