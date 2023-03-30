
## Overview

This document provides an overview of APIs and SDK code samples related to bucket copying.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://www.tencentcloud.com/document/product/436/19223) | Setting a bucket replication rule | Sets a bucket replication rule for a bucket |
| [GET Bucket replication](https://www.tencentcloud.com/document/product/436/19222) | Querying cross-bucket replication | Queries the bucket replication rule of a bucket |
| [DELETE Bucket replication](https://www.tencentcloud.com/document/product/436/19221) | Deleting a cross-bucket replication rule | Deletes a bucket replication rule of a bucket |


## Setting Cross-Bucket Replication

#### Feature description

This API (PUT Bucket replication) is used to set the cross-bucket replication rule for a bucket.

#### Method prototype

```
put_bucket_replication(Bucket, ReplicationConfiguration={}, **kwargs)
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


#### Field description

| Parameter | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format: BucketName-APPID | String | Yes |
| Role | Replication initiator identifier: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | String | No |
| Rule | Sets the rule, including ID, Status, Prefix, and Destination | List | Yes |
| ID | Rule ID | string | No |
| Status | Whether a rule is enabled. Valid values: `Enabled`, `Disabled` | String | Yes |
| Prefix | Specifies the prefix used to filter objects. If it is left empty, the rule applies to all objects in the bucket | String |  Yes |
| Destination | Describes the destination resource, including `Bucket` and `StorageClass`  | Dict | Yes |
| Bucket | Sets the destination bucket for cross-region replication. Format: `qcs::cos:[region]::[BucketName-APPID]`  | String  | Yes |
| StorageClass | Sets the storage class of the object copies. Valid values: `STANDARD`, `STANDARD_IA` | String | No |

#### Response description

This API returns `None`.

## Querying Cross-Bucket Replication

#### Feature description

This API (GET Bucket replication) is used to query the cross-bucket replication rule of a bucket.

#### Method prototype

```
get_bucket_replication(Bucket, **kwargs)
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

response = client.get_bucket_replication(
    Bucket='examplebucket-1250000000'
)
```

#### Field description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------ | ------ | -------- |
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
| ------------ | ------------------------------------------------------------ | ------ |
| Role | Replication initiator identifier: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | String | No |
| Rule | Sets the rule for cross-region replication, including ID, Status, Prefix, and Destination | List | Yes |
| Status  | Sets whether the rule is enabled. Valid values: `Enabled`, `Disabled` | String | Yes |
| Prefix | Specifies the prefix used to filter objects that are subject to the rule. If it is left empty, the rule applies to all objects in the bucket | String |  Yes |
| Destination |   Describes the destination resource, including `Bucket` and `StorageClass` | Dict | Yes |
| Bucket | Sets the destination bucket for cross-region replication. Format: `qcs::cos:[region]::[BucketName-APPID]`  | String  | Yes |
| StorageClass | Sets the storage class of the object copies. Valid values: `STANDARD`, `STANDARD_IA` | String | No |


## Deleting Cross-Bucket Replication

#### Feature description

This API (DELETE Bucket replication) is used to delete a cross-bucket replication rule from a bucket.

#### Method prototype

```
delete_bucket_replication(Bucket, **kwargs)
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

response = client.delete_bucket_replication(
    Bucket='examplebucket-1250000000',
)
```


#### Field description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |

#### Response description

This API returns `None`.






