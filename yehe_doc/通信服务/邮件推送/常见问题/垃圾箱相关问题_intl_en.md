### Why would my emails go to the spam folder?
>?Spam folder is a comprehensive judgment policy of recipients. If your emails go to the spam folder, Tencent Cloud recommends that you check the following situations for troubleshooting:
>
1. You are using a public domain or public IP to send emails. In this case, your reputation is shared and not well protected. Therefore, your emails may be considered as spams by other email service providers and be put into the spam folder.
2. You are using a new domain or IP. Because a new IP does not have any reputation, your emails have a certain chance to go to the spam folder at the beginning. However, every email service provider has a self-learning process. When they find that your emails are good, such as verification emails, they will gradually move them to the inbox.
3. You have sent a large number of emails within a short period using a new IP without a warm-up process, for example, sending 100,000 emails on the first day. In this case, it is very likely that email service providers with strict restrictions such as Hotmail and Yahoo Mail will reject and consider these emails as spams.
4. The invalidity rate of your email address is high, which will greatly damage your sender reputation. Tencent Cloud can automatically stop you from sending emails when 8% of your emails are blocklisted in order to protect your IP reputation.
5. Your emails are identified as spams by email service providers because they contain sensitive content such as pornography or ads. You are advised to design your emails based on the 2:8 ratio of images to text, with no more than 3 images in an email (please do not include content such as pornography and ads).

### What can I do to avoid emails going into spam folder？
The best way to prevent emails from going into the spam folder is to avoid the five situations mentioned above. If the average daily number of emails you send exceeds 500,000, you are advised to contact Tencent Cloud to assign a dedicated IP to you and do a warm-up. To ensure the efficiency and deliverability of your emails, please contact [Tencent Cloud technical team](https://console.cloud.tencent.com/workorder/category) or your sales rep to tailor a solution for you.

### How can I know that an email has gone to the spam folder?
You can use your email address to test, or log in to the console and check the email delivery rate and open rate to determine if your email has gone to the spam folder. If the email delivery rate and open rate are both low, probably your email has been delivered to the spam folder.

### What should I do if my emails go to the spam folder during the testing phase?
Spam folder is a comprehensive judgment policy of recipients. Please follow the instructions below:
1. Make sure you haven’t use your domain to send spams before. If your domain reputation is low, your emails may automatically go to the spam folder.
2. The recipient may consider your emails as spams due to inappropriate email subject and content. You can [use mail-tester tool](https://www.mail-tester.com/) to test the email content until you get a score higher than eight.
