## Overview
If you purchase an OV (including OV Pro) or EV (including EV Pro) SSL certificate (see [Purchasing Process](https://intl.cloud.tencent.com/document/product/1007/30159) for details), you need to submit materials as required.
After CA approves the materials, the certificate will be issued. You can download and install the paid certificate.

## Preparations
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and click **Pending Submission**.
2. Select the desired certificate and click **Submit Materials**.

## Directions
>!The information required varies by certificate type. A multi-domain certificate is taken as an example here.
>
### Step 1. Enter a domain name
Select one of the following CSR generation methods as needed.
- Select **Generate a CSR online** to [generate a CSR online](#csr1) (**Recommended, with a CSR and a private key generated**).
- Select **Paste CSR** to [paste the CSR](#csr2) (**CSR uploaded automatically, with no private key generated**).

**[Generate a CSR online](id:csr1)**
1. Enter domain information.

The main parameters are described as follows:
 - **Algorithm**: Select an encryption algorithm type for your certificate as needed.
 - **Key Length**: Select the key length for your certificate.
 - **Bound Domain**: Enter a single domain to be bound to the certificate, such as `tencent.com` or `ssl.tencent.com`.
 >?Some certificate brands support binding IP addresses. For details, see [SSL Certificates Supporting IP Address Binding](https://intl.cloud.tencent.com/document/product/1007/43937).
 >
 - **Other Domains**: Enter other domains to be bound to the certificate. They cannot be common names or be modified after submission to CA.
>?This parameter is not available for single-domain certificates.
 - **Private Key Password**: Optional. The password cannot be modified once entered or recovered, so please keep it in mind.
>?If you need to deploy Tencent Cloud services such as CLB or CDN, don′t set the private key password.
>
2. Enter your organization information.
    - **Existing Organization**: Use the information of an existing organization.
    - **New Organization**: Enter full name, department, city, address, and landline number of your organization.
3. Enter the administrator information.
    - **Existing administrator**: Use the information of an existing administrator.
    - **New administrator**: Enter the administrator’s name, position, phone number, and email.
4. Enter contact information. You may select **Same with the administrator**.
5. Click **Next** to go to [Step 2](#message).

**[Paste the CSR](id:csr2)**
1. Paste the CSR information into the text box (to detect domain information), enter organization information (or select **Existing Organization**), administrator information (or select **Existing administrator**), and contact information (or select **Same with the administrator**).

2. Click **Next** to go to [Step 2](#message).


### [Step 2. Upload the confirmation letter](id:message)
>!
>- If you use the organization and administrator information in [My Profile](https://console.cloud.tencent.com/ssl/info) that has been reviewed, the confirmation letter can be omitted.
>- For GlobalSign certificates, the confirmation letter is always required.
>- For GlobalSign EV certificates, the CA will email you the documents required for review in 2–3 business days after you submit the information, and you do not need to upload them to the console.
>
1. Click **Download the confirmation letter template** and enter information required in the confirmation letter.

2. Fill out, attach your organization's official seal on and scan the confirmation letter.
3. Click **Upload** and **Next**.
>? 
>- The confirmation letter can be a JPG, PNG, or PDF file of up to 1.4 MB.
>- During the manual review of the confirmation letter, you can re-upload it to modify the information.
>
4. In the **Confirmation letter uploaded successfully** pop-up window, click **OK**. Then, you can wait for the CA to confirm and review your information.


### Step 3. Wait for CA to review
After you upload the confirmation letter, the CA will contact you via your email and phone calls for identity verification.
>?It takes 3−5 business days to review OV certificates, and 5−7 business days to review EV certificates.

### Step 4. Wait for CA to issue the certificate
After the review is completed, the CA will issue your certificate. You can download and install it.

