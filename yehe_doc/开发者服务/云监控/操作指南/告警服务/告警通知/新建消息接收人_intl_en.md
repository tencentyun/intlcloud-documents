This document describes how to create a message recipient and bind an alarm policy for receiving Cloud Monitor alarm messages.

<dx-alert infotype="explain" title="Note">
<font><b>Message recipients are a user type under sub-accounts. They only need to verify their phone number, email address, and WeChat account to receive alarm messages, but cannot log in to the Tencent Cloud console or gain programming access.</b></font>
</dx-alert>

## Directions

### Step 1. Create a message recipient

1. Log in to the CAM console and select **Users** > **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. On the **User List** page, click **Create User** to enter the **Create User** page.
3. On the **Create User** page, click **Custom Creation** to enter the **User Type** page.
4. On the **User Type** page, click **Receive Messages Only** to enter the **User Information** page.
5. On the **User Information** page, enter the username, remarks, mobile number, and email address, select an option for **Receive WeChat Messages**. Among them, the remarks field is optional.
6. Click **Done**.
   ![](https://main.qcloudimg.com/raw/5cc6613f67fb4c9db64dbcee2f191ca3.png)

### Step 2. Verify the receipt channel

1. After successful creation, find the user in **[User List](https://console.cloud.tencent.com/cam)** and click the corresponding username.
2. Enter the **User Detail** page.
   - Mobile: click **Send Verification Code** on the right and enter it on the phone to complete mobile number verification.
   - Email: click **Send Verification Link** on the right and go to the inbox to complete email address verification.
   - WeChat: click **Send Verification Link** on the right, go to the inbox, and scan the QR code with WeChat to complete WeChat account verification.
     ![](https://main.qcloudimg.com/raw/e28857a9220e0d00798923b88f4d88db.png)

   

### Step 3. Add the alarm message recipient

1. Log in to the CM console and go to [Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy).
2. Click the name of the policy for which to add users to enter the alarm policy modification page.
3. In the **Recipient Object** drop-down list, select **User** and select the created message recipient.
4. After completing the configuration, click **OK**. ![](https://main.qcloudimg.com/raw/a65aaae95b8028356d3f93d21a6ea8cd.png)
