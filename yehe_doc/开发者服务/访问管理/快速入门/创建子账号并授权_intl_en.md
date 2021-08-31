## Overview
Sub-accounts include sub-users, collaborators, and message recipients. The differences between different types of users are as follows (for more information, please see [User Types](https://intl.cloud.tencent.com/document/product/598/32633)) :
- Sub-user: it is created and fully owned by a root account.
- Collaborator: it has the identity of a root account. After it is added as a collaborator of the current root account, it becomes one of the sub-accounts of the current root account and can switch back to its root account identity.
- Message recipient: it can only receive messages.

This document describes how to use the root account or admin user to create a sub-account (sub-user/collaborator) in the CAM console and bind it to a permission policy.

## Prerequisites
- To create a collaborator, please [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) first.
- To use an admin user to create a sub-account, please [create an admin user](https://intl.cloud.tencent.com/document/product/598/38247) first and then follow the steps below.


## Directions
You can click the following tabs to view the directions to create and authorize different types of sub-accounts.
<dx-tabs>
::: Creating\sand\sauthorizing\sa\ssub-user
1. Log in to the CAM console and select **User** > **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. On the user list page, click **Create User**.
3. On the user creation page, select the creation method. Taking custom creation as an example, the steps are as follows:
![](https://main.qcloudimg.com/raw/e5068f9b75decf185c3a4fa790cce61f.png)
4. On the user type selection page, select **Access Resources and Receive Messages** and click **Next** to enter the user information.
5. On the user information configuration page, set the user information, access, and other information and click **Next** to set the user permissions.
6. On the user permission configuration page, bind policies to the sub-user and click **Next** to review the information and permissions.
7. On the information and permissions review page, confirm that the configuration information is correct and click **Done**.
![](https://main.qcloudimg.com/raw/61e65dfbcac8dc5d428416e4872e2491.png)
8. You will be redirected to the page prompting that the user is successfully created, and you can get the sub-user information in the following two methods:
	- Click **Copy** to directly get and copy the login information of the sub-user.
	- Click **Send**, enter the email address, and the system will send the complete sub-user information to the specified email address.

:::
::: Creating\sand\sauthorizing\sa\scollaborator

1. Log in to the Tencent Cloud console, go to [User List](https://console.cloud.tencent.com/cam), and click **Create User** to enter the user creation page.
2. On the user creation page, click **Create a Collaborator**.
![](https://main.qcloudimg.com/raw/91fee17aab40e65a111f25cb1f5596af.png)
3. On the collaborator creation page, enter the user information and click **Next** to set the user permissions.
4. On the user permission configuration page, bind permissions and click **Next** to review the information and permissions.
5. On the information and permissions review page, confirm that the configuration information is correct and click **Done**.
6. You will be redirected to the page prompting that the user is successfully created, and you can get the sub-user information in the following two methods:
	- Click **Copy** to directly get and copy the login information of the sub-user.
	- Click **Send**, enter the email address, and the system will send the complete sub-user information to the specified email address.

:::
</dx-tabs>


