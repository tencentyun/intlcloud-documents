## Overview

This document provides SDK code samples related to server-side encryption when uploading and downloading objects. For more information about server-side encryption, see [Server-Side Encryption Overview](https://www.tencentcloud.com/document/product/436/18145).

## Using SSE-COS Server-Side Encryption

With this method, your master key and data are managed by COS. COS can automatically encrypt your data when written into the IDC and automatically decrypt it when accessed. Currently, COS supports AES-256 encryption using a COS master key pair.

#### Sample request: Uploading and downloading SSE-COS encrypted objects

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
scheme = 'https'           # Server-side encryption must use HTTPS

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)  # Obtain the object to configure
client = CosS3Client(config)

# Upload an SSE-COS encrypted object with the encryption type specified as AES256, which indicates SSE-COS encryption.
response = client.put_object(
    Bucket='examplebucket-125000000',
    Key='sdk-sse-cos',
    Body='123',
    ServerSideEncryption='AES256' 
)
print(response['x-cos-server-side-encryption']) # The server side returns 'AES256', indicating SSE-COS encryption.

# Download an SSE-COS encrypted object without the encryption header field, and the object is automatically decrypted by the server side.
response = client.get_object(
    Bucket='examplebucket-125000000',
    Key='sdk-sse-cos',
)
print(response['x-cos-server-side-encryption']) # The server side returns 'AES256', indicating SSE-COS encryption.
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | ----------------------------------------------- | ------ | ---- |
|ServerSideEncryption| Server-side encryption type. `AES256`: SSE-COS encryption; `cos/kms`: KMS encryption |String| No |

## Using SSE-KMS Server-Side Encryption

SSE-KMS is server-side encryption with a key managed by Tencent Cloud Key Management System (KMS). You can use the default key or create a key. For more information about keys, see [Creating a Key](https://www.tencentcloud.com/document/product/1030/31971). For more information about SSE-KMS, see the **SSE-KMS Encryption** section in [Server-side Encryption Overview](https://www.tencentcloud.com/document/product/436/18145#sse-kms-.E5.8A.A0.E5.AF.86).

#### Sample request: Uploading and downloading SSE-KMS encrypted objects

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos.cos_comm import to_byte

import sys
import os
import logging
import base64

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print information about the communication with the server.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = os.environ['COS_SECRET_ID']     #  User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://www.tencentcloud.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://www.tencentcloud.com/document/product/436/14048.
scheme = 'https'           # Server-side encryption must use HTTPS

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)  # Obtain the object to configure
client = CosS3Client(config)

# Upload an SSE-KMS encrypted object with the encryption type specified as `cos/kms`, which indicates SSE-KMS encryption.
response = client.put_object(
    Bucket='examplebucket-125000000',
    Key='sdk-sse-kms',
    Body='123',
    ServerSideEncryption='cos/kms', # For SSE-KMS encryption, the value must be `cos/kms`.
    SSEKMSKeyId='kms-key-id',  # Enter the Customer Master Key (CMK) of KMS. If no value is entered, the CMK created by COS by default will be used.
    SSEKMSContext=base64.standard_b64encode(to_bytes("{\"test\":\"test\"}")) # Encryption context. The value must be the Base64-encoded encryption context (key-value pairs in JSON format). This field is optional.
)
print(response['x-cos-server-side-encryption']) # The server side returns 'cos/kms', indicating that the object is encrypted via SSE-KMS.

# Download an SSE-KMS encrypted object without the encryption header field, and the object is automatically decrypted by the server side.
response = client.get_object(
    Bucket='examplebucket-125000000',
    Key='sdk-sse-kms',
)
print(response['x-cos-server-side-encryption']) # The server side returns 'cos/kms', indicating that the object is encrypted via SSE-KMS.

# (Advanced API) Upload an SSE-KMS encrypted object with the encryption type specified as `cos/kms`, which indicates SSE-KMS encryption.
response = client.upload_file(
    Bucket='examplebucket-125000000', 
    Key='sdk-sse-kms', 
    LocalFilePath="sdk-sse-kms.local", 
    ServerSideEncryption='cos/kms') # For SSE-KMS encryption, the value must be `cos/kms`.

# (Advanced API) Download an SSE-KMS encrypted object without the encryption header field, and the object is automatically decrypted by the server side.
response = client.download_file(
    Bucket='examplebucket-125000000', 
    Key='sdk-sse-kms', 
    DestFilePath='sdk-sse-kms.local')
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | ----------------------------------------------- | ------ | ---- |
|ServerSideEncryption| Server-side encryption type. `AES256`: SSE-COS encryption; `cos/kms`: KMS encryption |String| No |
|SSEKMSKeyId| If `ServerSideEncryption` is `cos/kms`, you can enter the Customer Master Key (CMK) of KMS. If no value is entered, the CMK created by COS by default will be used. |String| No |
|SSEKMSContext| If `ServerSideEncryption` is `cos/kms`, you can enter the Base64-encoded encryption context (key-value pairs in JSON format). |String| No |

## Using SSE-C Server-Side Encryption

With this method, the encryption key is provided by the customer. To upload an object, COS will apply AES-256 encryption to the data using the customer-provided encryption key pair.

> !
>- This type of encryption requires using HTTPS requests.
>- customerKey: The key provided by the user. The key must be a 32-bit string that contains digits, letters, and special characters, but not Chinese characters.
>- If this encryption method was used when you uploaded the source file, you should also use it when you GET (download) or HEAD (query) this file.
>

#### Sample requests: Uploading, downloading, copying, and retrieving SSE-C encrypted objects

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos.cos_comm import get_md5, to_byte

import sys
import os
import logging
import base64

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print information about the communication with the server.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = os.environ['COS_SECRET_ID']     #  User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://www.tencentcloud.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://www.tencentcloud.com/document/product/436/14048.
scheme = 'https'           # Server-side encryption must use HTTPS

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)  # Obtain the object to configure
client = CosS3Client(config)
bucket = 'examplebucket-125000000'
file_name = 'sdk-sse-c'

# Encoding and hashing encryption key
ssec_secret = '00000000000000000000000000000001' # The original key must be a 32-bit string
ssec_key = base64.standard_b64encode(to_bytes(ssec_secret)) # The key must be Base64-encoded
ssec_key_md5 = get_md5(ssec_secret)

# Upload an SSE-C encrypted object
response = client.put_object(
    Bucket=bucket, Key=file_name, Body="00000",
    SSECustomerAlgorithm='AES256', SSECustomerKey=ssec_key, SSECustomerKeyMD5=ssec_key_md5)
print(response['x-cos-server-side-encryption-customer-algorithm']) # The server side returns 'AES256', indicating SSE-C encryption.

# Download an SSE-C encrypted object
response = client.get_object(
    Bucket=bucket, Key=file_name,
    SSECustomerAlgorithm='AES256', SSECustomerKey=ssec_key, SSECustomerKeyMD5=ssec_key_md5)
print(response['x-cos-server-side-encryption-customer-algorithm']) # The server side returns 'AES256', indicating SSE-C encryption.

# HEAD an SSE-C encrypted object
response = client.head_object(
    Bucket=bucket, Key=file_name, 
    SSECustomerAlgorithm='AES256', SSECustomerKey=ssec_key, SSECustomerKeyMD5=ssec_key_md5)
print(response['x-cos-server-side-encryption-customer-algorithm']) # The server side returns 'AES256', indicating SSE-C encryption.

# (Advanced API) Upload an SSE-C encrypted object
response = client.upload_file(
    Bucket=bucket, Key=file_name, LocalFilePath="sdk-sse-c.local",
    SSECustomerAlgorithm='AES256', SSECustomerKey=ssec_key, SSECustomerKeyMD5=ssec_key_md5)

# (Advanced API) Download an SSE-C encrypted object
response = client.download_file(
    Bucket=bucket, Key=file_name, DestFilePath='sdk-sse-c.local',
    SSECustomerAlgorithm='AES256', SSECustomerKey=ssec_key, SSECustomerKeyMD5=ssec_key_md5)

# Copy an SSE-C encrypted object. The source and destination objects can have different encryption types and keys. In this example, the source and destination objects both adopt SSE-C encryption.
dest_ssec_secret = '00000000000000000000000000000002' # The key must be a 32-bit string.
dest_ssec_key = base64.standard_b64encode(to_bytes(dest_ssec_secret))
dest_ssec_key_md5 = get_md5(dest_ssec_secret)
copy_source = {'Bucket': bucket, 'Key': file_name, 'Region': region}
response = client.copy_object(
    Bucket=bucket, Key='sdk-sse-c-copy', CopySource=copy_source,
    SSECustomerAlgorithm='AES256', SSECustomerKey=dest_ssec_key, SSECustomerKeyMD5=dest_ssec_key_md5,
    CopySourceSSECustomerAlgorithm='AES256', CopySourceSSECustomerKey=ssec_key, CopySourceSSECustomerKeyMD5=ssec_key_md5
)

# (Advanced API) Copy an SSE-C encrypted object
response = client.copy(
    Bucket=bucket, Key='sdk-sse-c-copy', CopySource=copy_source, MAXThread=2,
    SSECustomerAlgorithm='AES256', SSECustomerKey=dest_ssec_key, SSECustomerKeyMD5=dest_ssec_key_md5,
    CopySourceSSECustomerAlgorithm='AES256', CopySourceSSECustomerKey=ssec_key, CopySourceSSECustomerKeyMD5=ssec_key_md5)

# Retrieve an SSE-C encrypted object
response = client.restore_object(
    Bucket=bucket, Key=file_name, RestoreRequest={
        'Days': 1,
        'CASJobParameters': {
            'Tier': 'Expedited'
        }
    }, 
    SSECustomerAlgorithm='AES256', SSECustomerKey=ssec_key, SSECustomerKeyMD5=ssec_key_md5)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | ----------------------------------------------- | ------ | ---- |
|SSECustomerAlgorithm| SSE-C encryption algorithm. Currently, only AES256 is supported. |String| No |
|SSECustomerKey| Encryption key of the user. The key must be a Base64-encoded 32-bit string that contains digits, letters, and special characters, but not Chinese characters. |String| Yes (when `SSECustomerAlgorithm` is valid) |
|SSECustomerKeyMD5| MD5 value of the user's encryption key. The MD5 value is used for verifying the key integrity on the server side. |String| Yes (when `SSECustomerAlgorithm` is valid) |
|CopySourceSSECustomerAlgorithm| In the copy API, if the source object uses SSE-C encryption, you need to use this parameter to specify the encryption algorithm for the source object. Currently, only AES256 is supported. |String| No |
|CopySourceSSECustomerKey| In the copy API, if the source object uses SSE-C encryption, you need to use this parameter to specify the encryption key for the source object. The key must be a Base64-encoded 32-bit string. |String| Yes (when `CopySourceSSECustomerAlgorithm` is valid) |
|CopySourceSSECustomerKeyMD5| In the copy API, if the source object uses SSE-C encryption, you need to use this parameter to specify the MD5 value of the encryption key for the source object. The MD5 value is used for verifying the key integrity on the server side. |  String  | Yes (when `CopySourceSSECustomerAlgorithm` is valid) |
