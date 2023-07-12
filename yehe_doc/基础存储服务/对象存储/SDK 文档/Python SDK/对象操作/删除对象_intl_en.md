## Overview

This document provides an overview of APIs and SDK code samples related to object deletion.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [DELETE Object](https://www.tencentcloud.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://www.tencentcloud.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects in a single request |


## Deleting a Single Object

#### Feature description

This API is used to delete a specified object.

#### Method prototype

```
delete_object(Bucket, Key, **kwargs)
```
#### Sample 1. Deleting an object

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

response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### Sample 2. Deleting a directory

In COS, a directory is a special object with a path ending in "/". You can directly call the `Delete Object` API to delete a directory. Note that only empty directories can be deleted. If you want to delete non-empty directories, see "Deleting objects with a specified prefix".

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

to_delete_dir='path/to/delete/dir/'
response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key=to_delete_dir,
)
print(response)
```

#### Sample 3: Deleting objects with a specified prefix

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

import sys
import os
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print information about the communication with the server.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = os.environ['COS_SECRET_ID']     #  User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://www.tencentcloud.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://www.tencentcloud.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

# Delete objects with the specified prefix.
bucket = 'examplebucket-1250000000'
is_over = False
marker = ''
prefix = 'root/logs'
while not is_over:
    response = client.list_objects(Bucket=bucket, Prefix=prefix, Marker=marker)
    if 'Contents' in response:
        for content in response['Contents']:
            print("delete object: ", content['Key'])
            client.delete_object(Bucket=bucket, Key=content['Key'])

        if response['IsTruncated'] == 'false':
            is_over = True
            marker = response['Marker']
```

#### Sample request with all parameters

```python
response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    VersionId='string',
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| VersionId | Version ID of the object if versioning is enabled  | String  | No |

#### Response description

This response contains information on the deleted object in dict format:

```python
{
    'x-cos-version-id': 'string',
    'x-cos-delete-marker': 'true'|'false',
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| x-cos-version-id    | Version ID of the deleted object  | String |
| x-cos-delete-marker | Whether the deleted object is a delete marker | String |

## Deleting Multiple Objects

#### Feature description

The API (DELETE Multiple Objects) is used to delete multiple objects.

#### Method prototype

```
delete_objects(Bucket, Delete={}, **kwargs)
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

response = client.delete_objects(
    Bucket='examplebucket-1250000000',
    Delete={
        'Object': [
            {
                'Key': 'exampleobject1'
            },
            {
                'Key': 'exampleobject2'
            }
        ]
    }
)
```
#### Sample request with all parameters

```python
response = client.delete_objects(
    Bucket='examplebucket-1250000000',
    Delete={
        'Object': [
            {
                'Key': 'exampleobject1',
                'VersionId': 'string'
            },
            {
                'Key': 'exampleobject2',
                'VersionId': 'string'
            },
        ],
        'Quiet': 'true'|'false'
    }
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Delete  | Response method and target objects to delete  | Dict | Yes |
| Objects | Information of each object to delete | List | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String |No |
| VersionId | Version ID of the target object if versioning is enabled | String  | No |
| Quiet | Response method. Valid values: `true`: returns only the failed results; `false` (default): returns all results. | String | No |

#### Response description
The response contains the deletion results in dict format:
```python
{
    'Deleted': [
        {
            'Key': 'string',
            'VersionId': 'string',
            'DeleteMarker': 'true'|'false',
            'DeleteMarkerVersionId': 'string'
        },
        {
            'Key': 'string',
        },
    ],
    'Error': [
        {
            'Key': 'string',
            'VersionId': 'string',
            'Code': 'string',
            'Message': 'string'
        },
    ]
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| Deleted | Information on the successfully deleted objects |  List |
| Key | Paths to the successfully deleted objects | String |
| VersionId | Version IDs of the successfully deleted objects | String |
| DeleteMarker | Whether a successfully deleted object is a delete marker | String |
| DeleteMarkerVersionId | Version IDs of the delete markers of the successfully deleted objects | String |
| Error  |  Information on the objects that failed to be deleted | List |
| Key | Paths to the objects that failed to be deleted | String |
| VersionId | Version IDs of the objects that failed to be deleted | String |
| Code | Error codes for the deletion failures | String |
| Message | Error messages for the deletion failures | String |


## Deleting Multiple Objects (Deleting a Directory)

#### Feature description
COS does not have the concept of directories, but you can use slashes (/) as the delimiter to simulate directories.

In COS, deleting a directory and the objects contained actually means deleting objects that have the same specified prefix. Currently, COS’s Python SDK does not provide a standalone API to perform this operation. However, you can still do so with a combination of basic operations (query object list + batch delete objects).

#### Sample request
```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos.cos_threadpool import SimpleThreadPool
import os
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

bucket = 'examplebucket-1250000000'
folder = 'folder/' # A directory to delete (an object name ending with a slash (/) is a directory)

def delete_cos_dir():
    pool = SimpleThreadPool()
    marker = ""
    while True:
        file_infos = []

        # List 100 objects in a response.
        response = client.list_objects(Bucket=bucket, Prefix=folder, Marker=marker, MaxKeys=100)

        if "Contents" in response:
            contents = response.get("Contents")
            file_infos.extend(contents)
            pool.add_task(delete_files, file_infos)

        # Quit after the listing.
        if response['IsTruncated'] == 'false':
            break
        
        # Get the next response.
        marker = response["NextMarker"]

    pool.wait_completion()
    return None   

def delete_files(file_infos):

    # Construct the batch delete request.
    delete_list = []
    for file in file_infos:
        delete_list.append({"Key": file['Key']})

    response = client.delete_objects(Bucket=bucket, Delete={"Object": delete_list})
    print(response)

if __name__ == "__main__":
    delete_cos_dir()
```
