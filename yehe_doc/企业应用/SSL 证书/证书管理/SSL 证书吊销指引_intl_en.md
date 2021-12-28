## Overview
To facilitate the management of certificates that are no longer needed, Tencent Cloud provides the certificate revocation feature. You can apply for revocation of SSL certificates on Tencent Cloud.
Generally, you may revoke SSL certificates in the following scenarios:
- You do not need to continue using the issued certificates.
- For security reasons, the issued certificates are no longer used.

>?If an issued certificate has not expired, you can delete it from the certificate list only after the certificate is revoked. A certificate that has not been revoked cannot be deleted.

## Notes
<table>
<tr>
<th>SSL Certificate Type</th>
<th>Notes</th>
</tr>
<tr>
<td rowspan="3">All certificates</td>
<td>After the application for revoking an SSL certificate is submitted, the certificate cannot be downloaded or deployed. In addition, certificate revocation cannot be canceled. Therefore, exercise caution when revoking a certificate.</td>
</tr>
<tr><td>After the SSL certificate revocation application is submitted and approved, the SSL certificate is deregistered from the issuing authority. After the certificate is revoked, the encryption effect is lost and the browser does not trust the certificate any more.</td></tr>
</tr>
<tr><td>Tencent Cloud SSL certificate revocation supports only certificates issued on Tencent Cloud, and third-party certificates uploaded to the Tencent Cloud do not support revocation.</td></tr>
<tr><td rowspan="3">Non-Wotrus international standard certificates and DNSPod GM (SM2) certificates</td><td>A certificate that is valid within 30 days and is to be renewed cannot be revoked.</td></tr>
<tr><td>A reissued certificate cannot be revoked. If revocation is required, you need to revoke the original certificate, and the reissued certificate will be automatically revoked together with the original certificate.</td></tr>
<tr><td>The self-service revocation feature is temporarily unavailable for certificates issued before March 25, 2020. To revoke such certificates, please contact <a href="https://intl.cloud.tencent.com/contact-sales">online technical support</a>.</td></tr>
</table>

## Prerequisite
You have logged in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl).

## Directions
>?If the domain name bound to the SSL certificate you apply for has expired and been deleted, and you need to revoke the certificate and perform related parsing operations, please [contact us](https://intl.cloud.tencent.com/contact-sales).
>
### Selecting the certificate to revoke
1. Go to the **My Certificates** page and select the certificate to revoke. Then, click **More** > **Revoke**, as shown in the following figure.

2. Go to the **Certificate Revocation Request** page and verify your certificate or submit the required materials based on your certificate type. For more information, please see [Revoking different types of certificates](#certificate).
    The following figure shows the revocation application page for a free TrustAsia DV SSL certificate.


>?After the certificate is revoked successfully, the certificate enters the revoked state, and you can log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), and delete the certificate from the Tencent Cloud system.


### [Revoking different types of certificates](id:certificate)
#### Revoking DNSPod GM (SM2) DV and Wotrus certificates
1. On the **Certificate Revocation Request** page, enter the revocation reason in the **Revocation Information** area.
2. Click **Next** to complete the revocation application.
3. Reviewers manually review the revocation information. After the review is passed, the certificate will be formally revoked.

#### Revoking DNSPod GM (SM2) EV and OV certificates
1. On the **Certificate Revocation Request** page, enter the revocation reason in the **Revocation Information** area.
2. Click **Next** to upload the certificate revocation application.
3. Click **Download application template** and enter application information in the template.
4. Upload a photo or scan of the application stamped with the official seal.
5. Click **Upload** to upload the application and click **Next**.
>?
>- The application file must be smaller than or equal to 1.4 MB in JPG, GIF, or PDF format.
>- After the application file is uploaded, it cannot be uploaded again. Ensure that the application file is uploaded correctly.
6. Reviewers manually review the revocation information. After the review is passed, the certificate will be formally revoked.


#### Revoking other DV certificates
1. On the **Certificate Revocation Request** page, click **Next** to submit an SSL certificate revocation application.
2. After submitting the SSL certificate revocation application, configure the verification information as instructed as soon as possible.
>?
>- If your DV certificate is purchased from TrustAsia (2-year or 3-year wildcard domain) and you have configured automatic DNS or file validation for the domain you are applying for, ownership verification is not required.
>- If your certificate originally adopts the automatic DNS validation mode but now the conditions for automatic validation are not met, the manual DNS validation mode will be automatically adopted.
>- If the certificate adopts the DNS validation mode, please add DNS records within 3 days. Otherwise, the revocation will fail. The certificate will be revoked after successful validation.
>- If the certificate adopts the file validation mode, please add file records within 3 days and ensure that the files can be accessed successfully. Otherwise, the revocation will fail. The certificate will be revoked after the successful validation. For related operations, please see [File Validation](https://intl.cloud.tencent.com/document/product/1007/43542).


#### Revoking OV/EV certificates of other brands
1. On the **Certificate Revocation Request** page, enter the revocation reason in the **Revocation Information** area.
2. Click **Next** to upload the certificate confirmation letter.
3. Click to **download the confirmation letter template** and enter information in the confirmation letter.
4. Upload a photo or scan of the confirmation letter stamped with the official seal.
5. Click **Upload** to upload the confirmation letter and click **Next**.
>?
>- The confirmation letter file must be smaller than or equal to 1.4 MB in JPG, PNG, or PDF format.
>- If automatic DNS or file validation has been configured for the domain name applied for, you do not need to upload the confirmation letter.
6. Reviewers manually review the revocation information. After the review is passed, the certificate will be formally revoked.
