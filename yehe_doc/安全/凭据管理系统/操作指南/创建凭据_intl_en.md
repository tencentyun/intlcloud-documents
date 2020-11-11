## Overview
You can create a secret in the SSM Console. After the secret is successfully created, you can enable, disable, edit, delete the secret on schedule, and perform other operations on the secret.
## Directions
1. Log in to the [SSM Console](https://console.cloud.tencent.com/ssm) and click **Credential List** in the left sidebar.
2. In the upper left corner of the **Credential List** page, choose a region to create a secret in and then click **Create**.
3. Enter the configuration in the pop-up **Create Credential** page and then click **Confirm** to return to the **Credential List**. The newly created secret will be at the top of the credential list.
![](https://main.qcloudimg.com/raw/75d8c8228a9d20c54d2c343382d5260f.png)
**Field description:**
	- **Credential Name**: The length can be 1-128 bytes, containing letters, digits, hyphens (-), and underscores (_). It must start with a letter or digit.
	- **Credential Version**: required.
	- **Credential Content**: required.
	- **Description**: optional.
	- **Encryption Key**:
		- Use the default CMK that SSM has created in KMS.
		- Use a custom encryption key.

>?If you are using SSM, you have activated [KMS](https://intl.cloud.tencent.com/product/kms). You can create an encryption key in either of the following ways:
>- Use the default Tencent Cloud managed CMK created in the [KMS Console](https://console.cloud.tencent.com/kms2) as the encryption key, and use the envelope encryption method for encrypted storage.
>- Use a custom key created in the [KMS Console](https://console.cloud.tencent.com/kms2) as the encryption key for encrypted storage.
