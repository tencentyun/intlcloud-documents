## Overview

This document provides an overview of APIs and SDK code samples for basic bucket operations.

>!
> - We recommend you use a temporary key as instructed in [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) to call the SDK for security purposes. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission on the permanent key.


| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying a bucket list | Queries the list of all buckets under the specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under a specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permissions | Checks whether a bucket exists and whether you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under a specified account |


## Querying a Bucket List

#### Feature description

This API (GET Service) is used to query the list of all buckets in an account.

#### Method prototype

```
list_buckets()
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
                           # For the list of regions supported by COS, see https://cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.list_buckets(
)
```

#### Response description

Query a bucket list in Dict format.

```python
{
    'Buckets': {
        'Bucket': [
            {
                'Name': 'string',
                'Location': 'string',
                'CreationDate': 'string'
            },
        ],
    },
    'Owner': {
        'DisplayName': 'string',
        'ID': 'string'
    }
}
```

| Parameter | Description | Type | 
| -------------- | -------------- |---------- |
| Buckets   | A buckets list  | Dict |
| Bucket   | A buckets list | List |
| Name   |  Bucket name  | String|
| Location   | Name of bucket region | String|                                     
| CreationDate   |  Time of Bucket creation | String|
| Owner   |  Bucket owner information  | Dict|
| DisplayName | Bucket owner name | String |
| ID   | Bucket owner ID | String|


## Creating a Bucket

#### Feature description

This API (PUT Bucket) is used to create a bucket under a specified account.

#### Method prototype

```
create_bucket(Bucket, BucketAZConfig=None, **kwargs)
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
                           # For the list of regions supported by COS, see https://cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

# The bucket name does not support uppercase letters, and the COS backend will automatically convert uppercase letters passed in to lowercase when creating the bucket.
response = client.create_bucket(
    Bucket='examplebucket-1250000000'
)
```
#### Sample request with all parameters

```python
response = client.create_bucket(
    Bucket='examplebucket-1250000000',
    BucketAZConfig='string',
    ACL='private'|'public-read'|'public-read-write',
    GrantFullControl='string',
    GrantRead='string',
    GrantWrite='string'    
)
```
#### Field description

| Parameter | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
|Bucket| Name of the bucket to be created in the format of `BucketName-APPID`. <br>The bucket name does not support uppercase letters, and the COS backend will automatically convert uppercase letters passed in to lowercase when creating the bucket. | String | Yes |
|BucketAZConfig| AZ configuration of the bucket. To create an MAZ bucket, specify 'MAZ'. |String| No |
| ACL | Sets the bucket ACL, such as 'private', 'public-read', 'public-read-write' | String | No |
| GrantFullControl | Grants a specified account full Read/Write permission for a bucket in the format of `id="OwnerUin"`| String | No |
|GrantRead | Grants a specified account Read permission for a bucket in the format of `id="OwnerUin"`| String | No |
| GrantWrite| Grants a specified account Write permission for a bucket in the format of `id="OwnerUin"`| String | No |

#### Response description
This API returns `None`.


## Checking a Bucket and Its Permissions

#### Feature description

This API is used to verify whether a bucket exists and you have permission to access it.

#### Method prototype

```
head_bucket(Bucket)
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
                           # For the list of regions supported by COS, see https://cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.head_bucket(
    Bucket='examplebucket-1250000000'
)
```
#### Field description

| Parameter | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | The name of a bucket to query. Format: BucketName-APPID | String | Yes |

#### Response description
This API returns `None`.


## Deleting a Bucket

#### Feature description

This API (DELETE Bucket) is used to delete an empty bucket under a specified account.

#### Method prototype

```
delete_bucket(Bucket)
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
                           # For the list of regions supported by COS, see https://cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.delete_bucket(
    Bucket='examplebucket-1250000000'
)
```
#### Field description

| Parameter | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | The name of a bucket to delete, must be in the format: BucketName-APPID | String | Yes |

#### Response description
This API returns `None`.


## Checking whether a bucket exists

#### Feature description

Checking Whether Buckets Exist

#### Method prototype

```
bucket_exists(Bucket)
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
                           # For the list of regions supported by COS, see https://cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.bucket_exists(
    Bucket='examplebucket-1250000000'
)
print(response)
```
#### Field description

| Parameter | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |

#### Response description
`True` indicates that the bucket exists. `False` indicates that the bucket does not exist.
