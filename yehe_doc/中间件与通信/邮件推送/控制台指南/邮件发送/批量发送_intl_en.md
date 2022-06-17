## Overview
This document describes how to batch send emails in the console. Batch sending is suitable for large-scale emailing scenarios and supports configuring different variable values for different recipients. Recipients can see only themselves in the "To" field of the email.

## Directions
1. Log in to the [SES console](https://console.cloud.tencent.com/ses/send), click **Email Sending** > **Batch**, and you can see the sending task list. The list displays the details of each sending task, including sending progress, task type, task status, and number of requests.
![](https://qcloudimg.tencent-cloud.cn/raw/03e8a8f74f5d0ab785bb016427712502.png)
2. Click **Create Sending Task**, select **Batch** for **Task Type**, and set all required fields for the task to send emails in batches.
![](https://qcloudimg.tencent-cloud.cn/raw/bd85315b7f512173a687f6c0ea4f706c.png)
>?The number and names of variables in the recipient list selected on the sending task page must be the same as those in the selected template.

### Scheduled
1. In the [SES console](https://console.cloud.tencent.com/ses/send), select **Email Sending** > **Batch**, click **Create Sending Task**, and select **Scheduled**.
![](https://qcloudimg.tencent-cloud.cn/raw/7e4f2dcdca1e2f11ba55e7d03861489e.png)
2. Select **Start Time** for the task, and the emails will be sent automatically at the specified time.
![](https://qcloudimg.tencent-cloud.cn/raw/55482b11771bbe336023ca840d346234.png)

### Recurring
1. In the [SES console](https://console.cloud.tencent.com/ses/send), select **Email Sending** > **Batch**, click **Create Sending Task**, and select **Recurring**.
![](https://qcloudimg.tencent-cloud.cn/raw/972566ee846e6629d9518f67686cec99.png)
2. Set task fields including **Start Time** and **Recurrence**. The console will automatically send emails based on the specified recurrence.
![](https://qcloudimg.tencent-cloud.cn/raw/e5ca62b26bbbfc467855d04d4e9c088e.png)

>?
>
>- The **Batch** feature in the console is suitable for batch sending of marketing or notification emails. To send trigger-based emails (such as authentication and transactional emails), we recommend you call the `SendEmail` API.
>- Automatic warm-up is built in the batch sending feature to intelligently determine the reputation of the sender domain/IP and the maximum number of sent emails allowed per day. When this daily limit is reached, email sending will stop and excessive emails will enter the cache queue and be sent 24 hours later. For the daily email limit for a domain/IP that has not been warmed up, see [Features](https://intl.cloud.tencent.com/document/product/1084/43285).
>- You can use a single domain for multiple sending tasks. When the total email volume exceeds the maximum number allowed per day, extra emails will enter the cache queue and be sent the next day.
>- When a task enters the cache queue, its status is **Paused** and the sending progress bar remains static. After you restart the task the next day, its status becomes **Sending** and the progress bar updates.
