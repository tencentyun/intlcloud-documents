## Scenario
You can configure email sending in the SES console. This document describes how to send an email.

## Directions
### Email Sending
1. Log in to the [SES console](https://console.cloud.tencent.com/ses/send) and click **Email Sending** to go to the **Email Sending** page.
![](https://main.qcloudimg.com/raw/3797c2f860e240f4e4864728aa09c80a.png)
2. Select an email template, enter a subject, select a sender address, enter recipient addresses, and click **Send** to send the email.
>? This page is only for testing email sending. Up to 20 recipient addresses are allowed for a single test.

### Batch
1. In the console, you see the sending task list on the **Email Sending** > **Batch** page. The sending task list displays the detailed information of each sending task, including **Sending Progress**, **Task Type**, **Task Status**, and **Requests**.
![](https://qcloudimg.tencent-cloud.cn/raw/03e8a8f74f5d0ab785bb016427712502.png)
2. Click **Create Sending Task**, select **Batch** for **Task Type**, and set all required fields for the task to send emails in batches.
![](https://qcloudimg.tencent-cloud.cn/raw/bd85315b7f512173a687f6c0ea4f706c.png)

### Scheduled
1. In the console, go to the **Email Sending** > **Batch** page, click **Create Sending Task** and select **Scheduled**.
![](https://qcloudimg.tencent-cloud.cn/raw/7e4f2dcdca1e2f11ba55e7d03861489e.png)
2. Select **Start Time** for the task and the emails will be sent automatically at the specified time.
![](https://qcloudimg.tencent-cloud.cn/raw/55482b11771bbe336023ca840d346234.png)


### Recurring
1. In the console, go to the **Email Sending** > **Batch** page, click **Create Sending Task** and select **Recurring**.
![](https://qcloudimg.tencent-cloud.cn/raw/972566ee846e6629d9518f67686cec99.png)
2. Set task fields including **Start Time** and **Recurrence**. The console will automatically send emails based on the specified recurrence.
![](https://qcloudimg.tencent-cloud.cn/raw/e5ca62b26bbbfc467855d04d4e9c088e.png)

>?
>
>- The **Batch** feature in the console is suitable for batch sending of marketing or notification emails. To send trigger-based emails (such as authentication and transactional emails), you are advised to call the `SendEmail` API.
>- Automatic warm-up is built in the batch sending feature to intelligently determine the reputation of the sender domain/IP and the maximum number of sent emails allowed per day. When this daily limit is reached, email sending will stop and extra emails will enter the cache queue and be sent 24 hours later. For the daily email limit for a domain/IP that has not been warmed up, see [Standard Warm-up Plan](https://intl.cloud.tencent.com/document/product/1084/43285#default).
>- You can use a single domain for multiple sending tasks. When the total email volume exceeds the maximum number allowed per day, extra emails will enter the cache queue and be sent the next day.
>- When a task enters the cache queue, its status is **Paused** and the sending progress bar remains static. After you restart the task the next day, its status becomes **Sending** and the progress bar grows.
