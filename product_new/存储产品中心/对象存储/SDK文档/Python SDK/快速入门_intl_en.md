## Download and Installation

### Relevant Resources
The resources of COS XML Python SDK can be downloaded [here](https://github.com/tencentyun/cos-python-sdk-v5).
The demo can be downloaded [here](https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py).

### Environment Requirements

COS XML Python SDK currently supports Python 2.6, 2.7, and 3.x.
>For the definitions of parameters such as SecretId, SecretKey, and Bucket, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/18507).

### Installing the SDK

You can install the SDK in three ways, i.e., installation via pip, manual installation, and offline installation.

#### Installing via Pip (Recommended)
```sh
 pip install -U cos-python-sdk-v5
```

#### Manual Installation
Download the source code [here](https://github.com/tencentyun/cos-python-sdk-v5) and install the SDK manually via setup by running the following command.
```python
 python setup.py install
```
#### Offline Installation
```python
# Run the following commands on a computer connected to the Internet
mkdir cos-python-sdk-packages
pip download cos-python-sdk-v5 -d cos-python-sdk-packages
tar -czvf cos-python-sdk-packages.tar.gz cos-python-sdk-packages

# Copy the installation package to a computer that is not connected to the Internet and run the following commands
# Please make sure that the Python versions on the two computers are the same; otherwise, the installation will fail
tar -xzvf cos-python-sdk-packages.tar.gz
pip install cos-python-sdk-v5 --no-index -f cos-python-sdk-packages
```


## Getting Started
The section below describes how to perform basic operations with COS Python SDK, such as initializing a client, creating a bucket, querying the bucket list, uploading an object, querying the object list, downloading an object, and deleting an object.

### Initialization
Please refer to the following sample code:
```python
# appid has been removed from the configuration. Please add the appid to the Bucket parameter which is in the format of BucketName-APPID
# 1. Set user profile, including secretId, secretKey, and Region
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

secret_id = 'COS_SECRETID'      # Replace with your secretId
secret_key = 'COS_SECRETKEY'      # Replace with your secretKey
region = 'ap-beijing'     # Replace with your region
token = None                # If a temporary key is used, Token needs to be passed in. This is optional and is null by default
scheme = 'https'            # Specify whether to use HTTP or HTTPS protocol to access COS. This is optional and is https by default
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
# 2. Get the client object
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

```python
#### Simple Upload of a File Stream
file_name = 'test.txt'
# It is strongly recommended to open the file in binary mode; otherwise, an error may occur
with open('test.txt', 'rb') as fp:
    response = client.put_object(
        Bucket='examplebucket-1250000000',
        Body=fp,
        Key=file_name,
        StorageClass='STANDARD',
        EnableMD5=False
    )
print(response['ETag'])

#### Simple Upload of a Byte Stream
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes',
    Key=file_name,
    EnableMD5=False
)
print(response['ETag'])


#### Simple Chunk Upload
import requests
stream = requests.get('https://intl.cloud.tencent.com/document/product/436/7778')

# Online streams will be transferred to COS in the Transfer-Encoding:chunked manner
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=stream,
    Key=file_name
)
print(response['ETag'])

#### Advanced Upload API (Recommended)
It can automatically select simple upload or multipart upload based on the file size. Multipart upload supports upload resumption.
response = client.upload_file(
    Bucket='examplebucket-1250000000',
    LocalFilePath='local.txt',
    Key=file_name,
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
#### Download to the local file system
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key=file_name,
)
response['Body'].get_stream_to_file('output.txt')

#### Download a file stream
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key=file_name,
)
fp = response['Body'].get_raw_stream()
print(fp.read(2))

#### Set the response HTTP header
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key=file_name,
    ResponseContentType='text/html; charset=utf-8'
)
print response['Content-Type']
fp = response['Body'].get_raw_stream()
print(fp.read(2))

#### Specify the download range
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key=file_name,
    Range='bytes=0-10'
)
fp = response['Body'].get_raw_stream()
print(fp.read())
```

### Deleting an Object
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
