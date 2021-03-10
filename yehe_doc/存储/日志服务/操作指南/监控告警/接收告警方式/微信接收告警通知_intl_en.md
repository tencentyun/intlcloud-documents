This document describes how to receive alarm notifications through WeChat.

## Prerequisites

Before WeChat can be used to receive alarm notifications, you need to bind the recipient's WeChat account in the console first as instructed below:

>!
Allowing notification receipt through WeChat is a sufficient condition; that is, if it is not enabled, even if WeChat notification receipt has been set, corresponding alarm notifications still cannot be received.

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam).
2. Click **User** > **User List** on the left sidebar to enter the user list page.
3. Find the user for whom to configure the WeChat notification channel and click the username to enter the user details page.
4. Click **Edit Info** in the top-right corner to edit the user information.
5. Enable **Receive WeChat Messages**.
6. Click **OK**.
7. Tencent Cloud will send an email titled **Tencent Cloud WeChat Message Receipt Verification** to you. The email contains a verification QR code. Scan the code with the WeChat account of the notification recipient. Follow the **Tencent Cloud Assistant** service account as prompted to bind the recipient's WeChat account.
8. Successful binding is as shown below:

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor/notice/create).
2. On the left sidebar, click **Monitoring Alarm** > **Alarm Policy** to enter the alarm policy list page.
3. Find the policy for which to enable WeChat notification receipt and click the policy name to enter the policy editing page.
4. Select the recipient group, click **Edit**, and select **WeChat** in the pop-up configuration box.
5. Click **Save** to enable the WeChat alarm channel.

