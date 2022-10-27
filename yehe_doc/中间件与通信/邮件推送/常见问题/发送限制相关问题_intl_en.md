[](id:que1) 
### Can I send emails from any email address?
**No**, you can use SES to send emails only from addresses or domains that you own.

First, you must verify the domain to prove that you own it. Each Tencent Cloud account can have up to 10 domains. For more information on verifying email addresses and domains, see [Email Configuration](https://www.tencentcloud.com/document/product/1084/48862) of Getting Started.

[](id:que2) 
### Is there a limit on the size of an email sent via SES?
Yes, an email (including images and attachments) cannot exceed 4 MB.

[](id:que3) 
### Are there any limits on the number of emails that I can send?
Each SES account has a set of sending limits, including:

- Maximum number of emails per day: The maximum number of emails that you can send in 24 hours. The initial value for a new account is 500, which can be increased as needed. For the increasing rules, see [Reputation Level](https://www.tencentcloud.com/document/product/1084/48864).
- Maximum sending rate: The maximum number of emails you can send per second. By default, this limit is 20 emails per second per account.
- Maximum sends to the same email address per hour: 10 (default). Extra emails to this address beyond this limit will be blocked. You can resend them 1 hour later. This mechanism is set to avoid business and push exceptions.

>! If we find a quality problem of your emails, such as a high complaint rate or bounce rate, we have the right to suspend your email sending via SES.

[](id:que4) 
### Are there any restrictions on the email subject format?
The email subject should be in UTF-8 format and contain no more than 998 characters. Otherwise, the email won’t be sent. We recommend you keep the subject within 78 characters.

[](id:que5) 
### Are there any restrictions on recipient addresses when sending emails via API calls?
No. However, the recipient addresses must be valid (not obtained by crawling or purchased from a third party), and active triggers or subscriptions from the recipients are required.

[](id:que6) 
### How to send emails with custom content?
You can only send such emails using a template.
