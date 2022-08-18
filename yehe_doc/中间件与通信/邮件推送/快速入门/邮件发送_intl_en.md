SES only allows sending emails through templates.

## Directions
### Step 1. Configure the template[](id:Step1)
1. Go to the **Overview** page in the SES console and click [**Email Template**](https://console.cloud.tencent.com/ses/template).
2. Click **Create** on the **Email Template** page.
3. Set the following parameters as needed:
	- Template Name: Enter a template name, for example, `test`.
	- Template Type: Select **HTML rich text**.
	- Email Summary: Enter an email summary, for example, `notification email template`.
	- Email Body: Click **Upload** and select an HTML file as the email body.
>?The email content can be in plain text or rich text format, the latter of which requires HTML code.

4. Click **Preview** to preview the email template.
5. Click **Submit** and wait for the review.
>?The template will be reviewed after submission and can be used to send emails upon approval. The review process will take one business day.

### Step 2. Send the email[](id:Step2)
SES offers three ways to send emails:
- Sending in the console
- Sending through the API
- Sending through SMTP

For brief directions on how to send emails in the console, see this documentation in Getting Started; for detailed directions, see Console Guide. For more information on the other two ways, see [API Category](https://intl.cloud.tencent.com/document/product/1084/39387) and [SMTP Email Sending Guide](https://intl.cloud.tencent.com/document/product/1084/44458).

1. Click [**Email Sending**](https://console.cloud.tencent.com/ses/send) to enter the **Email Sending** page.
>?This page only supports sending a small number of emails (involving up to 20 recipient addresses at a time). To email more addresses, see [Batch sending](https://intl.cloud.tencent.com/document/product/1084/47542) in the console or use the API or SMTP for email sending as instructed in [API Category](https://intl.cloud.tencent.com/document/product/1084/39387) or [SMTP Email Sending Guide](https://intl.cloud.tencent.com/document/product/1084/44458).
2. Set the following parameters as needed:
 - Template: Select an approved email template.
 - Subject: Enter an email subject.
 - From: Select the configured sender address.
 - To: Enter the email addresses and separate them by carriage return.
 - Variables: Enter variables, or leave them empty if your template contains no variables.
 - Unsubscription Management: If it is enabled, an unsubscribe link will be automatically inserted at the end of the email.
3. After the email is sent successfully, view the statistics on the [**Statistics**](https://console.cloud.tencent.com/ses/stats) page to track the email, as data may be subject to a certain latency.

