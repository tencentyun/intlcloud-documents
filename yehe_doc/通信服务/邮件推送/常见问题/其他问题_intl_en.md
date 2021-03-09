### Does Tencent Cloud SES support sending emails to foreign countries?
Yes. Tencent Cloud SES is available in over 200 countries/regions, helping you deliver emails instantly to email addresses around the world. It features a 99% deliverability (except for invalid email addresses and restricted corporate mailboxes) and supports major email service providers such as Gmail, Yahoo, Hotmail, 163.com, and QQmail. In general, SES has high service stability and email deliverability.

### The API documentation says that `Region` only supports Hong Kong, China. Can I send emails to other regions?
Yes. `Region` only indicates the location of the server and does not affect the regions where emails are sent to.

### Does SES supports sending emails to multiple recipients at a time without them seeing each other.
No.

### Does SES have postpaid plans?
No. In SES, postpaid means you only pay as you go.

### Are there any version restrictions of SES SDK?
General versions can meet users’ needs. However, if your environment version is too outdated, you need to upgrade your SDK as instructed.

### How can I query email sending records?
You can query email sending records via API calls. For more information, see [GetSendEmailStatus](https://intl.cloud.tencent.com/document/product/1084/39502).

### How can I apply to access SES?
For details, see [Getting Started](https://intl.cloud.tencent.com/document/product/1084/39332).

### Dose SES support sending emails over SMTP?
No. SES only supports TencentCloud APIs.

### Does SES support access over other protocols?
No. Currently SES only supports access via TencentCloud APIs 3.0.

### Why is my email in the inbox, but the open rate is 0%?
- For HTML emails, Tencent Cloud can capture the open events and calculate the open rates.
- For plain text emails, Tencent Cloud cannot calculate the open rate.




