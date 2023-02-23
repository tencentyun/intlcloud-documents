## Feature overview
Provided by Tencent Cloud IDaaS, the user management feature allows you to set up an account system for CVD end users. It offers quick account sync, multi-source authentication management, and secure login configuration services.
![](https://qcloudimg.tencent-cloud.cn/raw/80bf33f1ab284f469f13dc2cbec45ac7.png)

## Viewing the department and structure
The **User Management** page displays the department structure and the information of department members who use CVD instances, including user ID, name, mobile number, email, account status, and CVD policy. The user management feature is provided by IDaaS.
>? The user list does not display users and admins in **Left** status.
 
## Creating a user

1. Log in to the [CVD console](https://console.cloud.tencent.com/cvd).
2. On the **User Management** page, click **User Management** to go to IDaaS, **which provides the user creation service**.
![](https://main.qcloudimg.com/raw/018fb1b6daf270f78deba32ad2261b45.png)
3. Click **Create user** and configure the following items:

| Field   | Description |  Required |
| ----------------- | --------------- | --------------- |
| Name | The name of the CVD user. | Yes |
| User ID | The login account of the user. | Yes |
| Primary email | The email address of the user to receive CVD activation and other emails, which must be correct. | Yes |
| Secondary email | Another email address of the user. | No |
| Mobile number | The mobile number of the user to receive SMS messages. | No |
| Department | The department of the user, which facilitates user management. | Yes |
| Secondary department | The secondary department of the user. | No | User group | xxxx | No |
| Primary user group | Enter it as needed. | No |
| Supervisor | Enter it as needed. | No |
| Employee ID | Enter it as needed. | No |
| Order | Set it as needed to sort users. | No |
| Activation method | You can select **No activation for now**, **Send the link to the primary email address** (default), or **Set a temporary password**. | No |

4. After confirming that everything is correct, click **Confirm and next** to create more users as needed. Then, click **OK**.
5. Go back to the CVD console and refresh. Then, the created users will be displayed.

## Creating a department

1. Log in to the [CVD console](https://console.cloud.tencent.com/cvd).
2. On the **User Management** page, click **User Management** to go to IDaaS, **which provides the user creation service**.
3. Click **Create department**, enter the department name and superior department information, and select the department leader.
4. After confirming that everything is correct, click **Confirm and next** to create more departments as needed. Then, click **OK**.
5. Go back to the CVD console and refresh. Then, the created departments will be displayed.
