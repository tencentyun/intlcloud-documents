## Overview
The Python SDK provides APIs to obtain request signatures, pre-signed URLs, and pre-signed download URLs for request distribution.The method for getting a pre-signed URL is the same whether you are using permanent or temporary keys, with the only difference being that the latter requires `x-cos-security-token` included in the header or query_string.
For details about how to use a pre-signed URL for uploads, see [Upload via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14114). For details about how to use a pre-signed URL for downloads, see [Download via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14116).

>?
> - When getting a signature, you are strongly advised to include sensitive request headers and parameters in the signature to prevent related request headers and parameters from being tampered with by users and prevent permission trespassing. In addition, the SDK will include the requested domain name in the signature by default. If the requested domain name is modified after distribution, the access will fail. In this case, you can ignore the requested domain name in the input parameters when getting the signature. See the request examples below for details. 
> - You are advised to use a temporary key to generate pre-signed URLs for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://www.tencentcloud.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
> 

## Getting Pre-Signed URLs

#### Feature description

The SDK allows you to get a pre-signed URL that can be used for distribution purposes.

#### Method prototype

```
get_presigned_url(Bucket, Key, Method, Expired=300, Params={}, Headers={})
```

#### Sample request 1. Generate a pre-signed upload URL

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import os
import logging
import requests

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

# Generate an upload URL without specifying request headers and parameters
url = client.get_presigned_url(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(url)

# Generate an upload URL with a specified storage class and upload speed
url = client.get_presigned_url(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Headers={
        'x-cos-storage-class':'STANDARD_IA', 
        'x-cos-traffic-limit':'819200' # The pre-signed URL itself does not include request headers, but request headers are signed in the signature. Therefore, the URL must carry request headers and their values specified here.
    },
    Expired=300  # Expire in 300 seconds. Specify the expiration time as needed.
)
print(url)

# Generate an upload URL that can only be used to upload specified file content
url = client.get_presigned_url(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Headers={'Content-MD5':'string'}, # When the URL is used to upload an object, an MD5 request header must be carried, and the value of the request header must be the value specified here, thus limiting the content of the file.
    Expired=300  # Expire in 300 seconds. Specify the expiration time as needed.
)
print(url)

# Generate an upload URL that can only be used for ACL upload
url = client.get_presigned_url(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Params={'acl':''}, # If a request parameter is specified, it will be carried in the URL and included in the signature, and its value cannot be modified by users.
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(url)

# Generate an upload URL, where the request domain name is not signed and users need to modify the request domain name before usage
url = client.get_presigned_url(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    SignHost=False, # Exclude the request domain name from the signature. This setting will bring certain security risks. Use it only when you need to allow users to modify the request domain name after signing.
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(url)

# Use an upload URL
response = requests.put(url=url, data=b'123')
print(response)
```

#### Sample request 2. Generate a pre-signed download URL

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import os
import logging
import requests

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

# Generate a download URL without specifying request headers and parameters
url = client.get_presigned_url(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(url)

# Generate a download URL, specifying the `content-disposition` header in the response to save the file in the browser instead of displaying it
url = client.get_presigned_url(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Params={
        'response-content-disposition':'attachment; filename=example.xlsx' # Save the object as a specified file during download
        # Other request parameters supported in addition to `response-content-disposition` include `response-cache-control`, `response-content-encoding`, `response-content-language`,
        # `response-content-type`, and `response-expires`. For more information, see the object download API at https://cloud.tencent.com/document/product/436/7753.
    }, 
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(url)

# Generate a download URL with a specified download speed
url = client.get_presigned_url(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Headers={'x-cos-traffic-limit':'819200'}, # The pre-signed URL itself does not include request headers, but request headers are included in the signature. Therefore, the URL must carry the request headers and their values specified here.
    Expired=300  # Expire in 300 seconds. Specify the expiration time as needed.
)
print(url)

# Generate a download URL that can only be used for ACL download
url = client.get_presigned_url(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Params={'acl':''}, # If a request parameter is specified, it will be carried in the URL and included in the signature, and its value cannot be modified by users.
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(url)

# Generate a download URL that does not include the request domain name in the signature and is used when users need to modify the request domain name after signing
url = client.get_presigned_url(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    SignHost=False, # Exclude the request domain name from the signature. This setting will bring certain security risks. Use it only when you need to allow users to modify the request domain name after signing.
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(url)

# Use the download URL
response = requests.get(url)
print(response)
```

#### Sample request 3. Generate a pre-signed download URL with a temporary key

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import os
import logging
import requests

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

# Generate a download URL
url = client.get_presigned_url(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Headers={'x-cos-traffic-limit':'819200'}, # The pre-signed URL itself does not include request headers, but request headers are included in the signature. Therefore, the URL must carry the request headers and their values specified here.
    Params={
        'x-cos-security-token': 'string' # If you use a temporary key, you need to enter the token as a request parameter.
    },
    Expired=120,  # Expire in 120 seconds. Specify the expiration time as needed.
    SignHost=False # Do not sign the request domain name. This setting will bring certain security risks. Use it only when you need to allow users to modify the request domain name after signing.
)
print(url)

# Use the download URL
response = requests.get(url)
print(response)
```

#### Sample request with all parameters

```python
response = client.get_presigned_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Method='PUT'|'POST'|'GET'|'DELETE'|'HEAD',
    Expired=300,
    Headers={
        'header1': 'string',
        'header2': 'string',
    },
    Params={
        'param1': 'string',
        'param2': 'string'
    },
    SignHost=True|False
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`. (**Users do not need to encode the URL.**) | String | Yes |
| Method  | Operation method. Valid values: 'PUT', 'POST', 'GET', 'DELETE', 'HEAD'|  String |  Yes |
| Expired | Specifies the time in seconds before a signature expires | Int| No |
| Params | Request parameters in a pre-signed URL. If a request parameter is specified, it will be carried in the URL and included in the signature, and its value cannot be modified by users. The request parameters that can be signed depend on the corresponding operations. For example, for request parameters that can be carried and signed for object download, see the description of the request parameters of the [GET Object](https://www.tencentcloud.com/document/product/436/7753) API. | Dict | No |
| Headers | Request headers that need to be signed in a pre-signed URL. The pre-signed URL itself does not include request headers, but request headers are included in the signature. Therefore, the URL must carry the request headers and their values specified by this parameter. The request headers that can be signed depend on the corresponding operations. For example, for request headers that can be signed for object upload, see the description of the request headers of the [PUT Object](https://www.tencentcloud.com/document/product/436/7749) API. | Dict | No |
| SignHost | Whether to include the request domain name in the signature. The default value is `True`. To allow users to modify the request domain name after signing, set this parameter to `False`. | Bool | No |

#### Response description

A pre-signed URL is returned upon success.

## Getting Pre-Signed Download URLs

#### Feature description
The SDK allows you to get a pre-signed download URL that can be used to directly download an object.

#### Method prototype

```
get_presigned_download_url(Bucket, Key, Expired=300, Params={}, Headers={})
```

#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import os
import logging
import requests

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

# Generate a download URL without specifying request headers and parameters
url = client.get_presigned_download_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(url)

# Generate a download URL, specifying the `content-disposition` header in the response to save the file in the browser instead of displaying it
url = client.get_presigned_download_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Params={
        'response-content-disposition':'attachment; filename=example.xlsx' # Save the object as a specified file during download
        # Other request parameters supported in addition to `response-content-disposition` include `response-cache-control`, `response-content-encoding`, `response-content-language`,
        # `response-content-type`, and `response-expires`. For more information, see the object download API at https://cloud.tencent.com/document/product/436/7753.
    }, 
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(url)

# Generate a download URL with a specified download speed
url = client.get_presigned_download_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Headers={'x-cos-traffic-limit':'819200'}, # The pre-signed URL itself does not include request headers, but request headers are included in the signature. Therefore, the URL must carry the request headers and their values specified here.
    Expired=300  # Expire in 300 seconds. Specify the expiration time as needed.
)
print(url)

# Generate a download URL that can only be used for ACL download
url = client.get_presigned_download_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Params={'acl':''}, # If a request parameter is specified, it will be carried in the URL and included in the signature, and its value cannot be modified by users.
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(url)

# Generate a download URL that does not include the request domain name in the signature and is used when users need to modify the request domain name after signing
url = client.get_presigned_download_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    SignHost=False, # Exclude the request domain name from the signature. This setting will bring certain security risks. Use it only when you need to allow users to modify the request domain name after signing.
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(url)

# Generate a download URL with a temporary key
url = client.get_presigned_download_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Params={
        'x-cos-security-token': 'string'  # Token is required for temporary keys but not permanent keys.
    }
)
print(url)

# Use the download URL
response = requests.get(url)
print(response)
```

#### Sample request with all parameters

```python
response = client.get_presigned_download_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expired=300,
    Headers={
        'header1': 'string'
    },
    Params={
        'param1': 'string',
        'param2': 'string'
    },
    SignHost=True|False
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`. (**Users do not need to encode the URL.**) | String | Yes |
| Expired | Specifies the time in seconds before a signature expires | Int| No |
| Params | Request parameters in a pre-signed URL. If a request parameter is specified, it will be carried in the URL and included in the signature, and its value cannot be modified by users. The request parameters that can be signed depend on the corresponding operations. For example, for request parameters that can be carried and signed for object download, see the description of the request parameters of the [GET Object](https://www.tencentcloud.com/document/product/436/7753) API. | Dict | No |
| Headers | Request headers that need to be signed in a pre-signed URL. The pre-signed URL itself does not include request headers, but request headers are included in the signature. Therefore, the URL must carry the request headers and their values specified by this parameter. The request headers that can be signed depend on the corresponding operations. For example, for request headers that can be signed for object upload, see the description of the request headers of the [PUT Object](https://www.tencentcloud.com/document/product/436/7749) API. | Dict | No |
| SignHost | Whether to include the request domain name in the signature. The default value is `True`. To allow users to modify the request domain name after signing, set this parameter to `False`. | Bool | No |

#### Response description

A pre-signed download URL is returned upon success.

## Getting Signatures

#### Feature description
The SDK allows you to obtain a signature for a specified operation. This feature is commonly used for signature distribution to mobile devices.

#### Method prototype

```
get_auth(Method, Bucket, Key, Expired=300, Headers={}, Params={})
```

#### Sample request 1. Generate an upload signature

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

# Generate an upload signature without specifying request headers and parameters
response = client.get_auth(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(response)

# Generate an upload signature with a specified storage class and upload speed
response = client.get_auth(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Headers={
        'x-cos-storage-class':'STANDARD_IA', 
        'x-cos-traffic-limit':'819200' # When the signature is used, this URL speed limiting request header and its value specified here must be carried.
    },
    Expired=300  # Expire in 300 seconds. Specify the expiration time as needed.
)
print(response)

# Generate an upload signature that can only be used to upload specified file content
response = client.get_auth(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Headers={'Content-MD5':'string'}, # When the signature is used, this MD5 request header must be carried, and the value of the request header must be the value specified here, thus limiting the content of the file.
    Expired=300  # Expire in 300 seconds. Specify the expiration time as needed.
)
print(response)

# Generate an upload signature that can only be used for ACL upload
response = client.get_auth(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Params={'acl':''}, # When the signature is used, this ACL request parameter must be carried so that the request can only be used for object ACL upload.
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(response)

# Generate an upload signature that does not include the request domain name and is used by users when they need to modify the request domain name after signing
response = client.get_auth(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    SignHost=False, # Exclude the request domain name from the signature. This setting will bring certain security risks. Use it only when you need to allow users to modify the request domain name after signing.
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(response)
```

#### Sample request 2: Generate a download signature

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


# Generate a download signature without specifying request headers and parameters
response = client.get_auth(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(response)

# Generate a download signature with a specified download speed
response = client.get_auth(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Headers={'x-cos-traffic-limit':'819200'}, # When the signature is used, this URL speed limiting request header must be carried, and the value of the request header must be the value specified here.
    Expired=300  # Expire in 300 seconds. Specify the expiration time as needed.
)
print(response)

# Generate a download signature that can only be used for ACL download
response = client.get_auth(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Params={'acl':''}, # When the signature is used, this ACL request parameter must be carried so that the request can only be used for object ACL download.
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(response)

# Generate a download signature that does not include the request domain name and is used by users when they need to modify the request domain name after signing
response = client.get_auth(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    SignHost=False, # Exclude the request domain name from the signature. This setting will bring certain security risks. Use it only when you need to allow users to modify the request domain name after signing.
    Expired=120  # Expire in 120 seconds. Specify the expiration time as needed.
)
print(response)

# Generate a download signature with a temporary key
response = client.get_auth(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Params={
        'x-cos-security-token': 'string'  # Token is required for temporary keys but not permanent keys.
    }
)
print(response)
```

#### Sample request with all parameters

```python
response = client.get_auth(
    Method='PUT'|'POST'|'GET'|'DELETE'|'HEAD',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expired=300,
    Headers={
        'header1': 'string',
        'header2': 'string'
    },
    Params={
        'param1': 'string',
        'param2': 'string'
    },
    SignHost=True|False
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Method  | Operation method. Valid values: 'PUT', 'POST', 'GET', 'DELETE', 'HEAD'|  String |  Yes |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key  | Specifies the root path `/` for a bucket operation or the file path for an object operation (**Users do not need to encode the URL.**) | String | Yes|
| Expired | Specifies the time in seconds before a signature expires | Int| No |
| Params | Request parameters that need to be signed in a signature. When the signature is used, the request parameters and their values specified by this parameter must be carried. The request parameters that can be signed depend on the corresponding operations. For example, for request parameters that can be carried and signed for object download, see the description of the request parameters of the [GET Object](https://www.tencentcloud.com/document/product/436/7753) API. | Dict | No |
| Headers | Request headers that need to be signed in a signature. When the signature is used, the request headers and their values specified by this parameter must be carried. The request headers that can be signed depend on the corresponding operations. For example, for request headers that can be signed for object upload, see the description of the request headers of the [PUT Object](https://www.tencentcloud.com/document/product/436/7749) API. | Dict | No |
| SignHost | Whether to include the request domain name in the signature. The default value is `True`. To allow users to modify the request domain name after signing, set this parameter to `False`. | Bool | No |

#### Response description

The signature value for the corresponding operation is returned upon success.
