[](id:senderConfig)
## Sender Configuration Options
Simple Email Service (SES) offers three ways to send emails:
- SES console
- SES API
- SES SMTP

You can [call APIs](https://intl.cloud.tencent.com/document/product/1084/39387) through the SES CLI or SDK or [call SMTP APIs](https://intl.cloud.tencent.com/document/product/1084/44458) to send emails. To send emails from the console, see [Regular Sending](https://intl.cloud.tencent.com/document/product/1084/47540).

## Flexible Deployment Options
### Shared IP Addresses
Generally, SES sends emails from shared IP addresses in the shared IP pool by default. Shared addresses are a fast and easy-to-use option for users who want to start sending with established IPs immediately. Tencent Cloud helps ensure the quality of shared IPs and a high delivery rate.
### Dedicated IP Addresses
A dedicated IP is an IP specially assigned to you by Tencent Cloud for sending emails. Generally, it either has never been used to send emails or has a good reputation in the past. This ensures that it will not be marked as a spam IP by anti-spam organizations. Dedicated IPs are unavailable currently.

## Sender Identity Management and Security
When receiving an email, an internet service provider (ISP) will check whether it is authenticated before delivering it to the recipient. Authentication proves to the ISP that you are the owner of the email address you are sending from. SES supports all industry-standard authentication mechanisms, including Sender Policy Framework (SPF), Domain Keys Identified Mail (DKIM), and Domain-Based Message Authentication, Reporting and Conformance (DMARC). It can ensure that your emails pass the ISP checks and are delivered to recipients successfully.
## Sending Statistics
SES provides a variety of methods to monitor email sending activities. For example, it can capture the information about the entire email response funnel (including the numbers of deliveries, opens, clicks, and bounces), and provide accurate data analysis. In addition, you can check the sending status of a specific email by calling the API for [Email Event Notification](https://intl.cloud.tencent.com/document/product/1084/39492) and adjust your email sending policy accordingly.

[](id:warmUp)
## Automatic Warm-up
Automatic warm-up refers to automatically warming up your IP addresses or sender domains without manual intervention throughout the process. For more information, see [Getting Started > What is warm-up?](https://intl.cloud.tencent.com/document/product/1084/42368).
### Description
Automatic warm-up is started in the batch sending mode by default to intelligently determine the reputation of the sender domain/IP and the maximum number of emails allowed per day. If the reputation level upgrade rule is not met during the sending process, but the daily limit is reached, email sending will automatically stop, and excessive emails will enter the cache queue and be sent 24 hours later. This process does not require manual intervention. For the daily limit at different reputation levels, see [Reputation Level Description](https://intl.cloud.tencent.com/document/product/1084/48864).

[](id:batch)

## Batch Feature Set
This is suitable for batch sending marketing or notification emails. To send trigger-based emails (such as authentication and transactional emails), we recommend you call the `SendEmail` API.
### Features
You can use the SES batch sending feature in either of the following ways:
• Console: A template is required, the email size cannot exceed 10 MB, and attachments are not supported.
• API: A template is required, the email size cannot exceed 10 MB, and attachments are supported.

### Description
You can manage sender addresses on the **Email Sending** > **Recipient Groups** page in the console.

## Batch Sending
To send emails in batches, create a sending task in the console, select **Batch** for **Task Type**, and set all required fields for the task.
## Scheduled Sending
Emails can be sent at a scheduled time. If you select **Start Time** for the task, the emails will be sent automatically at the specified time.
## Recurring Sending
To send recurring emails, specify fields such as**Start Time** and **Recurrence** in the console. The console will automatically send emails based on the specified recurrence.
## Mailbox Simulator
The SES mailbox simulator can help you easily test your application responses in various scenarios (such as bounces) without affecting sender reputation. You can send test emails to simulate successful delivery, bounce, unsubscription, and other scenarios with the mailbox simulator.
- Emails sent to the mailbox simulator are not real ones but simulated ones only.
- You can simulate email sending free of charge in the console.
- Each simulated scenario corresponds to a specific email address.
