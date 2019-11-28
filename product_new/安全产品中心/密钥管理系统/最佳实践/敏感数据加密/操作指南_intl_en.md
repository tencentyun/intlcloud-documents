
This operation guide takes Python as an example. Operations in other programming languages can be performed in a similar way.

## Preparations
- Dependent environment: Python v2.7 to 3.x.
- Activate KMS: You can do so in the Tencent Cloud Console.
- Activate TencentCloud API key service: Get the `SecretID`, `SecretKey`, and endpoint. The general format of the endpoint is `*.tencentcloudapi.com`. For example, the endpoint of KMS is `kms.tencentcloudapi.com`. For more information, please see the documentation of the specified product.
- Install the SDK: Run the following command. For more information, please see the [tencentcloud-sdk-python project](https://github.com/TencentCloud/tencentcloud-sdk-python) on GitHub.
```
pip install tencentcloud-sdk-python
```


## Process
You can follow the four steps below to encrypt sensitive data.

1. Create a customer master key (CMK) in the console or through the CreateKey API.
2. Call the Encrypt API to encrypt your sensitive data and get the ciphertext.
3. Store the ciphertext data based on your business needs.
4. When reading data, call the Decrypt API to decrypt the ciphertext into plaintext.

## Directions

### Step 1. Create a CMK
For more information on how to create a CMK, please see [Creating CMK](https://intl.cloud.tencent.com/document/product/1030/31971).


### Step 2. Encrypt the sensitive data

#### Prerequisites: Make sure that the CMK created in step 1 is enabled.

#### Via the console
The online tools are suitable for one-time or non-batch encryption and decryption operations, such as the initial generation of key ciphertext. With the online tools, you can focus on your core business without developing tools for non-batch encryption and decryption. For more information, please see [Encryption and Decryption](https://intl.cloud.tencent.com/document/product/1030/31973).


#### Via the SDK for Python
The Encrypt API is used to encrypt up to 4 KB of data, such as database passwords, RSA keys, or other sensitive information. This document describes how to encrypt data through the SDK for Python. You can also use other supported programming languages.

The `KeyId` and `Plaintext` parameters are required for this API. For more information, please see the [Encrypt](https://intl.cloud.tencent.com/document/product/1030/32189) API document.

#### Encryption in the SDK for Python
KMS is used to encrypt the sensitive configuration file `test_encry.dat` and transfer the ciphertext to the server for use, ensuring that the plaintext data does not get stored in the disk. The sample code below demonstrates how to use the specified CMK for data encryption.

#### Python sample code
```
# -*- coding: utf-8 -*-
import base64

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
# Import the KMS module
from tencentcloud.kms.v20190118 import kms_client, models

# Import the optional configuration classes
from tencentcloud.common.profile.client_profile import ClientProfile
from tencentcloud.common.profile.http_profile import HttpProfile

def KmsInit(region="ap-guangzhou"):
    SecretId = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    SecretKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

    try:
        cred = credential.Credential(
            SecretId,
            SecretKey)

        # Instantiate an HTTP option (optional; skip if there are no special requirements)
        httpProfile = HttpProfile()
        httpProfile.reqMethod = "GET"  # GET request; POST by default
        httpProfile.reqTimeout = 30  #  Request timeout period in seconds (60 seconds by default)
        httpProfile.endpoint = "kms.tencentcloudapi.com"  # Specify the access domain name (nearby access by default)

        # Instantiate a client option (optional; skip if there are no special requirements)
        clientProfile = ClientProfile()
        clientProfile.signMethod = "TC3-HMAC-SHA256"  # Specify the signature algorithm
        clientProfile.language = "en-US"
        clientProfile.httpProfile = httpProfile

        # Instantiate a CLIENT object of KMS
        client = kms_client.KmsClient(cred, region, clientProfile)

        return client
    except TencentCloudSDKException as err:
        print(err)
        return None
def EncryptData(client, keyid, plaintext):
    try:
        # Use the CMK to encrypt the configuration file
        req = models.EncryptRequest()
        encrypt_params = '''{
            "KeyId" : "%s",
            "Plaintext" : "%s"
            }
        '''%(keyid,bytes.decode(plaintext))
        print(encrypt_params)
        req.from_json_string(encrypt_params)

        # Call the Encrypt API
        encryptResp = client.Encrypt(req)
        # Output the encryption result
        print(encryptResp.to_json_string(indent=2))
        # Write the ciphertext into a file
        open('test_encry.dat','w').write(encryptResp.CiphertextBlob)
    except TencentCloudSDKException as err:
        print(err)

if __name__ == '__main__':
    client = KmsInit()
    plaintext = base64.b64encode(b'this plaintext for test')
    EncryptData(client,"KeyId", plaintext)
```


### Step 3. Store the encrypted data
Store the encrypted data according to the application scenarios of your business.

### Step 4. Decrypt the sensitive data

#### Via the console
For more information, please see [Encryption and Decryption](https://intl.cloud.tencent.com/document/product/1030/31973).


#### Via the SDK for Python

The Decrypt API is used to decrypt data. The examples below are implemented in the Tencent Cloud SDK for Python, which can also be implemented in other supported programming languages.

The `CiphertextBlob` parameter is required for this API. For more information, please see the [Decrypt](https://intl.cloud.tencent.com/document/product/1030/32198) API document.


#### Python sample code
```
def DecryptData(client, ciphertext):
    try:
        req = models.DecryptRequest()
        ciphertext_params = '''{
            "CiphertextBlob" : "%s"
            }
        '''%(ciphertext)

        req.from_json_string(ciphertext_params)
        # Call the Decrypt API
        ciphertextResp = client.Decrypt(req)
        # Output the decryption result
        print(ciphertextResp.to_json_string(indent=2))
        # Output the plaintext
        print(base64.b64decode(ciphertextResp.Plaintext))

    except TencentCloudSDKException as err:
        print(err)
if __name__ == '__main__':
    # Decrypt the configuration file for an application
    ciphertext = open('test_encry.dat', 'r').read()
    DecryptData(client, ciphertext)
```
