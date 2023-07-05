## Overview

This document describes how to reissue an SSL certificate, in case your certificate key has been compromised, or you need to generate a new certificate due to other reasons.

>?
> 
> - Certificate reissue is available only if your certificate **has been issued and will expire in more than 30 days**.
> - Each free DV certificate can be reissued only once.
> - If the certificate of a subdomain under a primary domain is being reissued, certificates of other subdomains under this primary domain cannot be reissued at the same time.
> - In the reissue process, the reissue feature of the certificate is disabled, and you cannot apply for a reissue for this certificate again.
> - Certificate reissue will not renew the certificate. In other words, the validity period will be the same as the original one.


## Prerequisites

Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) and successfully applied for an SSL certificate.

## Directions

### Selecting the certificate to be reissued
1. Go to the **My Certificates** page, select the target certificate, and click **More** > **Reissue**.

2. Go to the **Certificate Reissue Application** page and verify your certificate or submit the required information based on your certificate type. For more information, see [Reissuing different types of certificates](https://write.woa.com/#issue).

### Reissuing different types of certificates



[WoTrus/DNSPod (OV/EV)]

**Reissuing WoTrus international standard certificates and DNSPod Chinese SM (SM2) OV/EV certificates**
1. On the **Certificate re-issuance application** page, select a CSR algorithm, enter and confirm the configurations, and click ****Next**.

  - **Using the CSR of the original certificate**: Use the CSR of the original certificate.

  - **Generating a CSR online**: Generate and manage the CSR by Tencent Cloud SSL Certificate Service.

  - **Using an existing CSR**: Paste the content of an existing CSR to the certificate.

  - **Binding the certificate to a domain**: Enter a single domain, such as `tencent.com` or `ssl.tencent.com`.

  - **Selecting an algorithm**: Select the encryption algorithm for the certificate to be reissued.

  - **Key length**: Select the key length for the certificate to be reissued.

  - **Private key password**: To ensure the security of your private key, **password recovery is NOT supported**, so keep the password in mind.


>?
> 
> If you need to deploy the SSL certificate to Tencent Cloud services such as CLB and CDN, do not enter the private key password.
> 

  - **Reissue reason**: Enter the reissue reason in brief.

2. In the pop-up window, click **Confirm**.

3. Validate the domain ownership on the “Domain Ownership Validation” page, and click **Validate Now** after operations are completed.

4. After your domain is validated, wait for manual approval, upon which the certificate will be reissued. For more information on how to validate a domain, see [Domain Validation Guide](https://www.tencentcloud.com/document/product/1007/53581).


>?
> 
> - If you have successfully applied for this certificate and the organization information submitted in the re-application is consistent with that recorded in the system, manual approval is not required.
> - If the span between the reissue submission time and original issue time is less than three days, domain validation is not required.
> - If the submitted CSR is different from that of the original certificate, domain validation is required; otherwise, it is not required.


[Other brands (OV/EV)]

**Reissuing OV/EV certificates of other brands**
1. On the **Certificate re-issuance application** page, select a CSR algorithm, confirm other configurations, and click **Next**.

  - **Using the CSR of the original certificate**: Use the CSR of the original certificate.

  - **Generating a CSR online**: Generate and manage the CSR by Tencent Cloud SSL Certificate Service.

  - **Using an existing CSR**: Paste the content of an existing CSR to the certificate.

  - **Binding the certificate to a domain**: Enter a single domain, such as `tencent.com` or `ssl.tencent.com`.

  - **Selecting an algorithm**: Select the encryption algorithm for the certificate to be reissued.

  - **Key length**: Select the key length for the certificate to be reissued.

  - **Private key password**: To ensure the security of your private key, **password recovery is NOT supported**, so keep the password in mind.


>?
> 
> If you need to deploy the SSL certificate to Tencent Cloud services such as CLB and CDN, do not enter the private key password.
> 

  - **Reissue reason**: Enter the reissue reason in brief.

2. In the pop-up window, click **Confirm**.

3. CA will contact you offline for identity verification. Please pay heed to your emails and phone calls.


[(DV) Paid]

**Reissuing paid DV certificates**
1. On the **Certificate re-issuance application** page, select a CSR algorithm, enter and confirm the configurations, and click ****Confirm**.

  - **Using the CSR of the original certificate**: Use the CSR of the original certificate.

  - **Generating a CSR online**: Generate and manage the CSR by Tencent Cloud SSL Certificate Service.

  - **Using an existing CSR**: Paste the content of an existing CSR to the certificate.

  - **Binding the certificate to a domain**: Enter a single domain, such as `tencent.com` or `ssl.tencent.com`.

  - **Selecting an algorithm**: Select the encryption algorithm for the certificate to be reissued.

  - **Key length**: Select the key length for the certificate to be reissued.

  - **Private key password**: To ensure the security of your private key, **password recovery is NOT supported**, so keep the password in mind.


>?
> 
> If you need to deploy the SSL certificate to Tencent Cloud services such as CLB and CDN, do not enter the private key password.
> 

  - **Reissue reason**: Enter the reissue reason in brief.

2. In the pop-up window, click **Confirm**.

3. On the **Validate Domain** page, verify the domain ownership and click **Validate**. For more information on how to validate a domain, see [Domain Validation Guide](https://www.tencentcloud.com/document/product/1007/53581).


>?
> 
> If your DV certificate is purchased from TrustAsia (2-year or 3-year wildcard domain) and you have configured automatic DNS or file validation for the domain you are applying for, ownership verification is not required.
> 

4. After the domain is verified, the reissue is completed.


>?
> 
> - In the last 13 months, if domain identity verification has been completed for the certificate to be reissued using the same organization name, domain validation will not be performed.
> - If the span between the reissue submission time and original issue time is less than three days, domain validation is not required.
> - If the submitted CSR is different from that of the original certificate, domain validation is required; otherwise, it is not required.


[(DV) Free]

**Reissuing free DV certificates**
1. On the **Certificate re-issuance application** page, enter and confirm the configurations, and click **Next**.

  - **Selecting an algorithm**: Select the encryption algorithm for the certificate to be reissued.

  - **Private key password**: To ensure the security of your private key, **password recovery is NOT supported**, so keep the password in mind.


>?
> 
> If you need to deploy the SSL certificate to Tencent Cloud services such as CLB and CDN, do not enter the private key password.
> 

2. In the pop-up window, click **Confirm**.

3. Go to the **Domain ownership validation** page. The validation method that is used when you first applied for this certificate will be used. You can perform validation as you did before.

4. After your domain is validated successfully, the certificate will be reissued. For more information on how to validate a domain, see [Domain Validation Guide](https://www.tencentcloud.com/document/product/1007/53581).
