After you successfully purchase an OV, OV Pro, EV, or EV Pro SSL certificate (for more information, see the purchase process), you need to submit relevant information for review.
After the CA approves the information, it will issue the certificate officially, which you can download for installation.

### Entry for Information Submission
1. Log in to the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl).
2. On the "Certificate List" page, select a certificate you have purchased and click "Submit info", as shown below:
![](https://main.qcloudimg.com/raw/6c27ff363427df1a493a3feaf1f4ae62.jpg)

### Entering the Domain Name
Select the CSR generation method based on your actual needs.
- Select "Generate CSR online" to [generate the CSR online](#csr1).
- Select "Paste CSR" to [paste the CSR](#csr2).

**Generate CSR online**<span id="csr1"></span>

>The information required varies by certificate type. Below is an example with a multi-domain name certificate.

1. Enter the domain name information, as shown below:
![](https://main.qcloudimg.com/raw/fc8ce0770690f9d8767f0ae6e359ec87.jpg)
Main parameters include:
 - Generic Name: Enter the domain name/wildcard domain name to be bound to the certificate.
 - Domain Name: Enter domain names/wildcard domain names other than the generic name.
>This parameter is not available for single-domain name certificates.
 - Private Key Password: This is optional and cannot be modified once entered.
2. Enter your organization information.
>?Please truthfully enter the information of your organization, including full name, department, city, address, and landline number.
>
3. Click **Next** to [provide additional information](#message).

**Paste CSR**<span id="csr2"></span>

>The information required varies by certificate type. Below is an example with a single-wildcard domain name certificate.

1. Paste the prepared CSR information into the text box, enter the domain name information, and truthfully enter the information of your organization, including full name, department, city, address, and landline number, as shown below:
![](https://main.qcloudimg.com/raw/5374fcbc0ad212a8ff10697c664bc069.jpg)
2. Click **Next** to [provide additional information](#message).

<span id="message"></span>
### Providing Additional Information
1. Enter the information of the manager and the contact. If they are the same person, select "Same as the manager", as shown below:
    ![](https://main.qcloudimg.com/raw/ecb42402bcbf11cacd0617d288ae368e.jpg)
2. Click **Next**.

### Waiting for Approval
After the certificate information is submitted, the certificate status will change to "pending verification". You need to wait for the review staff to verify the information by phone and confirm the domain name via email. It usually take 3-5 business days to issue an OV certificate and 5-7 business days to issue an EV certificate.

![](https://main.qcloudimg.com/raw/d73e322ce3806abc67f6a9ac96f5dd29.jpg)