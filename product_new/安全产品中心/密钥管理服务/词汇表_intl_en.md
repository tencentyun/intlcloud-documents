
### Encryption Context
Encryption context is a piece of data in JSON format. If you input this data when calling the API Encrypt, you must provide the same JSON data during decryption, otherwise the decryption may fail. You can regularly update the encryption context to improve business security or quickly block unauthorized access without disabling CMK.


### Data Encryption Key
Data encryption keys (DEK) are protected by CMK and used to encrypt business data. They can be customized or created via KMS API.

### Envelope Encryption
Envelope encryption is a high-performance encryption and decryption solution for massive amounts of data. It uses DEKs to encrypt and decrypt business data by means of high-performance symmetric encryption and ensures the secure use of the DEKs through KMS. It can ensure data security while providing high data read/write performance.


### Customer Master Key
Customer master keys (CMK) are master keys that Tencent Cloud keeps for you. They are protected by a third-party certified hardware security module (HSM) and used to encrypt and decrypt sensitive data used in your business such as passwords, certificates, and DEKs. They can be created and
managed in the console or through APIs.
There are two types of CMKs: Customer Managed CMKs and Tencent Cloud Managed CMKs.

### Customer Managed CMK
Customer managed CMKs are CMKs that you created in the console or through APIs. You can create, enable, disable, rotate, and manage permissions of your customer managed CMKs.

### Tencent Cloud Managed CMK
Tencent Cloud managed CMKs are CMKs that Tencent Cloud automatically created for you when a Tencent Cloud product (such as COS or TDSQL) calls the KMS service.
You can query and rotate Tencent Cloud managed CMKs but cannot disable or delete them.
