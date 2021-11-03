## Scenarios
This document describes how to create an SSH key pair and encrypt the SSH private key on the [SSM console](https://console.cloud.tencent.com/ssm).
> ! You should meet the following requirements to use **CVM SSH Key**.
- You have [enabled KMS services](https://buy.cloud.tencent.com/kms), as SSM encrypts data based on keys managed in KMS.
- You have created a CVM instance. For details, see [Guidelines for Creating Instances](https://intl.cloud.tencent.com/document/product/213/36302).

## Directions
1. Log in to the [SSM Console](https://console.cloud.tencent.com/ssm) and click **CVM SSH Key** on the left sidebar.
   ![](https://qcloudimg.tencent-cloud.cn/raw/8fbd29fd45d563503b3f68dd9ef94336.png)
2. On the **CVM SSH Key** page, click the drop-down list in the top left corner to select a region.
   ![](https://qcloudimg.tencent-cloud.cn/raw/8c0901b331cf756f3519dd89701bd57b.png)
3. Click **Create** in the top left corner of this page to create an SSH key secret.
4. Enter the information and then click **OK**. You will see the new secret at the top of the list on the management page.
    ![](https://qcloudimg.tencent-cloud.cn/raw/b708e55c58035960525dc9f54e7427e9.png)

**Field description**
- **Secret Name**: must be unique in the same region. It supports up to 128 bytes of letters, digits, hyphens and underscores and must begin with a letter or digit.
- **Description**: description, such as what it is used for. It contains up to 2,048 bytes.
- **Project ID**: ID of the project to which the created key pair belongs.
- **Tag**: optional item.
- **Encryption Key**:
 - Use the default CMK that SSM has created in KMS.
 - Use a custom encryption key. 

> ! If you are using SSM, you have activated [KMS](https://intl.cloud.tencent.com/product/kms). You can create an encryption key in either of the following ways:
>- Use the default Tencent Cloud managed CMK created on the [KMS console](https://intl.cloud.tencent.com/product/kms) as encryption key, and use the envelope encryption method for encrypted storage.
>- Use a custom key created on the [KMS console](https://intl.cloud.tencent.com/product/kms) as encryption key for encrypted storage.
