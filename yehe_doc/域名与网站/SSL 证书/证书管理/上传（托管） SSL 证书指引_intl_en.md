## Overview

You can upload all your SSL certificates to the SSL Certificate Service console for unified management. This document describes how to upload certificates.

## Directions

>?
> 
> If your certificate failed to be uploaded, troubleshoot as instructed in ["DNS Query Failed. Check Whether the Certificate Conforms to the Standard" Is Prompted During Certificate Upload](https://www.tencentcloud.com/document/product/1007/53582).
> 


### Uploading an international standard certificate
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), go to the **My Certificates** page, and click **Upload Certificate**.

2. In the **Upload Certificate** pop-up window, select **International standard** and enter the relevant information as shown below:
   

   >?
   > 
   >   - If you download the certificate from Tencent Cloud, upload it by using files in the Nginx folder.
   >   - If you download the certificate from another service provider, contact it for assistance.



  - **Certificate Name**: Enter a certificate name.

  - **Signature Certificate**:

    - A certificate is usually a file with an extension such as .crt or .pem. Please use a text editor to open the certificate file and copy the certificate to the **Certificate** text box.

    - The certificate should start with "-----BEGIN CERTIFICATE-----" and end with "-----END CERTIFICATE-----".

    - The certificate content should include the complete certificate chain.

  - **Signature Private Key**:

    - A private key is usually a file with an extension such as .key and .pem. Please use a text editor to open the private key file and copy the private key to the corresponding text box.

    - The private key starts with "-----BEGIN (RSA) PRIVATE KEY-----" and ends with "-----END (RSA) PRIVATE KEY-----".

  - **Tag**: Select your tag key and tag value to better manage existing Tencent Cloud resources by category.
    

      >?
      > 
      > You can add a tag as instructed in [Querying Resources by Tag](https://intl.cloud.tencent.com/document/product/651/32582).
      > 

  - **Project**: Select a project for the certificate.

3. Click **Upload** to upload the certificate to the certificate list.


### Uploading a Chinese SM (SM2) certificate
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), go to the **My Certificates** page, and click **Upload Certificate**.

2. In the **Upload Certificate** pop-up window, select **Chinese SM (SM2)** and enter the relevant information as shown below:
   

   >?
   > 
   >   - If you download the certificate from Tencent Cloud, upload it by using files in the Nginx folder.
   >   - If you download the certificate from another service provider, contact it for assistance.


  - **Certificate Name**: Enter a certificate name.

  - **Signature Certificate**:

    - A certificate is usually a file with an extension such as .crt or .pem. Please use a text editor to open the certificate file and copy the certificate to the **Certificate** text box.

    - The certificate should start with "-----BEGIN CERTIFICATE-----" and end with "-----END CERTIFICATE-----".

    - The certificate content should include the complete certificate chain.

  - **Signature Private Key**:

    - A private key is usually a file with an extension such as .key and .pem. Use a text editor to open the private key file and copy the private key to the corresponding text box of the certificate.

    - The private key starts with "-----BEGIN EC PRIVATE KEY-----" and ends with "-----END PRIVATE KEY-----".

  - **Encryption Certificate**:

    - A certificate is usually a file with an extension such as .crt or .pem. Please use a text editor to open the certificate file and copy the certificate to the **Certificate** text box.

    - The certificate should start with "-----BEGIN CERTIFICATE-----" and end with "-----END CERTIFICATE-----".

    - The certificate content should include the complete certificate chain.

  - **Encryption Private Key**:

    - A private key is usually a file with an extension such as .key and .pem. Use a text editor to open the private key file and copy the private key to the corresponding text box of the certificate.

    - The private key starts with "-----BEGIN PRIVATE KEY-----" and ends with "-----END PRIVATE KEY-----".
      

         >?
         > 
         > A private key file with an extension such as .key or .pem is provided by default for a DNSPod Chinese SM certificate. It is required for both the signature private key and encryption private key.
         > 

  - **Tag**: Select your tag key and tag value to better manage existing Tencent Cloud resources by category.
    

      >?
      > 
      > You can add a tag as instructed in [Querying Resources by Tag](https://intl.cloud.tencent.com/document/product/651/32582).
      > 

  - **Project**: Select a project for the certificate.

3. Click **Upload** to upload the certificate to the certificate list.


## Subsequent Operations

You can deploy the uploaded certificate to a cloud service.