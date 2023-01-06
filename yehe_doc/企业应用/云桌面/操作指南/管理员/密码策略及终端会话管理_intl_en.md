## User Password Policy Settings
### Adding an end user password policy
1. On the **User Management** page in the [CVD console](https://console.cloud.tencent.com/cvd), click **User Management** to go to [Tencent Cloud IDaaS](https://cloud.tencent.com/product/tcid), which provides the end user password policy settings.
![](https://main.qcloudimg.com/raw/376065d917bc2c47e9d27a00f83d93ba.png)
2. Click **Security** > **Password policy** to enter the password policy management page. Then, click **Add policy**.
3. Enter the policy name and description. When you set the password requirements, the password length is required, and other items are optional. The higher the required password complexity, the higher the security.
4. Set the requirements for user password expiration and password reset.
5. Set the requirements for secure login. You can configure login authentication and account lock/unlock as needed. If you enable self-service unlock, users can unlock their accounts via email or security question; otherwise, they need to contact the admin for assistance.
6. Set the scope of the password policy.
You can select **All users** or specify a **custom** user type by user, user attribute, user department, or department. You can also enter up to 20 users to be excluded in the **Exclude the following users** input box.
7. After completing the above settings, click **OK**.

### Sorting password policies by priority
In the password policy list:
- Click the **up** icon to increase the priority.
- Click the **down** icon to decrease the priority.

## End User Session Management
1. Log in to the [CVD console](https://console.cloud.tencent.com/cvd).
2. On the **User Management** page, click **User Management** to go to [IDaaS](https://cloud.tencent.com/product/tcid).
>? [IDaaS](https://cloud.tencent.com/product/tcid) provides the session expiration settings.
3. Click **Security** > **Session management**.
On the session management page, configure the following items:

### Session expiration time
In the **Session expiration time settings** section, set the expiration time for **Access authentication token** and **Access refresh token**.
### Session termination behavior
In the **Session termination behavior settings** section, set the associated behaviors of **Browser close** and **Idleness**.
>? For the duration of **Idleness**, the minimum value is 10 minutes, and the maximum value cannot be after the expiration time of the access refresh token, which is 30 minutes by default.


## Custom Portal Settings
1. Log in to the [CVD console](https://console.cloud.tencent.com/cvd).
2. On the **User Management** page, click **User Management** to go to [IDaaS](https://cloud.tencent.com/product/tcid), **which provides the custom portal settings**.
3. Click **Settings** > **System appearance settings** and configure the following items:


| Item | Description | 
|---------|---------|
| Browser tab | Click the logo area to change the logo of the browser tab. The logo image must meet the system requirements. Edit the text of the browser tab in the input box and click **OK** to save the change. | 
| Portal appearance | Click the logo area to change the logo of the login page. The logo image must meet the system requirements. Click the background area of the login page to change the background image, which also must meet the system requirements. Click **OK** to save the change. | 
