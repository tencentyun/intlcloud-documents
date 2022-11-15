>!This document describes the access management feature of International Partners. For more information on access management for other Tencent Cloud services, see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

International Partners access management essentially binds sub-accounts to policies or grants policies to sub-accounts. You can use preset policies directly in the console to implement some simple authorization operations.

International Partners currently provides the following preset policies:

| Policy | Description |
| -------------- | ------------------------------------------------------------ |
| QcloudIntlpartnersmgtFullAccess | Full read/write access to International Partners |
| QcloudIntlpartnersmgtReadOnlyaccess | Read-only access to International Partners |

### Example of Using Preset Policies

#### Creating a sub-account with International Partners permissions

1. Access the [**User List**](https://console.cloud.tencent.com/cam) page in the CAM console as a Tencent Cloud [root account](https://www.tencentcloud.com/document/product/598/32633) and click **Create User**.

2. Select **Custom Creation** to enter the **Create Sub-User** page.

>?Finish the steps before **User Permissions** as instructed in [Creating Sub-User](https://intl.cloud.tencent.com/document/product/598/13674).

#### Granting an existing sub-account permissions to access International Partners

1. Access the [**User List**](https://console.cloud.tencent.com/cam) page in the CAM console as a Tencent Cloud [root account](https://www.tencentcloud.com/document/product/598/32633) and click the sub-account to which you want to grant permissions.

2. On the **User Details** page, click the **Permission** tab and click **Add Permissions**. If **there are available permissions**, click **Associate Policy** instead.

3. Click the **Select policies from the policy list** tab, search for the preset policy **Intlpartnersmgt** and select it, then finish the further steps as prompted.

#### Disassociating International Partners permissions from a sub-account

1. Access the [**User List**](https://console.cloud.tencent.com/cam) page in the CAM console as a Tencent Cloud [root account](https://www.tencentcloud.com/document/product/598/32633) and click the sub-account from which you want to disassociate permissions.

2. On the **User Details** page, click the **Permission** tab, click **Disassociate** on the right of the preset policy **Intlpartnersmgt**, then finish the further steps as prompted.

