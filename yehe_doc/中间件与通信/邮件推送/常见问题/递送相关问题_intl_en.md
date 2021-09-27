[](id:que1) 
### How does SES ensure reliable email transmission?
After you create an email template, we will review the template content to ensure that it meets the ISP's requirements. To further improve your email delivery rate, SES provides a feedback mechanism that includes email bounces, complaints, and delivery notifications.

[](id:que2) 
### Can SES ensure successful delivery of my emails?
No email service provider can guarantee a 100% delivery rate because the delivery of emails is related to many factors such as the email content, domain reputation, open rate, and user complaints. If the recipients do not want to receive your emails, the ISP will reject or discard your emails. In some cases, the ISP may lose your emails. SES will closely monitor the ISP's guidelines to help safely deliver legitimate, high-quality emails to recipients' inboxes.

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
### Why do some emails get blocked？
Tencent Cloud maintains an address blocklist database and blocks sending emails to these blocklisted addresses. This helps customers filter out malicious email requests. Moreover, in order to protect customers’ sender reputation, Tencent Cloud adds the recipient addresses that have been rejected recently to the blocklist database. The blocklist database is shared across all accounts, so the address blocklists generated in different accounts are added to the same database. The email addresses in the blocklist database will be blocked for 14 days. You can log in to the [SES console](https://console.cloud.tencent.com/ses/stats) or call the API to unblocklist them. If the recipient addresses are valid and not in your blocklist, they may be blocklisted by other accounts. In this case, you can contact [Tencent Cloud technical team](https://console.cloud.tencent.com/workorder/category) to unblocklist them.
