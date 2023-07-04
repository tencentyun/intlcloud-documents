## Overview

This document describes how to permanently delete an expired or revoked SSL certificate from the certificate list in the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview).

## Prerequisites
- The SSL certificate has expired or been revoked or its review has been canceled.
  

   > **Notes**
   > 
   >   - You can delete an expired certificate at any time.
   >   - If a certificate has not expired, you must revoke it before deleting it. Revoking a certificate is deregistering an issued certificate from the issuing authority. After the certificate is revoked, the encryption effect is lost and the browser does not trust the certificate any more. For detailed directions, see [Revoking an SSL Certificate](https://intl.cloud.tencent.com/document/product/1007/44062).
   >   - If you have applied for a certificate, you can delete it only after the review is canceled.

- You can delete a third-party certificate manually uploaded to the SSL Certificate Service for management at any time.
  

   > **Notes**
   > 
   >   - Make sure that the SSL certificate has not been deployed on any Tencent Cloud product such as WAF and CDN.
   >   - If a certificate has been deployed on a Tencent Cloud product, deleting it may interrupt the business of that product.


## Directions
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and click **My Certificates** on the left sidebar.

2. On the **My Certificates** page, view the target certificate and perform the corresponding operation based on its status:

  - For a certificate uploaded for hosting: Click **More** > **Delete**. 

  - For an expired or revoked certificate or a certificate with its review canceled: Click **Delete**. 

3. In the **Note** pop-up window, click **OK**.
