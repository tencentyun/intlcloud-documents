## Overview

With Tencent Cloud resource hosting, a new SSL certificate can be automatically deployed to the same Tencent Cloud resources such as CLB and CDN as the original certificate after successful renewal and issue (or reapplication for a free certificate).

After a new SSL certificate is issued, you can enable Tencent Cloud resource hosting and bind relevant Tencent Cloud resources. When this SSL certificate is renewed and a new certificate is generated, the Tencent Cloud resources bound to the original certificate will be automatically bound to the new one.

> **Notes**
> 
> - Tencent Cloud resource hosting will not automatically install a new certificate to the web application on your server. Therefore, you still need to manually install the new certificate issued after the renewal to your web service (to replace the original one) even if Tencent Cloud resource hosting is enabled. If your SSL certificate is only deployed to Tencent Cloud resources, this hosting feature will automate the entire process.
> - Tencent Cloud resource hosting is free of charge.


## Strengths of Tencent Cloud resource hosting

For SSL certificate deployment to Tencent Cloud resources, after you have deployed a certificate to Tencent Cloud resources for the first time and enabled resource hosting, Tencent Cloud will take over the deployment of additional certificates you apply for.

## Use limits
- After Tencent Cloud resource hosting is enabled for the original certificate, automatic deployment to Tencent Cloud resources will take effect only if the SSL certificate applied for has the same specifications as the original one, including domain type, certificate type, and certificate brand.

- After Tencent Cloud resource hosting is enabled for a paid certificate, the certificate issued after this certificate is renewed can be automatically deployed to Tencent Cloud resources.

- After Tencent Cloud resource hosting is enabled for a free certificate, the certificate issued after this certificate is reapplied for can be automatically deployed to Tencent Cloud resources.


## Directions
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) and go to the **My Certificates** page.

2. On the **My Certificates** page, select the target certificate and click the **Certificate Name** to enter the **Certificate Details** page.

3. In the **Basic Info** module, click **View** in **Tencent Cloud Resource Hosting**.

4. In the **Tencent Cloud Resource Hosting** pop-up window, select the target Tencent Cloud resources.

5. Click **OK** to complete the operation.
