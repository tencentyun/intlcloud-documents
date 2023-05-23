

## Feature Overview

This document provides an overview of APIs and SDK code samples for COS inventory.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------- |
| [PUT Bucket inventory](https://www.tencentcloud.com/document/product/436/30625) | Setting an inventory job | Sets an inventory job for a bucket |
| [GET Bucket inventory](https://www.tencentcloud.com/document/product/436/30623) | Querying inventory jobs | Queries the inventory jobs of a bucket |
| [DELETE Bucket inventory](https://www.tencentcloud.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job from a bucket |

## Creating an Inventory Job

#### Feature description

This API (PUT Bucket inventory) is used to create an inventory job for a bucket.

#### Method prototype

```
put_bucket_inventory(Bucket, Id, InventoryConfiguration={}, **kwargs)
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

response = client.put_bucket_inventory(
    Bucket='examplebucket-1250000000',
    Id='string',
    InventoryConfiguration={
        'Destination': {
            'COSBucketDestination': {
                'AccountId': '100000000001',
                'Bucket': 'qcs::cos:ap-guangzhou::examplebucket-1250000000',
                'Format': 'CSV',
                'Prefix': 'string',
                'Encryption': {
                    'SSECOS': {}
                }
            }
        },
        'IsEnabled': 'true'|'false',
        'Filter': {
            'Prefix': 'string'
        },
        'IncludedObjectVersions':'All'|'Current',
        'OptionalFields': {
            'Field': [
                'Size',
                'LastModifiedDate',
                'ETag',
                'StorageClass',
                'IsMultipartUploaded',
                'ReplicationStatus'
            ]
        },
        'Schedule': {
            'Frequency': 'Daily'|'Weekly'
        }
    }
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for inventory job setting, in the format of `BucketName-APPID`. For more information, see [Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312). | String | Yes |
| Id | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String | Yes       |
| Destination            | Inventory job delivery destination information                                      | Dict   | Yes       |
| COSBucketDestination   | Destination bucket information for inventory job result delivery                             | Dict   | Yes       |
| AccountId              | Destination bucket account information                                         | String | No |
| Bucket                 | Destination bucket name                                             | String | Yes       |
| Format                 | File format of the inventory result. Valid value: CSV | String | Yes |
| Prefix                 | Delivery path prefix in the destination bucket                                     | String | No       |
| Encryption             | Encryption information for file delivery to the destination bucket. Valid value: SSECOS                  | Dict   | No       |
| IsEnabled              | Inventory job status flag. Valid values: true, false                   | String | Yes       |
| Filter                 | Filter for inventory analysis objects                                       | Dict   | No       |
| Prefix                 | Filter prefix for inventory analysis objects                                       | String | No       |
| IncludedObjectVersions | Versioning information inclusion status. Valid values: All, Current                        | String | Yes       |
| OptionalFields         | Optional inventory fields                                               | Dict   | No       |
| Field                  | Field names, including `Size`, `LastModifiedDate`, `ETag`, `StorageClass`, `IsMultipartUploaded`, and `ReplicationStatus` | List   | No       |
| Schedule               | Inventory job execution schedule                                           | Dict   | Yes       |
| Frequency              | Inventory job execution frequency. Valid values: Daily, Weekly                     | String | Yes       |

#### Response description

This API returns `None`.

#### Error codes

The following describes some common errors that may occur when you call this API:

| Error Code | Description | Status Code |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument | Invalid parameter value | HTTP 400 Bad Request |
| TooManyConfigurations | The number of inventories has reached the upper limit of 1,000 | HTTP 400 Bad Request |
| AccessDenied          | Unauthorized access. You most likely do not have access permission for the bucket | HTTP 403 Forbidden   |

## Querying Inventory Jobs

#### Feature description

This API is used to query the inventory jobs of a bucket.

#### Method prototype

```
get_bucket_inventory(Bucket, Id, **kwargs)
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

response = client.get_bucket_inventory(
    Bucket='examplebucket-1250000000',
    Id='string'
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for inventory job query, in the format of `BucketName-APPID`. For more information, see [Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312). | String | Yes |
| Id       | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String | Yes       |

#### Response description

Inventory job configuration of the bucket in `dict` type.

```
{
    'Id': 'string',
    'Destination': {
        'COSBucketDestination': {
            'AccountId': '100000000001',
            'Bucket': 'qcs::cos:ap-guangzhou::examplebucket-1250000000',
            'Format': 'CSV',
            'Prefix': 'string',
            'Encryption': {
                'SSECOS': {}
            }
        }
    },
    'IsEnabled': 'true'|'false',
    'Filter': {
        'Prefix': 'string'
    },
    'IncludedObjectVersions':'All'|'Current',
    'OptionalFields': {
        'Field': [
            'Size',
            'LastModifiedDate',
            'ETag',
            'StorageClass',
            'IsMultipartUploaded',
            'ReplicationStatus'
        ]
    },
    'Schedule': {
        'Frequency': 'Daily'|'Weekly'
    }
}
```

| Parameter | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ------ |
| Id       | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String |
| Destination            | Inventory job delivery destination information                                      | Dict   |
| COSBucketDestination   | Destination bucket information for inventory job result delivery                             | Dict   |
| AccountId              | Destination bucket account information                                         | String |
| Bucket                 | Destination bucket name                                             | String |
| Format                 | File format of the inventory result. Valid value: CSV | String |
| Prefix                 | Delivery path prefix in the destination bucket                                     | String |
| Encryption             | Encryption information for file delivery to the destination bucket. Valid value: SSECOS                  | Dict   |
| IsEnabled              | Inventory job status flag. Valid values: true, false                   | String |
| Filter                 | Filter for inventory analysis objects                                       | Dict   |
| Prefix                 | Filter prefix for inventory analysis objects                                       | String |
| IncludedObjectVersions | Versioning information inclusion status. Valid values: All, Current                        | String |
| OptionalFields         | Optional inventory fields                                               | Dict   |
| Field                  | Field names, including `Size`, `LastModifiedDate`, `ETag`, `StorageClass`, `IsMultipartUploaded`, and `ReplicationStatus` | List   |
| Schedule               | Inventory job execution schedule                                           | Dict   |
| Frequency              | Inventory job execution frequency. Valid values: Daily, Weekly                     | String |

## Deleting an Inventory Job

#### Feature description

This API is used to delete a specified inventory job from a bucket.

#### Method prototype

```
delete_bucket_inventory(Bucket, Id, **kwargs)
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

response = client.delete_bucket_inventory(
    Bucket='examplebucket-1250000000',
    Id='string'
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for inventory job deletion, in the format of `BucketName-APPID`. For more information, see [Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312). | String | Yes |
| Id       | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String | Yes       |

#### Response description

This API returns `None`.
