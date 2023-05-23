

## Feature Overview

This document provides an overview of APIs and SDK code samples for static website.

| API | Operation | Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://www.tencentcloud.com/document/product/436/30617) | Configuring a static website | Configures a static website for a bucket |
| [GET Bucket website](https://www.tencentcloud.com/document/product/436/30616) | Querying static website configuration | Queries the static website configuration of a bucket |
| [DELETE Bucket website](https://www.tencentcloud.com/document/product/436/30629) | Deleting static website configuration | Deletes the static website configuration from a bucket |

## Setting Static Website Configuration

#### Feature description

This API is used to configure a static website for a bucket.

#### Method prototype

```
put_bucket_website(Bucket, WebsiteConfiguration={}, **kwargs)
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

response = client.put_bucket_website(
    Bucket='bucket',
    WebsiteConfiguration={
        'IndexDocument': {
            'Suffix': 'string'
        },
        'ErrorDocument': {
            'Key': 'string'
        },
        'RedirectAllRequestsTo': {
            'Protocol': 'http'|'https'
        },
        'RoutingRules': [
            {
                'Condition': {
                    'HttpErrorCodeReturnedEquals': 'string',
                    'KeyPrefixEquals': 'string'
                },
                'Redirect': {
                    'HttpRedirectCode': 'string',
                    'Protocol': 'http'|'https',
                    'ReplaceKeyPrefixWith': 'string',
                    'ReplaceKeyWith': 'string'
                }
            }
        ]
    }
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for which a static website is configured, in the format of `BucketName-APPID`. For more information, see [Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312). | String | Yes |
| IndexDocument               | Sets the homepage of static website                                       | Dict   | Yes       |
| Suffix                      | Configures suffix for the homepage address of static website                                   | String | Yes       |
| ErrorDocument               | Sets the error page configuration of static website                                     | Dict   | No       |
| Key                         | Error page address                                                 | String | No       |
| RedirectAllRequestsTo       | Sets the global redirect configuration                                           | Dict   | No       |
| Protocol                    | Global redirect protocol. Valid values: http, https                          | String | No       |
| RoutingRules                | Sets the routing rules of static website                                         | List   | No       |
| Condition                   | Routing condition, including error code-triggered redirect and prefix-triggered redirect                      | Dict   | No       |
| HttpErrorCodeReturnedEquals | Condition for error code-triggered redirect                                           | String | No       |
| KeyPrefixEquals             | Condition for prefix-triggered redirect                                             | String | No       |
| Redirect                    | Specific rule for redirect                                             | Dict   | No       |
| HttpRedirectCode            | Error code during redirect                                             | String | No       |
| Protocol                    | Redirect protocol. Valid values: http, https                             | String | No       |
| ReplaceKeyPrefixWith        | Replaces the prefix with a specified `Key` during redirect                                  | String | No       |
| ReplaceKeyWith              | Replaces the entire path with a specified `Key` during redirect                              | String | No       |

#### Response description

This API returns `None`.

## Querying Static Website Configuration

#### Feature description

This API (`GET Bucket website`) is used to query the static website configuration associated with a bucket.

#### Method prototype

```
get_bucket_website(Bucket, **kwargs)
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

response = client.get_bucket_website(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description                        |

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for static website configuration query, in the format of `BucketName-APPID`. For more information, see [Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312) | String | Yes |

#### Response description

Static website configuration of the bucket in dict type.

```
{
    'IndexDocument': {
        'Suffix': 'string'
    },
    'ErrorDocument': {
        'Key': 'string'
    },
    'RedirectAllRequestsTo': {
        'Protocol': 'http'|'https'
    },
    'RoutingRules': [
        {
            'Condition': {
                'HttpErrorCodeReturnedEquals': 'string',
                'KeyPrefixEquals': 'string'
            },
            'Redirect': {
                'HttpRedirectCode': 'string',
                'Protocol': 'http'|'https',
                'ReplaceKeyPrefixWith': 'string',
                'ReplaceKeyWith': 'string'
            }
        }
    ]
}
```

| Parameter | Description | Type |
| --------------------------- | ---------------------------------------- | ------ |
| IndexDocument               | Sets the homepage of static website                                       | Dict   |
| Suffix                      | Configures suffix for the homepage address of static website                                   | String |
| ErrorDocument               | Sets the error page configuration of static website                                     | Dict   |
| Key                         | Error page address                                                 | String |
| RedirectAllRequestsTo       | Sets the global redirect configuration                                           | Dict   |
| Protocol                    | Global redirect protocol. Valid values: http, https                          | String |
| RoutingRules                | Sets the routing rules of static website                                         | List   |
| Condition                   | Routing condition, including error code-triggered redirect and prefix-triggered redirect                      | Dict   |
| HttpErrorCodeReturnedEquals | Condition for error code-triggered redirect                                           | String |
| KeyPrefixEquals             | Condition for prefix-triggered redirect                                             | String |
| Redirect                    | Specific rule for redirect                                             | Dict   |
| HttpRedirectCode            | Error code during redirect                                             | String |
| Protocol                    | Redirect protocol. Valid values: http, https                             | String |
| ReplaceKeyPrefixWith        | Replaces the prefix with a specified `Key` during redirect                                  | String |
| ReplaceKeyWith              | Replaces the entire path with a specified `Key` during redirect                              | String |

## Deleting Static Website Configuration

#### Feature description

This API (`DELETE Bucket website`) is used to delete the static website configuration of a bucket.

#### Method prototype

```
delete_bucket_website(Bucket, **kwargs)
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

response = client.delete_bucket_website(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for static website configuration deletion, in the format of `BucketName-APPID`. For more information, see [Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312) | String | Yes |

#### Response description

This API returns `None`.
