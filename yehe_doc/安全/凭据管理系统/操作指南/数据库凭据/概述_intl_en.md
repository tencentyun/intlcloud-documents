There are security challenges your account may face, such as improper use of management permission, your password unchanged for a long time, and key information in plaintext, leading to a loss of digital assets. Given these risks, **database credentials** will be periodically rotated to create strong passwords and manage sensitive configuration information, securing your data while reducing security risks and threats to your account.

## Key Features
- SSM allows the application and distribution of database accounts on the console.
- Combing with Tencent Cloud [KMS](https://intl.cloud.tencent.com/product/kms), SSM can secure your sensitive information by encryption.
- SSM can automatically create a strong password for periodic rotation.
- SSM enables you to set a period of time that automatic rotation repeats.

## Product Architecture
![](https://main.qcloudimg.com/raw/93b5e7074a63ca3a9f818254f6994a88.png)

#### Process Description
1. Create a database instance and set its account and password as an admin.
2. Create a database credential object on SSM as an admin.
 - Grant SSM permissions to access MySQL management services.
 - Set the database credential’s username prefix.
 - Configure the automatic rotation policy.
3. When the application system needs to access the database, it can request access to the credential via the GetSecretValue API. For details, see [GetSecretValue](https://intl.cloud.tencent.com/document/product/1078/38649).
4. The application system parses the plaintext credential based on the content returned by the API, and obtains its account and password, thereby accessing the target database.

## Usage Limits

Automatic rotation is only available on **TencentDB for MySQL** and **TDSQL for MySQL**.

## Usage Guide
- [Creating a Database Credential](https://intl.cloud.tencent.com/document/product/1078/41801)
- [Editing a Database Credential](https://intl.cloud.tencent.com/document/product/1078/41802)
- [Deleting a Database Credential](https://intl.cloud.tencent.com/document/product/1078/41804)
- [Access Control](https://intl.cloud.tencent.com/document/product/1078/38610)
