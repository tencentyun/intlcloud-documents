This document describes how to activate Key Management Service (KMS) in Secrets Manager (SSM) and authorize SSM. It also guides you on how to use KMS to encrypt secrets in SSM.
## Background
Secret management is important for the OPS security of an enterprise IT system. You can use SSM to host secrets of all types, including access keys, API keys, private keys, account passwords, and much more. SSM uses keys hosted in Tencent Cloud KMS to encrypt and protect secrets, ensuring secret security on the server. With a more secure and convenient SSM, you no longer need to build and maintain infrastructure for secret management.
>!When SSM uses KMS hosted keys for encryption, KMS fees might be incurred. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/1078/38595).

## Directions

### Step 1: Activate KMS and authorize SSM
- SSM uses KMS to store encrypted sensitive secrets. Therefore, before using SSM, ensure that [KMS](https://intl.cloud.tencent.com/product/kms) is activated.
- To ensure that you can use SSM normally, please grant service role permissions to SSM in KMS. You can go to [CAM](https://console.cloud.tencent.com/cam/role/grant?roleName=SSM_QCSRole&policyName=QcloudAccessForSSMRole&principal=eyJzZXJ2aWNlIjoic3NtLnFjbG91ZC5jb20ifQ%3D%3D&serviceType=ssm&s_url=https://console.cloud.tencent.com/ssm) to authorize SSM.

To activate KMS and authorize SSM, you can perform the following steps:
1. Log in to the [SSM console](https://console.cloud.tencent.com/kms2) and click [CAM](https://console.cloud.tencent.com/cam/role/grant?roleName=SSM_QCSRole&policyName=QcloudAccessForSSMRole&principal=eyJzZXJ2aWNlIjoic3NtLnFjbG91ZC5jb20ifQ%3D%3D&serviceType=ssm&s_url=https://console.cloud.tencent.com/ssm) in the instructions at the top of the page.
![](https://main.qcloudimg.com/raw/020c50b0e3adfd536f59d04c60789d9e.png)
2. On the **Service Authorization** page, click **Grant**.
![](https://main.qcloudimg.com/raw/f88e4f4759480bb21e51662cc5a7fe80.png)
3. After service role authorization, click [KMS](https://buy.cloud.tencent.com/kms) in the instructions at the top of the page.
![](https://main.qcloudimg.com/raw/dda6eb82ea6e9afe884f3738eac93beb.png)
4. On the KMS activation page, click **Activate Now**.

### Step 2: Select a key for secret encryption
As the core resources of KMS, CMKs are protected by hardware security modules certified by third parties. CMK contains metadata information such as key ID, creation date, description, and key status.
When using SSM to [create secrets](https://intl.cloud.tencent.com/document/product/1078/38601), you will be provided with two types of encryption keys. Select a type as needed.
- After KMS is activated, KMS will create a Tencent Cloud managed CMK for SSM by default. The default key cannot be deleted or disabled. You can use the default key as the encryption key.
![](https://main.qcloudimg.com/raw/1f7b701aff87cae221188b01e12d5d03.png)
- You can also go to the [KMS console](https://console.cloud.tencent.com/kms2) to create a key on your own and define the key policies and usage. KMS enables users to choose keys as needed. You can either **create keys in KMS** or **import external keys** (BYOK). For more information, please see [Creating Keys](https://intl.cloud.tencent.com/document/product/1030/31971) and [Importing External Keys](https://intl.cloud.tencent.com/document/product/1030/32795) for KMS. 
![](https://main.qcloudimg.com/raw/9c0650e85a3829e323add4e2f084329e.png)


