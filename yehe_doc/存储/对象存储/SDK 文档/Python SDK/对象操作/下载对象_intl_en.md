## Overview

This document provides an overview of APIs and SDK code samples for simple operations, multipart operations, and other object operations.


| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://www.tencentcloud.com/document/product/436/7753) | Downloading an object | Downloads an object to local |

## Advanced APIs (Recommended)

### Downloading an object (checkpoint restart)

#### Feature description
This advanced download API can determine whether to download a file in whole or in parts based on the file size. It downloads files smaller than or equal to 20 MB in whole and files larger than 20 MB in parts. It also supports automatic checkpoint restart for suspended multipart downloads.

#### Method prototype

```
download_file(Bucket, Key, DestFilePath, PartSize=20, MAXThread=5, EnableCRC=False, **Kwargs)
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

# Use the advanced API to download once without retry. In this case, the checkpoint restart feature is not used.
response = client.download_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    DestFilePath='local.txt'
)

# Use the advanced API for checkpoint restart, and the successfully uploaded parts will not be downloaded again during retries (10 retries here).
for i in range(0, 10):
    try:
        response = client.download_file(
            Bucket='examplebucket-1250000000',
            Key='exampleobject',
            DestFilePath='local.txt')
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

response = client.download_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    DestFilePath='local.txt',
    PartSize=1,
    MAXThread=5,
    EnableCRC=True,
    TrafficLimit='1048576'
    IfMatch='"9a4802d5c99dafe1c04da0a8e7e166bf"',
    IfModifiedSince='Wed, 28 Oct 2014 20:30:00 GMT',
    IfNoneMatch='"9a4802d5c99dafe1c04da0a8e7e166bf"',
    IfUnmodifiedSince='Wed, 28 Oct 2014 20:30:00 GMT',
    ResponseCacheControl='string',
    ResponseContentDisposition='string',
    ResponseContentEncoding='string',
    ResponseContentLanguage='string',
    ResponseContentType='string',
    ResponseExpires='string',
    VersionId='string',
    progress_callback=upload_percentage
)
```
#### Parameter description


| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
|  DestFilePath  | Local path to save the downloaded file |  String |  Yes |
| PartSize | Part size for multipart download. Default value: 20 MB |  Int | No |
|  MAXThread  | Maximum number of concurrent threads for a multipart download. Default value: 5 |  Int |  No |
| EnableCRC | Whether to enable CRC for local and remote files. Default: `False` | Bool | No |
|  TrafficLimit | Bandwidth limit in bit/s for a single request (or a single thread for the advanced download API). Value range: 819200 - 838860800, i.e., 100 KB/s - 100 MB/s | String |  No |
|  IfMatch  | `ETag` that needs to be matched. The object is downloaded only if its `ETag` matches the value. | String  | No |
| IfModifiedSince |  Required modification time. The object is downloaded only if it has been modified after the specified time.  | String | No |
|  IfNoneMatch  |  `ETag` that cannot be matched. The object is downloaded only if its `ETag` does not match the value. | String  | No |
| IfUnmodifiedSince | Required unmodified time. The object is downloaded only if it has not been modified since the specified time.   | String | No |
| ResponseCacheControl | `Cache-Control` of the response header | String | No |
| ResponseContentDisposition | `Content-Disposition` of the response header | String | No |
| ResponseContentEncoding | `Content-Encoding` of the response header | String | No |
| ResponseContentLanguage | `Content-Language` of the response header | String | No |
| ResponseContentType | `Content-Type` of the response header | String | No |
| ResponseExpires | `Expires` of the response header | String | No |
| VersionId | Version ID of the object to download| String | No |
| progress_callback | Callback function for the upload progress. You can customize this function to query the upload progress. | Func | No |

#### Response description
None


### Batch downloading files (downloading a COS directory)

#### Feature description
The following example shows how to use the SDK’s basic APIs to download a COS directory to local storage.

#### Sample request

```python
# -*- coding=utf-8
import logging
import sys
import json
import os

from qcloud_cos import CosConfig, CosServiceError
from qcloud_cos import CosS3Client
from qcloud_cos.cos_threadpool import SimpleThreadPool

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print information about the communication with the server.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = os.environ['COS_SECRET_ID']     #  User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://www.tencentcloud.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://www.tencentcloud.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)  # Obtain the object to configure
client = CosS3Client(config)

# Bucket information
test_bucket = 'examplebucket-1250000000'
start_prefix = 'data/'
# COS uses slashes (/) to indicate folders.
# The delimiter parameter is left empty by default, which lists all subdirectories under the directories to achieve the recursive effect of a local folder.
# If the delimiter parameter is set to "/", you need to handle subdirectories recursively in the SDK.
delimiter = ''


# List and return information about all subdirectories under the current directory.
def listCurrentDir(prefix):
    file_infos = []
    sub_dirs = []
    marker = ""
    count = 1
    while True:
        response = client.list_objects(test_bucket, prefix, delimiter, marker)
        # Debug the output.
        # json_object = json.dumps(response, indent=4)
        # print(count, " =======================================")
        # print(json_object)
        count += 1

        if "CommonPrefixes" in response:
            common_prefixes = response.get("CommonPrefixes")
            sub_dirs.extend(common_prefixes)

        if "Contents" in response:
            contents = response.get("Contents")
            file_infos.extend(contents)

        if "NextMarker" in response.keys():
            marker = response["NextMarker"]
        else:
            break

    print("=======================================================")

    # If the delimiter parameter is set to "/", you need to handle subdirectories recursively.
    # sorted(sub_dirs, key=lambda sub_dir: sub_dir["Prefix"])
    # for sub_dir in sub_dirs:
    #     print(sub_dir)
    #     sub_dir_files = listCurrentDir(sub_dir["Prefix"])
    #     file_infos.extend(sub_dir_files)

    print("=======================================================")

    sorted(file_infos, key=lambda file_info: file_info["Key"])
    for file in file_infos:
        print(file)
    return file_infos


# Download files to a local directory. Local files with the same name (if any) will be overwritten.
# If the directory structure does not exist, a directory structure will be created according to that in COS.
def downLoadFiles(file_infos):
    localDir = "./download/"

    pool = SimpleThreadPool()
    for file in file_infos:
        # Download files to local.
        file_cos_key = file["Key"]
        localName = localDir + file_cos_key

        # If the local directory does not exist, create it recursively.
        if not os.path.exists(os.path.dirname(localName)):
            os.makedirs(os.path.dirname(localName))

        # skip dir, no need to download it
        if str(localName).endswith("/"):
            continue

        # Download files
        # Use a thread pool.
        pool.add_task(client.download_file, test_bucket, file_cos_key, localName)

        # Download in whole
        # response = client.get_object(
        #     Bucket=test_bucket,
        #     Key=file_cos_key,
        # )
        # response['Body'].get_stream_to_file(localName)

    pool.wait_completion()
    return None


# Encapsulate the feature. Download a COS directory to local.
def downLoadDirFromCos(prefix):
    global file_infos

    try:
        file_infos = listCurrentDir(prefix)

    except CosServiceError as e:
        print(e.get_origin_msg())
        print(e.get_digest_msg())
        print(e.get_status_code())
        print(e.get_error_code())
        print(e.get_error_msg())
        print(e.get_resource_location())
        print(e.get_trace_id())
        print(e.get_request_id())

    downLoadFiles(file_infos)
    return None


if __name__ == "__main__":
    downLoadDirFromCos(start_prefix)
```

## Simple Operations

### Downloading an object

#### Feature description

This API (`GET Object`) is used to download an object.

#### Method prototype

```
 get_object(Bucket, Key, **kwargs)
```
#### Sample 1: downloading an object

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

response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
response['Body'].get_stream_to_file('exampleobject')
```

#### Sample 2: partially downloading an object

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
                           # For the list of regions supported by COS, see https://www.tencentcloud.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://www.tencentcloud.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Range='bytes=0-100'
)
response['Body'].get_stream_to_file('exampleobject')
```
#### Sample request with all parameters

```python
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Range='string',
    IfMatch='"9a4802d5c99dafe1c04da0a8e7e166bf"',
    IfModifiedSince='Wed, 28 Oct 2014 20:30:00 GMT',
    IfNoneMatch='"9a4802d5c99dafe1c04da0a8e7e166bf"',
    IfUnmodifiedSince='Wed, 28 Oct 2014 20:30:00 GMT',
    ResponseCacheControl='string',
    ResponseContentDisposition='string',
    ResponseContentEncoding='string',
    ResponseContentLanguage='string',
    ResponseContentType='string',
    ResponseExpires='string',
    VersionId='string',
    TrafficLimit='819200'
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
| Range | Byte range of the object to download. Format: `bytes=first-last` | String | No |
|  IfMatch  | `ETag` that needs to be matched. The object is downloaded only if its `ETag` matches the value. | String  | No |
| IfModifiedSince |  Required modification time. The object is downloaded only if it has been modified after the specified time.  | String | No |
|  IfNoneMatch  |  `ETag` that cannot be matched. The object is downloaded only if its `ETag` does not match the value. | String  | No |
| IfUnmodifiedSince | Required unmodified time. The object is downloaded only if it has not been modified since the specified time.   | String | No |
| ResponseCacheControl | `Cache-Control` of the response header | String | No |
| ResponseContentDisposition | `Content-Disposition` of the response header | String | No |
| ResponseContentEncoding | `Content-Encoding` of the response header | String | No |
| ResponseContentLanguage | `Content-Language` of the response header | String | No |
| ResponseContentType | `Content-Type` of the response header | String | No |
| ResponseExpires | `Expires` of the response header | String | No |
| VersionId | Version ID of the object to download| String | No |
|  TrafficLimit | Bandwidth limit in bit/s for a single request (or a single thread for the advanced download API). Value range: 819200 - 838860800, i.e., 100 KB/s - 100 MB/s | String |  No |

#### Response description

The response contains the content and metadata of the downloaded object in dict format:

```python
{
    'Body': StreamBody(),
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'Accept-Ranges': 'bytes',
    'Content-Range': 'bytes 0-16086/16087',
    'Cache-Control': 'max-age=1000000',
    'Content-Type': 'application/octet-stream',
    'Content-Disposition': 'attachment; filename="filename.jpg"',
    'Content-Encoding': 'gzip',
    'Content-Language': 'zh-cn',
    'Content-Length': '16807',
    'Expires': 'Wed, 28 Oct 2019 20:30:00 GMT',
    'x-cos-meta-test': 'test',
    'x-cos-version-id': 'MTg0NDUxODMzMTMwMDM2Njc1ODA',
    'x-cos-request-id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

<table>
   <tr>
      <th>Parameter</th>
      <th>Description</th>
      <th>Type</th>
   </tr>
   <tr>
      <td>Body</td>
      <td>Content of the downloaded object. You can use the `get_raw_stream()` method to get a file stream and the `get_stream_to_file(local_file_path)` method to download the object’s content to a specified local file.</td>
      <td>StreamBody</td>
   </tr>
   <tr>
      <td>ETag</td>
      <td>MD5 checksum of the object</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Last-Modified</td>
      <td>Time when the object was last modified</td>
      <td>String</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Accept-Ranges</td>
      <td>Range unit. HTTP standard header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Range</td>
      <td>Content range. HTTP standard header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Cache-Control</td>
      <td>Cache policy. HTTP standard header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>Content type. HTTP standard header</td>
      <td>String</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Content-Disposition</td>
      <td>Filename. HTTP standard header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Encoding</td>
      <td>Encoding format. HTTP standard header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Language</td>
      <td>Language type. HTTP standard header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Length</td>
      <td>Object size</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Expires</td>
      <td>Cache expiration time. HTTP standard header</td>
      <td>String</td>
   </tr>
   <tr>
      <td>x-cos-meta-*</td>
      <td>User-defined object metadata. It must start with `x-cos-meta`; otherwise, it will be ignored.</td>
      <td>String</td>
   </tr>
   <tr>
      <td>x-cos-version-id</td>
      <td>Version ID of the object if versioning is enabled</td>
      <td>String</td>
   </tr>
</table>
