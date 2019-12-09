A customer master key (CMK) is a basic element of the KMS service. The CMK contains key ID, key metadata (alias, description, status, etc.), and key material used to encrypt/decrypt data.

By default, the underlying encryptor of KMS creates secure key material for a CMK when the CMK is created in KMS. If you want to use your own key material, i.e., implementing a Bring Your Own Key (BYOK) solution, you can use KMS to generate a CMK with the key material left empty, and then import your own key material into the CMK to form an external CMK. The external CMK can be distributed and managed by KMS.



## Features
- KMS allows you to use your own key to encrypt/decrypt sensitive data by implementing a Bring Your Own Key (BYOK) solution in Tencent Cloud.
- KMS gives you full control over the key services used in Tencent Cloud, including importing and deleting key material as needed.
- You can back up your key material in local key management infrastructure as an additional disaster recovery measure for KMS.
- You can use your own key material for encryption/decryption operations in the cloud to meet your industry-specific compliance requirements.

## Precautions
- You need to ensure the security of the key material:
 - When using the key importing feature, you need to ensure that the random material generation source is secure and reliable. Currently, the SM-CRYPTO edition of KMS only supports importing 128-bit symmetric keys, while the FIPS-compliant edition only supports importing 256-bit symmetric keys.
- You need to ensure the availability of the key material:
 - KMS provides high availability of its own services and the capability for restoring from backups, but the availability of your key material is your responsibility. It is strongly recommended that you keep the original backup of the key material in a safe and reliable way, so that if the key material is deleted accidentally or expired, the backup can be imported into KMS timely.
- You need to ensure the correctness of the key importing operations:
 - Once the key material is imported into an external CMK, the two will be associated permanently, i.e., other key materials cannot be imported into this CMK. If this CMK is used for data encryption, the encrypted data can only be decrypted with the CMK used for encryption (i.e., the CMK metadata and key material should match the imported key material); otherwise, decryption would fail. Please be cautious about deleting key materials and CMKs.
