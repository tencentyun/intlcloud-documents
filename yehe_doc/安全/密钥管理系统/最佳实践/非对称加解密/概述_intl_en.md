Asymmetric encryption provides a pair of keys: a public key and a private key. Content encrypted with a public key cannot be decrypted with it but the corresponding private key. In data communication scenarios, asymmetric encryption is securer than symmetric encryption, and it is usually used between systems with different trust levels. For example, in scenarios where sensitive data in small size need to be transferred, you can consider using asymmetric keys for data encryption.

## Asymmetric Key Types

KMS supports the following types of asymmetric encryption algorithms: 
#### RSA
Currently, KMS supports RSA keys with a modulus of 2,048 bits (KeyUsage = ASYMMETRIC_DECRYPT_RSA_2048).

#### SM2
SM2 is a public-key algorithm that meets the standards issued by the State Cryptography Administration (SCA) of China. It is used to replace the RSA algorithm in China's commercial cryptography system. You can consider using this type of keys for applications with requirements for compliance with SCA standards (KeyUsage = ASYMMETRIC_DECRYPT_SM2).

## Typical Scenarios of Asymmetric Encryption

Asymmetric encryption is widely used in secret communication scenarios and has three major participants: information sender, information recipient, and transmission medium. The encryption process mainly includes the following steps:

1. The information recipient creates a public key-private key pair and sends the public key to one or multiple information senders.
2. The information sender uses the public key to encrypt the sensitive information and sends the encrypted ciphertext to the information recipient through a transmission medium.
3. After getting the data from the transmission medium, the information recipient uses the private key to decrypt the data and restore the original information.

Ciphertext can be decrypted only with a confidential private key, therefore, even if information leakage occurs due to low security of the transmission medium, those who get the ciphertext still cannot decrypt it, which ensures the security of sensitive information. This encrypted data transfer method is usually used in key exchange scenarios.

Because of the characteristics of use cases of the public key-private key pair, KMS does not support the automatic rotation of asymmetric CMKs. If you need to update the used keys regularly or from time to time, you can create new asymmetric keys.
