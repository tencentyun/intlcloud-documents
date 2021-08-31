Tencent Cloud Key Management Service (KMS) is a security management solution that lets you to easily create and manage keys and protect their confidentiality, integrity, and availability, helping meet your key management and compliance needs in multi-application and multi-business scenarios.

KMS operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|-------------------|------|-------------------------------------|
| Decrypting with RSA asymmetric key        | kms  | AsymmetricRsaDecrypt                |
| Decrypting with SM2 asymmetric key        | kms  | AsymmetricSm2Decrypt                |
| Binding key to Tencent Cloud resource   | kms  | BindCloudResource                   |
| Canceling the scheduled deletion of CMK         | kms  | CancelKeyDeletion                   |
| Creating CMK             | kms  | CreateKey                           |
| Creating white-box key            | kms  | CreateWhiteBoxKey                   |
| Decrypting                | kms  | Decrypt                             |
| Deleting imported key material         | kms  | DeleteImportedKeyMaterial           |
| Deleting white-box key            | kms  | DeleteWhiteBoxKey                   |
| Getting CMK attribute           | kms  | DescribeKey                         |
| Getting attributes of multiple CMKs         | kms  | DescribeKeys                        |
| Getting white-box decryption key          | kms  | DescribeWhiteBoxDecryptKey          |
| Getting the device fingerprint list of specified key     | kms  | DescribeWhiteBoxDeviceFingerprints  |
| Getting the service status of white-box key        | kms  | DescribeWhiteBoxServiceStatus       |
| Disabling CMK             | kms  | DisableKey                          |
| Disabling key rotation            | kms  | DisableKeyRotation                  |
| Disabling CMKs in batches           | kms  | DisableKeys                         |
| Disabling white-box key            | kms  | DisableWhiteBoxKey                  |
| Disabling white-box keys in batches          | kms  | DisableWhiteBoxKeys                 |
| Enabling CMK             | kms  | EnableKey                           |
| Enabling key rotation            | kms  | EnableKeyRotation                   |
| Enabling CMKs in batches           | kms  | EnableKeys                          |
| Enabling white-box key            | kms  | EnableWhiteBoxKey                   |
| Enabling white-box keys in batches          | kms  | EnableWhiteBoxKeys                  |
| Encrypting                | kms  | Encrypt                             |
| Encrypting with white-box key        | kms  | EncryptByWhiteBox                   |
| Generating data key            | kms  | GenerateDataKey                     |
| Generating random number           | kms  | GenerateRandom                      |
| Getting CMK attribute           | kms  | GetKeyAttributes                    |
| Querying key rotation status          | kms  | GetKeyRotationStatus                |
| Getting the parameters of imported CMK material | kms  | GetParametersForImport              |
| Getting the public key of asymmetric key        | kms  | GetPublicKey                        |
| Getting the region where the service is available         | kms  | GetRegions                          |
| Querying service status            | kms  | GetServiceStatus                    |
| Importing key material            | kms  | ImportKeyMaterial                   |
| Listing encryption methods supported in the current region | kms  | ListAlgorithms                      |
| Getting CMK list           | kms  | ListKey                             |
| Getting CMK list details         | kms  | ListKeyDetail                       |
| Getting CMK list           | kms  | ListKeys                            |
| Overwriting the device fingerprint information of specified key     | kms  | OverwriteWhiteBoxDeviceFingerprints |
| Refreshing ciphertext              | kms  | ReEncrypt                           |
| Scheduling CMK deletion           | kms  | ScheduleKeyDeletion                 |
| Modifying CMK attribute           | kms  | SetKeyAttributes                    |
| Unbinding CMK from Tencent Cloud resource    | kms  | UnbindCloudResource                 |
| Modifying alias              | kms  | UpdateAlias                         |
| Modifying CMK description         | kms  | UpdateKeyDescription                |
