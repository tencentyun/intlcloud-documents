## Operation Process

If you need to encrypt sensitive information before transferring it (in scenarios such as key exchange), you can use the asymmetric key-based encryption and decryption scheme. As an information recipient, you need to perform the following operations:

1. Create an asymmetric encryption key on KMS. For more information, please see [CreateKey](https://intl.cloud.tencent.com/document/product/1030/32199).
2. Get the public key on KMS. For more information, please see [GetPublicKey](https://intl.cloud.tencent.com/document/product/1030/35179).
3. The information recipient distributes the public key to the information sender.
4. The information sender uses the obtained public key to encrypt the sensitive data locally and sends the ciphertext to the information recipient.
5. The information recipient calls the KMS decryption API to decrypt the ciphertext. For more information on the API, please see [AsymmetricSm2Decrypt](https://intl.cloud.tencent.com/document/product/1030/35180) and [AsymmetricRsaDecrypt](https://intl.cloud.tencent.com/document/product/1030/35181). For operations using TCCLI, please see [Asymmetric key decryption](https://intl.cloud.tencent.com/document/product/1030/35539).

Ciphertext is transferred throughout the entire sensitive data transfer process, and the only key that can decrypt the ciphertext is managed and protected by KMS, which cannot be obtained by other people including Tencent Cloud. This scheme greatly improves the security of encrypted sensitive data transfer.

## Operation Directions

### RSA sample

1. Create an asymmetric encryption key
Request:
```
tccli kms CreateKey --Alias test --KeyUsage ASYMMETRIC_DECRYPT_RSA_2048
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
		"KeyUsage": "ASYMMETRIC_DECRYPT_RSA_2048",
		"RequestId": "0e3c62db-a408-406a-af27-dd5ced******"
	}
}
```
2. 	Download the public key
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
        "PublicKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzQk7x7ladgVFEEGYDbeUc5aO9TfiDplIO4WovBOVpIFoDS31n46YiCGiqj67qmYslZ2KMGCd3Nt+a+jdzwFiTx3O87wdKWcF2vHL9Ja+95VuCmKYeK1uhPyqqj4t9Ch/cyvxb0xaLBzztTQ9dXCxDhwj08b24T+/FYB9a4icuqQypCvjY1X9j8ivAsPEdHZoc9Di7JXBTZdVeZC1igCVgl6mwzdHTJCRydE2976zyjC7l6QsRT6pRsMF3696N07WnaKgGv3K/Zr/6RbxebLqtmNypNERIR7jTCt9L+fgYOX7anmuF5v7z0GfFsen9Tqb1LsZuQR0vgqCauOj************",
        "PublicKeyPem": "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzQk7x7ladgVFEEGYDbeU\nc5aO9TfiDplIO4WovBOVpIFoDS31n46YiCGiqj67qmYslZ2KMGCd3Nt+a+jdzwFi\nTx3O87wdKWcF2vHL9Ja+95VuCmKYeK1uhPyqqj4t9Ch/cyvxb0xaLBzztTQ9dXCx\nDhwj08b24T+/FYB9a4icuqQypCvjY1X9j8ivAsPEdHZoc9Di7JXBTZdVeZC1igCV\ngl6mwzdHTJCRydE2976zyjC7l6QsRT6pRsMF3696N07WnaKgGv3K/Zr/6RbxebLq\ntmNypNERIR7jTCt9L+fgYOX7anmuF5v7z0GfFsen9Tqb1LsZuQR0************\n1QIDAQAB\n-----END PUBLIC KEY-----\n"
    }
}
```
3. 	Use the public key for encryption
   ① Store the public key `PublicKey` in the file `public_key.base64` and Base64-decode it.
      Store it in the file:
```
echo "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzQk7x7ladgVFEEGYDbeUc5aO9TfiDplIO4WovBOVpIFoDS31n46YiCGiqj67qmYslZ2KMGCd3Nt+a+jdzwFiTx3O87wdKWcF2vHL9Ja+95VuCmKYeK1uhPyqqj4t9Ch/cyvxb0xaLBzztTQ9dXCxDhwj08b24T+/FYB9a4icuqQypCvjY1X9j8ivAsPEdHZoc9Di7JXBTZdVeZC1igCVgl6mwzdHTJCRydE2976zyjC7l6QsRT6pRsMF3696N07WnaKgGv3K/Zr/6RbxebLqtmNypNERIR7jTCt9L+fgYOX7anmuF5v7z0GfFsen9Tqb1LsZuQR0vgqCauOj************" > public_key.base64
```
Base64-decode the public key to get its content:
```
openssl enc -d -base64 -A -in public_key.base64 -out public_key.bin
```
	② Create a testing plaintext file:
```
	echo "test" > test_rsa.txt
```
	③ Use OpenSSL to encrypt the file `test_rsa.txt` with the public key.
```
	openssl pkeyutl -in test_rsa.txt -out encrypted.bin -inkey public_key.bin -keyform DER -pubin -encrypt -pkeyopt rsa_padding_mode:oaep -pkeyopt rsa_oaep_md:sha256
```
	④ Base64-encode the data encrypted with the public key for transmission.
```
	openssl enc -e -base64 -A -in encrypted.bin -out encrypted.base64
```
⑤ Use the private key on KMS for decryption.
   Use the above-mentioned Base64-encoded ciphertext `encrypted.base64` as the `Ciphertext` parameter for `AsymmetricRsaDecrypt` to decrypt the ciphertext with the private key.
   Request:
```
tccli kms AsymmetricRsaDecrypt --KeyId 22d79428-61d9-11ea-a3c8-525400****** --Algorithm RSAES_OAEP_SHA_256 --Ciphertext "DEb/JBmuhVkYS34r0pR7Gv1WTc4khkxqf7S1WIr7/GXsAs/tfP/v/2+1SwsIG7BqW7kUZqr38/FGkaIEqYeewot37t3+Jx0t5w7/yXkUnyUfyfPpXlHXf94g3wFOjijEWWsjWWzaXTkTr8uWOfRBenq+bcaY783FIy03XjJW/Y0wKWjD3tULvKndCJO/3bkb65kn1Fbsfm20xrUUwqV/p2DVLXBdG1ymr0DjsbG7R0tb3ytc2LmH33YPAQE32eP27ciKzSml+w2tdUM3dw3nEZcTGMs1wFDGk0O1WB052jZ7TitUD9zCftFv2dKlZD3LRx1+vHqpNVgPhLmL******=="
```
Returned result:
```
{
    "Response": {
        "RequestId": "6758cbf5-5e21-4c37-a2cf-8d47f5******",
        "KeyId": "22d79428-61d9-11ea-a3c8-525400******",
        "Plaintext": "dGVzdAo="
    }
}
```

>? The process of using SM2 asymmetric keys for encryption and decryption is similar to this example. For more information on the private key-based decryption API, please see [AsymmetricSm2Decrypt](https://intl.cloud.tencent.com/document/product/1030/35180).


