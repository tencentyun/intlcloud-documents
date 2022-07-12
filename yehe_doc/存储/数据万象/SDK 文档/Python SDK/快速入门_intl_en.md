## Download and Installation

#### Related resources
- Download the source code of COS XML Python SDK [here](https://github.com/tencentyun/cos-python-sdk-v5).
- Download the XML Python SDK [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-python-sdk-v5/latest/cos-python-sdk-v5.zip).
- Download the [XML Python SDK demo](https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py).
- For all the code samples, see [here](https://github.com/tencentyun/cos-snippets/tree/master/Python).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/cos-python-sdk-v5/blob/master/CHANGELOG.md).
- For SDK FAQs, see [Python SDK](https://intl.cloud.tencent.com/document/product/436/42375).


>? If you encounter errors such as non-existent functions or methods when using the XML version of the SDK, update the SDK to the latest version and try again.
>

#### Environmental dependencies

Currently, COS XML Python SDK supports Python 2.7, 3.4, and later.
>?For the definitions of terms such as `SecretId`, `SecretKey`, bucket, and region, see [Introduction](https://intl.cloud.tencent.com/document/product/436/7751).

#### Installing SDK

You can install the SDK in three ways: installation via pip, manual installation, and offline installation.

- Installation via pip (recommended)
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
# Run the following commands on a device that is connected to the internet
mkdir cos-python-sdk-packages
pip download cos-python-sdk-v5 -d cos-python-sdk-packages
tar -czvf cos-python-sdk-packages.tar.gz cos-python-sdk-packages
# Copy the installation package to a device that is not connected to the internet and run the following commands
# Make sure that the two devices have the same version of Python installed; otherwise, the installation might fail.
tar -xzvf cos-python-sdk-packages.tar.gz
pip install cos-python-sdk-v5 --no-index -f cos-python-sdk-packages
```



## Getting Started
The section below describes how to use the COS Python SDK to perform basic operations, such as initializing a client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, or deleting an object.

### Initialization

You can initialize the Python SDK Client in the following ways as needed:

#### Initializing with the COS default domain name (default)

If you use the COS default domain name to access COS, the SDK will access COS at a domain name in the format of **{bucket-appid}.cos.{region}.myqcloud.com**.

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)
```

>! Usually, you only need to generate one CosS3Client instance for a region, and then you can upload/download objects repeatedly. Do not generate a CosS3Client instance for every access request; otherwise, the Python process will occupy too many connections and threads.

>? For more information on how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
>

#### Initializing with the COS default domain name and proxy

Configure this part when you need to access COS with a proxy. Otherwise, skip this part.

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
proxies = {
    'http': '127.0.0.1:80',  # Replace it with your HTTP Proxy IP
    'https': '127.0.0.1:443' # Replace with your HTTPS Proxy IP
}

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Proxies=proxies)
client = CosS3Client(config)
```

#### Initializing with the COS acceleration domain name

If you use a COS global acceleration domain name to access COS, the SDK will access COS at a domain name in the format of **{bucket-appid}.cos.accelerate.myqcloud.com**. `region` will not appear in the domain name.

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = None              # `region` does not need to be specified if you initialize with `Endpoint`.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

endpoint = 'cos.accelerate.myqcloud.com' # Replace it with your endpoint or the COS global acceleration domain name. To use a global acceleration domain name, you need to enable the global acceleration feature for the bucket first (visit https://intl.cloud.tencent.com/document/product/436/33406).
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Endpoint=endpoint, Scheme=scheme)
client = CosS3Client(config)
```

#### Initializing with custom domain name

If you use a custom domain name to access COS, the SDK will directly access COS at the configured **custom domain name**. Neither `bucket` nor `region` will appear in the domain name.

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = None              # `region` does not need to be specified if you initialize with a custom domain name
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

domain = 'user-define.example.com' # Your custom domain name. You need to enable the custom domain name for the bucket first (visit https://intl.cloud.tencent.com/document/product/436/31507).
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Domain=domain, Scheme=scheme)
client = CosS3Client(config)
```

#### Initializing with the CDN default domain name

If you use the CDN default domain name to access COS, the SDK will access **CDN** at a domain name in the format of **{bucket-appid}.file.mycloud.com** and then access COS via the CDN origin.

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = None              # `region` does not need to be specified if you initialize with `Endpoint`.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

endpoint = 'file.mycloud.com' # Replace it with your default CDN acceleration domain name. For more information on how to enable CDN acceleration, visit https://intl.cloud.tencent.com/document/product/436/18670.
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Endpoint=endpoint, Scheme=scheme)
client = CosS3Client(config)
```

#### Initializing with the CDN custom domain name

If you use a CDN custom domain name to access COS, the SDK will directly access **CDN** at the configured **custom domain name** and then access COS via the CDN origin. Neither `bucket` nor `region` will appear in the domain name.

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = None              # `region` does not need to be specified if you initialize with a custom domain name
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

domain = 'user-define.example-cdn.com' # Your CDN custom domain name. You need to enable the CDN custom domain name first (visit https://intl.cloud.tencent.com/document/product/436/18670).
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Domain=domain, Scheme=scheme)
client = CosS3Client(config)
```

### Creating bucket

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.create_bucket(
    Bucket='examplebucket-1250000000'
)
```

### Querying bucket list

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.list_buckets(
)
```

### Uploading object

>!Simple upload cannot be used to upload files larger than 5 GB. You can use the advanced upload API to upload larger files. For more information on parameters, see [Object Operations](https://www.tencentcloud.com/document/product/436/43582).

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

#### Uploading file stream through simple upload (for files larger than 5 GB, use the advanced API below)
# We strongly recommend you open the file in binary mode; otherwise, an error may occur.
with open('picture.jpg', 'rb') as fp:
    response = client.put_object(
        Bucket='examplebucket-1250000000',
        Body=fp,
        Key='picture.jpg',
        StorageClass='STANDARD',
        EnableMD5=False
    )
print(response['ETag'])

#### Uploading byte stream through simple upload
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes',
    Key='picture.jpg',
    EnableMD5=False
)
print(response['ETag'])


#### Uploading chunk through simple upload
import requests
stream = requests.get('https://intl.cloud.tencent.com/document/product/436/7778')

# Online streams will be transferred to COS in the `Transfer-Encoding:chunked` manner.
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

### Querying object list

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='folder1'
)
```

A single call to the `list_objects` API can query up to 1,000 objects. If you want to query all objects, you need to call it repeatedly.

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

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

### Downloading object

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

#### Downloading object to local file system
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='picture.jpg',
)
response['Body'].get_stream_to_file('output.txt')

#### Getting file stream
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='picture.jpg',
)
fp = response['Body'].get_raw_stream()
print(fp.read(2))

#### Setting response HTTP headers
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='picture.jpg',
    ResponseContentType='text/html; charset=utf-8'
)
print(response['Content-Type'])
fp = response['Body'].get_raw_stream()
print(fp.read(2))

#### Specifying download range
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='picture.jpg',
    Range='bytes=0-10'
)
fp = response['Body'].get_raw_stream()
print(fp.read())
```

### Deleting object

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, visit https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

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

