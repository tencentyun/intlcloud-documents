## DMS Overview

**What is Tencent Cloud DMS?**
Tencent Cloud Direct Mail Service (DMS) is a secure, efficient, cost-effective, and highly scalable emailing service for organizations and developers. It helps you quickly implement triggered and batch email delivery in any application and provides high-quality IP maintenance and email authentication options, so as to improve the email deliverability and protect the sender reputation. With DMS, you can securely send high numbers of emails in different regions around the world.

**How do I use DMS?**
Tencent Cloud allows you to configure and send emails in the following ways:
- **Console**: it is a web service UI provided by Tencent Cloud for email configuration and delivery. For detailed directions on how to use the DMS Console, please see [Operation Guide](https://intl.cloud.tencent.com/document/product/1070/38221).

- **API**: Tencent Cloud also provides APIs for you to send emails and transfer email data in any application. For more information, please see the API documentation.

**DMS emailing process**
Conditions occurring during emailing with DMS and emailing results are as shown below:
 [![Image from Gyazo](https://i.gyazo.com/86dc396f1e4624935cbda7366cc743cf.png)](https://gyazo.com/86dc396f1e4624935cbda7366cc743cf)

 1.  The client application acting as the email sender initiates a request of emailing to one or multiple recipients to DMS.

2.  If the request is valid, DMS will send the email to the recipient addresses.

3.  At this point, different results may happen; for example:
    a.  The ISP successfully delivers the email to the recipient's inbox.
    b.  The recipient's email address does not exist; therefore, the ISP notifies DMS of email bounce, which then forwards the notification to the sender.
    c.  The recipient receives the email but marks it as spam and makes a complaint to the ISP. The ISP forwards the complaint to DMS, which then forwards the complaint to the sender.