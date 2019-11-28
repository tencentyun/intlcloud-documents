Key Management Service (KMS) provides the capabilities for secure and compliant full-lifecycle key management, data encryption, and data decryption.

The core key components involved in KMS include customer master key (CMK) and data encryption key (DEK). A CMK is a first-level key used to encrypt and decrypt sensitive data and generate DEKs. A DEK is a second-level key used in the envelope encryption process. It is protected by a CMK, and used to encrypt business data.

For scenarios where CMKs and DEKs are used for business data encryption and decryption, please see [Sensitive Data Encryption](https://intl.cloud.tencent.com/document/product/1030/31975) and [Envelope Encryption Best Practice](https://intl.cloud.tencent.com/document/product/1030/31976).


## Key Overview
#### Customer master key (CMK)
A CMK, as a core resource in KMS, is protected by a third-party certified hardware security module (HSM) and used as a first-level key for encryption and decryption. KMS is mainly a management service for CMKs.

A CMK is a logical representation of a master key, and it contains metadata such as key ID, creation date, description, and key status. Generally, you can use the automatic CMK generation feature in KMS or import your own key to generate a CMK.


There are two types of CMKs: Customer Managed CMK and Tencent Cloud Managed CMK.
- A **Customer Managed CMK** is a CMK that you create in the console or through APIs. You can create, enable, disable, rotate keys and manage permissions of your user keys.
- A **Tencent Cloud Managed CMK** is a CMK that is automatically created for you when a Tencent Cloud product/service (such as CBS, COS, or TDSQL) calls the KMS service. You can query and rotate Tencent Cloud managed CMKs, but cannot disable them or set the schedule deletion for them.


#### Data encryption key (DEK)
A DEK is a second-level key generated based on a CMK, used for encrypting and decrypting local data.
KMS allows you to use your CMKs to generate DEKs, but KMS will not store, manage, or track them or use them to perform encryption operations. You have to use and manage your DEKs outside of KMS.

Generally, DEKs are used in envelop encryption to encrypt local business data. They are protected by CMKs and customizable. DEKs can be created through the [GenerateDataKey](https://intl.cloud.tencent.com/document/product/1030/32188) API.




## Operation Overview
| Operation | Description |
| ---------------- | ---------------------------------- |
| [Creating key](https://intl.cloud.tencent.com/document/product/1030/31971) | Creates a key quickly in the console. |
| [Viewing key](https://intl.cloud.tencent.com/document/product/1030/32776) | Views the ID and details of a key in the console. |
| [Editing key](https://intl.cloud.tencent.com/document/product/1030/32777) | Edits the name, description, and other information of a key in the console. |
| [Enabling and disabling key](https://intl.cloud.tencent.com/document/product/1030/32778)  | Enables and disables a key in the console. |
| [Rotating key](https://intl.cloud.tencent.com/document/product/1030/32779) | Enables key rotation in the console. |
| [Encryption and decryption](https://intl.cloud.tencent.com/document/product/1030/31973)   | Uses keys to encrypt and decrypt data in the console. |
| [Deleting key](https://intl.cloud.tencent.com/document/product/1030/32780) | Deletes a key quickly in the console. |
| [Access control](https://intl.cloud.tencent.com/document/product/1030/31978) | Sets KMS permissions for a sub-account. |
