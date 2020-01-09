## Introduction
This document describes how to create a custom sub-user and configure permissions for it. The sub-user can manage the resources under the root account within the scope of the permissions.
## Directions
1. Log in to the CAM Console and select **User** > **[User List](https://console.cloud.tencent.com/cam)** in the left sidebar.
2. On the User List page, click **Create User**.
3. Click **Create a custom user**.
4. On the User Type page, click **Access resources and receive messages**.
5. Enter a username (required), notes, a mobile phone number, and an email address.
 >
 > - Click **Add User** to add more users. You can create up to 10 users at a time. 
 > - The sub-user will log in with the username, so the username cannot be changed once the user is created.
6. Under **Receive WeChat Messages**, check off whether to receive WeChat messages. If you choose to receive WeChat messages, you can configure the WeChat message receipt operation by performing the following step.
 - You will receive an email containing a QR code. Scan the QR code with WeChat to follow the Official Account, and then you can receive notifications.
 - Go to **Message Center** > **[Message Subscription](https://console.cloud.tencent.com/message/subscription)** to set WeChat as the receipt method, after which you can receive messages.
7. Configure the **Access Mode** for the sub-user.
 - Programming access: enable SecretId and SecretKey, and the sub-user can use TencentCloud APIs, SDKs, and other development tools to manage the resources of the root account within the scope of permissions.
 - Tencent Cloud Console access: enable password, and the sub-user can log in to the Tencent Cloud console to manage the resources of the root account within the scope of permissions.
 > To ensure the security of your account, it is recommended to enable login and operation protection.
8. Click **Next**.
9. On the permissions configuration page, configure permissions for the new sub-user in one of the following ways according to your needs. After being associated with a policy, the sub-user will have the permissions described by the policy.
 - Select policies from the policy list: click **Select policies from the policy list** and select the policies you want to associate with the sub-user.
 - Use existing user policies: click **Use existing user policies** and select the user whose permissions you want to use; the new sub-user will be associated with the policies of the existing user.
 - Add the sub-user to a user group to associate it with the group permissions: this is the best way to manage user permissions by roles and functions. You can add the sub-user to an existing user group or a new user group, and the sub-user will be associated with the policies of the user group.
10. Click **Next** to go to the review page.
11. On the review page, double check the information, click **Done**, and you will see a prompt that you have successfully created a user.
12. You can obtain the sub-user information in the following ways.
 - Click **Enter user’s email** > **OK** and the information on the new sub-user will be sent to the email address.
 - Click **Download Security Credentials** and some of the information will be saved to a local Excel file.
