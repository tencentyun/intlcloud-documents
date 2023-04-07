

## Feature Overview

This document provides an overview of APIs and SDK code samples for custom domains.

| API | Operation | Description |
| -------------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting a custom domain | Sets a custom domain for a bucket |
| GET Bucket domain    | Querying a custom domain | Queries the custom domain of a bucket |
| DELETE Bucket domain | Deleting custom domains | Deletes custom domains from a bucket |

## Setting Custom Domains

#### Feature description

This API is used to set a custom domain for a bucket.

#### Method prototype

```
put_bucket_domain(Bucket, DomainConfiguration={}, **kwargs)
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

response = client.put_bucket_domain(
    Bucket='bucket',
    DomainConfiguration={
        'DomainRule': [
            {
                'Name': 'example.com',
                'Type': 'REST'|'WEBSITE'|'ACCELERATE',
                'Status': 'ENABLED'|'DISABLED',
                'ForcedReplacement': 'CNAME'|'TXT'
            },
        ]
    }
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for custom domain name configuration, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312). | String | Yes       |
| DomainRule        | Custom domain set                                             | List   | Yes       |
| Name              | Custom domain name                                               | String | Yes       |
| Type    | Type of the origin server to bind. Valid values: `REST`, `WEBSITE`                                                             | String      | Yes       |
| Status | Status of the domain name. Valid values: `ENABLED`, `DISABLED` | String | Yes       |
| ForcedReplacement | Replaces existing configurations. Valid values: `CNAME`, `TXT`                    | String | No       |

#### Response description

This API returns `None`.

#### Error codes

The following describes some common errors that may occur when you call this API:

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict | The domain record already exists, and forced overwrite is not specified in the request; OR the domain record does not exist, and forced overwrite is specified in the request |
| HTTP 451 Unavailable For Legal Reasons | The domain does not have an ICP filing in the Chinese mainland                          |

## Querying a Custom Domain

#### Feature description

This API is used to query the custom domain set for a bucket.

#### Method prototype

```
get_bucket_domain(Bucket, **kwargs)
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

response = client.get_bucket_domain(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description 

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for custom domain name query, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312). | String | Yes       |

#### Response description

Custom domain configuration of the bucket in `dict` type.

```
{
    'x-cos-domain-txt-verification': 'string',
    'DomainRule': [
        {
            'Name': 'example.com',
            'Type': 'REST'|'WEBSITE'|'ACCELERATE',
            'Status': 'ENABLED'|'DISABLED',
            'ForcedReplacement': 'CNAME'|'TXT'
        },
    ]
}
```

| Parameter | Description | Type |
| ----------------------------- | ------------------------------------------------------------ | ------ |
| x-cos-domain-txt-verification | Domain verification information. This field is an MD5 checksum of a character string in the format: `cos[Region][BucketName-APPID][BucketCreateTime]`, where `Region` is the bucket region and `BucketCreateTime` is the time the bucket was created in GMT format | String |
| DomainRule        | Custom domain set                                             | List   |
| Name              | Custom domain name                                               | String |
| Type    | Type of the origin server to bind. Valid values: `REST`, `WEBSITE`                                                             | String      |
| Status | Status of the domain name. Valid values: `ENABLED`, `DISABLED` | String |
| ForcedReplacement | Replaces existing configurations. Valid values: `CNAME`, `TXT`                    | String |

## Deleting Custom Domains

#### Feature description

This API (`DELETE  Bucket domain`) is used to delete all custom domains bound to a bucket.

#### Method prototype

```
delete_bucket_domain(Bucket, **kwargs)
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

response = client.delete_bucket_domain(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for custom domain deletion, in the format of `BucketName-APPID`. For more information, see [Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312). | String | Yes |

#### Response description

This API returns `None`.
