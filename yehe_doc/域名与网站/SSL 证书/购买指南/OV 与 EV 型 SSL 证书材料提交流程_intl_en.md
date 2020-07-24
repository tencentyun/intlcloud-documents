After you successfully purchase an OV, OV Pro, EV, or EV Pro SSL certificate (see [Purchase Procedure](https://intl.cloud.tencent.com/document/product/1007/30159?lang=en&pg=)), you need to submit the relevant information for review.
After the CA approves the information, the official paid certificate will be issued and you can download it for installation.

### Entry for Information Submission
1. Log in to the [SSL Certificate Services Console](https://console.cloud.tencent.com/ssl).
2. On the **Certificate Management** page, select a purchased certificate and click **Submit info**.

### Entering the Domain Name
Select one of the following CSR generation methods based on your actual needs:
- Select "Generate CSR Online" to [generate the CSR online](#csr1) (**this option is recommended, and the CSR and private key can be generated**).
- Select "Paste CSR" to [paste the CSR](#csr2) (**no private key can be generated with this option**).

**Generate CSR online**<span id="csr1"></span>
>The information required varies by certificate type. Below is an example with a multi-domain name certificate.

1. Enter the domain name information.
![](https://main.qcloudimg.com/raw/fc8ce0770690f9d8767f0ae6e359ec87.jpg)
The main parameters are described as follows:
 - Common name: enter the domain name/wildcard domain name to be bound to the certificate.
 - Domain name: enter domain names/wildcard domain names other than the common name.
>This parameter is not available for single-domain name certificates.
 - Private key password: this is optional and cannot be modified once entered.
2. Enter your company information.
>Please enter your organization name (full name), department, city, address, and telephone number.
>
3. Click **Next** to [provide additional information](#message).

**Paste CSR**<span id="csr2"></span>
>The information required varies by certificate type. Below is an example with a single-wildcard domain name certificate.

1. Paste the prepared CSR information into the text box, enter the domain name information, and enter your company name (full name), department, city, address, and telephone number.
![](https://main.qcloudimg.com/raw/5374fcbc0ad212a8ff10697c664bc069.jpg)
2. Click **Next** to [provide additional information](#message).

<span id="message"></span>
### Providing Additional Information
1. Enter the administrator and contact information. If the contact information is the same as the administrator information, you can select **Same as the manager** for **Contact info**.
![](https://main.qcloudimg.com/raw/ecb42402bcbf11cacd0617d288ae368e.jpg)
2. Click **Next**.
3. In the **Submit CSR** window that pops up, click **OK** to submit the CSR.
![](https://main.qcloudimg.com/raw/d73e322ce3806abc67f6a9ac96f5dd29.jpg)

### Uploading for Review
>For GlobalSign EV certificates, the CA will email you the documents required for review in 2–3 business days after you submit the information, and you do not need to upload them to the console.

1. Click **Download Confirmation Letter** and fill it out.
![](https://main.qcloudimg.com/raw/28fcfb8bd19748cccded7f0dc8addc57.png)
2. Fill out the confirmation letter, apply your organization's official stamp, and scan the document.
3. Click **Upload for Review** to upload the confirmation letter.
4. Verify the information displayed in the "Submitted" pop-up window, and click **OK**. TrustAsia and the CA will review the submitted information and notify you when the process is completed.
![](https://main.qcloudimg.com/raw/35b4a13f8b21b330c3ab6c314615e501.png)
