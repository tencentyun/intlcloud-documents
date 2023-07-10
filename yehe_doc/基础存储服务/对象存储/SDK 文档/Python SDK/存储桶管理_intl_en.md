## Overview
This document provides an overview of APIs and SDK code samples for CORS, lifecycle, versioning, and cross-region replication.

**CORS**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting CORS configuration | Sets the CORS configuration for a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying CORS configuration | Queries the CORS configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting CORS configuration | Deletes the CORS configuration of a bucket |

**Lifecycle**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle configuration | Sets the lifecycle configuration for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle configuration | Queries the lifecycle configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle configuration | Deletes the lifecycle configuration of a bucket |

**Versioning**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting the cross-region replication rule | Sets the cross-region replication rule for a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying the cross-region replication rule | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting the cross-region replication rule | Deletes the cross-region replication rule of a bucket |

**Permission policy**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | Setting the permission policy | Sets the permission policy for a bucket |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | Querying the permission policy | Queries the permission policy of a bucket |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | Deleting the permission policy | Deletes the permission policy of a bucket |

## CORS
### Setting CORS configuration

#### Feature description

This API (`PUT Bucket cors`) is used to set the CORS configuration for a bucket.

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

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
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
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String | Yes |
| CORSRule | Sets the CORS rule, including `ID`, `MaxAgeSeconds`, `AllowedOrigin`, `AllowedMethod`, `AllowedHeader`, and `ExposeHeader`. | List | Yes |
| ID | Sets the rule ID | String | No |
| MaxAgeSeconds | Sets the validity period of the OPTIONS request result | Int | No |
| AllowedOrigin | Sets allowed access sources, such as `"http://cloud.tencent.com"`. The wildcard `*` is supported. | Dict | Yes |
| AllowedMethod | Sets allowed methods, such as `GET`, `PUT`, `HEAD`, `POST`, and `DELETE`. | Dict | Yes |
| AllowedHeader | Sets custom HTTP request headers that can be included in a request. The wildcard `*` is supported. | Dict | No |
| ExposeHeader | Sets custom headers that can be received by the browser from the server. | Dict | No |

#### Response description
This API returns `None`.

### Querying CORS configuration

#### Feature description

This API (`GET Bucket cors`) is used to query the CORS configuration of a bucket.

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

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

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

This API returns the CORS configuration of the bucket of `dict` type.
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
| CORSRule | CORS rule, including `ID`, `MaxAgeSeconds`, `AllowedOrigin`, `AllowedMethod`, `AllowedHeader`, and `ExposeHeader`. | List |
| ID | Rule ID | String |
| MaxAgeSeconds  |  Validity period of the OPTIONS request result | String |
| AllowedOrigin  | Allowed access sources, such as `"http://cloud.tencent.com"`. The wildcard `*` is supported.  | Dict |
| AllowedMethod  |  Allowed methods, such as `GET`, `PUT`, `HEAD`, `POST`, and `DELETE`. | Dict |
| AllowedHeader  | Custom HTTP request headers that can be included in a request. The wildcard `*` is supported. |  Dict |
| ExposeHeader  | Custom headers that can be received by the browser from the server. | Dict |


### Deleting CORS configuration

#### Feature description

This API (`DELETE Bucket cors`) is used to delete the CORS configuration of a bucket.

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

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.delete_bucket_cors(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter description

| Parameter | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String | Yes |

#### Response description

This API returns `None`.


## Lifecycle
### Setting lifecycle configuration

#### Feature description

This API (`PUT Bucket lifecycle`) is used to set the lifecycle configuration for a bucket.

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

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.put_bucket_lifecycle(
    Bucket='examplebucket-1250000000',
    LifecycleConfiguration={
        'Rule': [
            {
                'ID': 'string', # Set the rule ID, such as `Rule-1`.
                'Filter': { 
                    'Prefix': '', # If this field is left empty, the rule applies to all objects in the bucket.
                },
                'Status': 'Enabled', # `Enabled` indicates to enable the rule.
                'Expiration': {
                    'Days': 200 # Set the current version of the object to be expired and deleted in 200 days.
                },
                'Transition': [
                    {
                        'Days': 100, # Set the current version of the object to be transitioned in 100 days.
                        'StorageClass': 'Standard_IA' # Transition the storage class to STANDARD_IA.
                    },
                ],
                'AbortIncompleteMultipartUpload': {
                    'DaysAfterInitiation': 7 # Set parts that are not merged to be repossessed in 7 days.
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
                'ID': 'string', # Set the rule ID, such as `Rule-1`.
                'Filter': {
                    'Prefix': 'string', # If a prefix is specified, this rule applies only to objects with the prefix.
                    'Tag': [ # Set the tag filtering rule. The rule applies only to objects with the specified tag. You need to specify either `Tag` or `Prefix`.
                        {
                            'Key': 'string', 
                            'Value': 'string'
                        }
                    ]
                },
                'Status': 'Enabled'|'Disabled', # `Enabled` and `Disabled` indicate to enable and disable the rule respectively. You need to specify either `Enabled` or `Disabled`.
                'Expiration': { 
                    'Days': 100, # Set the current version of the object to be expired and deleted in 100 days.
                    'Date': get_date(2021, 4, 20) # Set the current version of the object to be expired and deleted after April 20, 2021. You need to specify either `Date` or `Days`.
                },
                'Transition': [
                    {
                        'Days': 60, # Set the current version of the object to be transitioned in 60 days.
                        'Date': get_date(2021, 4, 20), # Set the current version of the object to be transitioned after April 20, 2021. You need to specify either `Date` or `Days`.
                        'StorageClass': 'Archive' # Transition the storage class to ARCHIVE.
                    },
                ],
                'NoncurrentVersionExpiration': {
                    'NoncurrentDays': 100 # Set the non-current versions of the object to be expired and deleted in 100 days.
                },
                'NoncurrentVersionTransition': [
                    {
                        'NoncurrentDays': 60, # Set the non-current versions of the object to be transitioned in 60 days.
                        'StorageClass': 'Standard_IA' # Transition the storage class to STANDARD_IA.
                    },
                ],
                'AbortIncompleteMultipartUpload': {
                    'DaysAfterInitiation': 100 # Set parts that are not merged to be repossessed in 100 days.
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
| Rule | Sets the rule, including `ID`, `Filter`, `Status`, `Expiration`, `Transition`, `NoncurrentVersionExpiration`, `NoncurrentVersionTransition`, and `AbortIncompleteMultipartUpload`. | List | Yes |
| ID | Sets the rule ID. | String | No |
| Filter | Describes the set of objects that are subject to the rule. To set the rule for all objects in the bucket, leave `Prefix` empty. | Dict | Yes |
| Status | Sets whether the rule is enabled. Valid values: `Enabled`, `Disabled`. | Dict | Yes |
|  Expiration  | Sets the rule for when objects expire. You can specify the number of days (`Days`) or the date (`Date`) in GMT ISO 8601 format by using the `get_date` method. | Dict | No |
| Transition | Sets one or more rules for when objects are transitioned to the specified storage class. You can specify the number of days (`Days`) or the date (`Date`) in GMT ISO 8601 format by using the `get_date` method. Valid values of `StorageClass` include `Standard_IA`, `Archive`, and `Deep_Archive`. | List | No |
| NoncurrentVersionExpiration | Sets the rule for when non-current object versions expire. You can specify the number of days (`NoncurrentDays`). | Dict | No |
|  NoncurrentVersionTransition  | Sets one or more rules for when non-current objects are transitioned to the specified storage class. You can specify the number of days (`NoncurrentDays`). The valid value for `StorageClass` is `Standard_IA`. | List | No |
| AbortIncompleteMultipartUpload | Specifies the number of days within which a multipart upload must be completed after it starts. | Dict | No |


#### Response description

This API returns `None`.


### Querying lifecycle configuration

#### Feature description

This API (`GET Bucket lifecycle`) is used to query the lifecycle configuration of a bucket.

#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.get_bucket_lifecycle(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String | Yes |

#### Response description

This API returns the lifecycle configuration of the bucket of `dict` type.
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
| Rule | The rule, including `ID`, `Filter`, `Status`, `Expiration`, `Transition`, `NoncurrentVersionExpiration`, `NoncurrentVersionTransition`, and `AbortIncompleteMultipartUpload`. | List |
| ID | Rule ID | String |
| Filter | The set of objects that are subject to the rule. | Dict |
| Status | Whether the rule is enabled. Valid values: `Enabled`, `Disabled`. | Dict |
| Expiration | The rule for when objects expire. You can specify the number of days (`Days`) or the date (`Date`). | Dict |
| Transition | The rule for when objects are transitioned to the specified storage class. You can specify the number of days (`Days`) or the date (`Date`). Valid values of `StorageClass` include `STANDARD_IA` and `Archive`. | List |
| NoncurrentVersionExpiration | The rule for when non-current object versions expire. You can specify the number of days (`NoncurrentDays`). | Dict |
|  NoncurrentVersionTransition  | The rule for when non-current objects are transitioned to the specified storage class. You can specify the number of days (`NoncurrentDays`). The valid value for `StorageClass` is `Standard_IA`. | List |
| AbortIncompleteMultipartUpload | The number of days within which a multipart upload must be completed after it starts. | Dict |


### Deleting lifecycle configuration

#### Feature description

This API (`DELETE Bucket lifecycle`) is used to delete the lifecycle configuration of a bucket.

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

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.delete_bucket_lifecycle(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String | Yes |

#### Response description

This API returns `None`.


## Versioning
### Setting versioning

#### Feature description

This API (`PUT Bucket versioning`) is used to set the versioning configuration for a bucket.

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

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
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

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

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
| Status | Sets the versioning status of a bucket. Valid values: `Suspended`, `Enabled`. | String | Yes |


#### Response description

This API returns `None`.

### Querying versioning

#### Feature description

This API (`GET Bucket versioning`) is used to query the versioning configuration of a bucket.

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

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.get_bucket_versioning(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String | Yes |

#### Response description

This API returns the versioning configuration of the bucket of `dict` type.
```python
{
    'Status': 'Enabled'|'Suspended'
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| Status | The versioning status of a bucket. Valid values: `Suspended`, `Enabled`. | String |


## Cross-Region Replication
### Setting cross-region replication rule

#### Feature description

This API (`PUT Bucket replication`) is used to set the cross-bucket replication rule for a bucket.

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

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

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
| Bucket | Source Bucket name in the format of `BucketName-APPID`. | String | Yes |
| Role | Initiator identifier in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. | String | No |
| Rule | Sets the rule, including `ID`, `Status`, `Prefix`, and `Destination`. | List | Yes |
| ID | Sets the rule ID. | String | No |
| Status | Sets whether the rule is enabled. Valid values: `Enabled`, `Disabled`. | String | Yes |
| Prefix | Sets the prefix used to filter objects. If it is left empty, the rule applies to all objects in the bucket. | String |  Yes |
| Destination | Describes the destination resource, including `Bucket` and `StorageClass`.  | Dict | Yes |
| Bucket | Sets the destination bucket for cross-region replication in the format of `qcs::cos:[region]::[BucketName-APPID]`.  | String  | Yes |
| StorageClass | Sets the storage class of object copies. Valid values: `STANDARD`, `STANDARD_IA`. | String | No |

#### Response description

This API returns `None`.

### Querying cross-region replication rule

#### Feature description

This API (`GET Bucket replication`) is used to query the cross-bucket replication rule of a bucket.

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

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

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

This API returns the cross-region replication configuration of the bucket of `dict` type.
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
| Role | Initiator identifier in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. | String | 
| Rule | The rule for cross-region replication, including `ID`, `Status`, `Prefix`, and `Destination`. | List | 
|  ID  | ID of the cross-region replication rule. | String | 
| Status  | Whether the rule is enabled. Valid values: `Enabled`, `Disabled`. | String | 
| Prefix | The prefix used to filter objects. If it is left empty, the rule applies to all objects in the bucket. | String |  
| Destination |   The destination resource, including `Bucket` and `StorageClass`. | Dict | 
| Bucket | The destination bucket for cross-region replication in the format of `qcs::cos:[region]::[BucketName-APPID]`.  | String  | 
| StorageClass | The storage class of object copies. Valid values: `STANDARD`, `STANDARD_IA`. | String | 


### Deleting cross-region replication rule

#### Feature description

This API (`DELETE Bucket replication`) is used to delete the cross-bucket replication rule of a bucket.

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

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.delete_bucket_replication(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String | Yes |

#### Response description

This API returns `None`.


## Permission Policy
### Setting permission policy

#### Feature description

This API (`PUT Bucket policy`) is used to set the permission policy for a bucket.

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

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.put_bucket_policy(
    Bucket='examplebucket-1250000000',
    Policy={
        "Statement": [
            {
                "Principal": {
                    "qcs": [
                    "qcs::cam::uin/100000000001:uin/100000000011"
                    ]
                },
                "Effect": "allow",
                "Action": [
                    "name/cos:GetBucket"
                ],
                "Resource": [
                    "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
                ],
                "condition": {
                    "ip_equal": {
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
| Bucket | Bucket name in the format of `BucketName-APPID`. | String | Yes |
| Statement | Describes one or more permissions. | List | Yes |
| Principal | Describes the entity to which the permission is granted. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/18023). | Dict | Yes |
| Version | Policy syntax version. Default value: `2.0`. |String|Yes |
| Effect | `allow` or `deny`. |String| Yes |
| Action | COS API. You can specify one, several, or all (`*`) COS APIs as needed, such as `name/cos:GetService`. **Note that this value is case-sensitive.**    |List | Yes |
| Resource | The specific resource for which the permission is granted. It can be any resource, a resource in a path with a specified prefix, a resource in a specified absolute path, or a combination of these. |List | Yes |
| Condition | Rule condition, which is optional. For more information, see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603). |List | No |


#### Response description

This API returns `None`.


### Querying permission policy

#### Feature description

This API (`GET Bucket policy`) is used to query the permission policy of a bucket.

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
import json

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.get_bucket_policy(
    Bucket='examplebucket-1250000000',
)
policy = json.loads(response['Policy'])
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String | Yes |


#### Response description

This API returns the bucket permission policy of `dict` type, which contains a key-value pair, where `key` is the `'Policy'` string, and the value is a JSON string that represents the specific permission policy and can be converted to `dict` through `json.loads()`.
```python
{
    "Statement": [
        {
            "Principal": {
                "qcs": [
                "qcs::cam::uin/100000000001:uin/100000000011"
                ]
            },
            "Effect": "allow",
            "Action": [
                "name/cos:GetBucket"
            ],
            "Resource": [
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition": {
                "ip_equal": {
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
| Statement | Describes one or more permissions. | List | Yes |
| Principal | Describes the entity to which the permission is granted. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/18023). | Dict | Yes |
| Version | Policy syntax version. Default value: `2.0`. |String|Yes |
| Effect | `allow` or `deny`. |String| Yes |
| Action | COS API. You can specify one, several, or all (`*`) COS APIs as needed, such as `name/cos:GetService`. **Note that this value is case-sensitive.**    |List | Yes |
| Resource | The specific resource for which the permission is granted. It can be any resource, a resource in a path with a specified prefix, a resource in a specified absolute path, or a combination of these. |List | Yes |
| Condition | Rule condition, which is optional. For more information, see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603). |List | No |


### Deleting permission policy

#### Feature description

This API (`DELETE Bucket policy`) is used to delete the permission policy of a bucket.

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

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.delete_bucket_policy(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String | Yes |


#### Response description

This API returns `None`.

