## Notes
- If your domain is hosted in Tencent Cloud, log in to the [DNSPod console](https://console.cloud.tencent.com/cns) to configure the domain verification information; otherwise, configure it as needed.
- After the sender domain is configured and verified, make sure that MX, SPF, DKIM, and DMARC are configured correctly; otherwise, a sending exception may occur.
- Do not use a corporate email domain; otherwise, a configuration information conflict might occur.
- After the domain is configured, synchronization may take 5 minutes to 2 hours. Please wait for the verification to complete.
- Each Tencent Cloud account can be configured with up to 10 domains.

## Preparations
### 1. Logging in to the SES console
Log in to the [SES console](https://console.cloud.tencent.com/ses). If you do not have a Tencent Cloud account yet, then sign up for one first as instructed in [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985).
If you are prompted to verify your identity, complete identity verification in the [Account Center](https://console.cloud.tencent.com/developer). For detailed directions, see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).
### 2. Activating the SES service
Click **Activate SES**. 

## Directions
### Step 1. Configure the sender domain[](id:Step1)
>! A domain that has been registered for Tencent Exmail cannot be used as a sender domain.

1. Log in to the [SES console](https://console.cloud.tencent.com/ses) and click **Sender Domain**.
2. Click **Create** on the **Sender Domain** page.
3. Enter a sender domain in the **Domain** field, for example, `mail.qcloud.com`, and click **Submit**.[](id:Step3)
>! A sender domain is the basis of an email address and represents the sender's corporate identity. To verify a sender domain, you need to configure the DNS information for it. Therefore, you must have the admin permissions on the domain.

4. Click **Verify** and configure the DNS information of the domain based on the record value on the **Sender Domain** page.
   
	 >?For more information on how to perform domain verification, see [Identity Verification and Configuration](https://intl.cloud.tencent.com/document/product/1084/42371).
5. After the DNS configuration is completed, click **Submit** on the sender domain page. After the verification is passed, the status of the sender domain will become **Verified**.

### Step 2. Configure the sender address[](id:Step2)

1. Go back to the **Overview** page and click **Sender Address**.
2. Click **Create** on the **Sender Address** page.
3. Set the following parameters as needed:
	- Sender Domain: Select the **verified** sender domain created in [step 1](#Step3).
	- Email Prefix: Enter an email prefix, for example, `test`.
	- Sender Name: Enter a sender name, for example, `Lil C`.
>! A sender address should be a full email address suffixed with a **verified** sender domain.
> Example: <code>test@example.qcloudmail.com</code>.

4. Click **Submit** to complete the sender address configuration.
