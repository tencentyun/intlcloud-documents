## Overview
This document provides an overview of APIs and SDK code samples for for the ACL of buckets and objects.


**Bucket ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for the specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a specified bucket |

**Object ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets an ACL for an object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object |

## Bucket ACL

### Setting a bucket ACL

#### Description

The API (PUT Bucket acl) is used to set the ACL for a specified bucket. The `AccessControlPolicy` parameter and other permission parameters are mutually exclusive and cannot be specified at the same time.

#### Method prototype

```
put_bucket_acl(Bucket, AccessControlPolicy={}, **kwargs)
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
secret_id = os.environ['COS_SECRET_ID']     # User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.

region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.put_bucket_acl(
    Bucket='examplebucket-1250000000',
    ACL='public-read'
)
```
#### Sample request with all parameters

```python
response = client.put_bucket_acl(
    Bucket='examplebucket-1250000000',
    ACL='private'|'public-read'|'public-read-write',
    GrantFullControl='id="100000000002"',
    GrantRead='id="100000000003",id="100000000004"',
    GrantWrite='id="100000000005"',
    AccessControlPolicy={
        'AccessControlList': {
            'Grant': [
                {
                    'Grantee': {
                        'DisplayName': 'qcs::cam::uin/100000000002:uin/100000000002',
                        'Type': 'CanonicalUser'|'Group',
                        'ID': 'qcs::cam::uin/100000000002:uin/100000000002', # The ID is required when `Type` is `CanonicalUser`
                        'URI': 'http://cam.qcloud.com/groups/global/AllUsers' # The URI is required when `Type` is `Group`
                    },
                    'Permission': 'FULL_CONTROL'|'WRITE'|'READ'
                },
            ]
        },
        'Owner': {
            'DisplayName': 'qcs::cam::uin/100000000001:uin/100000000001', 
            'ID': 'qcs::cam::uin/100000000001:uin/100000000001' # It must be the ID of the bucket owner
        }
    }
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| ACL  | ACL of the bucket, such as `private`, `public-read`, and `public-read-write`. For more information, see [ACL](https://intl.cloud.tencent.com/document/product/436/30583).                  | String | No |
| GrantFullControl | Grants a specified account read/write permission for a bucket in the format of `id="OwnerUin"`. You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
|GrantRead | Grants a specified account read permission for a bucket in the format of `id="OwnerUin"`. You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| GrantWrite | Grants a specified account write permission for a bucket in the format of `id="OwnerUin"`. You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| AccessControlPolicy| Grants a specified account access permission for a bucket. This parameter and other permission parameters are mutually exclusive and cannot be specified at the same time. |Dict| No |

`AccessControlPolicy` parameter description:

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Owner | Information on the bucket owner, including `DisplayName` and `ID` | Dict | Yes |
| AccessControlList  | Information on the user to whom a bucket permission is granted, including `Grant` list | Dict | Yes |

`Owner` parameter description:

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| ID | ID of the grantee when `Type` is `CanonicalUser`, in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, for example, `qcs::cam::uin/100000000001:uin/100000000001`. | string | Yes |
| DisplayName       | Name of the grantee. This parameter can be left empty or be consistent with the value of `ID`       | String | No |

`AccessControlList` parameter description:

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Grant | Information on the user to whom a bucket permission is granted, including `Grantee` and `Permission` | List | Yes |
| Grantee | Information on the grantee, including `DisplayName`, `Type`, `ID`, and `URI` | Dict | Yes |
| Type | Type of the grantee: `CanonicalUser` or `Group` | String | Yes |
| ID | ID of the grantee when `Type` is `CanonicalUser`, in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, for example, `qcs::cam::uin/100000000001:uin/100000000001`. |String| Yes when `Type` is `CanonicalUser` |
| URI | URI of the preset user group when `Type` is `Group`, for example, `http://cam.qcloud.com/groups/global/AllUsers`. For more information, see [ACL](https://intl.cloud.tencent.com/document/product/436/30583). |String| Yes when `Type` is `Group` |
| Permission | Bucket permissions granted to the grantee. Valid values: `FULL_CONTROL` (read/write permission), `WRITE` (write permission), and `READ` (read permission) | String | Yes |

#### Response description
This API returns `None`.

### Querying a bucket ACL

#### Description

This API is used to query the ACL of a specified bucket.

#### Method prototype

```
get_bucket_acl(Bucket, **kwargs)
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
secret_id = os.environ['COS_SECRET_ID']     # User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.

region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.get_bucket_acl(
    Bucket='examplebucket-1250000000'
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |


#### Response description

This response returns bucket ACL information in Dict format.
```python
{
    'Owner': {
        'DisplayName': 'qcs::cam::uin/100000000001:uin/100000000001',
        'ID': 'qcs::cam::uin/100000000001:uin/100000000001'
    },
    'AccessControlList': {
        'Grant': [
            {
                'Grantee': {
                    'DisplayName': 'qcs::cam::uin/100000000002:uin/100000000002',
                    'Type': 'CanonicalUser'|'Group',
                    'ID': 'qcs::cam::uin/100000000002:uin/100000000002',
                    'URI': 'http://cam.qcloud.com/groups/global/AllUsers'
                },
                'Permission': 'FULL_CONTROL'|'WRITE'|'READ'
            },
        ]
    }
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| Owner | Information on the bucket owner, including `DisplayName` and `ID`. For more information, see `PUT Bucket acl`. | Dict |
|  AccessControlList  | Information on the user to whom a bucket permission is granted, including `Grant` list. For more information, see `PUT Bucket acl`. | Dict |



## Object ACL

### Setting an object ACL

#### Description

The API is used to set the ACL for an object in a bucket. The `AccessControlPolicy` parameter and other permission parameters cannot be specified at the same time.

#### Method prototype

```
put_object_acl(Bucket, Key, AccessControlPolicy={}, **kwargs)
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
secret_id = os.environ['COS_SECRET_ID']     # User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.

region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.put_object_acl(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    ACL='public-read'
)
```
#### Sample request with all parameters

```python
response = client.put_object_acl(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    ACL='default'|'private'|'public-read',
    GrantFullControl='id="100000000003"',
    GrantRead='id="100000000003",id="100000000004"',
    AccessControlPolicy={
        'AccessControlList': {
            'Grant': [
                {
                    'Grantee': {
                        'DisplayName': 'qcs::cam::uin/100000000002:uin/100000000002',
                        'Type': 'CanonicalUser'|'Group',
                        'ID': 'qcs::cam::uin/100000000002:uin/100000000002', # The ID is required when `Type` is `CanonicalUser`
                        'URI': 'http://cam.qcloud.com/groups/global/AllUsers' # The URI is required when `Type` is `Group`
                    },
                    'Permission': 'FULL_CONTROL'|'READ'
                },
            ]
        },
        'Owner': {
            'DisplayName': 'qcs::cam::uin/100000000001:uin/100000000001',
            'ID': 'qcs::cam::uin/100000000001:uin/100000000001'
        }
    }
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| ACL  | ACL of the object, such as `default`, `private`, and `public-read`. For more information, see [ACL](https://intl.cloud.tencent.com/document/product/436/30583).                  | String | No |
| GrantFullControl | Grants a specified account full permission for an object in the format of `id="OwnerUin"`. You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| GrantRead | Grants a specified account read permission for an object in the format of `id="OwnerUin"`. You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| AccessControlPolicy | Grants a specified account access permission for an object. This parameter and other permission parameters are mutually exclusive and cannot be specified at the same time. |Dict| No |

`AccessControlPolicy` parameter description:

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Owner | Information on the bucket owner, including `DisplayName` and `ID` | Dict | Yes |
| AccessControlList  | Information on the user to whom a bucket permission is granted, including `Grant` list | Dict | Yes |

`Owner` parameter description:

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| ID | ID of the grantee when `Type` is `CanonicalUser`, in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, for example, `qcs::cam::uin/100000000001:uin/100000000001`. | string | Yes |
| DisplayName       | Name of the grantee. This parameter can be left empty or be consistent with the value of `ID`       | String | No |

`AccessControlList` parameter description:

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Grant | Information on the user to whom a bucket permission is granted, including `Grantee` and `Permission` | List | Yes |
| Grantee | Information on the grantee, including `DisplayName`, `Type`, `ID`, and `URI` | Dict | Yes |
| Type | Type of the grantee: `CanonicalUser` or `Group` | String | Yes |
| ID | ID of the grantee when `Type` is `CanonicalUser`, in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, for example, `qcs::cam::uin/100000000001:uin/100000000001`. |String| Yes when `Type` is `CanonicalUser` |
| URI | URI of the preset user group when `Type` is `Group`, for example, `http://cam.qcloud.com/groups/global/AllUsers`. For more information, see [ACL](https://intl.cloud.tencent.com/document/product/436/30583). |String| Yes when `Type` is `Group` |
| Permission | Permissions granted to the grantee. Valid values: `FULL_CONTROL` (full access) and `READ` (read permission) | String | Yes |

#### Response description

This API returns `None`.

### Querying an object ACL

#### Description

The API is used to query the ACL of an object.

#### Method prototype

```
get_object_acl(Bucket, Key, **kwargs)
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
secret_id = os.environ['COS_SECRET_ID']     # User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.

region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.get_object_acl(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |


#### Response description

Object ACL information in `dict` type:
```python
{
    'Owner': {
        'DisplayName': 'qcs::cam::uin/100000000001:uin/100000000001',
        'ID': 'qcs::cam::uin/100000000001:uin/100000000001'
    },
    'AccessControlList': {
        'Grant': [
            {
                'Grantee': {
                    'DisplayName': 'qcs::cam::uin/100000000002:uin/100000000002',
                    'Type': 'CanonicalUser'|'Group',
                    'ID': 'qcs::cam::uin/100000000002:uin/100000000002',
                    'URI': 'http://cam.qcloud.com/groups/global/AllUsers'
                },
                'Permission': 'FULL_CONTROL'|'READ'
            },
        ]
    }
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| Owner   | Information on the object owner, including `DisplayName` and `ID`. For more information, see `PUT Object acl`. | Dict |
|  AccessControlList  | Information on the user to whom an object permission is granted, including `Grant` list. For more information, see `PUT Object acl`. | Dict |
