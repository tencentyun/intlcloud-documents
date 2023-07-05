## Overview

This document describes how to deploy an SSL certificate to CDN.

## Prerequisites

You have logged in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and obtained the certificate successfully.

## Directions

>!
> 
> - The domain should be already connected to CDN and in "deploying" or "enabled" status. You cannot deploy a certificate for a disabled domain. For detailed directions, see [Adding Domain Names](https://www.tencentcloud.com/document/product/228/5734).
> - If CDN acceleration is enabled for COS or CI, certificates cannot be configured for the domain `.file.myqcloud.com` or `.image.myqcloud.com` by default.
> - Currently, certificates cannot be configured for SVN hosted origins.

1. Click the **Issued** tab, select the target certificate, and click **Certificate Details**.

2. On the **Certificate Details** page, click **Quick Deployment**.

3. In the **Select a deployment type** pop-up window, select **CDN** and click **OK**.

4. Go to the **Configure certificate** page in the [CDN console](https://console.cloud.tencent.com/cdn), which displays the corresponding **domain name**, **certificate source**, and **certificate ID**.

5. Select the origin-pull protocol. You can select the origin-pull method for getting resources from the origin by the CDN node.

  - If **HTTP** Origin-pull is selected, the requests sent from users to CDN nodes support HTTPS/HTTP, and the requests sent from CDN nodes to the origin server all use HTTP.

  - If you have selected **Follow protocol** for origin-pull, the origin server must have a valid certificate deployed; otherwise, origin-pull may fail. When the deployment is complete, the requests sent from CND nodes to the origin server follows the same protocol as the requests sent from users to CDN nodes, using either HTTP or HTTPS. 

  - If the HTTPS port on the domain name's origin server is modified to a port number other than 443, the configuration will fail.

  - Domain names connected with the COS origin or FTP origin only support using HTTP as the origin-pull method.

6. After the configuration is completed, you can view the configured domain and certificate on the **Certificate Management** page.
