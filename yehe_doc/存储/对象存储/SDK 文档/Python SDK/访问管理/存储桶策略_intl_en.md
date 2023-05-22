## Overview

This document provides an overview of APIs and SDK code samples related to bucket policies.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [PUT Bucket policy](https://www.tencentcloud.com/document/product/436/8282) | Setting a bucket policy | Sets a permission policy for the specified bucket |
| [GET Bucket policy](https://www.tencentcloud.com/document/product/436/8276) | Querying bucket policy | Queries the permission policy of the specified bucket |
| [DELETE Bucket policy](https://www.tencentcloud.com/document/product/436/8285) | Deleting bucket policies | Deletes the permission policies of a specified bucket |

## Setting a bucket policy

#### Feature description

This API is used to set an access policy on a bucket.

#### Method prototype

```
put_bucket_policy(Bucket, Policy, **kwargs)
```

#### Request example

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
secret_id = os.environ['COS_SECRET_ID']     #  User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, see https://cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

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
                ],
                "condition":{
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

#### Field description

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Statement | Detailed information about one or more permissions | Struct |Yes |
| Principal | Specifies the entity to which the permission is granted. For more information, see [Access Policy Language Overview](https://www.tencentcloud.com/document/product/436/18023)|Dict| Yes |
| Effect | Allow or deny |String| Yes |
| Action | COS API. You can specify one, several, or all (`*`) COS APIs as needed, e.g. `name/cos:GetService`. **Note that this value is case-sensitive**.    |List | Yes |
| Resource | Specifies the resource for which permission is granted. It can be any resource, a resource in a path with a specified prefix, a resource in a specified absolute path, or a combination thereof. |List | Yes |
| Condition | (Optional) Specifies the rule condition. For more information, see [condition](https://www.tencentcloud.com/document/product/598/10603) |List | No |


#### Response description

This API returns `None`.


## Querying a bucket policy

#### Feature description

This API is used to query the access policy on a bucket.

#### Method prototype

```
get_bucket_policy(Bucket, **kwargs)
```

#### Request example

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import os
import logging
import json

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

response = client.get_bucket_policy(
    Bucket='examplebucket-1250000000',
)
policy = json.loads(response['Policy'])
```

#### Field description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |



#### Response description

This API returns the bucket permission policy of `dict` type, which contains a key-value pair, where `key` is the `'Policy'` string, and the value is a JSON string that represents the specific permission policy and can be converted to `dict` through `json.loads()`.

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
            ],
            "condition":{
                "ip_equal":{
                "qcs:ip": "10.121.2.10/24"
                }
            }
        }
    ],
    "version": "2.0"
}
```


| Parameter | Description | Type |
| --------- | ------------------------------------------------------------ | ------ |
| Statement | Specifies one or more permissions |List| 
| Principal | Specifies the entity to which the permission is granted. For more information, see [Access Policy Language Overview](https://www.tencentcloud.com/document/product/436/18023)|Dict| 
| version | The policy syntax version. The default is 2.0. |String | 
| Effect | Allow or explicitly deny | String |
| Action | COS API. You can specify one, several, or all (`*`) COS APIs as needed, e.g. `name/cos:GetService`. **Note that this value is case-sensitive**.    |List | 
| Resource | Specifies the resource for which permission is granted. It can be any resource, a resource in a path with a specified prefix, a resource in a specified absolute path, or a combination thereof. |List |
| Condition | (Optional) Specifies the rule condition. For more information, see [condition](https://www.tencentcloud.com/document/product/598/10603) |List | 


## Deleting a bucket policy

#### Feature description

This API is used to delete the access policy from a specified bucket.

#### Method prototype

```
delete_bucket_policy(Bucket, **kwargs)
```

#### Request example

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
secret_id = os.environ['COS_SECRET_ID']     #  User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, see https://cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.delete_bucket_policy(
    Bucket='examplebucket-1250000000',
)
```


#### Field description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |


#### Response description

This API returns `None`.

