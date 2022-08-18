[](id:que1) 
### How do I test email sending in some simple ways?
You can use your own accounts for testing. SES offers a free tier of 1,000 emails currently but does not offer test accounts.

[](id:que5) 
### Can I send a large number of emails right from the start?
Due to the restrictions of recipient ISPs, we recommend you not send a large number of emails immediately at the beginning from a new domain/IP; instead, you should warm the domain/IP up first to achieve better emailing results.

[](id:que6) 
### What is warm-up?
Warm-up refers to warming up a sender domain/IP. The email delivery process is very complicated. Different ISPs generally have restrictions on the daily number of emails sent from one domain/IP. You should not send a large number of emails per day at the beginning. To achieve a higher email deliverability, the number of sent emails must be increased gradually every day. This daily increase process is called warm-up. Warm-up generally only needs to be performed once for each domain/IP.

SES supports automatic warm-up. For more information, see [Features > Automatic Warm-up](https://intl.cloud.tencent.com/document/product/1084/43285).

