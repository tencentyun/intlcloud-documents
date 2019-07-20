After you successfully purchase an OV, OV Pro, EV, or EV Pro SSL certificate (see purchase process for details), you need to submit relevant information for review.
After the CA approves the information, the official certificate will be issued and you can download the paid certificate for installation.

### Information Submission Portal
1. Log in to the [SSL Certificates Service Console](https://console.cloud.tencent.com/ssl).
2. On the "Certificate List" page, select a certificate you have purchased and click "Submit info", as shown below:
![](https://main.qcloudimg.com/raw/7da48ce027298fe506b847d5421e5b7b.png)

### Entering the Domain Name
Select the CSR generation method based on your actual needs.
- Select "Generate CSR online" to [generate the CSR online](#csr1).
- Select "Paste CSR" to [paste the CSR](#csr2).

**Generate CSR online**<span id="csr1"></span>
>?The information required varies by certificate type. Below is an example with a multi-domain name certificate.

1. Enter the domain name information, as shown below:
![](https://main.qcloudimg.com/raw/58ea9fd0a8c774c3b5dda49b739e932b.png)
Key parameters are as follows:
 - Generic Name: Enter the domain name/wildcard domain name to be bound to the certificate.
 - Domain Name: Enter domain names/wildcard domain names other than the generic name.
>?This parameter is not available for single-domain name certificates.
 - Private Key/Passphrase: This is optional and cannot be modified once entered.
2. Enter your organization information.
>?Please enter the company name (full name), departments, city, address, and telephone number.
>
3. Click **Next** to [provide additional information](#message).

**Paste CSR**<span id="csr2"></span>
>?The information required varies by certificate type. Below is an example with a single-wildcard domain name certificate.

1. Paste the prepared CSR information into the text box, enter the domain name information, and enter the company name (full name), departments, city, address, and telephone number as shown below:
![](https://main.qcloudimg.com/raw/6a1be163c94ff202a34fa8084e0a585c.png)
2. Click **Next** to [provide additional information](#message).

<span id="message"></span>
### Providing Additional Information
1. Fill in the administrator and contact information. If they are the same, you can check "Same as the administrator", as shown below:
![](https://main.qcloudimg.com/raw/f42858c5f9c807f5aa38641b0392041b.png)
2. Click **Next**.
3. In the "Submit CSR" window that pops up, click **OK** to submit the CSR, as shown below:
![](https://main.qcloudimg.com/raw/1ee5d7cbb369c873cbad4614bf402de3.png)

### Uploading for Review
>!For GlobalSign EV certificates, the CA will email you the documents required for review in 2-3 business days after you submit the information, and you do not need to upload them to the console.

1. Click **Download Confirmation Letter** and fill it out as shown below:
![](https://main.qcloudimg.com/raw/69417f911eddb7ad1c5075fe2395e83c.png)
2. Fill out the confirmation letter, apply your organization's official stamp, and scan the document.
3. Click **Upload for Review** to upload the scanned confirmation letter.
4. Verify the information displayed in the "Submitted" pop-up window,  and click **OK**. TrustAsia and the CA will review the submitted information and notify you when the process is completed.
![](https://main.qcloudimg.com/raw/b2b6c66130f6537ed10695b6e49535bf.png)
