[](id:que1) 
### Why would my emails go to the spam folder?
A spam folder is a comprehensive judgment policy of recipients. If your emails end up in spam folders, Tencent Cloud recommends that you check the following situations for troubleshooting:

<table id="case">
<tr><th width=8%>No.</th><th>Description</th></tr>
<tr>
<td>Case 1</td>
<td>You are using a public domain or public IP to send emails. In this case, your reputation is shared and not well protected. Therefore, your emails may be considered as spams by other email service providers and be put into spam folders.</td>
</tr><tr>
<td>Case 2</td>
<td>You are using a new domain or IP. Because a new IP does not have any reputation, your emails have a certain chance of going to spam folders at the beginning. However, every email service provider has a self-learning process. When they find that your emails are good, such as verification emails, they will gradually move them to the inbox.</td>
</tr><tr>
<td>Case 3</td>
<td>You have sent a large number of emails within a short period using a new IP without a warm-up process, for example, sending 100,000 emails on the first day. In this case, it is very likely that email service providers with strict restrictions such as Hotmail and Yahoo Mail will reject these emails and consider them as spams.</td>
</tr><tr>
<td>Case 4</td>
<td>The invalidity rate of your email address is high, which will greatly damage your sender reputation. Tencent Cloud can automatically stop you from sending emails when 8% of your emails are blocklisted in order to protect your IP reputation.</td>
</tr><tr>
<td>Case 5</td>
<td>Your emails are identified as spams by email service providers because they contain restricted content such as pornography or ads. You are advised to design your emails based on the 2:8 ratio of images to text, with no more than 3 images in an email (please do not include content such as pornography and ads).</td>
</tr></table>

[](id:que2) 
### What can I do to avoid emails going into spam folders?
The best way to prevent emails from going into spam folders is to **avoid the [five cases](#case) mentioned above**.
Whether an email goes to spam folders is connected to the email content, domain reputation, open rate, and user complaints. Different email service providers have different spam folder policies, over which we have no control. However, Tencent Cloud SES can guarantee the quality of sender IPs.
A new domain does not have reputation with email service providers, so it is normal that emails sent from it go to spam folders. If there is no problem with your email content, the situation will improve as long as you do a warm-up for at least one month, pay attention to the open rate, and reduce the complaint rate.

[](id:que3) 
### How do I know that an email has gone to spam folders?
You can use your email address to test, or log in to the console and check the email delivery rate and open rate to determine if your email has gone to the spam folder. If the email delivery rate and open rate are both low, probably your email has been delivered to the spam folder.

[](id:que4) 
### What should I do if my emails go to spam folders during the test phase?
Spam folder is a comprehensive judgment policy of recipients. Please follow the instructions below:
1. Make sure you haven’t use your domain to send spams before. If your domain reputation is low, your emails may automatically go to the spam folder.
2. The recipients may consider your emails as spam due to inappropriate email subject and content. You can [use the mail-tester tool](https://www.mail-tester.com/) to test the email content until you get a score higher than eight.
