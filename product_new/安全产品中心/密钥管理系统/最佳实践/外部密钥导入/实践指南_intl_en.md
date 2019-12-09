## Process
You can follow the four steps below to create an external CMK.
1. Create a CMK whose source is "external" in the console or through the API, i.e., creating an external CMK.
2. Call an API to get the parameters of the material to be imported into a CMK, including a public key used to encrypt the key material and an import token.
3. Use an encryptor or other secure encryption measures to encrypt your key material locally with the public key obtained in step 2.
4. Call an API to import the encrypted key material and the import token obtained in step 2 into the external CMK.



## Directions
<span id="step1"></span>
### Step 1. Create an external CMK

You can create an external CMK in the console or through the API.

- **Via the console**
(1). Log in to the [KMS Console](https://console.cloud.tencent.com/kms2).
(2). Select the region where you want to create a key and click **Create**.
(3). In the "Create Key" window, enter the key name and select "External" for key material source, read the document on the methods of importing external key materials and the precautions, and check the box. <br><img src="https://main.qcloudimg.com/raw/ae2d358e712220793ab7289d2817ba26.png"  width="52%">
(4). Click **OK** to create the external CMK. You can view the created CMK in the console, where the "Key Source" is displayed as "External".

- **Via the API**
Below is an example using Tencent Cloud [TCCLI](https://cloud.tencent.com/product/cli), which can be called with any supported programming language.
	When requesting the CreateKey API, set the `Type` parameter to `2` by running the following command:
	```shell
	tccli kms CreateKey --Alias <alias> --Type 2
	```

	Sample source code of the `CreateKey` API:
	```
	def create_external_key(client, alias):
		"""
		Generate a BYOK key,
		:param Type = 2
		"""
		try:
			req = models.CreateKeyRequest()
			req.Alias = alias
			req.Type = 2
			rsp = client.CreateKey(req)
			return rsp, None
		except TencentCloudSDKException as err:
			return None, err
	```

<span id="step2"></span>
### Step 2. Get the parameters of the material to be imported into a CMK
To ensure the security of your key material, you need to encrypt your key material before importing it. You can get its parameters through an API, including a public key used to encrypt the key material and an import token.

Run the following command on TCCLI:
```
tccli kms GetParametersForImport --KeyId <keyid> --WrappingAlgorithm RSAES_PKCS1_V1_5 --WrappingKeySpec RSA_2048
```


Sample source code of the `GetParametersForImport` function:
```
def get_parameters_for_import(client, keyid):
    """
    Get the parameters of the material to be imported into a CMK,
    of which the returned `Token` is a parameter that executes the `ImportKeyMaterial` function,
    and the returned `PublicKey` is used to encrypt the key material.
    The `Token` and `PublicKey` will expire in 24 hours. After that, you need to call the API again to get new `Token` and `PublicKey`.
    `WrappingAlgorithm ` is used to specify the algorithm for key material encryption. Currently, `RSAES_PKCS1_V1_5`, `RSAES_OAEP_SHA_1`, and `RSAES_OAEP_SHA_256` are supported.
    `WrappingKeySpec` is used to specify the type of key material encryption. Currently, only `RSA_2048` is supported.
    """
    try:
        req = models.GetParametersForImportRequest()
        req.KeyId = keyid
        req.WrappingAlgorithm = 'RSAES_PKCS1_V1_5' # RSAES_PKCS1_V1_5 | RSAES_OAEP_SHA_1 | RSAES_OAEP_SHA_256
        req.WrappingKeySpec =  'RSA_2048' # RSA_2048       
        rsp = self.client.GetParametersForImport(req)
        return rsp, None
    except TencentCloudSDKException as err:
        return None, err
```


### Step 3. Encrypt your key material locally
Use the encryption public key obtained in [step 2](#step2) to encrypt your key material locally. The encryption public key is a 2,048-bit RSA public key, and the encryption algorithm used should be the same as specified for getting the parameters of the key material. As the encryption public key returned by the API is Based64-encoded, you need to Base64-decode it before using it. Currently, algorithms supported by KMS include `RSAES_OAEP_SHA_1`, `RSAES_OAEP_SHA_256`, and `RSAES_PKCS1_V1_5`.


Below is an example of encrypting the key material using OpenSSL. In actual use, it is recommended to encrypt your key material using an encryptor or other secure encryption measures.

(1). Call the GetParametersForImport API to get the `Token` and `PublicKey`, and write the `PublicKey` into the `public_key.base64` file.
(2). Generate a random number using OpenSSL.
```
openssl rand -out raw_material.bin 16
```
You can also use the GenerateRandom API to generate a random number for Base64-decoding.
>The length of a SM-CRYPTO key material must be 128 bits, while that of a FIPS-compliant one must be 256 bits.

(3). Decode the public key.
```
openssl enc -d -base64 -A -in public_key.base64 -out public_key.bin
```

(4). Use the public key to encrypt the key material.
```shell
# The command line corresponding to `RSAES_OAEP_SHA_1` is as follows:
openssl pkeyutl -in raw_material.bin -out encrypted_key_material.bin -inkey public_key.bin -keyform DER -pubin -encrypt -pkeyopt rsa_padding_mode:oaep -pkeyopt rsa_oaep_md:sha1

# The command line corresponding to `RSAES_PKCS1_V1_5` is as follows:
openssl pkeyutl -in raw_material.bin -out encrypted_key_material.bin -inkey public_key.bin -keyform DER -pubin -encrypt -pkeyopt rsa_padding_mode:pkcs1

# The command line corresponding to `RSAES_OAEP_SHA_256` is as follows:
openssl pkeyutl -in raw_material.bin -out encrypted_key_material.bin -inkey public_key.bin -keyform DER -pubin -encrypt -pkeyopt rsa_padding_mode:oaep -pkeyopt rsa_oaep_md:sha256
```

(5). Import the encoded ciphertext into KMS as a parameter.
```
openssl enc -e -base64 -A -in encrypted_key_material.bin -out encrypted_material.base64
```
Import the final output `encrypted_material.base64` into KMS as `EncryptedKeyMaterial`.


### Step 4. Import the key material
Call an API to import the encrypted key material and the import token obtained in [step 2](#step2) into the external CMK created in [step 1](#step1).

- The import token and the public key for key material encryption are bound, and a token can only be used to import key material for the CMK specified when it was generated. The import token is valid for 24 hours and can be reused within its validity period. If it expires, you need to get a new token and encryption public key.
- If the GetParametersForImport API is called multiple times to get the key material, only the token and publicKey obtained from the last call will be valid, while those returned from previous calls will expire automatically.
- You can import key material into an external key where no key materials have ever been imported, reimport key material that has expired or been deleted, or reset the expiration time of key material.

Make a request to import key material through the ImportKeyMaterial API. Below is a sample command:
```
tccli kms ImportKeyMaterial --EncryptedKeyMaterial <material> --ImportToken <token> --KeyId <keyid>
```

Sample source code of the `ImportKeyMaterial` function:
```
def import_key_material(client, material, token, keyid):
    try:
        req = models.ImportKeyMaterialRequest()
        req.EncryptedKeyMaterial = material
        req.ImportToken = token
        req.KeyId = keyid
        rsp = client.ImportKeyMaterial(req)
        return rsp, None
    except TencentCloudSDKException as err:
        return None, err
```

At this point, the external CMK has been imported. You can use it just like an ordinary key.

## More Operations
### Deleting an external CMK
Deleting an external CMK involves two kinds of operations: deleting the CMK at the scheduled time, and deleting the key material, which will lead to different results.

#### Deleting a CMK at the scheduled time
The schedule deletion feature can be used to delete an external CMK and has a mandatory waiting period of 7-30 days, after which the external key will be deleted. Please note that once deleted, the CMK cannot be recovered, and the data encrypted with it cannot be decrypted.


#### Deleting key material
You can delete key material in two ways. If the key material expires or is deleted, the external CMK can no longer be used, and the data encrypted with the CMK can no longer be decrypted, unless you import the same key material into the CMK again.
- You can call the DeleteImportedKeyMaterial API to delete the key material. After the key material is deleted, the key status will become `PendingImport`.
- In an ImportKeyMaterial API call, set the expiration time using the `ValidTo` input parameter, and KMS will automatically delete the key material upon expiration.

>Waiting for the key material to become invalid upon expiration and deleting it manually have the same effect.

Delete the key material by running the following command:
```
 tccli DeleteImportedKeyMaterial --KeyId <keyid>
```

Sample source code of the `DeleteImportedKeyMaterial` function:
```
def delete_key_material(client, keyid):
    try:
        req = models.DeleteImportedKeyMaterialRequest()
        req.KeyId = keyid
        rsp = client.DeleteImportedKeyMaterial(req)
        return rsp, None
    except TencentCloudSDKException as err:
        return None, err
```

>
>- Once the key material is imported into an external CMK, the two will be associated permanently, i.e., other key materials cannot be imported into this CMK. In other words, after the key material is deleted, if you need to import key material into the CMK again, you need to make sure that the key material to be imported is exactly the same as the deleted one; otherwise, the import will fail.
>- If a CMK is used for data encryption, the encrypted data can only be decrypted with the CMK used for encryption (i.e., the CMK metadata and key material should match the imported key material); otherwise, decryption would fail. Please be cautious when deleting key materials and CMKs.

