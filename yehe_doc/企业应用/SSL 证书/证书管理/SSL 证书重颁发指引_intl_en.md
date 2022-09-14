## Overview  
This document describes how to reissue an SSL certificate, in case your certificate key has been compromised, or you need to generate a new certificate due to other reasons.

>?
>- Certificate reissue is only available if **your certificate has been issued and its remaining effective time is longer than 30 days**.
>- Each free DV certificate can only be reissued once.
>- If the certificate of a sub-domain under a primary domain is being reissued, certificates of other sub-domains under this primary domain cannot be reissued at the same time.
>- During the reissue process, the reissue feature of this certificate is disabled, and you cannot apply for a reissue for this certificate again.
>- Certificate reissue will not renew the certificate. In other words, the validity period will be the same as the original one,

## Preparations  
Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) and successfully applied for an SSL certificate.

## Directions
### Selecting certificate reissue
1. Go to the **My Certificates** page and select the certificate to reissue. Then, click **More** > **Reissue**.
![](https://main.qcloudimg.com/raw/2c5c3623d0467555e13a8d4836afea16.png)
2. Go to the **Certificate re-issuance application** page and verify your certificate or submit the required materials based on your certificate type. For more information, see [Reissuing different types of certificates](#issue).



### [Reissuing different types of certificates](id:issue)
<dx-tabs>
::: Wotrus/DNSPod（OV/EV）
**Reissuing Wotrus international standard certificates and DNSPod SM (SM2) OV/EV certificates**
1. On the **Certificate re-issuance application** page, select a CSR algorithm, enter and confirm the configurations, and click **Next**.
  - **Using the CSR of the original certificate**: Use the CSR of the original certificate.
  - **Generating a CSR online**: Generate and manage the CSR by Tencent Cloud SSL Certificate Service.
  - **Using an existing CSR**: Paste the content of an existing CSR to the certificate.
  - **Binding the certificate to a domain**: Enter a single domain, such as `tencent.com` or `ssl.tencent.com`.
  - **Selecting an algorithm**: Select the encryption algorithm for the certificate to be reissued.
  - **Key length**: Select the key length for the certificate to be reissued.
  - **Private key password**: To ensure the security of your private key, **password recovery is NOT supported**, so keep the password in mind.
<b>Note：</b>
If you need to deploy Tencent Cloud services such as CLB and CDN, don′t enter the private key password.

  - **Reissue reason**: Enter the reissue reason in brief.
2. In the pop-up window, click **Confirm**.
3. Validate the domain ownership on the “Domain Ownership Validation” page, and click **Validate Now** after operations are completed.
4. Manual approval is required upon domain ownership validation, and then the certificate will be reissued. For validation instructions, see Domain Ownership Validation.

<b>Note：</b>
- If you have successfully applied for this certificate, manual approval is omitted when the enterprise info submitted in re-application is consistent with that recorded in the system.
- If the span between the reissue submission time and original issue time is less than 3 days, domain ownership validation is not required.
- If the submitted CSR is different from that of the original certificate, domain ownership needs to be validated. If they are the same, validation is not needed.

:::
::: OV/EV certificates of other brands
**Reissuing OV/EV certificates of other brands**
1. On the **Certificate re-issuance application** page, select a CSR algorithm, confirm other configurations, and click **Next**.
  - **Using the CSR of the original certificate**: Use the CSR of the original certificate.
  - **Generating a CSR online**: Generate and manage the CSR by Tencent Cloud SSL Certificate Service.
  - **Using an existing CSR**: Paste the content of an existing CSR to the certificate.
  - **Binding the certificate to a domain**: Enter a single domain, such as `tencent.com` or `ssl.tencent.com`.
  - **Selecting an algorithm**: Select the encryption algorithm for the certificate to be reissued.
  - **Key length**: Select the key length for the certificate to be reissued.
  - **Private key password**: To ensure the security of your private key, **password recovery is NOT supported**, so keep the password in mind.

<b>Note：</b>
If you need to deploy Tencent Cloud services such as CLB and CDN, don′t enter the private key password.

  - **Reissue reason**: Enter the reissue reason in brief.
2. In the pop-up window, click **Confirm**.
3. CA will contact you offline for identity verification. Please pay heed to your emails and phone calls.
:::
::: Paid DV certificates
**Reissuing paid DV certificates**
1. On the **Certificate re-issuance application** page, select a CSR algorithm, enter and confirm the configurations, and click **Confirm**.
  - **Using the CSR of the original certificate**: Use the CSR of the original certificate.
  - **Generating a CSR online**: Generate and manage the CSR by Tencent Cloud SSL Certificate Service.
  - **Using an existing CSR**: Paste the content of an existing CSR to the certificate.
  - **Binding the certificate to a domain**: Enter a single domain, such as `tencent.com` or `ssl.tencent.com`.
  - **Selecting an algorithm**: Select the encryption algorithm for the certificate to be reissued.
  - **Key length**: Select the key length for the certificate to be reissued.
  - **Private key password**: To ensure the security of your private key, **password recovery is NOT supported**, so keep the password in mind.

<b>Note：</b>
If you need to deploy Tencent Cloud services such as CLB and CDN, don′t enter the private key password.

  - **Reissue reason**: Enter the reissue reason in brief.
2. In the pop-up window, click **Confirm**.
3. Validate the domain ownership on the “Domain Ownership Validation” page, and click **Validate Now** after operations are completed. For validation methods, see Domain Ownership Validation.

<b>Note：</b>
If your DV certificate is purchased from TrustAsia (2-year or 3-year wildcard domain) and have configured auto-DNS verification or auto-file verification for the domain you are applying for, ownership verification is not required.
4. After the domain is verified, the reissue is completed.

<b>Note：</b>
- In the last 13 months, if domain ownership verification has been completed for the certificate to be reissued using the same organization name, domain ownership verification is not required.
- If the span between the reissue submission time and original issue time is less than 3 days, domain ownership validation is not required.
- If the submitted CSR is different from that of the original certificate, domain ownership needs to be verified. If they are the same, verification is not needed.

:::
::: Free DV certificates
**Reissuing free DV certificates**
1. On the **Certificate re-issuance application** page, enter and confirm the configurations, and click **Next**.
  - **Selecting an algorithm**: Select the encryption algorithm for the certificate to be reissued.
  - **Private key password**: To ensure the security of your private key, please keep the password in mind as **password recovery is NOT supported**.
<b>Note：</b>
If you need to deploy Tencent Cloud services such as CLB and CDN, don′t enter the private key password.
2. In the pop-up window, click **Confirm**.
3. Go to the **Domain ownership validation** page. The validation method that is used when you first applied for this certificate will be used. You can perform validation as you did before.
4. The certificate will be reissued upon successful domain ownership validation. For domain ownership validation, see instructions for domain ownership validation.
:::
</dx-tabs>

