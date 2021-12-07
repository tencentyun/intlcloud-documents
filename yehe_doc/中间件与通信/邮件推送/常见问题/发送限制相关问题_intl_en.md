[](id:que1) 
### Can I send emails from any email address?
**No**, you can use SES to send emails only from addresses or domains that you own.

First, you must verify the domain to prove that you own it. Each Tencent Cloud account can have up to 10 domains. For more information on verifying email addresses and domains, see **Step 4. Configure a Sender Domain** in [Getting Started](https://intl.cloud.tencent.com/document/product/1084/39332).

[](id:que2) 
### Is there a limit on the size of an email sent via SES?
Yes, an email (including images and attachments) cannot exceed 10 MB.

[](id:que3) 
### Are there any limits on the number of emails that I can send?
Each SES account has a set of sending limits, including:

- Maximum daily sends: the maximum number of emails that you can send within 24 hours. By default, this limit is 300,000 emails per day per account. However, you can raise this limit.
- Maximum sending rate: the maximum number of emails you can send per second. By default, this limit is 20 emails per second per account.
- Maximum sends to the same email address per hour: 10 (default). If this limit is exceeded, extra emails to this address will be blocked. You can resend it after 1 hour. This mechanism is to avoid business and push exceptions.

>! 
>- All the above three limits can be adjusted. Please contact Tencent Cloud technical support and provide the sending scenario and reason if you need to apply for adjustment.
>- If we find a problem with the quality of your email, such as a high complaint rate or bounce rate, we have the right to stop you from sending emails via SES.

[](id:que4) 
### Are there any restrictions on the email subject format?
The email subject should be in UTF-8 format and contain no more than 998 characters. Otherwise, the email won’t be sent. Tencent Cloud recommends you keep the subject within 78 characters.

[](id:que5) 
### Are there any restrictions on recipient email addresses when sending emails via API calls?
No. However, the recipient email addresses must be valid (not obtained by crawling or purchased from a third party) and active triggers or subscriptions from the recipients are required.

[](id:que6) 
### What should I do to be able to send custom content?
Customers who have enabled the feature to send custom content will need to undertake the risk that their accounts are placed under review due to sending illegal or harmful information. It will hurt your sender reputation if your email address is out of control or used to send spams. In serious cases, the ISP will block your sender domain. To enable this feature, you need to contact your sales rep to do it for you.
