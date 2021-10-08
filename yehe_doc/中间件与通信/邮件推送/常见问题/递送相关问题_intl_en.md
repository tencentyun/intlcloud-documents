[](id:que1) 
### How does SES ensure reliable email transmission?
After you create an email template, we will review the template content to ensure that it meets the ISP's requirements. To further improve your email delivery rate, SES provides a feedback mechanism that includes email bounces, complaints, and delivery notifications.

[](id:que2) 
### Can SES ensure successful delivery of my emails?
Whether it is SES or any other email service, it cannot guarantee 100% successful delivery of every email, which is affected by many factors, such as email content, domain name reputation, open rate, and user complaint. For more information, please see [How do I prevent my emails from being marked as spam?](https://intl.cloud.tencent.com/document/product/1084/42369).


[](id:que3) 
### How long does it take for an email sent via SES to reach the recipient's inbox?
Generally, an email will be delivered to the recipient's inbox within three seconds to five minutes, max 72 hours. A few emails may be delayed due to factors such as email content and the email service provider's policy. Therefore, it is normal to deliver an email in more than five minutes.

[](id:que4) 
### Will email bounces or complaints caused by other SES users affect my email delivery rate?
Usually, if you are using a shared IP, email bounces or complaints caused by other SES users may have a certain impact on your email delivery rate. If you are using a dedicated IP, there will be no impact.

[](id:que5) 
### What should I do if the image in the email is not displayed?
You can troubleshoot as below:

1. Check whether the image URL is correct.
2. Check whether your email client forbids loading images. If yes, click the **Show Image** button.
3. Check whether the image is blocked by the recipient.

[](id:que6) 
### What should I do if my email sent via SES is blocked by the enterprise email service?
Usually, enterprise email services block advertising emails, so do not contain advertising content in your email subject and content unless necessary.

[](id:que7) 
### Why did my email fail to be sent?
Please check the error code document first to determine the error type.

Then troubleshoot in the following order:
1. Whether the account has the `QcloudFullAccess` permission and whether `SecretId` and `SecretKey` are correct.
2. Whether the sender domain is verified. (Do not modify the configured DNS after it passes verification.)
3. Whether the recipient email address is correct.
4. Whether the template is approved and whether the format of `TemplateData` is correct.
5. If the error indicating **no permission to send custom content** is returned, contact your sales rep to activate the permission for you.

If the issue persists, contact [Tencent Cloud technical team](https://console.cloud.tencent.com/workorder/category) for support.

[](id:que8) 
### What is the unsubscription mechanism?
When an end user unsubscribes from emails sent by a customer, Tencent Cloud will notify the customer of the unsubscription event and record the end user's unsubscription status. In addition, the corresponding sender domain will no longer be able to send emails to this end user.

[](id:que9) 
### Why do some emails get blocked?
Tencent Cloud maintains an address blocklist database and blocks sending emails to these blocklisted addresses. This helps customers filter out malicious email requests. Moreover, in order to protect customers' sender reputation, Tencent Cloud adds the recipient addresses that have been rejected recently to the blocklist database. The blocklist database is shared across all accounts, so the address blocklists generated in different accounts are added to the same database. The email addresses in the blocklist database will be blocked for 14 days. You can log in to the [SES console](https://console.cloud.tencent.com/ses/stats) or call the API to unblocklist them. If the recipient addresses are valid and not in your blocklist, they may be blocklisted by other accounts. In this case, you can contact [Tencent Cloud technical team](https://console.cloud.tencent.com/workorder/category) to unblocklist them.

[](id:warmup)
### Email warm-up (vital)

Warm-up is a necessary process for each new email sending domain name or IP. The number of sent emails must be increased to the desired quantity gradually day by day rather than at one go. A good warm-up can gain a good reputation with the ISP. You should follow the warm-up plan below for every new domain name or IP:

| Time | Sent Emails/Day | Sending Frequency |
| --------- | ------------ | ---------------- |
| Day 1 | 1,000 | 200 emails/hour |
| Day 2 | 1,500 | 200 emails/hour |
| Day 3 | 2,000 | 400 emails/hour |
| Day 4 | 3,000 | 400 emails/hour |
| Day 5 | 4,500 | 500 emails/hour |
| Days 6–10 | 6,000–8,000 | 500–1,000 emails/hour |
| Days 11–15 | 8,000–10,000 | 800–2,000 emails/hour |
| Days 16–20 | 10,000–15,000 | 1,000–3,000 emails/hour |
| Days 21–30 | 15,000–25,000 | 3,000–5,000 emails/hour |
| Day N | Doubled daily | - |

- The values in this table are suggested values for reference only.
- Warm-up is used to increase the IP reputation. You should not conduct warm-up with the aim to find out the IP limit imposed by the ISP.
- If there are many email addresses in one single domain, you should appropriately reduce the number of warm-up emails.
- A high-quality IP or domain name should have a stable number of emails sent every day, and we recommend you send emails on at least 3 days per week.
- In the early stage, we recommend you randomly select addresses from the address library, and when the number of sent emails rises to a certain quantity, perform targeted warm-up according to the specific sending situation of each domain.
- The above values are recommended for one single IP. If you have multiple IPs, you can increase the values appropriately, but no more than 5 times the above values.
- Normal verification code email services can be gray scaled according to the current business ratio and may not strictly follow the above values as long as the upper limits are not exceeded.
- If your business conditions cannot satisfy the requirements of warm-up, you can switch to public domain names and shared IP that have already been warmed up to send emails, but you cannot control the reputation independently in that case.
- If your business conditions cannot satisfy the requirements of warm-up, your business volume is small, your sent emails are generally for account registrations with a high open rate, and the daily email quantity is below 10,000, you can consider skipping warm-up, but this is not recommended.

[](id:use)
### User open rate
The user open rate is also an important metric of whether an email will go to the inbox. The higher the user engagement rate, the more likely the ISP will increase the credibility of the domain name accordingly. Generally speaking, it is normal that the open rate of registered emails is above 80%. For notification emails, this metric depends on the business scenarios. For marketing emails, you should continuously optimize the email subject and content to engage users. If this metric is below 50%, sent emails will likely go to the spambox.


