### What is SSM?
Secrets Manager (SSM) is a management service that enables users to create, retrieve, update, and delete secrets through their lifecycle. You can use SSM together with resource-level role authorization and comprehensive audit control to centrally manage sensitive secrets easily.
### Why Tencent Cloud SSM?
SSM enables you to centrally retrieve, manage, encrypt, and store information such as database credentials, API keys, other keys, and sensitive configuration, avoiding plaintext leakage risks caused by hardcoding and business risks caused by out-of-control permissions.
### What is a secret?
A secret is the sensitive credential information (i.e., database credentials, account passwords, API keys, and SSH keys) used for identity verification of an application. You can use SSM to store various types of sensitive data, such as sensitive addresses and IP ports, as the secret content in the format of Name-Value pairs.
### Why should KMS be activated before activating SSM?
SSM uses the KMS-protected CMK as the encryption key, which can be the default CMK or the customized CMK, to centrally manage the keys of all types of applications. Therefore, you need to activate KMS before activating SSM.
### How do I connect my application to SSM?
Whether your application is in or outside Tencent Cloud, you can use the following two methods to connect it to SSM:
- Call SSM through the [SSM APIs or SDK].
- Use the [SSM console](https://console.cloud.tencent.com/ssm) to manage the lifecycle of secrets.
