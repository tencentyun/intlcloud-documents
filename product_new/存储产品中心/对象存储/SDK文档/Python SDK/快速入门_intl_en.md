## Download and Installation

#### Relevant Resources
The resources of COS XML SDK for Python can be downloaded [here](https://github.com/tencentyun/cos-python-sdk-v5).
Download Demo from: [XML Python Demo](https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py).

#### Environmental Requirements

COS XML SDK for Python currently supports Python 2.6, 2.7, and 3.x.
> For the definitions of parameters such as SecretId, SecretKey, and Bucket, see [COS Glossary](https://cloud.tencent.com/document/product/436/7751).

#### Installing the SDK

You can install the SDK in three ways, i.e., installation via pip, manual installation, and offline installation.

- Installing via Pip (Recommended)
```sh
 pip install -U cos-python-sdk-v5
```

- Manual Installation
Download the source code [here](https://github.com/tencentyun/cos-python-sdk-v5) and install the SDK manually via setup by running the following command.
```python
 python setup.py install
```

- Offline Installation
```python
# Run the following commands on a computer connected to the Internet
mkdir cos-python-sdk-packages
pip download cos-python-sdk-v5 -d cos-python-sdk-packages
tar -czvf cos-python-sdk-packages.tar.gz cos-python-sdk-packages
# Copy the installation package to a computer that is not connected to the Internet and run the following commands.
# Please make sure that the Python versions on the two computers are the same; otherwise, the installation will fail.
tar -xzvf cos-python-sdk-packages.tar.gz
pip install cos-python-sdk-v5 --no-index -f cos-python-sdk-packages
```



## Getting Started
The section below describes how to use COS SDK for Python to perform basic operations, such as initializing a client, creating a bucket, querying the bucket list, uploading an object, querying the object list, downloading an object, and deleting an object.

### Initialization
Please refer to the following code sample:
```python
# APPID has been removed from the configuration. Please add the APPID to the `Bucket` parameter which is in the format of `BucketName-APPID`.
# 1. Set user configuration, including secretId, secretKey and region
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

secret_id = 'COS_SECRETID'      # Replace with your secretId
secret_key = 'COS_SECRETKEY'      # Replace with your secretKey
region = 'ap-beijing'     # Replace with your region
token = None                # If a temporary key is used, token needs to be passed in. This is optional and is null by default
scheme = 'https'            # Specify whether to use HTTP or HTTPS protocol to access COS. This is optional and is https by default
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
# 2. Obtain client object
client = CosS3Client(config)
# Refer to the description below or the demo. For more information, see https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py
```

Setting Proxy：
```python
# APPID has been removed from the configuration. Please add the APPID to the `Bucket` parameter which is in the format of `BucketName-APPID`
# 1. Set user configuration, including secretId, secretKey and region
secret_id = 'COS_SECRETID'      # Replace with your secretId
secret_key = 'COS_SECRETKEY'      # Replace with your secretKey
region = 'ap-beijing'     # Replace with your region
proxies = {
    'http': '127.0.0.1:80' # Replace with your HTTP Proxy IP
    'https': '127.0.0.1:443' # Replace with your HTTPS Proxy IP
}
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Proxies=proxies)
# 2. Obtain client object
client = CosS3Client(config)
# Refer to the description below or the demo. For more information, see https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py
```

Setting endpoint:
```python
# APPID has been removed from the configuration. Please add the APPID to the `Bucket` parameter which is in the format of `BucketName-APPID`
# 1. Set user configuration, including secretId, secretKey and region
secret_id = 'COS_SECRETID'      # Replace with your secretId
secret_key = 'COS_SECRETKEY'      # Replace with your secretKey
region = 'ap-beijing'     # Replace with your region
endpoint = 'cos.accelerate.myqcloud.com' # Replace with your endpoint
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Endpoint=endpoint)
# 2. Obtain client object
client = CosS3Client(config)
# Refer to the description below or the demo. For more information, see https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py
```

For more information on how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

### Creating a Bucket
```python
response = client.create_bucket(
    Bucket='examplebucket-1250000000'
)
```

### Querying the Bucket List
```response
response = client.list_buckets(
)
```

### Uploading an Object

> Simple upload cannot be used to upload files larger than 5 GB. For files larger than 5 GB, please use the advanced upload API described below.

```python
#### Upload a file stream with simple upload (Simple upload cannot be used to upload files larger than 5 GB. For files larger than 5 GB, please use the advanced upload API described below)
# It is strongly recommended to open the file in binary mode; otherwise, an error may occur.
with open('picture.jpg', 'rb') as fp:
    response = client.put_object(
        Bucket='examplebucket-1250000000',
        Body=fp,
        Key='picture.jpg',
        StorageClass='STANDARD',
        EnableMD5=False
    )
print(response['ETag'])

#### Upload a byte stream with simple upload
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes',
    Key='picture.jpg',
    EnableMD5=False
)
print(response['ETag'])


#### Simple chunk upload
import requests
stream = requests.get('https://cloud.tencent.com/document/product/436/7778')

# Online streams will be transferred to COS in the Transfer-Encoding:chunked manner
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=stream,
    Key='picture.jpg'
)
print(response['ETag'])

#### Advanced Upload API (Recommended)
# This API can automatically select between simple upload and multipart upload based on the file size. It also supports checkpoint restart for multipart uploads.
response = client.upload_file(
    Bucket='examplebucket-1250000000',
    LocalFilePath='local.txt',
    Key='picture.jpg',
    PartSize=1,
    MAXThread=10,
    EnableMD5=False
)
print(response['ETag'])
```

### Querying the Object List
```python
response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='folder1'
)
```
A single call to the `list_objects` API can query up to 1,000 objects. If you want to query all objects, you need to call it repeatedly.
```python
marker = ""
while True:
    response = client.list_objects(
        Bucket='examplebucket-1250000000',
        Prefix='folder1',
        Marker=marker
    )
    print(response['Contents'])
    if response['IsTruncated'] == 'false':
        break 
    marker = response['NextMarker']
```

### Downloading an Object
```python
#### Download an object to the local file system
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='picture.jpg',
)
response['Body'].get_stream_to_file('output.txt')

#### Download a file stream
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='picture.jpg',
)
fp = response['Body'].get_raw_stream()
print(fp.read(2))

#### Set the response HTTP headers
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='picture.jpg',
    ResponseContentType='text/html; charset=utf-8'
)
print response['Content-Type']
fp = response['Body'].get_raw_stream()
print(fp.read(2))

#### Specify the download range
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='picture.jpg',
    Range='bytes=0-10'
)
fp = response['Body'].get_raw_stream()
print(fp.read())
```

### Deleting Objects
```python
# Delete an object
## deleteObject
response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)

# Delete multiple objects
## deleteObjects
response = client.delete_objects(
    Bucket='examplebucket-1250000000',
    Delete={
        'Object': [
            {
                'Key': 'exampleobject1',
            },
            {
                'Key': 'exampleobject2',
            },
        ],
        'Quiet': 'true'|'false'
    }
)
```
