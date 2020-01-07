## Introduction
This document describes how to configure restrictions on sub-accounts’ access to the console and how to apply for a temporary access. The sub-accounts will be subject to the restrictions when they access the console and manage the resources under the root account.
## Directions
### Configuring Login Restrictions
You can configure login restrictions to limit sub-accounts’ access to the console. Sub-accounts will be subject to the restrictions when they manage the resources under the root account.
1. Go to [User Settings](https://console.cloud.tencent.com/cam/security/subAccount) and scroll down to **Login Restrictions** as shown below:
![](https://main.qcloudimg.com/raw/8a5d2cd2c541fb0ee9e4c2617c0e0a7e.png)
2. After you enable this feature, sub-accounts (sub-users and collaborators) will be subject to restrictions when logging in to the console.
3. There are two restriction types available:
>- Whitelist: after you set up the whitelist, sub-accounts are allowed to log in to the console using the IPs (IP ranges) in the whitelist.
>- Blacklist: after you set up the blacklist, sub-accounts are not allowed to log in to the console using the IPs (IP ranges) in the blacklist.
4. Click **Set Now** in the **IP Addresses** area, and enter the IP addresses or IP ranges in the pop-up box.
5. You can choose whether to allow sub-accounts to apply for temporary access:
>- Deny: sub-accounts are not allowed to apply for temporary access when they are subject to the above restrictions. If you set this as “Deny,” jump to step 7.
>- Allow: sub-accounts are allowed to apply for temporary access when they are subject to the above restrictions. The applications will be sent to approvers for review via a valid message channel. If an application is approved, the sub-account will get a two-hour access to the console. If you set this as “Allow,” please take step 6. <span id="stepshenpi"></span>
6. Click **Set Now** under “Set Approver,” and check the approvers you want to set in the pop-up window. Click **OK**.
>? To ensure that the approvers can receive the application in a timely manner, they need to set up and verify their phone numbers. If an approver switches to a new phone number, the new number also needs to be verified.
7. Click **Apply Changes** to complete the configuration.

### Applying for Temporary Access
If a sub-account is allowed to apply for temporary access when it is subject to login restrictions, the sub-account can submit an application for temporary access. If the application is approved, the sub-account will get a two-hour access to the console.
1. If your sub-account is not allowed to log in to the console due to the login restrictions, click **Send Temporary Access Application** as shown below:
![](https://main.qcloudimg.com/raw/7d78ca3808b59080ca0331de4da8133a.png)
2. Your application will be sent to the approvers via a valid message channel and you will see a “Temporary access request pending review” prompt as shown below. An application will be valid for 30 minutes. You can copy the approval link and send it to the approvers to expedite the process.
![](https://main.qcloudimg.com/raw/558a09480d8956eadcc76cb3f9b5fede.png)
3. The approvers configured in step 6 in [Configuring Login Restrictions](#stepshenpi) can deny or approve the application through the link as shown below:
![](https://main.qcloudimg.com/raw/3545675435d710c0227aab98f4e1de8f.png)
4. If your application is approved, you will see that the temporary access request has been approved on your login interface as shown below. Click **Continue to log in** and you will be able to access the console with your sub-account for two hours.
![](https://main.qcloudimg.com/raw/fb08d22c3c3ee8a5bbd5d979a385e85d.png)
5. If your application is denied, you will see that the temporary access request has been denied on your login interface. We recommend that you submit a new application after communicating with the approvers.
