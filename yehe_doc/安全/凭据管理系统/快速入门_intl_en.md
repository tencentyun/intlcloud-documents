

You can use Secrets Manager (SSM) to centrally retrieve, manage, and store different types of secrets, including encrypted database credentials, API keys, other keys, and sensitive configuration. SSM enables you to effectively avoid plaintext leakage caused by hardcoding and business risks caused by out-of-control permissions.
### Step 1: Sign up
Sign up for a Tencent Cloud account and complete the identity verification. For more information, please see [Signing up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).
### Step 2: Purchase SSM
Go to the [SSM Purchase Page](https://buy.cloud.tencent.com/ssm), read and select the relevant billing description, and then click **Activate Now**.

### Step 3. Perform operations in the console
After SSM is activated, you can go to the console and use SDK or CLI to create, store, delete, and manage secrets through their lifecycle.

>!
>- SSM depends on KMS to store encrypted sensitive secrets. Therefore, before using SSM, ensure that [KMS](https://intl.cloud.tencent.com/product/kms) is activated.
>- To ensure that you can use SSM normally, please grant service role permissions of KMS to SSM. You can go to [CAM](https://console.cloud.tencent.com/cam/overview) to authorize SSM.
