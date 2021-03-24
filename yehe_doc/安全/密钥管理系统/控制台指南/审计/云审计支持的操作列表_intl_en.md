Tencent Cloud [CloudAudit](https://intl.cloud.tencent.com/document/product/1021) logs KMS operation events. The operations that can be logged by CloudAudit are as follows:

| Operation Name                      | Event Name                           |
| ------------------------------- | ----------------------------------- |
| Creating a CMK                    | CreateKey                           |
| Getting the attributes of a CMK                  | DescribeKey                         |
| Getting the attributes of multiple CMKs              | DescribeKeys                        |
| Getting the CMK list                  | ListKey                             |
| Getting the CMK list details              | ListKeyDetail                       |
| Modifying the CMK description              | UpdateKeyDescription                |
| Modifying an alias                        | UpdateAlias                         |
| Enabling a CMK                      | EnableKey                           |
| Disabling a CMK                      | DisableKey                          |
| Batch enabling CMKs                  | EnableKeys                          |
| Batch disabling CMKs                  | DisableKeys                         |
| Setting schedule deletion for a CMK                 | ScheduleKeyDeletion                 |
| Canceling schedule deletion for a CMK              | CancelKeyDeletion                   |
| Getting the parameters of the CMK materials to be imported | GetParametersForImport              |
| Importing key materials                    | ImportKeyMaterial                   |
| Creating a white-box key                    | CreateWhiteBoxKey                   |
| Encrypting data with a white-box key         | EncryptByWhiteBox                   |
| Enabling a white-box key                    | EnableWhiteBoxKey                   |
| Disabling a white-box key                    | DisableWhiteBoxKey                  |
| Batch enabling white-box keys                | EnableWhiteBoxKeys                  |
| Batch disabling white-box keys                 | DisableWhiteBoxKeys                 |
| Deleting a white-box key                     | DeleteWhiteBoxKey                   |
| Getting the white-box key service status            | DescribeWhiteBoxServiceStatus       |
| Overwriting the device fingerprint of a specified key      | OverwriteWhiteBoxDeviceFingerprints |
| Getting the device fingerprint list of a specified key      | DescribeWhiteBoxDeviceFingerprints  |
| Getting a white-box decryption key                | DescribeWhiteBoxDecryptKey          |
| Decrypting data                            | Decrypt                             |
| Encrypting data                            | Encrypt                             |
| Generating a signature                            | SignByAsymmetricKey                 |
| Verifying a signature                        | VerifyByAsymmetricKey               |
| Archiving a key                        | ArchiveKey                          |
| Canceling archive                    | CancelKeyArchive                    |
| Getting the service AZs              | GetRegions                          |
| Refreshing the ciphertext                        | ReEncrypt                           |
| Generating a random number                  | GenerateRandom                      |
| Generating a DEK                    | GenerateDataKey                     |
| Querying service status                    | GetServiceStatus                    |
| Listing the encryption methods supported in the current region    | ListAlgorithms                      |
| Disabling key rotation                    | DisableKeyRotation                  |
| Enabling key rotation                    | EnableKeyRotation                   |
| Querying key rotation status                | GetKeyRotationStatus                |
| Binding a CMK with a Tencent Cloud service  | BindCloudResource                 |
| Unbinding a CMK from a Tencent Cloud service       | UnbindCloudResource                 |
| Getting the public key of a pair of asymmetric keys            | GetPublicKey                        |
| Using SM2 to decrypt data with asymmetric keys               | AsymmetricSm2Decrypt                |
| Using RSA to decrypt data with asymmetric keys               | AsymmetricRsaDecrypt                |
