[](id:dns)
### DNS validity verification

You can use [DNS Checker](https://www.whatsmydns.net/) to verify whether your DNS configuration is valid.

[](id:test)
### Email sending test

You can use [mail-tester](https://www.mail-tester.com/) to evaluate your email before sending it. This tool can check DNS/IP configuration integrity and IP validity, as well as the quality of email content. In case of complete DNS configuration, the score mainly depends on the email content. Generally speaking, the score needs to be optimized to at least 8 points.

>? If you perform tests on your own, try not to send too many emails to one single email address on the same day (no more than 24 emails per day). In the production environment, try not to send more than 10 emails to the same user per day.

 
[](id:add)
### Email address validity
The email bounce rate is a rigid metric for email scoring by ISPs. The most possible reason for email bounce is invalid email address; that is, the email is sent to an incorrect address. If the bounce rate stays high, the ISP will determine the sender as malicious and then put emails in the spambox or block sending IPs. A good bounce rate should not exceed 5%. If the addresses of your recipients are of poor quality, you need to process and filter them in advance.

[](id:garbage)
### Spambox
No senders can guarantee that a sent email will not go to the recipient's spambox. Especially, when the sender's domain name is newly registered and thus has no credibility at the ISP, it is normal for emails to go to the spambox. It requires a good warm-up and user engagement to improve the reputation of the domain name. The ISP will dynamically adjust the spam policy based on the reputation and eventually send emails to the recipient's inbox. Therefore, we recommend you add the prompt "If you don't see the email, please check your spambox".

[](id:avoid)
### How do I prevent my emails from being marked as spam?
1. Write appropriate email subjects and avoid using unusual or obviously marketing words.
2. Avoid obvious "spam" and illegal content and excessively commercialized words, such as lucky draw for top-up, gambling, pornography, drugs, and obscenity.
3. Balance the number of words and images, do not use too many images, and avoid emails where there is only a large image with no text.
4. It is better not to add URLs in the email content; otherwise, the email can be easily identified as spam.
5. Use regular fonts instead of various colors or artistic fonts in the email content.
6. Be sure to add an easily visual unsubscription button in the email content. Doing so can prevent users from being disgusted with your emails when they don't need the products or services you provide, as they can simply click the unsubscription button instead of reporting or blocking your emails. This will leave a positive impression on users and reduce the chance of your emails being recognized as spam.
7. Standardize the email HTML code, as non-compliant code may be identified as spam by the email filter. You need to have professional coders or use professional email templates.
8. Encourage customers to add you as a friend or contact. In this way, your emails will definitely go to their inbox instead of spambox.
9. Clean the recipient list regularly. When you find that your email fails to deliver to many of your recipients, the spam filters of most email service providers will give your domain name or IP a higher spam index score.
10. Perform testing before sending emails formally. Before sending your emails to recipients formally, you can use your own account to test the delivery. In this way, you can also infer what kind of email is more likely to be recognized as spam and then optimize the content accordingly.
