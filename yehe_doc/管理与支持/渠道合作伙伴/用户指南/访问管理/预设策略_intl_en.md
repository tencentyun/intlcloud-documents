>!This document describes the access management feature of International Partners. For more information on access management for other Tencent Cloud services, see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

Essentially, this feature is used to bind sub-accounts to policies or grant policies to sub-accounts. You can use preset policies directly in the console to implement some simple authorization operations.

International Partners currently provides the following preset policies:

| Policy | Description |
| -------------- | ------------------------------------------------------------ |
| QcloudIntlpartnersmgtFullAccess | Full read/write access to International Partners |
| QcloudIntlpartnersmgtReadOnlyaccess | Read-only access to International Partners |

### Example of Using Preset Policies

#### Creating a sub-account with International Partners permissions

1. Access the [**User List**](https://console.cloud.tencent.com/cam) page in the CAM console as a Tencent Cloud [root account](https://www.tencentcloud.com/document/product/598/32633) and click **Create User**.

2. Select **Custom Creation** to enter the **Create Sub-User** page.

>?Finish the steps before going to the **User Permissions** page as instructed in [Creating Sub-User](https://intl.cloud.tencent.com/document/product/598/13674).

3. On the **User Permissions** page:

    1. Search for and select the preset policy `Intlpartnersmgt`.
    2. Click **Next**.

4. In the **Review** step, click **Complete**. After the sub-user is created successfully, download the login link and security credential file and keep them properly. They contain the following information.

| Information | Source | Purpose | Saving Required |
| -------------- |-------------- |-------------- |-------------- |
| Login URL | Copied on the page| For quick console login (there is no need to enter the root account) | No |
| Username | Security credential CSV file | For console login | Yes |
| Password | Security credential CSV file | For console login | Yes |
| SecretId | Security credential CSV file | For calling server APIs. For details, see [Access Key](https://www.tencentcloud.com/document/product/598/32675) | Yes |
| SecretKey | Security credential CSV file | For calling server APIs. For details, see [Access Key](https://www.tencentcloud.com/document/product/598/32675) | Yes |

5. With the above login URL and security credentials, the authorized sub-user will have the permission to perform operations related to International Partners, such as accessing the International Partners console and calling International Partners server APIs.

#### Granting an existing sub-account permissions to access International Partners

1. Access the [**User List**](https://console.cloud.tencent.com/cam) page in the CAM console as a Tencent Cloud [root account](https://www.tencentcloud.com/document/product/598/32633) and click the sub-account to which you want to grant permissions.

2. On the **User Details** page, click the **Permission** tab and click **Add Permissions**. If **there are available permissions**, click **Associate Policy** instead.

3. Click the **Select policies from the policy list** tab, search for the preset policy `Intlpartnersmgt` and select it, then finish the further steps as prompted.

#### Disassociating International Partners permissions from a sub-account

1. Access the [**User List**](https://console.cloud.tencent.com/cam) page in the CAM console as a Tencent Cloud [root account](https://www.tencentcloud.com/document/product/598/32633) and click the sub-account from which you want to disassociate permissions.

2. On the **User Details** page, click the **Permission** tab, click **Disassociate** on the right of the preset policy `Intlpartnersmgt`, then finish the further steps as prompted.

