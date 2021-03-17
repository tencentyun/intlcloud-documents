In sensitive information transmission, the information sender can provide the identity certification through asymmetric signature verification. The operation process is as follows:
1. Create a pair of asymmetric keys in the KMS console. For more information, please see [CreateKey](https://intl.cloud.tencent.com/document/product/1030/32199).
2. The information sender uses the created private key to generate a signature for the data to be transmitted. For more information, please see [SignByAsymmetricKey](https://intl.cloud.tencent.com/document/product/1030/39509).
3. The information sender transmits the signature and data to the information recipient.
4. After receiving the signature and data, the information recipient verifies the signature by one of the two methods below:
	 ① Call the KMS signature verification API to verify the signature. For more information, please see [VerifyByAsymmetricKey](https://intl.cloud.tencent.com/document/product/1030/39508).
	 ② Download the KMS public asymmetric key, and then locally verify the signature using GmSSL, OpenSSL, password library, KMS SM-CRYPTO Encryption SDK, or any other tools.

>?Asymmetric signature verification currently supports SM2, RSA, and ECC algorithms.
