

This document describes how to use the SM2 signature verification algorithm.
## Operation Directions

### Step 1: Creating an asymmetric signature key
>!To use the signature feature, the correct key purpose `KeyUsage= ASYMMETRIC_SIGN_VERIFY_SM2` is required when calling the KMS [CreateKey](https://intl.cloud.tencent.com/document/product/1030/32199) API to create a CMK.
>

Request:
```
tccli kms CreateKey --Alias test --KeyUsage ASYMMETRIC_SIGN_VERIFY_SM2
```
Returned result:
```
{
	"Response": {
		"KeyId": "22d79428-61d9-11ea-a3c8-525400******",
		"Alias": "test",
		"CreateTime": 1583739580,
		"Description": "",
		"KeyState": "Enabled",
		"KeyUsage": "ASYMMETRIC_SIGN_VERIFY_SM2",
		"TagCode": 0,
		"TagMsg": "",
		"RequestId": "0e3c62db-a408-406a-af27-dd5ced******"
	}
}
```

### Step 2: Downloading the public key

Request:
```
tccli kms GetPublicKey  --KeyId 22d79428-61d9-11ea-a3c8-525400******
```
Returned result:
```
{
	"Response": {
		"RequestId": "408fa858-cd6d-4011-b8a0-653805******",
		"KeyId": "22d79428-61d9-11ea-a3c8-525400******",
		"PublicKey":  "MFkwEwYHKoZIzj0CAQYIKoEcz1UBgi0DQgAEFLlge0vtct949CwtadHODzisgXJahujq+PvM***************bBs/f3axWbvgvHx8Jmqw==",
		"PublicKeyPem": "-----BEGIN PUBLIC KEY-----\nMFkwEwYHKoZIzj0CAQYIKoEcz1UBgi0DQgAEFLlge0vtct949CwtadHODzisgXJa\nhujq+PvM***************bBs/f3axWbvgvHx8Jmqw==\n-----END PUBLIC KEY-----\n"
	}
}
```
Convert the public key `PublicKeyPem` into the PEM format and save it in the file `public_key.pem`:
```
echo "-----BEGIN PUBLIC KEY-----
MFkwEwYHKoZIzj0CAQYIKoEcz1UBgi0DQgAEFLlge0vtct949CwtadHODzisgXJa
hujq+PvM***************bBs/f3axWbvgvHx8Jmqw==
-----END PUBLIC KEY-----" > public_key.pem
```

>?You can also log in to the [KMS console](https://console.cloud.tencent.com/kms2/index), click **Customer Managed CMK** on the left sidebar, click a key ID/name in the key list to view the key information, and download the public asymmetric key.

### Step 3: Creating the plaintext file

Create the testing plaintext file:
```
echo "test" > test_verify.txt
```
>! If there are any invisible characters such as line breaks in the generated content, you need to truncate the file (**truncate -s -1 test_verify.txt**) to provide a correct signature.

### Step 4: Calculating the message abstract

- If the message to be generated a signature for is not longer than 4,096 bytes, you can skip this step to [Step 5](#step5).
- If the message to be generated a signature for is longer than 4,096 bytes, you need to calculate a message abstract locally first.
Use GmSSL to calculate the message abstract for `test_verity.txt`:
```
gmssl sm2utl -dgst -in ./test_verify.txt -pubin -inkey ./public_key.pem -id 1234567812345678 > digest.bin
```

<span id="test5"></span>
### Step 5: Calling the KMS signature API to generate a signature

Call the KMS [SignByAsymmetricKey](https://intl.cloud.tencent.com/document/product/1030/39509) API to calculate the signature.
1. Base64-encode the original message or message abstract before signature calculation.
```
// Base64-encode the message abstract
gmssl enc -e -base64 -A -in digest.bin -out encoded.base64
// Base64-encode the original message
gmssl enc -e -base64 -A -in test_verify.txt -out encoded.base64
```
2. Calculate the signature.
Request:
	```
	// Generate the signature for the message abstract using the content of the file `encoded.base64` as the `Message` parameter of `SignByAsymmetricKey`.
	tccli kms SignByAsymmetricKey --KeyId 22d79428-61d9-11ea-a3c8-525400****** --Algorithm SM2DSA --Message "qJQj83hSyOuU7Tn0SRReGCk4yuuVWaeZ44BP******==" --MessageType DIGEST

	// Generate the signature for the Base64-encoded original message
	tccli kms SignByAsymmetricKey --KeyId 22d79428-61d9-11ea-a3c8-525400****** --Algorithm SM2DSA --Message "dG***Ao=" --MessageType RAW
	```
	Returned result:
	```
	{
			"Response": {
				"Signature": "U7Tn0SRReGCk4yuuVWaeZ4******",
				"RequestId": "408fa858-cd6d-4011-b8a0-653805******"
			}
	}
	```
	Save the signature content `Signature` in the file `signContent.sign`:
	```
	echo "U7Tn0SRReGCk4yuuVWaeZ4******" | base64 -d > signContent.bin
	```


### Step 6: Verifying the signature

- Call the KMS signature verification API to verify the signature (**recommended**).
	Request:
	```
// Verify the Base64-encoded original message
tccli kms VerifyByAsymmetricKey --KeyId 22d79428-61d9-11ea-a3c8-525400****** --SignatureValue "U7Tn0SRReGCk4yuuVWaeZ4******" --Message "dG***Ao=" --Algorithm SM2DSA --MessageType RAW
// Verify the message abstract (verify the signature for the message abstract using the content of the file `encoded.base64` mentioned in step 4 as the `Message` parameter of `VerifyByAsymmetricKey`).
tccli kms VerifyByAsymmetricKey --KeyId 22d79428-61d9-11ea-a3c8-525400****** --SignatureValue "U7Tn0SRReGCk4yuuVWaeZ4******" --Message "QUuAcNFr1Jl5+3GDbCxU7te7Uekq+oTxZ**********=" --Algorithm SM2DSA --MessageType DIGEST
	```
	>?The value of the parameter `Message` and `MessageType` used in the signature API call should be the same as those of the signature verification API call.
	>
	Returned result:
	```
{
		"Response": {
			  "SignatureValid": true,
			  "RequestId": "6758cbf5-5e21-4c37-a2cf-8d47f5******"
		}
}
	```
- Verify the signature locally using the KMS public key and signature content.
	Request:
	```
	gmssl  sm2utl -verify -in ./test_verify.txt -sigfile ./signContent.bin -pubin -inkey ./public_key.pem -id 1234567812345678
	```
	Returned result:
	```
	Signature Verification Successful
	```
