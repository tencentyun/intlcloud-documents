## Overview
This document provides an overview of APIs and SDK code samples related to cross-origin access, lifecycle, versioning, and cross-region replication.

**CORS**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting CORS | Sets CORS permissions for a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying CORS configuration | Queries the CORS configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting CORS configuration | Deletes the CORS configuration of a bucket |

**Lifecycle**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle configuration | Sets lifecycle management configuration for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying a lifecycle configuration | Queries the lifecycle configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle configuration | Deletes the lifecycle management configuration from a bucket |

**Versioning**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting a cross-region replication rule | Sets a cross-region replication rule for a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying a cross-region replication rule | Queries the cross-region replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting a cross-region replication rule | Deletes the cross-region replication rule from a bucket |

**Access policy**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | Setting a bucket policy | Sets an access policy for a bucket |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | Querying a bucket policy | Queries the access policy of a bucket |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | Deleting a bucket policy | Deletes the access policy from a bucket |

## CORS
### Setting CORS

#### Description

This API (PUT Bucket cors) is used to set CORS for a bucket.

#### Method prototype

```
put_bucket_cors(Bucket, CORSConfiguration={}, **kwargs)
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
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

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
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format: BucketName-APPID | String | Yes |
| CORSRule | Specifies the cross-origin access rule, including ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, and ExposeHeader | List | Yes|
| ID | Sets rule ID | String | No |
| MaxAgeSeconds | Sets the validity period of the OPTIONS request result | Int | No |
| AllowedOrigin | Sets allowed access sources, e.g. `"http://cloud.tencent.com"`. The wildcard "*" is supported. | Dict | Yes |
| AllowedMethod | Sets allowed methods, including GET, PUT, HEAD, POST, DELETE | Dict | Yes |
| AllowedHeader | Sets custom HTTP request headers that can be included in a request. The wildcard "*" is supported. | Dict | No |
| ExposeHeader | Configures custom headers that can be received by the browser from the server. | Dict | No |

#### Response description
This API returns `None`.

### Querying a CORS configuration

#### Description

This API is used to query the cross-origin access configuration of a bucket.

#### Method prototype

```
get_bucket_cors(Bucket, **kwargs)
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
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.get_bucket_cors(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
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
| -------------- | -------------- |---------- |
| CORSRule | Specifies the cross-origin access rule, including ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, and ExposeHeader | List |
| ID | Rule ID | String |
| MaxAgeSeconds | Sets the validity period of the OPTIONS request result | String |
| AllowedOrigin | Allowed access sources, e.g. `"http://cloud.tencent.com"`. The wildcard "*" is supported. | Dict |
| AllowedMethod | Allowed methods, including GET, PUT, HEAD, POST, DELETE | Dict |
| AllowedHeader | Sets custom HTTP request headers that can be included in a request. The wildcard "*" is supported. | Dict |
| ExposeHeader | Configures custom headers that can be received by the browser from the server. | Dict |


### Deleting CORS configuration

#### Description

This API (DELETE Bucket cors) is used to delete the CORS configuration of a bucket.

#### Method prototype

```
delete_bucket_cors(Bucket, **kwargs)
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
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.delete_bucket_cors(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter description

| Parameter | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format: BucketName-APPID | String | Yes |

#### Response description

This API returns `None`.


## Lifecycle
### Setting lifecycle configuration

#### Description

This API (PUT Bucket lifecycle) is used to set the lifecycle configuration for a bucket.

#### Method prototype

```
put_bucket_lifecycle(Bucket, LifecycleConfiguration={}, **kwargs)
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
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.put_bucket_lifecycle(
    Bucket='examplebucket-1250000000',
    LifecycleConfiguration={
        'Rule': [
            {
                'ID': 'string', # Rule ID, such as `Rule-1`
                'Filter': { 
                    'Prefix': '', # If this field is left empty, the rule applies to all objects in the bucket.
                },
                'Status': 'Enabled', # `Enabled` means to enable the rule.
                'Expiration': {
                    'Days': 200 # Set the current version of the object to be expired and deleted 200 days later.
                },
                'Transition': [
                    {
                        'Days': 100, # Set the current version of the object to be transitioned 100 days later.
                        'StorageClass': 'Standard_IA' # Transition the storage class to STANDARD_IA.
                    },
                ],
                'AbortIncompleteMultipartUpload': {
                    'DaysAfterInitiation': 7 # Set parts that are not merged to be repossessed 7 days later.
                }
            }
        ]   
    }
)
```
#### Sample request with all parameters

```python
from qcloud_cos import get_date
response = client.put_bucket_lifecycle(
    Bucket='examplebucket-1250000000',
    LifecycleConfiguration={
        'Rule': [
            {
                'ID': 'string', # Rule ID, such as `Rule-1`
                'Filter': {
                    'Prefix': 'string', # If a prefix is specified, this rule applies only to the objects with the prefix.
                    'Tag': [ # Set the tag filtering rule. The rule applies only to objects that match the tag. You need to specify either `Tag` or `Prefix`, not both.
                        {
                            'Key': 'string', 
                            'Value': 'string'
                        }
                    ]
                },
                'Status': 'Enabled'|'Disabled', # `Enabled` means to enable the rule. `Disabled` means to disable the rule. Specify either `Enabled` or `Disabled`.
                'Expiration': { 
                    'Days': 100 # Set the current version of the object to be expired and deleted 100 days later.
                    'Date': get_date(2021, 4, 20) # Set the current version of the object to be expired and deleted after April 20, 2021. You need to specify either `Date` or `Days`, not both.
                },
                'Transition': [
                    {
                        'Days': 60, # Set the current version of the object to be transitioned 60 days later.
                        'Date': get_date(2021, 4, 20), # Set the current version of the object to be transitioned after April 20, 2021. You need to specify either `Date` or `Days`, not both.
                        'StorageClass': 'Archive' # Transition the storage class to ARCHIVE.
                    },
                ],
                'NoncurrentVersionExpiration': {
                    'NoncurrentDays': 100 # Set the non-current versions of the object to be expired and deleted 100 days later.
                },
                'NoncurrentVersionTransition': [
                    {
                        'NoncurrentDays': 60, # Set the non-current versions of the object to be transitioned 60 days later.
                        'StorageClass': 'Standard_IA' # Transition the storage class to STANDARD_IA.
                    },
                ],
                'AbortIncompleteMultipartUpload': {
                    'DaysAfterInitiation': 100 # Set parts that are not merged to be repossessed 100 days later.
                }
            }
        ]   
    }
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Rule | Sets the rule, including ID, Filter, Status, Expiration, Transition, NoncurrentVersionExpiration, NoncurrentVersionTransition, AbortIncompleteMultipartUpload | List | Yes |
| ID | Sets rule ID. | String | No |
| Filter | Describes a set of objects that are subject to the rule. To set the rule for all objects in the bucket, leave `Prefix` empty. | Dict | Yes |
| Status | Sets whether the rule is enabled. Valid values: `Enabled`, `Disabled` | Dict | Yes |
|  Expiration  | Specifies when objects expire. It can be an expiry date or the number of days before objects expire. The date must be in GMT ISO 8601 format. You can specify the date using the `get_date` method. | Dict | No |
| Transition | Sets one or more rules for when an object transitions to a specified storage class. You can specify the number of days before the transition occurs or a transition date. The date must be in GMT ISO 8601 format. You can specify the date using the `get_date` method. The valid values for StorageClass include Standard_IA, Archive, and Deep_Archive. | List | No |
| NoncurrentVersionExpiration | Sets when noncurrent object versions expire. You can specify the number of days before objects expire (NoncurrentDays). | Dict | No |
|  NoncurrentVersionTransition  | Sets one or more transition rules that describe when noncurrent objects transition to another storage class. You can specify the number of days (NoncurrentDays). The valid value for `StorageClass` is Standard_IA. | List | No |
| AbortIncompleteMultipartUpload | Indicates the number of days within which the upload must be completed after the multipart upload starts. | Dict | No |


#### Response description

This API returns `None`.


### Querying a lifecycle configuration

#### Description

This API is used to query the lifecycle configuration of a bucket.

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
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.get_bucket_lifecycle(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format: BucketName-APPID | String | Yes |

#### Response description

This API returns the lifecycle configuration on a bucket in dict format.
```python
{
    'Rule': [
        {
            'ID': 'string',
            'Filter': {
                'Prefix': 'string',
                'Tag': [
                        {
                            'Key': 'string',
                            'Value': 'string'
                        }
                ]
            },
            'Status': 'string',
            'Expiration': {
                'Days': 100,
                'Date': 'string'
            },
            'Transition': [
                {
                    'Days': 100,
                    'Date': 'string',
                    'StorageClass': 'STANDARD_IA'|'Archive'
                },
            ],
            'NoncurrentVersionExpiration': {
                'NoncurrentDays': 100
            },
            'NoncurrentVersionTransition': [
                {
                    'NoncurrentDays': 100,
                    'StorageClass': 'STANDARD_IA'
                },
            ],
            'AbortIncompleteMultipartUpload': {
                'DaysAfterInitiation': 100
            }
        }
    ]   
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| Rule | Sets the rule, including ID, Filter, Status, Expiration, Transition, NoncurrentVersionExpiration, NoncurrentVersionTransition, AbortIncompleteMultipartUpload | List |
| ID | Rule ID | String |
| Filter | Describes a set of objects that are subject to the rule. | Dict |
| Status | Sets whether the rule is enabled. Valid values: `Enabled`, `Disabled` | Dict |
| Expiration | Specifies when objects expire. It can be an expiry date (`Date`) or the number of days before objects expire (`Days`) | Dict |
| Transition | Specifies when objects transition to another storage class. It can be an expiry date (`Date`) or the number of days before objects transition (`Days`). Valid values for StorageClass: STANDARD_IA, Archive | List |
| NoncurrentVersionExpiration | Sets the expiration rule for noncurrent object versions. You can specify the number of days before the object expires (NoncurrentDays). | Dict |
|  NoncurrentVersionTransition  | Specifies the rule for transitioning noncurrent objects to another storage class. You can specify the number of days (NoncurrentDays). Valid value for StorageClass: STANDARD_IA. | List |
| AbortIncompleteMultipartUpload | Specifies the number of days within which the upload must be completed after the multipart upload starts. | Dict |


### Deleting a lifecycle configuration

#### Description

This API is used to delete the lifecycle configuration from a bucket.

#### Method prototype

```
delete_bucket_lifecycle(Bucket, **kwargs)
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
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.delete_bucket_lifecycle(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format: BucketName-APPID | String | Yes |

#### Response description

This API returns `None`.


## Versioning
### Setting versioning

#### Description

This API (PUT Bucket versioning) is used to set the versioning configuration for a bucket.

#### Method prototype
```
put_bucket_versioning(Bucket, Status, **kwargs)
```

#### Sample request

##### Enabling versioning
```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

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

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.put_bucket_versioning(
    Bucket='examplebucket-1250000000',
    Status='Suspended'
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Status | Sets the versioning status of a bucket. Valid values: `Suspended`, `Enabled` | String | Yes |


#### Response description

This API returns `None`.

### Querying versioning

#### Description

This API (GET Bucket versioning) is used to query the versioning configuration of a bucket.

#### Method prototype

```
get_bucket_versioning(Bucket, **kwargs)
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
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.get_bucket_versioning(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format: BucketName-APPID | String | Yes |

#### Response description

This API returns the versioning configuration on a bucket in dict format.
```python
{
    'Status': 'Enabled'|'Suspended'
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| Status | Sets the versioning status of a bucket. Valid values: `Suspended`, `Enabled` | String |


## Cross-Region Replication
### Setting a cross-region replication rule

#### Description

This API (PUT Bucket replication) is used to set the cross-bucket replication rule for a bucket.

#### Method prototype

```
put_bucket_replication(Bucket, ReplicationConfiguration={}, **kwargs)
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
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.put_bucket_replication(
    Bucket='examplebucket-1250000000',
    ReplicationConfiguration={
        'Role': 'qcs::cam::uin/100000000001:uin/100000000001',
        'Rule': [
            {
                'ID': 'string',
                'Status': 'Enabled',
                'Destination': {
                    'Bucket': 'qcs::cos:ap-shanghai::destinationbucket-1250000000',
                    'StorageClass': 'STANDARD'
                }
            }
        ]   
    }
)
```
#### Sample request with all parameters

```python
response = client.put_bucket_replication(
    Bucket='examplebucket-1250000000',
    ReplicationConfiguration={
        'Role': 'qcs::cam::uin/100000000001:uin/100000000001',
        'Rule': [
            {
                'ID': 'string',
                'Status': 'Enabled'|'Disabled',
                'Prefix': 'string',
                'Destination': {
                    'Bucket': 'qcs::cos:ap-beijing::destinationbucket-1250000000',
                    'StorageClass': 'STANDARD'|'STANDARD_IA'
                }
            },
            {
                'ID': 'string',
                'Status': 'Enabled'|'Disabled',
                'Prefix': 'string',
                'Destination': {
                    'Bucket': 'qcs::cos:ap-beijing::destinationbucket2-1250000000',
                    'StorageClass': 'STANDARD'|'STANDARD_IA'
                }
            },
        ]   
    }
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format: BucketName-APPID | String | Yes |
| Role | Replication initiator identifier: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | String | No |
| Rule | Sets the rule, including ID, Status, Prefix, and Destination | List | Yes |
| ID | Sets rule ID. | String | No |
| Status  | Sets whether the rule is enabled. Valid values: `Enabled`, `Disabled` | String | Yes |
| Prefix | Specifies the prefix used to filter objects. If it is left empty, the rule applies to all objects in the bucket | String |  Yes |
| Destination | Describes the destination resource, including `Bucket` and `StorageClass`  | Dict | Yes |
| Bucket | Sets the destination bucket for cross-region replication. Format: `qcs::cos:[region]::[BucketName-APPID]`  | String  | Yes |
| StorageClass | Sets the storage class of the object copies. Valid values: `STANDARD`, `STANDARD_IA` | String | No |

#### Response description

This API returns `None`.

### Querying a cross-region replication rule

#### Description

This API (GET Bucket replication) is used to query the cross-bucket replication rule of a bucket.

#### Method prototype

```
get_bucket_replication(Bucket, **kwargs)
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
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.get_bucket_replication(
    Bucket='examplebucket-1250000000'
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |

#### Response description

This API returns the cross-region replication configuration on a bucket in dict format.
```python
{
    'Role': 'qcs::cam::uin/100000000001:uin/100000000001',
    'Rule': [
        {
            'ID': 'string',
            'Status': 'Enabled'|'Disabled',
            'Prefix': 'string',
            'Destination': {
                'Bucket': 'qcs::cos:ap-beijing::destinationbucket-1250000000',
                'StorageClass': 'STANDARD'|'STANDARD_IA'
            }
        },
        {
            'ID': 'string',
            'Status': 'Enabled'|'Disabled',
            'Prefix': 'string',
            'Destination': {
                'Bucket': 'qcs::cos:ap-beijing::destinationbucket2-1250000000',
                'StorageClass': 'STANDARD'|'STANDARD_IA'
            }
        },
    ]  
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| Role | Replication initiator identifier: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | String | No |
| Rule | Sets the rule for cross-region replication, including ID, Status, Prefix, and Destination | List | Yes |
|  ID  | Specifies the ID of the cross-region replication rule| String |  No |
| Status  | Sets whether the rule is enabled. Valid values: `Enabled`, `Disabled` | String | Yes |
| Prefix | Specifies the prefix used to filter objects that are subject to the rule. If it is left empty, the rule applies to all objects in the bucket | String |  Yes |
| Destination |   Describes the destination resource, including `Bucket` and `StorageClass` | Dict | Yes |
| Bucket | Sets the destination bucket for cross-region replication. Format: `qcs::cos:[region]::[BucketName-APPID]`  | String  | Yes |
| StorageClass | Sets the storage class of the object copies. Valid values: `STANDARD`, `STANDARD_IA` | String | No |


### Deleting a cross-region replication rule

#### Description

This API (DELETE Bucket replication) is used to delete the cross-bucket replication rule from a bucket.

#### Method prototype

```
delete_bucket_replication(Bucket, **kwargs)
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
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.delete_bucket_replication(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format: BucketName-APPID | String | Yes |

#### Response description

This API returns `None`.


## Access Policy
### Setting an access policy

#### Description

This API is used to set an access policy on a bucket.

#### Method prototype

```
put_bucket_policy(Bucket, Policy, **kwargs)
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
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.put_bucket_policy(
    Bucket='examplebucket-1250000000',
    Policy={
        "Statement":[
            {
                "Principal":{
                    "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000011"
                    ]
                },
                "Effect": "allow",
                "Action":[
                    "name/cos:GetBucket"
                ],
                "Resource":[
                    "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
                ]
                "condition": {
                    "ip_equal":{
                    "qcs:ip": "10.121.2.10/24"
                    }
                }
            }
        ],
        "version": "2.0"
    }
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format: BucketName-APPID | String | Yes |
| Statement | Specifies one or more permissions |List| Yes |
| Principal | Specifies the entity to which the permission is granted. For more information, see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023)|Dict| Yes |
| Version |Specifies the version of policy syntax. Default: 2.0|String|Yes |
| Effect | Allow or deny |String| Yes |
| Action | COS API. You can specify one, several, or all (`*`) COS APIs as needed, e.g. `name/cos:GetService`. **Note that this value is case-sensitive**.    |List | Yes |
| Resource | Specifies the resource for which permission is granted. It can be any resource, a resource in a path with a specified prefix, a resource in a specified absolute path, or a combination thereof. |List | Yes |
| Condition | (Optional) Specifies the rule condition. For more information, see [condition](https://intl.cloud.tencent.com/document/product/598/10603) |List | No |


#### Response description

This API returns `None`.


### Querying an access policy

#### Description

This API is used to query the access policy on a bucket.

#### Method prototype

```
get_bucket_policy(Bucket, **kwargs)
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
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.get_bucket_policy(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format: BucketName-APPID | String | Yes |


#### Response description

This API returns the access policy on a bucket in dict format.
```python
{
    "Statement":[
        {
            "Principal":{
                "qcs":[
                "qcs::cam::uin/100000000001:uin/100000000011"
                ]
            },
            "Effect": "allow",
            "Action":[
                "name/cos:GetBucket"
            ],
            "Resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ]
            "condition": {
                "ip_equal":{
                "qcs:ip": "10.121.2.10/24"
                }
            }
        }
    ],
    "version": "2.0"
}
```

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Statement | Specifies one or more permissions |List| Yes |
| Principal | Specifies the entity to which the permission is granted. For more information, see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023)|Dict| Yes |
| Version |Specifies the version of policy syntax. Default: 2.0|String|Yes |
| Effect | Allow or deny |String| Yes |
| Action | COS API. You can specify one, several, or all (`*`) COS APIs as needed, e.g. `name/cos:GetService`. **Note that this value is case-sensitive**.    |List | Yes |
| Resource | Specifies the resource for which permission is granted. It can be any resource, a resource in a path with a specified prefix, a resource in a specified absolute path, or a combination thereof. |List | Yes |
| Condition | (Optional) Specifies the rule condition. For more information, see [condition](https://intl.cloud.tencent.com/document/product/598/10603) |List | No |


### Deleting an access policy

#### Description

This API is used to delete the access policy from a specified bucket.

#### Method prototype

```
delete_bucket_policy(Bucket, **kwargs)
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
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.delete_bucket_policy(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format: BucketName-APPID | String | Yes |


#### Response description

This API returns `None`.

