## Overview
If you purchased an OV (including OV Pro) or EV (including EV Pro) SSL certificate (see [Purchasing Process](https://intl.cloud.tencent.com/document/product/1007/30159) for details), you need to submit relevant information.
After CA approves the information, the certificate will be issued. You can download and install the paid certificate.

## Prerequisites
1. You have logged in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and clicked **Pending Submission**.
2. You have selected the desired certificate and clicked **Submit Information**.

## Directions
>!The information required varies by certificate type. This document uses a multi-domain certificate as an example.
>
### Step 1. Enter the domain name
Select one of the following CSR generation methods as needed.
- Select **Generate CSR Online** to [generate the CSR online](#csr1) (**this option is recommended, and the CSR and private key can be generated**).
- Select **Paste CSR** to [paste the CSR](#csr2) (**no private key can be generated with this option**).

**[Generate a CSR online](id:csr1)**
1. Enter the domain name information, as shown below:
![](https://main.qcloudimg.com/raw/fc8ce0770690f9d8767f0ae6e359ec87.jpg)
Main parameters are described as follows:
 - **Algorithm**: Select an encryption algorithm type for your certificate as needed.
 - **Key Length**: Select the key length for your certificate.
 - **Bound Domain**: Enter a single domain to bind to the certificate, such as `tencent.com` or `ssl.tencent.com`.
 - **Other Domains**: Enter other domains to bound to the certificate. Note that they cannot be the same as the common name and cannot be modified after submitted to the CA.
 >?This parameter is not available for single-domain certificates.
 - **Private Key Password**: This field is optional and cannot be modified or restored once entered. Please keep the password in mind.
 >?If you need to deploy Tencent Cloud services such as CLB or CDN, don′t set the private key password.
>
2. Enter your organization information.
    - **Existing Organization**: You can use the information of an existing organization directly.
    - **New organization information**: Enter your organization’s full name, department, city, address, and landline number.
3. Enter the administrator information.
    - **Existing administrator**: You can use the information of an existing administrator directly.
    - **New administrator information**: Enter the administrator’s name, position, phone number, and email.
4. Enter the contact information. You can check **Same as the administrator**.
5. Click **Next** to go to [Step 2](#message).

**[Paste the CSR](id:csr2)**
1. Paste the CSR information into the text box (your domain information will be detected), enter the organization information (you can also select **Existing Organization**), administrator information (you can also select **Existing administrator**), and contact information (you can check **Same as administrator**), as shown in the following figure.

2. Click **Next** to go to [Step 2](#message).


### [Step 2. Upload the confirmation letter](id:message)
>!
>- If you use the organization and administrator information in [My Profile](https://console.cloud.tencent.com/ssl/info) that has been reviewed, you don’t need to upload the confirmation letter.
>- If you use GlobalSign certificates, you still need to upload the confirmation letter.
>- For GlobalSign EV certificates, the CA will email you the documents required for review in 2–3 business days after you submit the information, and you do not need to upload them to the console.
>
1. Click **Download Confirmation Letter** and fill it out as shown below:

2. Fill out the confirmation letter, stick your organization's official stamp, and scan the document.
3. Click **Upload** to upload the confirmation letter. Then, click **Next**.
>? 
>- The confirmation letter must be smaller than or equal to 1.4 MB in JPG, PNG, or PDF format.
>- After the confirmation letter is uploaded, you can re-upload the confirmation letter and modify the information during the manual review process.
>
4. In the **Confirmation letter uploaded successfully** pop-up window, click **OK**, as shown in the following figure. Then, you can wait for the CA to confirm and review your information.

### Step 3. Wait for CA’s manual review
After you upload the confirmation letter, the CA will contact you for identity verification. Please check your email and phone calls.
>?It takes 3−5 business days to review OV certificates, and 5−7 business days to review EV certificates.

### Step 4. Wait for CA to issue the certificate
After the review is completed, the CA will issue your certificate. You can download and install it.
