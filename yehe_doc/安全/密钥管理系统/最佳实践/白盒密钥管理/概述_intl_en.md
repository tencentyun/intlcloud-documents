
Tencent Cloud KMS provides a white-box key management solution. White-box encryption is an encryption technology that can resist white-box attacks. Specifically, even after an attacker gains full control of the encryption device terminal, can observe and change the internal data of the program runtime, and can perform reverse analysis of the cryptographic operation process, white-box encryption can still effectively protect the security of encrypted data and keys. Compared with traditional encryption technologies, this technology makes it more difficult to extract keys even in the white-box environment, guaranteeing the security of sensitive key information and encrypted data.

The white-box key is used to protect the sensitive root key information on the end, such as `API SecretKey`, authentication keys or tokens used by internal systems, and other local sensitive root key information, helping implement end-to-end full-linkage data security solutions. The white-box key management solution integrates keys and algorithms, and effectively hides keys by using randomized factors, which greatly increases the difficulty of sniffing and cracking keys, thereby protecting keys as extremely sensitive information.



## Features
#### High security

Based on high-strength obfuscation and reinforcement algorithms and multi-layer security protection technologies, KMS white-box encryption guarantees the security of keys used for cryptographic operations on untrusted devices.

#### Dynamic white box
An original key can be converted to a white-box key through the same white-box encryption technology, which enables dynamic key rotation without changing the white-box library required.

#### Algorithm support
KMS white-box encryption supports the globally popular algorithm AES and mainstream Chinese algorithm SM4 to meet the encryption compliance needs in different scenarios.

#### Multi-platform support
It is suitable for various platforms such as Windows and Linux.



## Usage
The white-box key management service is currently in beta test. To try it out, please submit an application. After your application is approved, the Tencent Cloud KMS product team will confirm your needs and conduct business negotiation with you. 
For more information on this product, please [contact us](https://intl.cloud.tencent.com/support).
