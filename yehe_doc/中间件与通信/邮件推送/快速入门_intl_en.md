## Notes
- You must have the admin permissions on the sender domain.
- If your domain is hosted on Tencent Cloud, log in to the [DNSPod console](https://console.cloud.tencent.com/cns) to configure the domain. Otherwise, configure it as instructed in the checklist.
- It takes five minutes to two hours to sync the domain configuration. Please wait patiently.
- After the domain verification is completed, do not delete or modify the configured SPF and MX records to avoid errors in email sending.
- Do not use a corporate email domain to avoid SPF and MX records conflicts. Instead, you can create and use a second-level domain under your existing corporate email domain.
- Each Tencent Cloud account can be configured with up to 10 domains.

## Step 1. Log in to the console[](id:Step1)
Log in to the [SES console](https://console.cloud.tencent.com/ses). If you do not have a Tencent Cloud account yet, see [Signing Up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985) to create one.

## Step 2. Conduct identity verification[](id:Step2)
If the identity of your account is not verified, conduct identity verification in the [Account Center](https://console.cloud.tencent.com/developer). For more information, see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).

## Step 3. Activate SES[](id:Step3)
If the identity of your account is verified, click **Activate** to activate SES. After successful activation, you will get a free tier of 1,000 emails, and emails sent beyond the free tier will be charged.

## Step 4. Configure a sender domain[](id:Step4)
>! A domain that has been registered for Tencent Exmail cannot be used as a sender domain.

1. Log in to the [SES console](https://console.cloud.tencent.com/ses) and click **Sender Domain**.
2. Click **Create** on the **Sender Domain** page.
3. Enter a sender domain in the **Domain** field, for example, `mail.qcloud.com`, and click **Submit**.
>! A sender domain is the basis of an email address and represents the sender's corporate identity. To verify a sender domain, you need to configure the DNS information for it. Therefore, you must have the admin permissions on the domain.

4. Click **Verify** and configure the DNS information of the domain based on the record value on the **Sender Domain** page.
5. After the DNS is configured, click **Submit** on the **Sender Domain** page. Make sure `Record Value` and `Current Value` are identical and the status is `Verified`.
   

## Step 5. Configure a sender address[](id:Step5)

1. Go back to the **Overview** page and click **Sender Address**.
2. Click **Create** on the **Sender Address** page.
   
3. Set the following parameters as needed:
	- Sender Domain: Select a **verified** sender domain created in [step 4](#Step4).
	- Email Prefix: Enter an email prefix, for example, `test`.
	- Sender Name: Enter a sender name, for example, `Lil C`.
>! A sender address should be a full email address suffixed with a **verified** sender domain.
> Example: <code>test@example.qcloudmail.com</code>.

4. Click **Submit** to complete the sender address configuration.

## Step 6. Configure a template[](id:Step6)
1. Go back to the **Overview** page and click **Email Template**.
2. Click **Create** on the **Email Template** page.
3. Set the following parameters as needed:
	- Template Name: Enter a template name, for example, `test`.
	- Template Type: Select **HTML rich text**.
	- Email Summary: Enter an email summary, for example, `notification email template`.
	- Email Body: click **Choose a file** and select an HTML file as the email body.
>? The email content can be in plain text or rich text format. The rich text format requires the HTML code prepared in advance. The template will be reviewed after submission and can be used upon approval. The review will be finished within one business day.

4. Click **Preview** to preview the email template.
5. Click **Submit** to complete the template configuration.

## Step 7. Send emails[](id:Step7)
After the domain registration is completed and the template is approved, you can send emails via the SES console or API calls.
1. Click **Email Sending** to go to the email sending page.
>? This page is for email sending tests only. Up to 20 recipient addresses are allowed for a single test. You can send emails to more recipients at a time by calling APIs. For more information, see [SendEmail](https://intl.cloud.tencent.com/document/product/1084/39408) in the API Documentation.
2. Set the following parameters as needed:
 - Template: Select an **approved** template created in [step 6](#Step6).
 - Subject: Enter an email subject.
 - From: Select a sender address **configured** in [step 5](#Step5).
 - To: Enter the email addresses to which you want to send the email.
 - Variables: Enter required variables.
3. After the email is sent successfully, click [**Statistics**](https://console.cloud.tencent.com/ses/stats) to view the statistics.

