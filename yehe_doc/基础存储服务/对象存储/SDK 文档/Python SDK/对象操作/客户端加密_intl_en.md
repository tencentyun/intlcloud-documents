## Overview

This document provides SDK code samples related to client encryption.

## Feature Overview

The SDK for Python allows client-side encryption, which encrypts files before upload and decrypts them at the time of download. There are two types of client-side encryption: AES (symmetric) and RSA (asymmetric).
They are only used for the encryption of the random keys generated. File data is always encrypted using the symmetric method AES256.
Client-side encryption is suitable for users who store sensitive data and may affect the upload speed. The SDK uses the serial method for multipart upload.

## Encryption upon Upload

1. Before each upload, COS randomly generates a symmetric key which is encrypted through the customer-provided symmetric or asymmetric key. The encryption result is then Base64-encoded and stored in object metadata.
2. During the upload, the file is encrypted in memory using the AES256 algorithm.

## Decryption upon Download

1. Get the necessary encryption information from the metadata of the file, Base64-decode it, and then decrypt it using the customer managed key (CMK) to get the encryption key at upload.
2. Use the resulting key to decrypt the downloaded input stream using AES256.

#### Sample request 1: Using symmetric AES256 encryption for randomly generated keys

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos.cos_encryption_client import CosEncryptionClient
from qcloud_cos.crypto import AESProvider
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

conf = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)

# Method 1: Initializing the encryption client using the key value
# Note: According to the requirements of the AES algorithm, `aes_key_value` needs to be Base64-encoded.
aes_provider = AESProvider(aes_key='aes_key_value')

# Method 2: Initializing the encryption client using the key path
aes_key_pair = AESProvider(aes_key_path='aes_key_path')

client_for_aes = CosEncryptionClient(conf, aes_provider)

# Upload an object, an operation fully compatible with non-encryption clients. For more information, see PUT Object documentation
response = client_for_aes.put_object(
                        Bucket='examplebucket-1250000000',
                        Body=b'bytes'|file,
                        Key='exampleobject',
                        EnableMD5=False)

# Download an object, an operation fully compatible with non-encryption clients. For more information, see GET Object documentation
response = client_for_aes.get_object(
                        Bucket='examplebucket-1250000000',
                        Key='exampleobject')

# Upload an object in parts, an operation compatible with non-encryption clients. Except for the last part, the size of each part must be an integer multiple of 16 bytes.
response = client_for_aes.create_multipart_upload(
                        Bucket='examplebucket-1250000000',
                        Key='exampleobject_upload')
uploadid = response['UploadId']
client_for_aes.upload_part(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                Body=b'bytes'|file,
                PartNumber=1,
                UploadId=uploadid)
response = client_for_aes.list_parts(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                UploadId=uploadid)
client_for_aes.complete_multipart_upload(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                UploadId=uploadid,
                MultipartUpload={'Part':response['Part']})

# Upload an object with checkpoint restart. The size of each part must be an integer multiple of 16 bytes.
response = client_for_aes.upload_file(
    Bucket='test04-123456789',
    LocalFilePath='local.txt',
    Key=file_name,
    PartSize=10,
    MAXThread=10
)

```

#### Sample request 2: Using asymmetric RSA encryption for randomly generated keys

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos.cos_encryption_client import CosEncryptionClient
from qcloud_cos.crypto import RSAProvider
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

conf = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)

# Method 1: initializing the encryption client using the key value
rsa_key_pair = RSAProvider.get_rsa_key_pair('public_key_value', 'private_key_value')

# Method 2: initializing the encryption client using the key path
rsa_key_pair = RSAProvider.get_rsa_key_pair_path('public_key_path', 'private_key_path')

rsa_provider = RSAProvider(key_pair_info=rsa_key_pair)
client_for_rsa = CosEncryptionClient(conf, rsa_provider)

# Upload an object, an operation fully compatible with non-encryption clients. For more information, see PUT Object documentation
response = client_for_rsa.put_object(
                        Bucket='examplebucket-1250000000',
                        Body=b'bytes'|file,
                        Key='exampleobject',
                        EnableMD5=False)

# Download an object, an operation fully compatible with non-encryption clients. For more information, see GET Object documentation
response = client_for_rsa.get_object(
                        Bucket='examplebucket-1250000000',
                        Key='exampleobject')

# Upload an object in parts, an operation compatible with non-encryption clients. Except for the last part, the size of each part must be an integer multiple of 16 bytes.
response = client_for_rsa.create_multipart_upload(
                        Bucket='examplebucket-1250000000',
                        Key='exampleobject_upload')
uploadid = response['UploadId']
client_for_rsa.upload_part(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                Body=b'bytes'|file,
                PartNumber=1,
                UploadId=uploadid)
response = client_for_rsa.list_parts(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                UploadId=uploadid)
client_for_rsa.complete_multipart_upload(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                UploadId=uploadid,
                MultipartUpload={'Part':response['Part']})

# Upload an object with checkpoint restart. The size of each part must be an integer multiple of 16 bytes.
response = client_for_rsa.upload_file(
    Bucket='test04-123456789',
    LocalFilePath='local.txt',
    Key=file_name,
    PartSize=10,
    MAXThread=10
)
```
