## Overview
After purchasing a Wotrus SSL certificate (OV or EV), you need to submit relevant information. For more information, please see [Purchasing Process](https://intl.cloud.tencent.com/document/product/1007/30159).

## Prerequisites
1. You have logged in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and clicked **Pending Submission**.
2. You have selected the desired certificate and clicked **Submit Information**.

## Directions
>!The information required varies by certificate type. This document uses a multi-domain OV certificate as an example.
>
### Step 1. Enter the domain name
Select one of the following CSR generation methods as needed.
- Select **Generate CSR Online** and then perform operations described in [Generate a CSR online](#csr1) (this option is recommended. Your private key and public key certificate information is generated and managed by the platform to prevent private key loss).
- Select **Paste CSR** to [paste the CSR](#csr2) (**no private key can be generated with this option**).

**[Generate a CSR online](id:csr1)**
1. Enter the domain name information, as shown below:
>?You can go to the **SSL Certificate Service console** > [My Profile](https://console.cloud.tencent.com/ssl/info) to manage the information of **Existing Organization** or **Existing administrator** if it does not meet your requirements.
>

Main parameters are described as follows:
 - **Algorithm**: Select an encryption algorithm for your certificate.
 - **Key Length**: Select the key length for your certificate.
 - **Bound Domain**: Enter a single domain to bind to the certificate, such as `tencent.com` or `ssl.tencent.com`.
 - **Other Domains**: Enter other domains to bound to the certificate. Note that they cannot be the same as the common name and cannot be modified after submitted to the CA.
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
1. Paste the CSR information into the text box (your domain information will be detected), enter or select the existing organization information, administrator information, and contact information, as shown in the following figure.

2. Click **Next** to go to [Step 2](#message).

### [Step. 2. Select the domain validation method](id:message)
1. On the **Select Validation Method** page, select the domain validation method, as shown in the following figure.

2. Click **Next** to go to the **Pre-review** page.


### Step 3. Wait for the pre-review to complete
After you submit the information and select the domain validation method, your certificate will be pre-reviewed, which usually takes **10 minutes−72 hours**.


### Step 4. Validate your domain
1. Validate the domain ownership by referring to the message displayed on the **Validate Domain** page. For example, if you have selected manual DNS validation, the following message will be displayed. Please go to the corresponding DNS hosting provider to add the DNS record, as shown in the following figure.

You can validate your domain as follows:
 - **DNS validation**: For detailed directions, please see [Domain Ownership Verification](https://intl.cloud.tencent.com/document/product/1007/30168).
 - **File validation**: For detailed directions, please see [Domain Ownership Verification](https://intl.cloud.tencent.com/document/product/1007/30168).
2. After the domain validation is completed, you can click **View Domain Validation Status** to see whether the validation is successful or not.

### Step 5. Wait for the manual review to complete
After your domain is validated, the CA will review the information submitted and call you to complete the validation.
>?It takes 3−5 business days to review OV certificates, and 5−7 business days to review EV certificates.
>

### Step 6. Wait for CA to issue the certificate
After the review is completed, the CA will issue your certificate. You can download and install it.
>?
>- The certificate will be issued only if both the manual review and domain validation are passed.
>- After you applied, there will be a manual review, during which you will receive a call from the US to your organization’s business registration number.
