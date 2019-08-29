KMS can be used by Tencent Cloud and non-Tencent Cloud resources for sensitive data encryption to meet security and compliance requirements and help resolve data encryption challenges in various industries.

## Protection of Sensitive Financial/Governmental Data
Challenge: All financial institutions and government agencies communications and data are highly confidential. The security and compliance of the encryption must be well executed.
Solution: KMS provides encryption, key protection, and permission management services through envelope encryption for important data such as various agreements, documents, and materials to meet security and compliance requirements.

## Protection of Configuration Information in Backend Service Development
Challenge: Configuration files for application development need to be encrypted to protect program data.
Solution: KMS can encrypt and protect the integrity of sensitive configuration information such as database connection information, database passwords, login keys, and backend service configurations.

## Protection of Enterprise Core Data
Challenge: Core private data such as intellectual properties, mobile numbers, ID numbers, and bank account numbers of end users, and passwords must be strictly protected. Although sensitive data can be stored after encryption, it is difficult to ensure the security of the data encryption keys.
Solution: KMS can encrypt all core data using data encryption keys in envelope encryption mode and then encrypt the keys too to provide another layer of security protection for the data.

## Website or Application Development Security
Challenge: If certificates and keys required for HTTPS services are stored in plaintext in the local file system, they can be easily obtained by hackers.
Solution: KMS can encrypt and decrypt keys. After encryption, the key files in ciphertext will be stored locally to be decrypted as needed. The key files will not be stored locally after decryption, making it impossible for hackers to obtain them, thereby ensuring the security of webpages and applications.

## Centralized Management of Password Policies
Challenge: A unified key management policy needs to be applied to decentralized business systems.
Solution: KMS can be called through APIs, SDKs, and Tencent Cloud products and services to achieve centralized key management for cloud-based and local application data.

