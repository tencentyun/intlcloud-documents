A **public key** and a **private key** are required for asymmetric encryption and decryption. These two are a pair of bidirectional keys in cryptography, that is the public key and private key both can be used for encryption. If one is used for encryption, the decryption can only be performed using another key. The public key can be disclosed to anyone even an unreliable party, but the private key must be kept confidential.

Comparing to symmetric encryption, asymmetric encryption does not require a reliable channel for key distribution, so that it is usually applied in communications between systems with different trust levels for encrypted transfer of sensitive data and digital signature verification. 

## Asymmetric Key Types

Tencent Cloud KMS currently supports the two asymmetric key algorithms below:

### RSA

Currently, KMS supports RSA keys with a modulus of 2,048 bits (KeyUsage = ASYMMETRIC_DECRYPT_RSA_2048).

### SM2

SM2 is a public-key algorithm that meets the standards issued by the State Cryptography Administration (SCA) of China. It is used to replace the RSA algorithm in China's commercial cryptography system. You can consider using this type of keys for applications with requirements for compliance with SCA standards (KeyUsage = ASYMMETRIC_DECRYPT_SM2).

>? Asymmetric signature verification currently only supports SM2 algorithm.

## Typical Scenarios of Asymmetric Encryption

There are two typical scenarios of asymmetric encryption and decryption in actual use cases, namely the **encrypted communication** and **digital signature**.

### Encrypted communication

Encrypted communication is a typical application of asymmetric encryption algorithm, of which the process is similar to symmetric encryption with the difference being that the public key is required for encryption and the private key is required for decryption.

How the encrypted communication works:
1. The information recipient creates a public key-private key pair and sends the public key to one or multiple information senders.
2. The information sender uses the public key to encrypt the sensitive information and sends the encrypted ciphertext to the information recipient through a transmission medium.
3. After getting the data from the transmission medium, the information recipient uses the private key to decrypt the data and restore the original information.

Ciphertext can be decrypted only with a confidential private key, therefore, even if information leakage occurs due to low security of the transmission medium, those who get the ciphertext still cannot decrypt it, which ensures the security of sensitive information.

Tencent Cloud KMS offers solutions for encrypted communication. For more information, please see [Asymmetric Data Encryption and Decryption](https://intl.cloud.tencent.com/document/product/1030/39478).

### Digital signature

Digital signature is another typical application of asymmetric encryption algorithm, which consists of signature generation and signature verification two processes. The private key is used for signature generation and the public key is used for signature verification, however, the implementation process of encrypted communication is in contrast.

How the digital signature works:
1. The information sender creates a public key-private key pair and sends the public key to one or multiple information recipients.
2. The information sender uses the Hash function to generate a message abstract from the original message, and then uses its private key to encrypt the abstract to get the digital signature of the original message. 
3. The information sender transmits the original message and digital signature to the information recipient.
4. After receiving the original message and digital signature, the information recipient uses the same Hash function to generate the abstract A from the original message and uses the public key given by the information sender to decrypt the digital signature to get the abstract B, and then compares the two abstracts to check whether they are identical and the original data is tampered. 

The signature is unique as it is generated and encrypted with a confidential private key. Digital signatures can guarantee confidential data transmission, the correctness of information senders, and the non-repudiation of transactions.

Tencent Cloud KMS offers solutions for digital signatures. For more information, please see Asymmetric Signature Verification.

>! Because of the characteristics of use cases of the public key-private key pair, KMS does not support the automatic rotation of asymmetric CMKs. If you need to update the used keys regularly or from time to time, you can create new asymmetric keys.
