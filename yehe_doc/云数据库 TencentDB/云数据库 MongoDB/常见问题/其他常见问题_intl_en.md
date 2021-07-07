### What is the latest version of TencentDB for MongoDB?
Currently, TencentDB for MongoDB 3.2, 3.6, and 4.0 are available.

### How do I delete a TencentDB for MongoDB instance? Will it be deleted automatically if I don't renew it after it expires?
A TencentDB for MongoDB instance will be automatically terminated if it is not renewed after expiration. Please confirm and back up your data promptly. You can also manually terminate it by selecting **More** > **Return and Refund**/**Terminate** in its **Operation** column in the instance list in the [console](https://console.cloud.tencent.com/mongodb).

### How do I apply for security credentials for TencentDB for MongoDB?
Before calling a TencentCloud API for the first time, you need to apply for security credentials in the Tencent Cloud [console](https://console.cloud.tencent.com/cam/capi).
Security credentials comprise a `SecretId` and a `SecretKey`:
 - `SecretId` is used to identify the API caller.
 - `SecretKey` is used to encrypt the strings to create a signature so that Tencent Cloud server can validate the identity of the caller.

>!API key is very important for creating TencentCloud API requests. With TencentCloud APIs, you can access and manage the resources in your Tencent Cloud account. For security reasons, store your keys safely and rotate them regularly (be sure to delete the old key when a new one is created). For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/240/32137).

### What are the restrictions on using the MongoDB username?
TencentDB for MongoDB comes with a default user `mongouser`. It supports the SCRAM-SHA-1 authentication mechanism, and its role is [readWriteAnyDatabase+dbAdmin](https://docs.mongodb.org/v3.0/reference/built-in-roles/). You can use it to read and write any database, but you are not permitted to perform high-risk operations.

TencentDB for MongoDB v3.2 supports another default user `rwuser`. It uses the MONGODB-CR authentication mechanism which, however, is no longer supported by MongoDB. We recommend you use the `mongouser` to connect to your instance.

You can also manage your account and permissions as needed in the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
