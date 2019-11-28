
This operation guide takes Python as an example. Operations in other programming languages can be performed in a similar way.

## Preparations

- Dependent environment: Python v2.7 to 3.x.
- Activate KMS: You can do so in the [Tencent Cloud Console](https://console.cloud.tencent.com/kms2).
- Activate TencentCloud API key service: Get the `SecretID`, `SecretKey`, and endpoint. The endpoint of KMS is `kms.tencentcloudapi.com`. For more information, please see the documentation of the specified product.
- Install the SDK: Run the following command. For more information, please see the open source [tencentcloud-sdk-python project](https://github.com/TencentCloud/tencentcloud-sdk-python) on GitHub.
```
pip install tencentcloud-sdk-python
```


## Process
You can follow the three steps below to complete envelop encryption.
1. Create a CMK.
2. Encrypt data using envelope encryption. Your application calls the KMS GenerateDataKey API to generate a DEK, and the system encrypts data with the plaintext key and stores the ciphertext key and ciphertext in the disk.
3. Decrypt data. The system reads the ciphertext key and ciphertext, decrypts the ciphertext key through the decryption API of KMS, returns the plaintext key, and finally decrypts the ciphertext data with the plaintext key.


## Steps
### Step 1. Create a CMK
For more information on how to create a CMK, please see [Creating CMK](https://cloud.tencent.com/document/product/573/38383).

### Step 2. Encrypt data using envelope encryption
If a new DEK is needed (e.g., data needs to be encrypted for new users or the reuse of a DEK exceeds the specified period of time), you can call an KMS API to create a new DEK, then encrypt data with the plaintext key in the memory, and store the ciphertext and ciphertext key in the disk.

#### Generating a DEK (in KMS SDK for Python)

The GenerateDataKey API is used to generate a DEK, which is a second-level key generated based on a CMK and used for encrypting and decrypting local data. KMS does not store or manage DEKs, which need to be stored by yourself instead.

The examples below are implemented in the Tencent Cloud SDK for Python, which can also be implemented in other supported programming languages.

The `KeyId` parameter is required for this API. For more information, please see the [GenerateDataKey](https://cloud.tencent.com/document/product/573/34419) API document.

#### Example in the SDK for Python
```
# -*- coding: utf-8 -*-
import base64,hashlib
from Crypto.Cipher import AES

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

def AddTo16(value):
    while len(value) % 16 != 0:
        value += '\0'
    return str.encode(value)  # Return bytes

def EncryptData(key,text):
    # Initialize the encryptor
    aes = AES.new(key, AES.MODE_ECB)
    # Encrypt text using AES encryption first
    encryptAes = aes.encrypt(AddTo16(text))
    # Convert text into string using Base64, perform encryption and transcoding, and return bytes
    encrypted_text = str(base64.encodebytes(encryptAes), encoding='utf-8')  
    return encrypted_text

def GenerateDatakey(client,keyid,keyspec='AES_128'):
    try:
        req = models.GenerateDataKeyRequest()
        generatedatakeyParams='''{
            "KeyId" : "%s",
            "KeySpec" : "%s"
        }
        '''%(keyid,keyspec)
        req.from_json_string(generatedatakeyParams)
        # Call the GenerateDataKey API
        generatedatakeyResp = client.GenerateDataKey(req)
        # Output the encryption result
        print(generatedatakeyResp.to_json_string(indent=2))
        return generatedatakeyResp
        # Note: The plaintext key needs to be used in the memory, while the ciphertext key is used for persistent storage

    except TencentCloudSDKException as err:
        print(err)
def Encrypt(key,ciphertext):
    try:
        req = models.EncryptRequest()
        plaintext = open('test_config.conf','r').read()
        entxt = EncryptData(key, plaintext)
        print(entxt)
        # Write the ciphertext into a file
        open('test_encode_text.conf', 'w').write(entxt)
        open('test_encode_256.key', 'w').write(ciphertext)
    except TencentCloudSDKException as err:
        print(err)

if __name__ == '__main__':
    # Set the request object to create the key
    client = KmsInit()
    generatedatakeyResp = GenerateDatakey(client, 'KeyId', 'AES_256')
	# Encrypt data with the plaintext DEK generated in the previous step
    Encrypt(generatedatakeyResp.Plaintext, generatedatakeyResp.CiphertextBlob)
```


### Step 3. Decrypt data
Read the ciphertext key stored in the disk, call the Decrypt API to decrypt the ciphertext key, and then decrypt data using the decrypted plaintext key.

#### Decrypting (in KMS SDK for Python)
The Decrypt API is used to decrypt data.

The examples below are called with the Tencent Cloud SDK for Python, which can also be called with any supported programming languages.

The `CiphertextBlob` parameter is required for this API. For more information, please see the [Decrypt](https://cloud.tencent.com/document/product/573/34429) API document.


#### Example in the SDK for Python
Read the ciphertext key stored in the disk and then call the Decrypt API to decrypt the ciphertext key.
```
def Decrypt(cipchertext):
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
        # Use the plaintext to decrypt the encrypted configuration file
        return base64.b64decode(ciphertextResp.Plaintext)
    except TencentCloudSDKException as err:
        print(err)
def DecryptData(key,text):
    # Initialize the encryptor
    aes = AES.new(key, AES.MODE_ECB)
    # Decrypt Base64-encoded text to bytes first
    base64Decrypted = base64.decodebytes(text.encode(encoding='utf-8'))
    # Perform decryption and transcoding, and return str
    decryptedText = str(aes.decrypt(base64Decrypted),encoding='utf-8').replace('\0','')
    print(decryptedText)
if __name__ == '__main__':
	# Decrypt the DEK
	ciphertext = open('test_encode_256.key', 'r').read()
	decryptData = Decrypt(ciphertext)
	# Decrypt data with the plaintext key
	DecryptData(decryptData, open('test_encode_text.dat', 'r').read())
```
