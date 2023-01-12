Email delivery is a complex process. Delivery capabilities and deliverability are subject to a variety of factors, including but not limited to emailing behavior, email content, and recipient operations.
If you continue to send emails to Email Service Providers in spite of a low email delivery quality, your sender IP address and domain will be severely affected. Therefore, SES dynamically determines the sender domain reputation level based on the email delivery quality, and the daily email sending limit varies by level.

## Reputation Level Rules
By default, the reputation level of a newly created sender domain in **Verification passed** status is level 1, which will be automatically raised immediately or lowered the next day based on the email delivery quality. The daily email sending limits for different reputation levels are listed as shown below. If you want to increase this limit, you can submit a ticket to us for application after your domain reputation level reaches level 20.

You can view the reputation level of each sender domain and the corresponding daily email sending limit on the [**Sender Domain**](https://console.cloud.tencent.com/ses/domain) page in the SES console.
>?
>- Even the reputation level of 1 can be automatically upgraded to level 20 on the same day, meaning that the maximum number of emails sent per day can reach 1,000,000. Manual adjustments are not supported before level 20.
>- As soon as the email delivery quality meets the upgrade requirements of the reputation level, the system will immediately increase the reputation level and the maximum number of emails sent per day. For more information, see "Level Raising and Lowering Rules" below.

| Reputation Level | Daily Email Sending Limit (Emails)        |
| ----- | ----------------- |
| 1     | 500               |
| 2     | 1,000              |
| 3     | 2,000              |
| 4     | 5,000              |
| 5     | 10,000             |
| 6     | 20,000             |
| 7     | 40,000             |
| 8     | 60,000             |
| 9     | 80,000             |
| 10    | 100,000            |
| 11    | 150,000            |
| 12    | 200,000            |
| 13    | 300,000            |
| 14    | 400,000            |
| 15    | 500,000            |
| 16    | 600,000            |
| 17    | 700,000            |
| 18    | 800,000            |
| 19    | 900,000            |
| 20    | 1,000,000           |
| Higher  | Submit a ticket to us for application |

## Level Raising and Lowering Rules
SES dynamically determines the reputation level of a sender domain based on the email delivery quality, which is measured against the **invalid address rate, deliverability, spam bounce rate, spam complaint rate, and email open rate**.

**The level will be raised when any one of the following rules is satisfied, and the raised daily email sending limit will take effect immediately:**
- The daily number of emails actually sent reaches 70% of the daily email sending limit for the current level, with an invalid address rate below 5%, a deliverability above 92%, a spam bounce rate below 2.5%, and a spam complaint rate below 0.1%.
- The daily number of emails actually sent reaches 70% of the daily email sending limit for the current level, with a deliverability above 90%, a spam complaint rate below 0.1%, and an email open rate above 50%.

**The level will be lowered when any one of the following rules is satisfied, and the lowered daily email sending limit will take effect the next day:**
- The daily number of emails actually sent exceeds 300, with an invalid address rate above 9%.
- The daily number of emails actually sent exceeds 300, with a deliverability below 65%.
- The daily number of emails actually sent exceeds 300, with a spam bounce rate above 5%.
- The daily number of emails actually sent exceeds 300, with a spam complaint rate above 0.5%.

You can view the email delivery quality information in the [**Statistics**](https://console.cloud.tencent.com/ses/stats) module in the SES console. To protect your sender IP address and domain, the SES has the right to adjust the rules and values and update the description properly.

## Rules Regarding Exceeding the Daily Email Sending Limit
### Batch sending
If no rule for raising the reputation level is satisfied, and the real-time number of emails actually sent reaches the daily email sending limit during batch sending, the system will automatically pause the sending and cache the unsent emails in the queue, which will be automatically sent in 24 hours. You can view the overall status of a batch sending task on the [**Batch**](https://console.cloud.tencent.com/ses/batch-send) page in the SES console or view the recent real-time sending status on the [**Real-time queue status**](https://console.cloud.tencent.com/ses/queue-status) page in the SES console.
### Regular sending
If no rule for raising the reputation level is satisfied, and the real-time number of emails actually sent reaches the daily email sending limit during sending, the sending will fail, and an error message will be returned.

## Temporary Blocking Rules
When any one of the following rules is satisfied, email sending will be blocked temporarily for the day, and emails unsent during batch sending will be regarded as failed:
- The daily number of emails actually sent exceeds 300, with an invalid address rate above 11%.
- The daily number of emails actually sent exceeds 300, with a spam bounce rate above 15%.

## Allowed Email Types
SES only allows sending emails to recipient addresses that are provided during member registration. You are not allowed to send unsolicited emails or send emails to addresses that are not provided by recipients themselves.
- Emails cannot contain sensitive words or social media information such as Weixin account, QQ account, QR code, and group information.
- Emails should contain detailed compliance information. We recommend you add the Unsubscription link in emails.
