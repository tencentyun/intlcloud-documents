## Overview

After successfully purchasing a DV SSL certificate, you need to submit relevant information for review.
After the CA approves the information, it will issue the certificate, which you can download and install.

## Prerequisites
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and click **Pending Submission**.

2. Click **Submit Information** on the row of the purchased certificate.


## Directions

> **Notes**
> 
> The required information varies by certificate type. Below is an example with a WoTrus DV multi-domain certificate.
> 


### Step 1. Enter a domain

Select one of the following CSR generation methods as needed.
- Select **Online** to [generate the CSR online](https://write.woa.com/#csr1). **We recommend that you generate the CSR online to allow the platform to generate and manage your private and public key certificate files. This avoids losing the private key file.**

- Select **By pasting** to [paste the CSR](https://write.woa.com/#csr2). **No private key can be generated with this option.**


#### Generating the CSR online
1. Enter domain information.
The main parameters are described as follows:

  - **Algorithm**: Select an encryption algorithm as needed.

  - **Key Length**: Select the key length as needed.

  - **Bound Domain**: Enter a single domain to bind to the certificate, such as `tencent.com` or `ssl.tencent.com`.

  - **Other Domains**: Enter other domains to be bound to the certificate. They cannot be common names or be modified after submission to CA.
    

      > **Notes**
      > 
      > This parameter is not available for single-domain certificates.
      > 

  - **Private Key Password**: Optional. The password cannot be modified once entered or recovered, so please keep it in mind.
    

      > **Notes**
      > 
      > If you need to deploy the SSL certificate to Tencent Cloud services such as CLB and CDN, do not enter the private key password.
      > 

2. Enter your organization information.

  - **Existing Organization**: Use the information of an existing organization.

  - **New Organization**: Enter full name, department, city, address, and landline number of your organization.

3. Enter the administrator information.

  - **Existing administrator**: Use the information of an existing administrator.

  - **New administrator**: Enter the administrator’s name, position, phone number, and email.

4. Enter contact information. You may select **Same with the administrator**.

5. Click **Next** to go to [step 2](https://write.woa.com/#message).


#### Pasting the CSR
1. Paste the CSR information into the text box and enter **Domain Information**, **Organization Information** (or select **Existing Organization**), **Administrator Information** (or select **Existing administrator**), and **Contact Information** (or select **Same as the administrator**).

2. Click **Next** to go to [step 2](https://write.woa.com/#message).


### 

Step 2. Select the validation method
1. The **Select Validation Method** page will display the available domain validation methods based on the type and validity period of the purchased certificate and whether the domain is resolved by DNSPod.

  - For a one-year DV certificate: DNS validation/File validation.

  - For a TrustAsia DV certificate (two-year or three-year wildcard domain): Automatic DNS validation/Automatic file validation.

2. Click **Next**.


### Step 3. Validate your domain
1. On the **Validate Domain** page, validate your domain as prompted. For example, if you select DNS validation, the following information will be displayed.

  - For a one-year DV certificate:

    - **DNS validation**: For detailed directions, please see [Domain Ownership Verification](https://intl.cloud.tencent.com/document/product/1007/45895).

    - **File validation**: For detailed directions, please see [Domain Ownership Verification](https://intl.cloud.tencent.com/document/product/1007/43542).

  - For a TrustAsia DV certificate (two-year or three-year wildcard domain):

    - **Automatic file validation**: For detailed directions, see [Automatic File Validation](https://intl.cloud.tencent.com/document/product/1007/44061).

2. After the domain validation is completed, click **View Domain Validation Status** to check whether the validation is successful.
   

>？
>   - The first domain validation for a DNSPod Chinese SM (SM2) DV certificate will remain valid for 13 months from approval.
>   - During the 13 months, no domain validation will be performed if you apply for a DNSPod Chinese SM (SM2) DV SSL certificate with the same organization name for the domain.


### Step 4. Wait for CA to issue the certificate

After the review is completed, the CA will issue your certificate. You can download and install it.