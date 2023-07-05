## Overview
You can upload all your SSL certificates to the SSL Certificate Service console for unified management. This document describes how to upload certificates.
>?Currently, SM2 certificates cannot be uploaded.

## Prerequisites
You have logged in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl).


## Directions
1. Click **My Certificates** > **Upload Certificate**.
![](https://main.qcloudimg.com/raw/8d68c7890edf5b01ad1159e3ae1e62b0.png)
2. Set information as required in the **Upload Certificate** dialog box.
![](https://main.qcloudimg.com/raw/0f7abc105e0f709df73f8c146d051007.png)
 - **Alias**: please enter a certificate name.
 - **Certificate**:
    - A certificate is usually a file with an extension such as .crt or .pem. Please use a text editor to open the certificate file and copy the certificate to the **Certificate** text box.
    - The certificate should start with "-----BEGIN CERTIFICATE-----" and end with "-----END CERTIFICATE-----".
    - The certificate content should include the complete certificate chain.
 - **Private key**:
    - A private key is usually a file with an extension such as .key and .pem. Please use a text editor to open the private key file and copy the private key to the corresponding text box.
    - The private key starts with "-----BEGIN (RSA) PRIVATE KEY-----" and ends with "-----END (RSA) PRIVATE KEY-----".

3. Click **Upload** to upload the certificate to the certificate list.

## Subsequent Operations
You can deploy the uploaded certificate to a cloud service.
