### What is the latest version of TencentDB for MongoDB?
Currently, TencentDB for MongoDB 3.2.10 and 3.6.3 are available.

### How do I apply for security credentials for TencentDB for MongoDB?
Before calling a TencentCloud API for the first time, you need to apply for security credentials in the Tencent Cloud CVM Console.
Security credentials comprise a `SecretId` and a `SecretKey`:
 - `SecretId` is used to identify the API caller.
 - `SecretKey` is used to encrypt the strings to create a signature so that Tencent Cloud server can validate the identity of the caller.

>API key is very important for creating TencentCloud API requests. With TencentCloud APIs, you can access and manage the resources in your Tencent Cloud account. For security reasons, store your keys safely and rotate them regularly (be sure to delete the old key when a new one is created). For more information, please see [Signature Algorithm](https://intl.cloud.tencent.com/document/product/240/8329).
 
### What are the restrictions on using the MongoDB username?
Tencent Cloud comes with two default users: `rwuser` and `mongouser`. The role for the built-in users is [readWriteAnyDatabase+dbAdmin](https://docs.mongodb.com/v3.0/reference/built-in-roles/), that is, with this role, you can read and write any database but are not permitted to perform critical operations.
Depending on the version of TencentDB for MongoDB, some instances only have `rwuser` (Tencent Cloud will upgrade such instances and contact you before doing so).
You can manage your accounts and permissions in the TencentDB for MongoDB Console to meet your business needs. For more information, please see [Use Limits](https://intl.cloud.tencent.com/document/product/240/31183).
 


