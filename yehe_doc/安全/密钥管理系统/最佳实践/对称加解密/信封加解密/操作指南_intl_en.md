This operation guide takes Python as an example. Operations in other programming languages can be performed in a similar way.

## Preparations

- Dependent environment of the sample code: Python 2.7.
- Activate KMS: you can do so in the [Tencent Cloud Console](https://console.cloud.tencent.com/kms2).
- Activate TencentCloud API key service: get the `SecretID`, `SecretKey`, and endpoint. The endpoint of KMS is `kms.tencentcloudapi.com`. For more information, please see the documentation of the specified product.
- Install the SDK: run the following command. For more information, please see the open-source [tencentcloud-sdk-python project](https://github.com/TencentCloud/tencentcloud-sdk-python) on GitHub.

```
pip install tencentcloud-sdk-python
```

## Process

You can follow the three steps below to complete envelope encryption.

1. Create a CMK.
2. Encrypt data through envelope encryption. Your application calls the KMS `GenerateDataKey` API to generate a DEK, and the system encrypts data with the plaintext key and stores the ciphertext key and ciphertext in the disk.
3. Decrypt data. The system reads the ciphertext key and ciphertext, decrypts the ciphertext key through the `Decrypt` API of KMS, returns the plaintext key, and finally decrypts the ciphertext data with the plaintext key.

## Steps

### Step 1. Create a CMK

For more information on how to create a CMK, please see [Creating a Key](https://intl.cloud.tencent.com/document/product/1030/32783).

### Step 2. Encrypt data through envelope encryption

If a new DEK is needed (e.g., data needs to be encrypted for new users or the reuse of a DEK exceeds the specified period of time), you can call a KMS API to create a new DEK, then encrypt data with the plaintext key in the memory, and store the ciphertext and ciphertext key in the disk.

#### Generating a DEK and encrypting your data

The `GenerateDataKey` API is used to generate a DEK, which is a second-level key generated based on a CMK and used for encrypting and decrypting local data. KMS does not store or manage DEKs, which need to be stored by yourself instead.

The examples below are implemented in the Tencent Cloud SDK for Python, which can also be implemented in other supported programming languages.

The `KeyId` parameter is required for this API. For more information, please see the [GenerateDataKey](https://intl.cloud.tencent.com/document/product/1030/32188) API document.

#### Example in the SDK for Python

```
# -*- coding: utf-8 -*-
import base64
from Crypto.Cipher import AES
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

def GenerateDatakey(client, keyId, keyspec='AES_128'):
    try:
        req = models.GenerateDataKeyRequest()
        req.KeyId = keyId
        req.KeySpec = keyspec
        # Call the `GenerateDataKey` API
        generatedatakeyResp = client.GenerateDataKey(req)
        # The plaintext key needs to be used in the memory, while the ciphertext key is used for persistent storage
        print "DEK cipher=", generatedatakeyResp.CiphertextBlob
        return generatedatakeyResp
    except TencentCloudSDKException as err:
        print(err)

def AddTo16(value):
    while len(value) % 16 != 0:
        value += '\0'
    return str.encode(value)

# User-defined logic. The example here is for reference only
def LocalEncrypt(dataKey="", plaintext=""):
    aes = AES.new(base64.b64decode(dataKey), AES.MODE_ECB)
    encryptedData = aes.encrypt(AddTo16(plaintext))
    ciphertext = base64.b64encode(encryptedData)
    print "plaintext=", plaintext, ", cipher=", ciphertext

if __name__ == '__main__':
    # User-defined parameters
    secretId = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    secretKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    region = "ap-guangzhou"
    keyId = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    keySpec = "AES_256"
    plaintext = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

    client = KmsInit(region, secretId, secretKey)
    rsp = GenerateDatakey(client, keyId, keySpec)

    LocalEncrypt(rsp.Plaintext, plaintext)
```

### Step 3. Decrypt data

Read the ciphertext key stored in the disk, call the `Decrypt` API to decrypt the ciphertext key, and then decrypt data through the decrypted plaintext key.

#### Decrypting (in KMS SDK for Python)

The `Decrypt` API is used to decrypt data.

The examples below are called with the Tencent Cloud SDK for Python, which can also be called with any supported programming languages.

The `CiphertextBlob` parameter is required for this API. For more information, please see the [Decrypt](https://intl.cloud.tencent.com/document/product/1030/32198) API document.

#### Example in the SDK for Python

Decrypt the DEK ciphertext key by calling the KMS `Decrypt` API, and then use the obtained DEK plaintext to decrypt the ciphertext data.

```
# -*- coding: utf-8 -*-
import base64
from Crypto.Cipher import AES
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

def DecryptDataKey(client, ciphertextBlob):
    try:
        req = models.DecryptRequest()
        req.CiphertextBlob = ciphertextBlob
        rsp = client.Decrypt(req) # Call the `Decrypt` API to decrypt the DEK
        return rsp
    except TencentCloudSDKException as err:
        print(err)

# User-defined logic. The example here is for reference only
def LocalDecrypt(dataKey="", ciphertext=""):
    aes = AES.new(base64.b64decode(dataKey), AES.MODE_ECB)
    decryptedData = aes.decrypt(base64.b64decode(ciphertext))
    plaintext = str(decryptedData)
    print "plaintext=", plaintext, ", cipher=", ciphertext

if __name__ == '__main__':
    # User-defined parameters
    secretId = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    secretKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    region = "ap-guangzhou"
    dekCipherBlob="xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    ciphertext="xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    
    client = KmsInit(region, secretId, secretKey)
    rsp = DecryptDataKey(client, dekCipherBlob)

    LocalDecrypt(rsp.Plaintext, ciphertext)
```
