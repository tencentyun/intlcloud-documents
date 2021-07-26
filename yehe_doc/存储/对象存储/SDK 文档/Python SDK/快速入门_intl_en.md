## Download and Installation

#### Related resources
- Download the source code of COS's XML Python SDK [here](https://github.com/tencentyun/cos-python-sdk-v5).
- Download the XML Python SDK [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-python-sdk-v5/latest/cos-python-sdk-v5.zip).
- Download the [XML Python Demo](https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py).
- For the complete sample code, please see [SDK Sample Code](https://github.com/tencentyun/cos-snippets/tree/master/Python).
- For the SDK changelog, please see [Changelog](https://github.com/tencentyun/cos-python-sdk-v5/blob/master/CHANGELOG.md).



>? If you encounter errors such as non-existent functions or methods when using the XML version of the SDK, please update the SDK to the latest version and try again.
>

#### Environment dependencies

Currently, COS’s XML Python SDK supports Python 2.7, Python 3.4, and later.
>?For the definitions of terms such as SecretId, SecretKey, Bucket, and Region, please see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).

#### Installing SDKs

You can install the SDK in three ways: installation via pip, manual installation, and offline installation.

- Installing via pip (recommended)
```sh
 pip install -U cos-python-sdk-v5
```

- Manual installation
Download the source code [here](https://github.com/tencentyun/cos-python-sdk-v5) and install the SDK manually via setup by running the following command:
```python
 python setup.py install
```

- Offline installation
```python
# Run the following commands on a computer connected to the Internet.
mkdir cos-python-sdk-packages
pip download cos-python-sdk-v5 -d cos-python-sdk-packages
tar -czvf cos-python-sdk-packages.tar.gz cos-python-sdk-packages
# Copy the installation package to a computer that is not connected to the Internet and run the following commands.
# Please make sure that the version of Python on the two computers is the same; otherwise, the installation will fail.
tar -xzvf cos-python-sdk-packages.tar.gz
pip install cos-python-sdk-v5 --no-index -f cos-python-sdk-packages
```



## Getting Started
The section below describes how to use the COS SDK for Python to perform basic operations, such as initializing a client, creating a bucket, querying the bucket list, uploading an object, querying the object list, downloading an object, and deleting an object.

### Initialization
Please refer to the following code sample:

[//]: # ".cssg-snippet-global-init"
```python
# -*- coding=utf-8
# APPID has been removed from the configuration. Please add the APPID to the Bucket parameter in the format of BucketName-APPID.
# 1. Set user configuration, including secretId, secretKey, and region.
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

secret_id = 'SECRETID'      # Replace with your secretId (obtained from the CAM console).
secret_key = 'SECRETKEY'      # Replace with your secretKey (obtained from the CAM console).
region = 'COS_REGION'     # Replace with your region.
token = None                # If a temporary key is used, token needs to be passed in. This is optional and is left empty by default.
scheme = 'https'            # Specify whether to use HTTP or HTTPS protocol to access COS. This is optional and is https by default.
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
# 2. Get the client object.
client = CosS3Client(config)
# Refer to the description below or the demo. For more information, please visit https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py.
```


>? For more information about how to generate and use a temporary key, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
>

Setting proxies:

[//]: # ".cssg-snippet-global-init-proxy"
```python
# APPID has been removed from the configuration. Please add the APPID to the Bucket parameter in the format of BucketName-APPID.
# 1. Set user configuration, including secretId, secretKey, and region.
secret_id = 'SECRETID'      # Replace with your secretId (obtained from the CAM console).
secret_key = 'SECRETKEY'      # Replace with your secretKey (obtained from the CAM console).
region = 'COS_REGION'     # Replace with your region
proxies = {
    'http': '127.0.0.1:80' # Replace with your HTTP Proxy IP.
    'https': '127.0.0.1:443' # Replace with your HTTPS Proxy IP.
}
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Proxies=proxies)
# 2. Get the client object.
client = CosS3Client(config)
# Refer to the description below or the demo. For more information, please visit https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py.
```

Setting an endpoint:

[//]: # ".cssg-snippet-global-init-endpoint"
```python
# APPID has been removed from the configuration. Please add the APPID to the Bucket parameter in the format of BucketName-APPID.
# 1. Set user configuration, including secretId, secretKey, and region.
secret_id = 'SECRETID'      # Replace with your secretId (obtained from the CAM console).
secret_key = 'SECRETKEY'      # Replace with your secretKey (obtained from the CAM console).
region = 'COS_REGION'     # Replace with your region.
endpoint = 'cos.accelerate.myqcloud.com' # Replace with your endpoint
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Endpoint=endpoint)
# 2. Get the client object.
client = CosS3Client(config)
# Refer to the description below or the demo. For more information, please visit https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py.
```

Set the custom domain name:
```python
# APPID has been removed from the configuration. Please specify it using the `Bucket` parameter in the format of `BucketName-APPID`.
# 1. Set user configuration, including secretId, secretKey, and region.
secret_id = 'SECRETID'      # Replace with your secretId (obtained from the CAM console).
secret_key = 'SECRETKEY'      # Replace with your secretKey (obtained from the CAM console).
region = 'COS_REGION'     # Replace with your region.

# Set `domain` to a user-defined domain name.
domain = 'user-define.example.com'
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Domain=domain)
# 2. Get the client object.
client = CosS3Client(config)
# Refer to the description below or the demo. For more information, please visit https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py.
```

Set a global acceleration domain name:
```python
# APPID has been removed from the configuration. Please specify it using the `Bucket` parameter in the format of `BucketName-APPID`.
# 1. Set user configuration, including secretId, secretKey, and region.
secret_id = 'SECRETID'      # Replace with your secretId (obtained from the CAM console).
secret_key = 'SECRETKEY'      # Replace with your secretKey (obtained from the CAM console).
region = 'COS_REGION'     # Replace with your region.

# “domain” is the custom domain, which does not need to be set in most cases. To use a global acceleration domain, set “domain” to the corresponding domain name, such as examplebucket-1250000000.cos.accelerate.myqcloud.com.
# For more information about global acceleration, please visit https://cloud.tencent.com/document/product/436/38864
domain = 'examplebucket-1250000000.cos.accelerate.myqcloud.com'
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Domain=domain)
# 2. Get the client object.
client = CosS3Client(config)
# Refer to the description below or the demo. For more information, please visit https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py.
```

### Creating a bucket

[//]: # ".cssg-snippet-put-bucket"
```python
response = client.create_bucket(
    Bucket='examplebucket-1250000000'
)
```

### Querying a bucket list

[//]: # ".cssg-snippet-get-service"
```python
response = client.list_buckets(
)
```

### Uploading an object

>!Simple upload cannot be used to upload files larger than 5 GB. You can use the advanced upload API to upload large files. For more information about the related parameters, please see [Object Operations](https://intl.cloud.tencent.com/document/product/436/31546).

[//]: # ".cssg-snippet-put-object-comp-comp"
```python
#### Upload a file stream with simple upload (which cannot be used to upload files larger than 5 GB. For files larger than 5 GB, please use the advanced upload API described below).
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

# Online streams will be transferred to COS in the Transfer-Encoding:chunked manner.
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=stream,
    Key='picture.jpg'
)
print(response['ETag'])

#### Advanced upload API (recommended)
# This API can automatically select between simple upload and multipart upload based on the file size. Multipart upload supports the checkpoint restart feature.
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

### Querying an object list

[//]: # ".cssg-snippet-get-bucket"
```python
response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='folder1'
)
```

A single call to the `list_objects` API can query up to 1,000 objects. If you want to query all objects, you need to call it repeatedly.

[//]: # ".cssg-snippet-get-bucket-recursive"
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

### Downloading an object

[//]: # ".cssg-snippet-get-object-comp"
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
print(response['Content-Type'])
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

### Deleting an object

[//]: # ".cssg-snippet-delete-object-comp"
```python
# Delete an object.
## deleteObject
response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)

# Delete multiple objects.
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
