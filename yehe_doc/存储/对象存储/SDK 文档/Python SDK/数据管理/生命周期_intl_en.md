## Overview

This document provides an overview of APIs and SDK code samples related to lifecycles.



| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket lifecycle](https://www.tencentcloud.com/document/product/436/8280) | Setting lifecycle | Sets lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://www.tencentcloud.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://www.tencentcloud.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |



## Setting a Lifecycle Configuration

#### Feature description

This API (PUT Bucket lifecycle) is used to set the lifecycle configuration for a bucket.

#### Method prototype

```
put_bucket_lifecycle(Bucket, LifecycleConfiguration={}, **kwargs)
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


#### Field description

| Parameter | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | -------- |
| Bucket  | Bucket name in the format of `BucketName-APPID`  | String | Yes  |
| Rule | Sets the rule, including ID, Filter, Status, Expiration, Transition, NoncurrentVersionExpiration, NoncurrentVersionTransition, AbortIncompleteMultipartUpload | List | Yes |
| ID | Rule ID | string | No |
| Filter | Describes a set of objects that are subject to the rule. To set the rule for all objects in the bucket, leave `Prefix` empty. | Dict | Yes |
| Status | Sets whether the rule is enabled. Valid values: `Enabled`, `Disabled` | Dict | Yes |
|  Expiration  | Specifies when objects expire. It can be an expiry date or the number of days before objects expire. The date must be in GMT ISO 8601 format. You can specify the date using the `get_date` method. | Dict | No |
| Transition | Sets one or more rules for when an object transitions to a specified storage class. You can specify the number of days before the transition occurs or a transition date. The date must be in GMT ISO 8601 format. You can specify the date using the `get_date` method. The valid values for StorageClass include Standard_IA, Archive, and Deep_Archive. | List | No |
| NoncurrentVersionExpiration | Sets when noncurrent object versions expire. You can specify the number of days before objects expire (NoncurrentDays). | Dict | No |
|  NoncurrentVersionTransition  | Sets one or more transition rules that describe when noncurrent objects transition to another storage class. You can specify the number of days (NoncurrentDays). The valid value for `StorageClass` is Standard_IA. | List | No |
| AbortIncompleteMultipartUpload | Indicates the number of days within which the upload must be completed after the multipart upload starts. | Dict | No |


#### Response description

This API returns `None`.


## Querying a Lifecycle Configuration

#### Feature description

This API is used to query the lifecycle configuration of a bucket.

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

response = client.get_bucket_lifecycle(
    Bucket='examplebucket-1250000000',
)
```


#### Field description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |

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
| ------------------------------ | ------------------------------------------------------------ | ------ |
| Rule | Sets the rule, including ID, Filter, Status, Expiration, Transition, NoncurrentVersionExpiration, NoncurrentVersionTransition, AbortIncompleteMultipartUpload | List |
| ID                             | Unique ID of the rule                                         | String | 

| Status | Sets whether the rule is enabled. Valid values: `Enabled`, `Disabled` | Dict |
| Expiration | Specifies when objects expire. It can be an expiry date (`Date`) or the number of days before objects expire (`Days`) | Dict |
| Transition | Specifies when objects transition to another storage class. It can be an expiry date (`Date`) or the number of days before objects transition (`Days`). Valid values for StorageClass: STANDARD_IA, Archive | List |
| NoncurrentVersionExpiration | Sets the expiration rule for noncurrent object versions. You can specify the number of days before the object expires (NoncurrentDays). | Dict |
|  NoncurrentVersionTransition  | Specifies the rule for transitioning noncurrent objects to another storage class. You can specify the number of days (NoncurrentDays). Valid value for StorageClass: STANDARD_IA. | List |
| AbortIncompleteMultipartUpload | Specifies the number of days within which the upload must be completed after the multipart upload starts. | Dict |


## Deleting a Lifecycle Configuration

#### Feature description

This API is used to delete the lifecycle configuration from a bucket.

#### Method prototype

```
delete_bucket_lifecycle(Bucket, **kwargs)
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

response = client.delete_bucket_lifecycle(
    Bucket='examplebucket-1250000000',
)
```

#### Field description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |


#### Response description

This API returns `None`.









