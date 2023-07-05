## Overview  
This document describes how to reissue an SSL certificate, in case your certificate key has been compromised, or you need to generate a new certificate due to other reasons.

>?
>- Certificate reissue is only available if **your certificate has been issued and its effective time is longer than 30 days**.
>- Each free DV certificate can only be reissued once.
>- If the certificate of a sub-domain under a primary domain is being reissued, other sub-domains under this primary domain cannot be reissued at the same time.
>- During the reissue process, the reissue feature of this certificate is disabled, and you cannot apply for a reissue for this certificate again.
>- Certificate reissue will not renew the certificate. In other words, the validity period will be the same as the original one,

## Prerequisites  
You have logged in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) and successfully applied for an SSL certificate.

## Directions
### Selecting certificate reissue
1. Go to the **My Certificates** management page and select the certificate to reissue. Then, click **More** > **Reissue**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/2c5c3623d0467555e13a8d4836afea16.png)
2. Go to the **Certificate re-issuance application** page and verify your certificate or submit the required materials based on your certificate type. For more information, please see [Reissuing different types of certificates](#issue).


<span id="issue"></span>
### Reissuing different types of certificates


#### OV/EV certificates of other brands
**Reissuing OV/EV certificates of other brands**
1. On the **Certificate re-issuance application** page, select a CSR algorithm, confirm other configurations, and click **Next**.
  - **Using the CSR of the original certificate**: The CSR of the original certificate is used.
  - **Generating a CSR online**: The CSR is generated and managed by Tencent Cloud SSL Certificate Service.
  - **Using an existing CSR**: Paste the content of an existing CSR to the certificate.
  - **Binding the certificate to a domain**: Enter a single domain, for example, `tencent.com` and `ssl.tencent.com`.
  - **Selecting an algorithm**: Select the encryption algorithm for the certificate to be reissued.
  - **Key length**: Select the key length for the certificate to be reissued.
  - **Private key password**: To ensure the security of your pirate key, please keep the password in mind as **password recovery is NOT supported**.
  >?If you need to deploy Tencent Cloud services such as CLB and CDN, please don′t enter the private key password.

  - **Reissue reason**: Enter the reissue reason in brief.
2. In the pop-up window, click **Confirm**.
3. CA will contact you offline for you to complete identity verification. Please pay heed to your emails and phone calls at that time.

#### Paid DV certificates
**Reissuing paid DV certificates**
1. On the **Certificate re-issuance application** page, select a CSR algorithm, enter and confirm the configurations, and click **Confirm application**.
  - **Using the CSR of the original certificate**: The CSR of the original certificate is used.
  - **Generating a CSR online**: The CSR is generated and managed by Tencent Cloud SSL Certificate Service.
  - **Using an existing CSR**: Paste the content of an existing CSR to the certificate.
  - **Binding the certificate to a domain**: Enter a single domain, for example, `tencent.com` and `ssl.tencent.com`.
  - **Selecting an algorithm**: Select the encryption algorithm for the certificate to be reissued.
  - **Key length**: Select the key length for the certificate to be reissued.
  - **Private key password**: To ensure the security of your pirate key, please keep the password in mind as **password recovery is NOT supported**.
  >?If you need to deploy Tencent Cloud services such as CLB and CDN, please don′t enter the private key password.

  - **Reissue reason**: Enter the reissue reason in brief.
2. In the pop-up window, click **Confirm**.
3. Go to the **Domain verification** page to verify the ownership of the domain. After this, click **Verify Now**. For more information about how to verify a domain, please see [Domain Verification](https://intl.cloud.tencent.com/document/product/1007/30168).

4. After the domain is verified, the reissue is completed.

>?
>- In the last 13 months, if domain ownership verification has been completed for the certificate to be reissued using the same organization name, domain ownership verification is not required.
>- If the span between the reissue submission time and original issue time is less than 3 days, domain ownership verification is not required.
>- If the submitted CSR is different from that of the original certificate, domain ownership needs to be verified. If they are the same, verification is not needed.

#### Free DV certificates
**Reissuing free DV certificates**

1. On the **Certificate re-issuance application** page, enter and confirm the configurations, and click **Next**.
  - **Selecting an algorithm**: Select the encryption algorithm for the certificate to be reissued.
  - **Private key password**: To ensure the security of your pirate key, please keep the password in mind as **password recovery is NOT supported**.
  >?If you need to deploy Tencent Cloud services such as CLB and CDN, please don′t enter the private key password.
2. In the pop-up window, click **Confirm**.
3. Go to the **Domain verification** page. The verification method that is used when you first applied for this certificate will be used. You can verify as you did before.
4. After the domain is verified, the reissue is completed. For more information about how to verify a domain, please see [Domain Verification](https://intl.cloud.tencent.com/document/product/1007/30168).
