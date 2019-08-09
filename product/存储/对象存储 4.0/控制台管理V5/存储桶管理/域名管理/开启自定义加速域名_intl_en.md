## Overview

This document only describes how to add a custom accelerated domain name and enable CDN acceleration on the COS Console. For more information on how to add a custom domain name on the CDN Console, see [Domain Names Access](https://intl.cloud.tencent.com/document/product/228/5734).

> A maximum of 10 custom domain names can be added on the COS Console.

### Procedure

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5). Click **Bucket List** on the left sidebar to open the Bucket List page.
2. Click the bucket for which you need to set a domain name to go the COS configuration page, as shown below:
![](https://main.qcloudimg.com/raw/3eed29ea9c5fbb974fd459552d1d00ae.png)
3. Click **Domain Management** at the top, click **Add Domain** in the column **Custom Acceleration Domain**, and configure as follows:
 - **Domain Name**: Enter the custom domain name to be bound (e.g. `www.example.com`). Ensure that the domain name entered has gone through the filing procedure, and that CNAME corresponding to this domain name has been set at the DNS service provider for the domain name. For more information, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).
 - **Origin-pull Authentication**: Enable origin-pull authentication. For private-read buckets, enable **Origin-pull Authentication** to protect the origin server.
![](https://main.qcloudimg.com/raw/1278367aed8eada850c00fa4d5e18a4b.png)
> For private-read buckets, if both origin-pull authentication and CDN service authorization are enabled, then signature is not required for accessing the origin server via CDN, and cached resources in CDN will be distributed on the public network, which will affect the data security. Therefore, it is recommended to enable CDN authentication (Step 5).
4. After the configuration, click **Save** on the operation column on the right to add the domain name. After it is saved, the Enable button for CDN authentication appears in the **CDN Authentication** column. You can click the button to enable the CDN authentication for custom domain name.
**CDN Authentication:**Timestamp authentication can be configured to prevent stealing by malicious users. You can enable the feature after adding the domain name.
5. Log in to [CDN Console](https://console.cloud.tencent.com/cdn/access). On the left sidebar, click **Domain Name Management**.
6. Locate the domain name you need to configure, click **Management** on the operation column on the right to go to the domain name management page, and then click **Security Configuration** at the top. For more information, see [Authentication Configuration](https://cloud.tencent.com/document/product/228/33115).

> After CDN acceleration is enabled for a domain name, anyone can directly access the origin server via the domain name. Therefore, if you need to keep your data private, be sure to protect your data in the origin server through **Authentication Configuration**.

