## Notes:
- You must have the admin permissions on the sender domain.
- If your domain is hosted on Tencent Cloud, please log in to the [DNSPod console](https://console.cloud.tencent.com/cns) to configure the domain. If your domain is hosted on another domain service provider, please configure it according to the checklist.
- After the domain is configured, synchronization may take five minutes to two hours. Please wait patiently for the verification to finish.
- After the domain verification is completed, do not delete or modify the configured SPF and MX records, otherwise errors may occur when sending emails.
- To avoid conflicts between SPF and MX records, do not use corporate email domains.
- Each Tencent Cloud account can be configured with up to 10 domains.

<span id ="Step1"></span>
## Step 1. Log in to the Console
Log in to the [SES console](https://console.cloud.tencent.com/ses). If you do not have a Tencent Cloud account yet, please see [Signing up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985) to create one.

<span id ="Step2"></span>
## Step 2. Perform Organization Verification
If you haven't completed identity verification for your account, please go to [Account Center](https://console.cloud.tencent.com/developer) for identity verification. For more information, see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).

<span id ="Step3"></span>
## Step 3: Activate SES
If you have already completed identity verification for your account, click **Activate** to active SES. After successful activation, you will get a free tier of 1,000 emails.
After the free tier is used up, your plans will be used automatically. If no plans are available, you will be charged on a pay-as-you-go basis.

<span id ="Step4"></span>
## Step 4. Configure a Sender Domain
1. Log in to the [SES console](https://console.cloud.tencent.com/ses) and click **Sender Domain**.
2. On the **Sender Domain** page, click **Create**.
3. Enter a sender domain in the **Domain** field, for example, `mail.qcloud.com`, and click **Submit**.
    
>!A sender domain is the basis of an email address and represents the identity of the sender's corporate. To verify a sender domain, you need to configure the DNS information for it. Therefore, you must have the admin permissions on the domain.
   
4. After finishing DNS configuration, click **Verify**.
5. In the **Sender Domain Configuration** dialog box, click **Submit** to verify the sender domain.

<span id ="Step5"></span>
## Step 5. Configure a Sender Address

1. Return to the **Overview** page and click **Sender Address**.
2. On the **Sender Address** page, click **Create**.
3. Set the following parameters:
	- Sender Domain: select a **verified** sender domain created in [step 4](#Step4).
	- Email Prefix: for example, `test`.
	- Sender Name: for example, `Lil C`.
>!Your sender address should be a full email address suffixed with a **verified** sender domain.
>For example, <code>test@example.qcluodmail.com</code>.

4. Click **Submit** to complete the sender address configuration.

<span id ="Step6"></span>
## Step 6. Configure a Template
1. Return to the **Overview** page and click **Email Template**.
2. On the **Email Template** page, click **Create**.
3. Set the following parameters:
	- Template Name: for example, `test`.
	- Template Type: select **HTML rich text**.
	- Email Summary: for example, `notification email template`.
	- Email Body: click **Choose a file** and select an HTML file as the email body.
>?The email content can be in plain text or rich text format. The rich text format requires HTML code prepared in advance. After the template is submitted, it will enter the review stage and can be used upon approval. The review will be finished within one business days.

4. Click **Preview** to preview the email template.

5. Click **Submit** to complete the template configuration.

<span id ="Step7"></span>
## Step 7. Send Emails
After the domain registration is completed and the template is approved, you can send emails via the SES console or API calls.
1. Click **Email Sending** to go to the email sending page.
>?This page is only for testing email sending. Up to 20 recipient addresses are allowed for a single test. You can send emails to more recipients at a time via API calls. For more information, please see [here](https://intl.cloud.tencent.com/document/product/1084/39408).
2. Set the following parameters:
 - Template: select an **approved** template created in [step 6](#Step6).
 - Subject: enter the corresponding email subject.
 - From: select a sender address configured in [step 5](#Step5).
 - To: enter the email addresses to which you want to send the email.
 - Variables: enter the corresponding variables.
3. After the email is sent successfully, click [Statistics](https://console.cloud.tencent.com/ses/stats) to view the statistics.

