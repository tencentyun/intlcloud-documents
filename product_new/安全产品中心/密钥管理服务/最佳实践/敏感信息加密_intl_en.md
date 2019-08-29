## Overview
Sensitive information encryption is a core capability of KMS. It is a service mainly used to protect sensitive data (less than 4 KB) on server disks such as keys, certificates, and configuration files.
A CMK is used to encrypt sensitive data information instead of placing plaintext directly in the CVM instance. During decryption, the key is decrypted to the memory, ensuring that the plaintext does not get stored in the disk. In this way, even if the CVM instance is accessed by an unauthorized person due to negligence, the data information will not be leaked.

### Schematic Diagram
![](https://main.qcloudimg.com/raw/c83f3053bce1e98e0d6084847aa31bfd.png)


## Example of Sensitive Information

| | Key; Certificate | Backend configuration file |
|-|:-:|:-:|
| Usage | Encrypt business data, communication channels, and digital signatures | Store system architecture and other business information, such as database IP, password |
| Risk of data loss | Confidential information is stolen; encrypted tunnels are monitored; signatures are faked | Business data breached and used to attack other systems |

## Plan Ahead for Security
Sensitive information is the key to accessing company's confidential records and secure tunnels. Data security should be one of the critical factors taken into consideration from the start of the business development. One of the most basic protection step is to never **place unencrypted sensitive information** on CVM disks, but to encrypt it through key management service before storage. Then, you can decrypt the information to memory to **avoid writing plaintext to disk**.
The benefit of doing so is that even if the CVM was accessed by unidentified individuals due to personal negligence, sensitive plaintext information cannot be accessed directly. Attackers need to speculate the use of the ciphertext file, obtain the decryption access permission and write a decryption program after they obtain the ciphertext information, all of which greatly increases the difficulty of obtaining the plaintext information. The added complexity also makes it easier to detect attacks. 

## Why does Tencent Cloud not directly store your sensitive information?
An important measure to enhance security is separation of permissions. For example, separating the ownership of information and the encryption permission of information, the ownership belongs to you, and Tencent Cloud is responsible for encryption-related operations and permissions control. This is a simple but effective way to enhance security.

## Directions
### Protecting Backend Application Configuration Files

The steps are as follows:
1. Prerequisites
	- A CVM instance.
	- Deploy a backend service framework you are familiar with, such as Python, to the CVM instance.
	- A backend application configuration file used by your business, such as a file configured with a database IP and a password.
	- Create a KMS CMK for a specified region in the console or through TencentCloud API and keep it enabled.
2. Generate a configuration file in ciphertext
	Method 1: Generate it using the [online tool](https://intl.cloud.tencent.com/document/product/1030/31973).
	Method 2: Generate it using the KMS SDK.
	Place the generated configuration file in ciphertext in a location that your backend application can access.
3. Decrypt the file in the application and use it
Write code in your backend application, read the configuration file in ciphertext, and decrypt it with the KMS SDK for use. 

