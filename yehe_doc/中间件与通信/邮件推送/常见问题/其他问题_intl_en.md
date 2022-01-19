[](id:que1) 
### Does SES support sending emails to email addresses outside the Chinese mainland?
Yes. Tencent Cloud SES is available in over 200 countries/regions, helping you deliver emails instantly to email addresses around the world. It features a 99% deliverability (except for invalid email addresses and restricted corporate mailboxes) and supports major email service providers such as Gmail, Yahoo, Hotmail, 163.com, and QQmail. In general, SES has high service stability and email deliverability.


[](id:que2) 
### The API documentation says that `Region` only supports Hong Kong (China). Can I send emails to other regions?
**Yes.** `Region` only indicates the location of the server and does not affect the regions where emails are sent to.

[](id:que3) 
### Does SES support sending emails to multiple recipients at a time without them seeing each other.
No.

[](id:que4) 
### Is there a version limit for SES?
General versions can meet users' needs. However, if your environment version is too outdated, you need to upgrade your SDK as instructed.

[](id:que5) 
### How can I query email sending records?
You can query email sending records via API calls. For more information, see [GetSendEmailStatus](https://intl.cloud.tencent.com/document/product/1084/39502).
 
 [](id:que6) 
### What sending methods does SES support?
SES supports three sending methods, namely, sending via console, API, and SMTP.


[](id:que7) 
### Why is that my email is in the inbox but the open rate is 0?
- For HTML emails, Tencent Cloud can capture the open events and calculate the open rates.
- For plain text emails, Tencent Cloud cannot calculate the open rate.
