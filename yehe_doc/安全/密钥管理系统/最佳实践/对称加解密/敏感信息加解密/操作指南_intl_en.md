This operation guide takes Python as an example. Operations in other programming languages can be performed in a similar way.

## Preparations

- Dependent environment of the sample code: Python 2.7.
- Activate KMS: you can do so in the [Tencent Cloud Console](https://console.cloud.tencent.com/kms2).
- Activate TencentCloud API key service: get the `SecretID`, `SecretKey`, and endpoint. The general format of the endpoint is `*.tencentcloudapi.com`. For example, the endpoint of KMS is `kms.tencentcloudapi.com`. For more information, please see the documentation of the specified product.
- Install the SDK: run the following command. For more information, please see the [tencentcloud-sdk-python project](https://github.com/TencentCloud/tencentcloud-sdk-python) on GitHub.

```
pip install tencentcloud-sdk-python
```

## Process

You can follow the four steps below to encrypt sensitive data.

1. Create a customer master key (CMK) in the console or through the `CreateKey` API.
2. Call the `Encrypt` API of KMS to encrypt your sensitive data and get the ciphertext.
3. Store the ciphertext data based on your business needs.
4. When reading data, call the `Decrypt` API of KMS to decrypt the ciphertext into plaintext.

## Directions

### Step 1. Create a CMK

For more information on how to create a CMK, please see [Creating a Key](https://intl.cloud.tencent.com/document/product/1030/31971).

### Step 2. Encrypt the sensitive data

#### Prerequisite: the CMK created in step 1 is enabled.

#### In the console

The online tools are suitable for one-time or non-batch encryption and decryption operations, such as the initial generation of key ciphertext. With the online tools, you can focus on your core business without developing tools for non-batch encryption and decryption. For more information, please see [Encryption and Decryption](https://intl.cloud.tencent.com/document/product/1030/31973).

#### In the SDK for Python

The `Encrypt` API is used to encrypt up to 4 KB of data, such as database passwords, RSA keys, or other sensitive information. This document describes how to encrypt data through the SDK for Python. You can also use other supported programming languages.

The `KeyId` and `Plaintext` parameters are required for this API. For more information, please see the [Encrypt](https://intl.cloud.tencent.com/document/product/1030/32189) API document.

#### Encryption in the SDK for Python

The sample code below demonstrates how to use the specified CMK for data encryption.

#### Python sample code

```
# -*- coding: utf-8 -*-
import base64

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.common.profile.client_profile import ClientProfile
from tencentcloud.common.profile.http_profile import HttpProfile
from tencentcloud.kms.v20190118 import kms_client, models

def KmsInit(region="ap-guangzhou", secretId="", secretKey=""):
    try:
        credProfile = credential.Credential(secretId, secretKey)
        client = kms_client.KmsClient(credProfile, region)
        return client
    except TencentCloudSDKException as err:
        print(err)
        return None

def Encrypt(client, keyId="", plaintext=""):
    try:
        req = models.EncryptRequest()
        req.KeyId = keyId
        req.Plaintext = base64.b64encode(plaintext)
        rsp = client.Encrypt(req) # Call the `Encrypt` API
        return rsp
    except TencentCloudSDKException as err:
        print(err)
        return None

if __name__ == '__main__':
    # User-defined parameters
    secretId = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    secretKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    region = "ap-guangzhou"
    keyId = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    plaintext = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

    client = KmsInit(region, secretId, secretKey)
    rsp = Encrypt(client, keyId, plaintext)
    print "plaintext=", plaintext, ", cipher=", rsp.CiphertextBlob
```

### Step 3. Store the encrypted data

Store the ciphertext according to the application scenarios of your business.

### Step 4. Decrypt the sensitive data

#### In the console

For more information, please see [Encryption and Decryption](https://intl.cloud.tencent.com/document/product/1030/31973).

#### In the SDK for Python

The `Decrypt` API is used to decrypt data.

The `CiphertextBlob` parameter is required for this API. For more information, please see the [Decrypt](https://intl.cloud.tencent.com/document/product/1030/32198) API document.

#### Python sample code

```
# -*- coding: utf-8 -*-
import base64
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.common.profile.client_profile import ClientProfile
from tencentcloud.common.profile.http_profile import HttpProfile
from tencentcloud.kms.v20190118 import kms_client, models

def KmsInit(region="ap-guangzhou", secretId="", secretKey=""):
    try:
        credProfile = credential.Credential(secretId, secretKey)
        client = kms_client.KmsClient(credProfile, region)
        return client
    except TencentCloudSDKException as err:
        print(err)
        return None

def Decrypt(client, keyId="", ciphertextBlob=""):
    try:
        req = models.DecryptRequest()
        req.CiphertextBlob = ciphertextBlob
        rsp = client.Decrypt(req) # Call the `Decrypt` API
        return rsp
    except TencentCloudSDKException as err:
        print(err)
        return None

if __name__ == '__main__':
    # User-defined parameters
    secretId = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    secretKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    region = "ap-guangzhou"
    keyId = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    ciphertextBlob = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

    client = KmsInit(region, secretId, secretKey)
    rsp = Decrypt(client, keyId, ciphertextBlob)
    print "cipher=", ciphertextBlob, ", base64 decoded plaintext=", base64.b64decode(rsp.Plaintext)
```
