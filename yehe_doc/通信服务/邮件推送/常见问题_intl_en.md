### Why emails fail to be sent?
Please check the error codes document first to determine what error it is.
#### Check the following items in order:
1. Whether the app key is correct.
2. Whether the sender address has been approved.
3. Whether the recipient address is correct.
4. Whether the field type is correct.
5. Whether the `html` or `text` field is mistakenly passed in.
6. Whether the business type is correct.

If the issue persists, please contact [Tencent Cloud technical team](https://console.cloud.tencent.com/workorder/category) for support.

### Why do some emails get blocked？
Tencent Cloud maintains an address blocklist database and blocks sending emails to these blocklisted addresses. This helps customers filter out malicious email requests. Moreover, in order to protect customers’ sender reputation, Tencent Cloud adds the recipient addresses that have been rejected recently to the blocklist database. The blocklist database is shared across all accounts, so the address blocklists generated in different accounts are added to the same database. The email addresses in the blocklist database will be blocked for 14 days. To unblock them, please contact [Tencent Cloud technical team](https://console.cloud.tencent.com/workorder/category).

### Why would my emails go to the spam folder?
>?If your emails go to the spam folder, you can check the following situations for troubleshooting:
>
1. You are using a public domain or public IP to send emails. In this case, your reputation is shared and not well protected. Therefore, your emails may be considered as spams by other email service providers and be put into the spam folder.
2. You are using a new domain or IP. Because a new IP does not have any reputation, your emails have a certain chance to go to the spam folder at the beginning. However, every email service provider has a self-learning process. When they find that your emails are good, such as verification emails, they will gradually move them to the inbox.
3. You have sent a large number of emails within a short period using a new IP without a warm-up process, for example, sending 100,000 emails on the first day. In this case, it is very likely that email service providers with strict restrictions such as Hotmail and Yahoo Mail will reject and consider these emails as spams.
4. The invalidity rate of your email address is high, which will greatly damage your IP reputation. Tencent Cloud can automatically stop you from sending emails when 8% of your emails are blocklisted in order to protect your IP reputation.
5. Your emails are identified as spams by email service providers because they contain sensitive content such as pornography or ads. You are advised to design your emails based on the 2:8 ratio of images to text, with no more than 3 images in an email (please do not include content such as pornography and ads).

### What can I do to avoid emails going into spam folder？
The best way to prevent emails from going into the spam folder is to avoid the five situations mentioned above. It is recommended that you use a dedicated IP and do a warm-up. To ensure the efficiency and deliverability of your emails, please contact [Tencent Cloud technical team](https://console.cloud.tencent.com/workorder/category) to tailor a solution for you.

### How can I know that an email has gone to the spam folder?
You can use your email address to test, or log in to the console and check the email delivery rate and open rate to determine if your email has gone to the spam folder. If the email delivery rate and open rate are both low, probably your email has been delivered to the spam folder.

### Why is my email in the inbox, but the open rate is 0%?
If the email you sent is an HTML email, Tencent Cloud can capture the open events and calculate the open rate. If it is a plain text email, Tencent Cloud cannot calculate the open rate.

### What is a dedicated IP?
A dedicated IP is an IP specially assigned to you by Tencent Cloud for sending emails. Generally, it either has never been used to send emails or has a good reputation in the past. This ensures that it will not be marked as a spam IP by anti-spam organizations.

### What is warm-up?
Warm-up is a way to establish a reputation for a new IP. Generally all email service providers have a limit on the daily number of emails sent from an IP. You need to start with a smaller number of emails and gradually increase the number each day.
>?Tencent Cloud recommends that you increase your email volume each day, with 200 emails on the first day, 
500 on the second day, 1,000 on the third day, 2,000 on the fourth day, 5,000 on the fifth day, 10,000 on sixth day, and so on.
>
### What if I want to send a great number of emails at the very beginning?
For any special requirements, Tencent Cloud needs to do some specific initialization for you. Please contact [Tencent Cloud technical team](https://console.cloud.tencent.com/workorder/category) to tailor a solution for you.

### How should I configure the domain DNS?
- If you are using Tencent Cloud’s DNS service, log in to the [Tencent Cloud console](https://console.cloud.tencent.com/cns) to configure.
- If you are using DNS service from another domain service provider, you can transfer your domain to Tencent Cloud for DNS resolution. 
- In other cases, please configure it at your domain service provider.

### Does the email service have any requirements on DNS resolution?
The email sender domain must be a fourth-level domain, such as `mail._domainkey.domain.com`. 
