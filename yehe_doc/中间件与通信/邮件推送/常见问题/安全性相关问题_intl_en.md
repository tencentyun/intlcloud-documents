[](id:que1) 
### Can SES access the emails I send and receive? 

SES uses internal anti-spam technologies to filter emails that contain poor content. In addition, it scans all emails containing attachments to check for viruses and other malicious content. It will not save your email content though.

[](id:que2) 
### Can my emails be encrypted?
During email transfer, SES will encrypt the content of your emails.

[](id:que3) 
### Does SES use Transport Layer Security (TLS) to send emails over an encrypted connection?
SES supports TLS 1.2, TLS 1.1, and TLS 1.0 for TLS connection.

By default, SES uses opportunistic TLS. This means that SES will always try to establish a secure connection with the recipient's email server. If it cannot establish a secure connection, it will send the email in an unencrypted manner. You can change this option so that SES will only send emails when a secure connection can be established.

[](id:que4) 
### How does SES ensure that incoming emails are not spam and are virus-free?
SES adopts many spam and virus protection measures. Tencent Cloud specifically maintains a blocked email address library and blocks emails from such addresses to help you filter malicious emails. SES scans every incoming email containing attachments for viruses. It provides you with various spam detection methods; for example, in addition to spam and virus scan results, it also provides DKIM and SPF check results.

[](id:que5) 
### What technologies can prevent SES users from sending spam? 

SES uses internal content filtering technologies to detect spam. In addition, it also provides email quality scoring tools to help you check email content on your own. If it finds that an account is sending spam or malicious content, it will suspend the account's ability to send other emails.
>! Not being spam does not mean that the email will not go to the spambox. The email quality score is for reference only. Spambox policy is at the email service provider level. Whether or not an email will go to the spambox is subject to the email content, domain name credibility, open rate, user complaint, etc., and spam policy varies by email service provider, which are out of SES' control. SES can guarantee the quality of the sending IPs.

