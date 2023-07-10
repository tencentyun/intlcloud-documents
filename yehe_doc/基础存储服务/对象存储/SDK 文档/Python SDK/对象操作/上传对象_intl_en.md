## Feature Overview

This document provides an overview of APIs and SDK code samples related to advanced upload, simple upload, multipart upload, and other object operations.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://www.tencentcloud.com/document/product/436/7749) | Simply uploading an object | Uploads an object to a bucket |
| [APPEND Object](https://www.tencentcloud.com/document/product/436/7741) | Appending parts | Appends object parts to a bucket.                      |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://www.tencentcloud.com/document/product/436/7736) | Querying multipart uploads | Queries the information on ongoing multipart uploads |
| [Initiate Multipart Upload](https://www.tencentcloud.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload job |
| [Upload Part](https://www.tencentcloud.com/document/product/436/7750) | Uploading a part | Uploads a file part | 
| [Upload Part - Copy](https://www.tencentcloud.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://www.tencentcloud.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in a specified multipart upload operation |
| [Complete Multipart Upload](https://www.tencentcloud.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://www.tencentcloud.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |


## Advanced APIs (Recommended)

### Uploading an object (checkpoint restart)

#### Feature description
This advanced upload API can automatically select between the `PUT Object` API and the `Upload Part` API according to the file size. It uses the former for files smaller than or equal to 20 MB and the latter for files larger than 20 MB. It also supports automatic checkpoint restart for suspended multipart uploads.
You can use the `progress_callback` function to query the multipart upload progress.

#### Method prototype

```
upload_file(Bucket, Key, LocalFilePath, PartSize=1, MAXThread=5, EnableMD5=False, progress_callback=None, **kwargs)
```
#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos.cos_exception import CosClientError, CosServiceError
import sys
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

# Use the advanced API to upload once without retry. In this case, the checkpoint restart feature is not used.
response = client.upload_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    LocalFilePath='local.txt',
    EnableMD5=False,
    progress_callback=None
)

# Use the advanced API for checkpoint restart, and the successfully uploaded parts will not be uploaded again during retries (ten times here).
for i in range(0, 10):
    try:
        response = client.upload_file(
        Bucket='examplebucket-1250000000',
        Key='exampleobject',
        LocalFilePath='local.txt')
        break
    except CosClientError or CosServiceError as e:
        print(e)
```

#### Sample request with all parameters
```python
def upload_percentage(consumed_bytes, total_bytes):
    """Callback function that calculates the upload progress (in percentage)

    :param consumed_bytes: uploaded data amount
    :param total_bytes: total data amount
    """
    if total_bytes:
        rate = int(100 * (float(consumed_bytes) / float(total_bytes)))
        print('\r{0}% '.format(rate))
        sys.stdout.flush()

response = client.upload_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    LocalFilePath='local.txt',
    PartSize=1,
    MAXThread=5,
    progress_callback=upload_percentage,
    EnableMD5=False|True,
    ACL='private'|'public-read', # Please note that the maximum number (1000) of ACLs allowed may be reached if you use this parameter
    GrantFullControl='string',
    GrantRead='string',
    StorageClass='STANDARD'|'STANDARD_IA'|'ARCHIVE',
    Expires='string',
    CacheControl='string',
    ContentType='string',
    ContentDisposition='string',
    ContentEncoding='string',
    ContentLanguage='string',
    ContentLength='123',
    ContentMD5='string',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    },
    TrafficLimit='1048576'
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| LocalFilePath | Path to the local file | String | Yes |
| PartSize | Part size. Default value: 1 MB |  Int | No |
|  MAXThread  | Maximum number of threads for concurrent multipart uploads. Default value: 5 |  Int |  No |
| progress_callback | Callback function for the upload progress. You can customize this function to query the upload progress. | Func | No |
| EnableMD5 | Whether to calculate the Content-MD5 checksum, which will extend the upload time. It’s not calculated by default. | Bool | No |
| ACL  | ACL of the object, such as private or public-read                      | String | No |
| GrantFullControl | Grants full permission. Format: `id="OwnerUin"` | String | No |
| GrantRead | Grants read permission. Format: `id="OwnerUin"` | String | No |
| StorageClass | Storage class of the object. For more information about storage classes such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`, please see [Storage Class Overview](https://www.tencentcloud.com/document/product/436/30925). | String | No |
| Expires | Expiration time | String | No |
| CacheControl | Cache policy | String | No |
| ContentType | Content type | String | No |
| ContentDisposition | Filename | String | No |
| ContentEncoding | Encoding type  | String | No |
| ContentLanguage | Language type  | String | No |
| ContentLength | Length of the content  | String | No |
| ContentMD5 | MD5 checksum of the uploaded object, which is used for verification | String | No |
|  Metadata | User-defined object metadata | Dict |  No |
|  TrafficLimit | Bandwidth limit in bit/s for a single request (or a single thread for the advanced download API). Value range: 819200 - 838860800, i.e., 100 KB/s - 100 MB/s | String |  No |

#### Response description
The response contains the attributes of the copied object in dict format:

```python
{
    'Content-Type': 'string',
    'Transfer-Encoding': 'string',
    'Connection': 'string',
    'Date': 'string',
    'Server': 'string',
    'x-cos-hash-crc64ecma': 'string',
    'x-cos-request-id': 'string',
    'x-cos-storage-class': 'string',
    'Location': 'string',
    'Bucket': 'string',
    'Key': 'string',
    'ETag': 'string'
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| Content-Type | Content type. Standard HTTP header | String | 
|  Transfer-Encoding  | Transfer encoding type. Standard HTTP header | String |
|  Connection | Connection method. Standard HTTP header | String |
|  Date | Request date. Standard HTTP header | String |
|  Server | Server flag. Standard HTTP header | String |
|  x-cos-hash-crc64ecma | CRC64 checksum of the file | String |
|  x-cos-request-id | Request ID | String |
|  x-cos-storage-class | Object storage class | String |
|  Location | Object access URL | String |
|  Bucket | Bucket name | String |
|  Key | Object name | String |
| ETag | For multipart upload, this value is not necessarily the MD5 checksum of the object. It is used to verify the uniqueness of the multipart uploaded object. | String |


### Batch uploading files (uploading a local folder)

#### Feature description
The following example shows how to use the SDK’s basic APIs to upload a local folder to COS.

#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos import CosServiceError
from qcloud_cos import CosClientError
from qcloud_cos.cos_threadpool import SimpleThreadPool

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

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  # Get the configured object
client = CosS3Client(config)

uploadDir = '/root/logs'
bucket = 'examplebucket-125000000'
g = os.walk(uploadDir)
# Create a thread pool for the upload.
pool = SimpleThreadPool()
for path, dir_list, file_list in g:
    for file_name in file_list:
        srcKey = os.path.join(path, file_name)
        cosObjectKey = srcKey.strip('/')
        # Determine whether the object exists in COS.
        exists = False
        try:
            response = client.head_object(Bucket=bucket, Key=cosObjectKey)
            exists = True
        except CosServiceError as e:
            if e.get_status_code() == 404:
                exists = False
            else:
                print("Error happened, reupload it.")
        if not exists:
            print("File %s not exists in cos, upload it", srcKey)
            pool.add_task(client.upload_file, bucket, cosObjectKey, srcKey)


pool.wait_completion()
result = pool.get_result()
if not result['success_all']:
    print("Not all files upload sucessed. you should retry")
```

## Simple Operations

### Uploading an object using simple upload

#### Feature description

This API (`PUT Object`) is used to upload an object to a bucket.

#### Method prototype

```
put_object(Bucket, Body, Key, **kwargs)
```
#### Sample 1. Simple object upload

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
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

# Simple upload using file stream
file_name = 'test.txt'
with open('test.txt', 'rb') as fp:
    response = client.put_object(
        Bucket='examplebucket-1250000000',  # Bucket name format: BucketName-APPID
        Body=fp,
        Key=file_name,
        StorageClass='STANDARD',
        ContentType='text/html; charset=utf-8'
    )
    print(response['ETag'])

# Byte stream (upload in whole)
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'abcdefg',
    Key=file_name
)
print(response['ETag'])

# Local path (upload in whole)
response = client.put_object_from_local_file(
    Bucket='examplebucket-1250000000',
    LocalFilePath='local.txt',
    Key=file_name,
)
print(response['ETag'])

# HTTP header (upload in whole)
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'test',
    Key=file_name,
    ContentType='text/html; charset=utf-8'
)
print(response['ETag'])

# Custom header (upload in whole)
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'test',
    Key=file_name,
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    }
)
print(response['ETag'])

# Limiting the upload speed
with open('test.bin', 'rb') as fp:
    response = client.put_object(
        Bucket='examplebucket-1250000000',  
        Key='exampleobject',
        Body=fp,
        TrafficLimit='819200'
    )
    print(response['ETag'])
```
#### Sample 2: creating a directory
In COS, a directory is an object whose name ends with a slash (/). Therefore, you can call the `Put Object` API.

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
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

# Create a directory.
dir_to_create='path/to/create/dir/'
response = client.put_object(
    Bucket='examplebucket-1250000000',  # Bucket name format: BucketName-APPID
    Key=dir_to_create,
    Body=b'',
)
print(response)
```
#### Sample 3: uploading an object to a specified directory

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
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

# When you upload an object whose name is separated with slashes, a directory that contains this object will be created automatically. To upload a new object to this COS directory, set the key prefix of the object to this directory.
dir_name = 'path/to/dir/'
file_name = 'test.txt'
object_key = dir_name + file_name
with open('test.txt', 'rb') as fp:
    response = client.put_object(
        Bucket='examplebucket-1250000000',  # Bucket name format: BucketName-APPID
        Body=fp,
        Key=object_key,
        StorageClass='STANDARD',
        ContentType='text/html; charset=utf-8'
    )
    print(response['ETag'])
```

#### Sample request with all parameters

```python
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes'|file,
    Key='exampleobject',
    EnableMD5=False|True,
    ACL='private'|'public-read', # Please note that the maximum number (1000) of ACLs allowed may be reached if you use this parameter
    GrantFullControl='string',
    GrantRead='string',
    StorageClass='STANDARD'|'STANDARD_IA'|'ARCHIVE',
    Expires='string',
    CacheControl='string',
    ContentType='string',
    ContentDisposition='string',
    ContentEncoding='string',
    ContentLanguage='string',
    ContentLength='123',
    ContentMD5='string',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    },
    TrafficLimit='1048576'
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
|  Body  | Content of the object to be uploaded. It can be a file stream or a byte stream. |  file/bytes | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| EnableMD5 | Whether to calculate the Content-MD5 checksum, which will extend the upload time. It’s not calculated by default. | Bool | No |
| ACL | ACL of the object, such as `private` and `public-read` | String | No |
| GrantFullControl | Grants full permission. Format: `id="OwnerUin"` | String | No |
| GrantRead | Grants read permission. Format: `id="OwnerUin"` | String | No |
| StorageClass | Storage class of the object. For storage classes such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`, please see [Storage Class Overview](https://www.tencentcloud.com/document/product/436/30925). | String     | No |
| Expires | Expiration time | String | No |
| CacheControl | Cache policy | String | No |
| ContentType | Content type | String | No |
| ContentDisposition | Object name | String | No |
| ContentEncoding | Encoding type  | String | No |
| ContentLanguage | Language type  | String | No |
| ContentLength | Length of the content  | String | No |
| ContentMD5 | MD5 checksum of the uploaded object, which is used for verification | String | No |
| Metadata | User-defined object metadata. This parameter must start with `x-cos-meta`; otherwise, it will be ignored. | Dict | No |
|  TrafficLimit | Bandwidth limit for a single request in bit/s. Value range: 819200-838860800, i.e., 100 KB/s - 100 MB/s | String |  No |

#### Response description
The response contains the attributes of the copied object in dict format:

```python
{
    'ETag': 'string',
    'x-cos-version-id': 'string'
}
```


| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| ETag | MD5 checksum of the uploaded object | String |
| x-cos-version-id | Version ID of the object if versioning is enabled | String  |


### Appending parts 

#### Feature description

This API (`APPEND Object`) is used to append object parts to a bucket.

#### Method prototype

```
append_object(Bucket, Key, Position, Data, **kwargs)
```
#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
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

response = client.append_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Position=0,
    Data=b'b'*1024*1024
)
```
#### Sample request with all parameters

```python
response = client.append_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Position=0,
    Data=b'bytes'|file
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| Position | Starting point for the append operation (in bytes). For the first append, the value of this parameter is 0. For subsequent appends, the value is the `Content-Length` of the current object. | Int | Yes |
|Data|Content of the parts to upload, which may be a file stream or byte stream | file/bytes|Yes|

#### Response description
The response contains the attributes of the object in dict format after the append operation.
```python
{
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'x-cos-next-append-position': '12',
    'x-cos-request-id': 'NjEwN2Q0ZGZfMWNhZjU4NjRfMzM1M19hNzQzYjc2'
}
```

## Multipart Operations
Multipart operations include:

- Uploading an object in parts: initializing a multipart upload, uploading parts, and completing a multipart upload
- Resuming a multipart upload: querying uploaded parts, uploading remaining parts, and completing a multipart upload
- Deleting uploaded parts

### Querying multipart uploads

#### Feature description

This API is used to query in-progress multipart uploads in a specified bucket.

#### Method prototype

```
list_multipart_uploads(Bucket, Prefix="", Delimiter="", KeyMarker="", UploadIdMarker="", MaxUploads=1000, EncodingType="", **kwargs)
```
#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
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

response = client.list_multipart_uploads(
    Bucket='examplebucket-1250000000',
    Prefix='dir'
)
```
#### Sample request with all parameters

```python
response = client.list_multipart_uploads(
    Bucket='examplebucket-1250000000',
    Prefix='string',
    Delimiter='string',
    KeyMarker='string',
    UploadIdMarker='string',
    MaxUploads=100,
    EncodingType='url'
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Prefix | Object key prefix to filter multipart uploads by. It is left empty by default. | String | No |
| Delimiter | Separator, left empty by default | String | No |
| KeyMarker | The key of the object after which the returned list begins. It is used together with `UploadIdMarker`. | String | No |
| UploadIdMarker | The upload ID of the object after which the returned list begins. It is used together with `KeyMarker`. If `KeyMarker` is not specified, `UploadIdMarker` will be ignored. | String | No |
| MaxUploads | Maximum number of multipart uploads returned at a time, which is `1000` (the maximum value allowed) by default | Int | No |
| EncodingType | Encoding method of the returned value. The value is not encoded by default. Valid value: `url` | String | No |

#### Response description

This response contains information on the multipart uploads in dict format:

```python
{
    'Bucket': 'examplebucket-1250000000',
    'Prefix': 'string',
    'Delimiter': 'string',
    'KeyMarker': 'string',
    'UploadIdMarker': 'string',
    'NextKeyMarker': 'string',
    'NextUploadIdMarker': 'string',
    'MaxUploads': '1000',
    'IsTruncated': 'true'|'false',,
    'EncodingType': 'url',
    'Upload':[
        {
            'UploadId': 'string',
            'Key': 'string',
            'Initiated': 'string',
            'StorageClass': 'STANDARD',
            'Owner': {
                'DisplayName': 'string',
                'ID': 'string'
            },
            'Initiator': {
                'ID': 'string',
                'DisplayName': 'string'
            }
        },
    ],
    'CommonPrefixes':[
        {
            'Prefix': 'string'
        },
    ],
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String |
| Prefix | Object prefix key by which multipart uploads are queried. It is left empty by default. | String |
| Delimiter | Separator, which is left empty by default. | String |
| KeyMarker | The key of the object after which the returned list begins. It is used together with `UploadIdMarker`. | String |
| UploadIdMarker | The upload ID of the object after which the returned list begins. If `KeyMarker` is not specified, `UploadIdMarker` will be ignored. | String |
| NextKeyMarker | The key of the object after which the next returned list begins if `IsTruncated` is `true` | String |
| NextUploadIdMarker | The upload ID of the object after which the next returned list begins if `IsTruncated` is `true` | String |
| MaxUploads | Maximum number of multipart uploads returned at a time, which is `1000` (the maximum value allowed) by default  | Int |
| IsTruncated | Whether the returned multipart upload list is truncated | String |
| EncodingType | Encoding type of the returned value. The returned value is not encoded by default. Valid value: `url` | String |
| Upload | List of information on all the returned multipart uploads, including `UploadId`, `StorageClass`, `Key`, `Owner`, `Initiator`, and `Initiated` | List |
| CommonPrefixes | All keys starting with the specified prefix and ending with the specified delimiter | List |


### Initializing a multipart upload

#### Feature description

This API (`Initiate Multipart Upload`) is used to initialize a multipart upload and obtain its `uploadId`.

#### Method prototype

```
create_multipart_upload(Bucket, Key, **kwargs):
```
#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
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

response = client.create_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    StorageClass='STANDARD'
)
```
#### Sample request with all parameters

```python
response = client.create_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='multipart.txt',
    StorageClass='STANDARD'|'STANDARD_IA'|'ARCHIVE',
    Expires='string',
    CacheControl='string',
    ContentType='string',
    ContentDisposition='string',
    ContentEncoding='string',
    ContentLanguage='string',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    },
    ACL='private'|'public-read',
    GrantFullControl='string',
    GrantRead='string'
)
# Obtain UploadId for subsequent API calls
uploadid = response['UploadId']
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| StorageClass | Storage class of the object. For storage classes such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`, please see [Storage Class Overview](https://www.tencentcloud.com/document/product/436/30925). | String     | No |
| Expires | Expiration time | String | No |
| CacheControl | Cache policy | String | No |
| ContentType | Content type | String | No |
| ContentDisposition | Filename | String | No |
| ContentEncoding | Encoding type | String | No |
| ContentLanguage | Language type | String | No |
|  Metadata | User-defined object metadata | Dict |  No |
| ACL | ACL of the object, such as `private` and `public-read` | String | No |
| GrantFullControl | Grants full permission. Format: `id="OwnerUin"` | String | No |
| GrantRead | Grants read permission. Format: `id="OwnerUin"` | String | No |

#### Response description

This response contains information on the initialization of the multipart upload in dict format:

```python
{
    'UploadId': '150219101333cecfd6718d0caea1e2738401f93aa531a4be7a2afee0f8828416f3278e5570',
    'Bucket': 'examplebucket-1250000000', 
    'Key': 'exampleobject' 
}

```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| UploadId | ID of the multipart upload | String |
| Bucket | Bucket name in the format of `BucketName-APPID` | String |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String |

### Uploading parts

This API (`Upload Part`) is used to upload an object in parts.

#### Method prototype

```
upload_part(Bucket, Key, Body, PartNumber, UploadId, **kwargs)
```
#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
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

# Note: You can upload at most 10,000 parts at a time.
response = client.upload_part(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Body=b'b'*1024*1024,
    PartNumber=1,
    UploadId='exampleUploadId'
)
```
#### Sample request with all parameters

```python
# Note: You can upload at most 10,000 parts at a time.
response = client.upload_part(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Body=b'bytes'|file,
    PartNumber=1,
    UploadId='string',
    EnableMD5=False|True,
    ContentLength='123',
    ContentMD5='string',
    TrafficLimit='1048576'
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| Body  | Content of the parts to upload. It can be a local file stream or a byte stream | file/bytes |  Yes|
| PartNumber | Part number | Int | Yes |
| UploadId | ID of the multipart upload | String | Yes |
| EnableMD5 | Whether to calculate the Content-MD5 checksum, which will extend the upload time. It’s not calculated by default. | Bool | No |
| ContentLength | Length of the content  | String | No |
| ContentMD5 | MD5 checksum of the uploaded object, which is used for verification | String | No |
|  TrafficLimit | Bandwidth limit for a single request in bit/s. Value range: 819200-838860800, i.e., 100 KB/s - 100 MB/s | String |  No |

#### Response description

This response contains the attributes of the uploaded parts in dict format:

```python
{
    'ETag': 'string'
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| ETag | MD5 checksum of the uploaded parts | String |

### Copying an object part

This API (`Upload Part - Copy`) is used to copy a part of an object.

#### Method prototype

```
upload_part_copy(Bucket, Key, PartNumber, UploadId, CopySource, CopySourceRange='', **kwargs)
```
#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
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

response = client.upload_part_copy(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    PartNumber=1,
    UploadId='exampleUploadId',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou'
    }
)
```
#### Sample request with all parameters

```python
response = client.upload_part_copy(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    PartNumber=100,
    UploadId='string',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'sourceObject', 
        'Region': 'COS_REGION', #Replace it with the source bucket’s region
        'VersionId': 'string'
    },
    CopySourceRange='string',
    CopySourceIfMatch='string',
    CopySourceIfModifiedSince='string',
    CopySourceIfNoneMatch='string',
    CopySourceIfUnmodifiedSince='string'
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| PartNumber | Part number | Int | Yes |
| UploadId | ID of the multipart upload | String | Yes |
| CopySource | Path of the source object to copy, which contains `Bucket`, `Key`, `Region`, and `VersionId` |  Dict | Yes |
| CopySourceRange | Byte range of the source object to copy in the format of `bytes=first-last`. The entire source will be copied by default if no range is specified. | String | No |
| CopySourceIfMatch | `ETag` that must be matched. The object is copied only if its `ETag` matches the value. | String | No |
| CopySourceIfModifiedSince | Required modification time. The object is copied only if it has been modified since the specified time. | String | No |
| CopySourceIfNoneMatch | `ETag` that cannot be matched. The object is copied only if its `ETag` does not match the specified value. | String | No |
| CopySourceIfUnmodifiedSince | Required unmodified time. The object is copied only if it hasn’t been modified since the specified time. | String | No |

#### Response description

This response contains the attributes of the copied parts in dict format:
```python
{
    'ETag': 'string',
    'LastModified': 'string',
    'x-cos-copy-source-version-id': 'string',
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| ETag | MD5 checksum of the copied parts | String |
| LastModified | Time when the copied parts were last modified | String |
| x-cos-copy-source-version-id | Version ID of the source object | String |

### Querying uploaded parts

#### Feature description

This API (`List Parts`) is used to query the uploaded parts of a multipart upload.

#### Method prototype

```
list_parts(Bucket, Key, UploadId, MaxParts=1000, PartNumberMarker=0, EncodingType='', **kwargs)
```
#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
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

response = client.list_parts(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId='exampleUploadId'
)
```
#### Sample request with all parameters

```python
response = client.list_parts(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId=uploadid,
    MaxParts=1000,
    PartNumberMarker=100,
    EncodingType='url'
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| UploadId | ID of the multipart upload | String | Yes |
| MaxParts | Maximum number of parts returned at a time, which is `1000` (the maximum value allowed) by default | Int | No |
| PartNumberMarker | The number of the part after which the list begins. The value of this parameter is `0` by default, which means the list begins from the first part. | Int | No |
| EncodingType | Encoding method of the returned value. The value is not encoded by default. Valid value: `url`  | String | No |

#### Response description

This response contains information on all the uploaded parts in dict format:

```python
{
    'Bucket': 'examplebucket-1250000000', 
    'Key': 'exampleobject', 
    'UploadId': '1502192444bdb382add546a35b2eeab81e06ed84086ca0bb75ea45ca7fa073fa9cf74ec4f2', 
    'EncodingType': None, 
    'MaxParts': '1000',
    'IsTruncated': 'true',
    'PartNumberMarker': '0', 
    'NextPartNumberMarker': '1000', 
    'StorageClass': 'Standard',
    'Part': [
        {
            'LastModified': '2017-08-08T11:40:48.000Z',
            'PartNumber': '1',
            'ETag': '"8b8378787c0925f42ccb829f6cc2fb97"',
            'Size': '10485760'
        },
    ], 
    'Initiator': {
        'DisplayName': '3333333333', 
        'ID': 'qcs::cam::uin/3333333333:uin/3333333333'
    }, 
    'Owner': {
        'DisplayName': '124564654654',
        'ID': '124564654654'
    }
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String |
| UploadId | ID of the multipart upload | String |
| EncodingType | Encoding type of the returned value. The returned value is not encoded by default. Valid value: `url` | String |
| MaxParts | Maximum number of parts returned at a time, which is `1000` (the maximum value allowed) by default  | String |
| IsTruncated | Whether the returned part list is truncated | String |
| PartNumberMarker | The number of the part after which the list begins. The value of this parameter is `0` by default, which means the list begins from the first part. | String |
| NextPartNumberMarker | The number of the part after which the next returned list begins | String |
| StorageClass | Storage class of the object. For more information about storage classes such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`, please see [Storage Class Overview](https://www.tencentcloud.com/document/product/436/30925). | String |
| Part | Information on the uploaded parts, including `ETag`, `PartNumber`, `Size`, and `LastModified` | String |
| Initiator | Initiator of the multipart upload, including `DisplayName` and `ID` | Dict |
| Owner | Information on the object owner, including `DisplayName` and `ID` | Dict |



### Completing a multipart upload

#### Feature description

This API (`Complete Multipart Upload`) is used to complete a multipart upload.

#### Method prototype

```
complete_multipart_upload(Bucket, Key, UploadId, MultipartUpload={}, **kwargs)
```
#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
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

response = client.complete_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId='exampleUploadId',
    MultipartUpload={
        'Part': [
            {
                'ETag': 'string',
                'PartNumber': 1
            },
            {
                'ETag': 'string',
                'PartNumber': 2
            },
        ]
    },
)

```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| UploadId | ID of the multipart upload | String | Yes |
| MultipartUpload | Information on all parts, including `ETag` and `PartNumber` | Dict |Yes |

#### Response description

The response contains information on the object assembled from the uploaded parts in dict format:

```python
{
    'ETag': '"3f866d0050f044750423e0a4104fa8cf-2"', 
    'Bucket': 'examplebucket-1250000000', 
    'Location': 'examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject', 
    'Key': 'exampleobject'
}
```

| Parameter | Description | Type |
| -------------- | -------------- |---------- |
| ETag | The unique tag of the assembled object. This value is not necessarily the MD5 checksum of the object. It is used to verify the uniqueness of the object. To verify the object content, you can check the `ETag` of each part during the upload process. | String |
| Bucket | Bucket name in the format of `BucketName-APPID` | String |
| Location | URL address | String |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String |


### Aborting a multipart upload

#### Feature description

This API (`Abort Multipart Upload`) is used to abort a multipart upload and delete the uploaded parts.

#### Method prototype

```
abort_multipart_upload(Bucket, Key, UploadId, **kwargs)
```
#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
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

response = client.abort_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId='exampleUploadId'
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| UploadId | ID of the multipart upload | String | Yes |

#### Response description
This API returns `None`.
