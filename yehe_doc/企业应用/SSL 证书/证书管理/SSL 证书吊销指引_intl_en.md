## Overview

To facilitate the management of certificates that are no longer needed, Tencent Cloud provides the certificate revocation feature. You can apply for revocation of SSL certificates on Tencent Cloud.
Generally, you may revoke SSL certificates in the following scenarios:
- You do not need to continue using the issued certificates.

- For security reasons, the issued certificates are no longer used.
  

   > **Notes**
   > 
   > If an issued certificate has not expired, you can delete it from the certificate list only after the certificate is revoked. A certificate that has not been revoked cannot be deleted.
   > 


## Must-Knows
<table>
<tr>
<td rowspan="1" colSpan="1" >Certificate Type</td>
<td rowspan="1" colSpan="1" >Notes</td>
</tr>
<tr>
<td rowspan="3" colSpan="1" >All certificates</td>
<td rowspan="1" colSpan="1" >After the application for revoking an SSL certificate is submitted, the certificate cannot be downloaded or deployed. In addition, certificate revocation cannot be canceled. Therefore, exercise caution when revoking a certificate.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >After the SSL certificate revocation application is submitted and approved, the SSL certificate is deregistered from the issuing authority. After the certificate is revoked, the encryption effect is lost and the browser does not trust the certificate any more.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >You can use the SSL certificate revocation feature to revoke only certificates issued in Tencent Cloud but not any uploaded third-party certificates.</td>
</tr>
<tr>
<td rowspan="3" colSpan="1" >Non-WoTrus international standard certificates and DNSPod Chinese SM (SM2) certificates</td>
<td rowspan="1" colSpan="1" >You cannot revoke certificates that will expire within 30 days and are in the "to be renewed" status.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >To revoke a reissued order, you need to revoke the original one, and the reissued order will be automatically revoked along with the original one.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >You cannot revoke certificates issued before March 25, 2020 on your own. If you have such needs, [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance.</td>
</tr>
</table>




## Prerequisites

You have logged in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl).

## Directions

> **Notes**
> 
> If the domain bound to the SSL certificate you apply for has expired and been deleted, and you need to revoke the certificate and perform related parsing operations, [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance.
> 


### Selecting the certificate to revoke
1. Go to the **My Certificates** page, select the target certificate, and click **More** > **Revoke**.

2. On the **Certificate Revocation Request** page, validate your certificate or submit the required information based on your certificate type. For more information, see [Revoking different types of certificates](https://write.woa.com/#certificate).



   > **Notes**
   > 
   > After the certificate is revoked successfully, the certificate enters the revoked status. You can log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) and delete the certificate from the Tencent Cloud system.
   > 


### 

Revoking different types of certificates

#### Revoking DNSPod Chinese SM (SM2) DV and WoTrus certificates
1. On the **Certificate Revocation Request** page, enter the revocation reason in the **Revocation Information** area.

2. Click **Next** to complete the revocation application.

3. Reviewers manually review the revocation information. After the review is passed, the certificate will be formally revoked.


#### Revoking DNSPod GM (SM2) EV and OV certificates
1. On the **Certificate Revocation Request** page, enter the revocation reason in the **Revocation Information** area.

2. Click **Next** to upload the certificate revocation application.

3. Click **Download application template** and enter application information in the template.

4. Upload a photo or scan of the application stamped with the official seal.

5. Click **Upload** to upload the application and click **Next**.
   

   > **Notes**
   > 
   >   - The application file can be up to 1.4 MB in JPG, GIF, or PDF format.
   >   - After the application file is uploaded, it cannot be uploaded again. Make sure that the application file is uploaded correctly.

6. Reviewers manually review the revocation information. After the review is passed, the certificate will be formally revoked.


#### Revoking other DV certificates
1. On the **Certificate Revocation Request** page, click **Next** to submit an SSL certificate revocation application.

2. After submitting the SSL certificate revocation application, configure the verification information as instructed as soon as possible.
   

   > **Notes**
   >   - If your DV certificate is purchased from TrustAsia (2-year or 3-year wildcard domain) and you have configured automatic DNS or file validation for the domain you are applying for, ownership verification is not required.
   >   - If your certificate originally adopts the automatic DNS validation mode but now the conditions for automatic validation are not met, the manual DNS validation mode will be automatically adopted.
   >   - If the certificate adopts the DNS validation mode, add DNS records within three days; otherwise, the revocation will fail. The certificate will be revoked after the successful validation. For detailed directions, see [DNS Validation](https://intl.cloud.tencent.com/document/product/1007/45895).
   >   - If the certificate adopts the file validation mode, add file records within three days and make sure that the files can be accessed successfully; otherwise, the revocation will fail. The certificate will be revoked after the successful validation. For detailed directions, see [File Validation](https://intl.cloud.tencent.com/document/product/1007/43542).


#### Revoking OV/EV certificates of other brands
1. On the **Certificate Revocation Request** page, enter the revocation reason in the **Revocation Information** area.

2. Click **Next** to upload the certificate confirmation letter.

3. Click to **download the confirmation letter template** and enter information in the confirmation letter.

4. Upload a photo or scan of the confirmation letter stamped with the official seal.

5. Click **Upload** to upload the confirmation letter and click **Next**.
   

   > **Notes**
   > 
   >   - The confirmation letter file can be up to 1.4 MB in JPG, PNG, or PDF format.
   >   - If automatic DNS or file validation has been configured for the domain applied for, you do not need to upload the confirmation letter.

6. Reviewers manually review the revocation information. After the review is passed, the certificate will be formally revoked.
