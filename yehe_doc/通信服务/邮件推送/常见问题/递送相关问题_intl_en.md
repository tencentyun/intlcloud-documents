### After I send an email by calling the SES API, how long does it usually take to deliver an email sent via SES API call?
Usually it will be delivered within 3 seconds to 5 minutes.

### I was prompted that the delivery was successful after I sent an email by calling the SES API, but the delivery was delayed. Why is that?
It can take up to 72 hours to deliver an email. Usually an email will be delivered within 5 minutes. However, a few emails may take longer than 5 minutes depending on the content and email service providers' policies.

### What should I do if the images in the email are not displayed?
You should do the following:
1. Check whether the image URLs are correct.
2. Check whether your email client forbids loading images. If yes, click the "Show Image" button.
3. Check whether the images are blocked by the recipient.

### What should I do if emails sent via Tencent Cloud SES are blocked by Tencent Exmail?
Tencent Exmail blocks advertising emails. Do not contain advertising content in your email subject and content unless necessary.

### Why emails fail to be sent?
Please check the error codes document first to determine the error type.
Then check the following items in order:
1. Whether the account has the `QcloudFullAccess` permission and whether `SecretId` and `SecretKey` are correct.
2. Whether the sender domain is verified. (Do not modify the configured DNS after it passes verification.)
3. Whether the recipient email address is correct.
4. Whether the template is approved and whether the format of `TemplateData` is correct.
5. If the error indicating "no permission to send custom content" is returned, contact your sales rep to activate the permission for you.

If the issue persists, contact [Tencent Cloud technical team](https://console.cloud.tencent.com/workorder/category) for support.

### What is warm-up?
Warm-up is a way to establish a reputation for a new IP. Generally all email service providers have a limit on the daily number of emails sent from an IP. You need to start with a smaller number of emails and gradually increase the number each day.

### What is the unsubscription mechanism?
When an end user unsubscribes from emails sent by a customer, Tencent Cloud will notify the customer of the unsubscription event and record the end user's unsubscription status. In addition, the corresponding sender domain will no longer be able to send emails to this end user.

### Why do some emails get blocked？
Tencent Cloud maintains an address blocklist database and blocks sending emails to these blocklisted addresses. This helps customers filter out malicious email requests. Moreover, in order to protect customers’ sender reputation, Tencent Cloud adds the recipient addresses that have been rejected recently to the blocklist database. The blocklist database is shared across all accounts, so the address blocklists generated in different accounts are added to the same database. The email addresses in the blocklist database will be blocked for 14 days. You can log in to the [SES console](https://console.cloud.tencent.com/ses/stats) or call the API to unblocklist them. If the recipient addresses are valid and not in your blocklist, they may be blocklisted by other accounts. In this case, you can contact [Tencent Cloud technical team](https://console.cloud.tencent.com/workorder/category) to unblocklist them.


