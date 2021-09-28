## Scenarios
You can create a secret in the SSM console. After creation, you can manage the secret by enabling, disabling, editing, and scheduling deletion.
## Directions
1. Log in to the [SSM Console](https://console.cloud.tencent.com/ssm) and click **Custom Secret** on the left sidebar.
2. In the upper left corner, choose a region and click **Create** to create a secret.
3. Enter the configuration in the pop-up **Create Credential** window and then click **Confirm** to return to the **Credential List**. The newly created secret will be at the top of the credential list.
![](https://main.qcloudimg.com/raw/75d8c8228a9d20c54d2c343382d5260f.png)

**Field description:**
   - **Credential Name**: its length can be 1-128 bytes, containing letters, digits, hyphens (-), and underscores (_). It must start with a letter or digit.
   - **Credential Version**: required.
   - **Credential Content**: required.
   - **Description**: optional.
   - **Tag**: optional.
   - **Encryption Key**:
	- Use the default CMK that SSM has created in KMS.
	- Use a custom encryption key.

>?If you are using SSM, you have activated [KMS](https://intl.cloud.tencent.com/product/kms). You can create an encryption key in either of the following ways:
>- Use the default Tencent Cloud managed CMK created in the [KMS console](https://console.cloud.tencent.com/kms2) as the encryption key, and use the envelope encryption method for encrypted storage.
>- Use a custom key created in the [KMS console](https://console.cloud.tencent.com/kms2) as the encryption key for encrypted storage.
