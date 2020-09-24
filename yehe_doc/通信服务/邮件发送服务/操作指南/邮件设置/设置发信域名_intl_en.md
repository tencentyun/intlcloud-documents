## Setting Sender Domain
Setting the sender domain is the first step to use DMS. You can send emails only with a verified sender domain, which is like an ID number used in emailing. DMS requires you to verify your ownership of the sender domain, which helps improve your credibility at your email service provider during emailing.

When the entire domain name is verified, all email addresses under it will be verified; for example, if you have verified _example.com_, you can send emails from _user1@example.com_, _user2@example.com_, or any other user addresses under _example.com_.

**Create a domain name**
1.  Log in to the [DMS Console](https://console.cloud.tencent.com/dms).
2.  On the left sidebar in the console, click **Email Settings** > **Sender Domain** > **Add Domain Name**, and a dialog box for adding domain name will pop up.
3.  In the dialog box, enter your domain name, select its **type**, and click **OK** to create the domain name.

We recommend you comply with the following requirements when creating a sender domain:

-   Use a domain name that can identify your organization.
-   Use a sub-domain name to avoid affecting the primary domain name by issues such as emailing reputation.
-  Use a domain name that has not been configured with a domain name resolution related to emailing so to avoid verification failure due to multiple resolutions.
-   Create two different domain names for triggered and batch emails, respectively. DMS provides different emailing policies for different domain names based on emailing operations.

**Domain name configuration**

After creating a domain name, you need to complete required configuration first to use it. Such configuration items are the basis of successful email delivery from the domain name.

1.  In the domain name list on the **Sender Domain** page, click **Configure** for the target domain name to enter the domain name configuration page.
![Image from Gyazo](https://main.qcloudimg.com/raw/265d8e4186a4c7f804bf09b4fdad4d1e.png)
-   SPF verification  
    Sender Policy Framework (SPF) is an email verification standard designed to prevent email spoofing. The domain owner uses SPF to notify the email service provider of which servers are allowed to send emails from the domain.
    
-   DKIM verification
	DomainKeys Identified Mail (DKIM) is a standard that allows the sender to use an encrypted key as the email signature, which can be used by the email service provider to check whether the email is tampered with by any third party during delivery.
	
-   DMARC verification
	Domain-based Message Authentication, Reporting, and Conformance (DMARC) is an email authentication protocol that uses SPF and DKIM to detect email spoofing. To meet the DMARC standards, emails must be authenticated through SPF and/or DKIM.
	
-   MX verification  
    A mail exchanger (MX) record points to an email server and is used by the email system to locate the email server based on the recipient address suffix during emailing.

2. Complete the configuration on your DNS server based on the above configuration information.
3.  After completing the configuration, return to the **Domain Name Management** page. In the domain name list, click **Verify** for the domain name or wait for the system to automatically update. It will take 1–10 minutes for the configuration to take effect.
        
>If the domain name status is **Pending verification**, at least one configuration item failed to be verified. You can click **Configure** to view the specific verification result of each item.
>If the domain name status is **Verified**, you can use all sender addresses under this domain name to send emails.

**Note:**
- Please configure a correct sender domain and make sure that SPF and MX resolutions always point to the server address required by DMS; otherwise, emailing will fail.
- You can verify up to five sender domains. Once verified, a domain name cannot be deleted.
- For domain name configuration examples, please see [Domain Name Configuration](https://intl.cloud.tencent.com/document/product/1070/38232).