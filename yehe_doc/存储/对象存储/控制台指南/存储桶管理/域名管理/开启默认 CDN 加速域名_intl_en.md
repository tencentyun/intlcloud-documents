## Overview
This document describes how to enable a custom acceleration domain name following the directions below:

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Click the bucket for which you need to set a domain name and enter the COS configuration page.
![](https://main.qcloudimg.com/raw/e7864a63d1a7a1c1cde36d186b067c97.png)
3. Click **Domain Name Management** on the left, click **Edit** in **Default CDN Acceleration Domain**, set the status to **On**, and configure as follows:
	- **Origin Server Type**: The origin server type usually defaults to **Default Origin Server**, but if you have enabled static website for the origin server bucket and want to accelerate content delivery for the static website, select **Static Website Origin Server**.
		![](https://main.qcloudimg.com/raw/f6b32eea091da0d4d9c72e670c7135e8.png)
	- **Origin-pull Authentication**: For public-read buckets, you don't need to enable **Origin-pull Authentication**. For private-read buckets, enable [Origin-pull Authentication](#step1) after adding CDN service authorization.
>**Domain Management** is unaccessible if you have never used the CDN service. To activate it, go to the [CDN Console](https://console.cloud.tencent.com/cdn).
4. Click **Save** to activate CDN acceleration.
>For private-read buckets, if both origin-pull authentication and CDN service authorization are enabled, signature is not required for access to origin server via CDN, and cached resources in CDN will be distributed on the public network, which will affect data security. Therefore, we recommended you enable CDN authentication.


<span id="step1"></span>
#### Enabling origin-pull authentication

If the bucket permission is private-read, authorize the CDN service and enable origin-pull authentication.
1. In the Domain Management page, click **Add CDN Service Authorization**, and follow the on-screen instructions to authorize the CDN service.
![](https://main.qcloudimg.com/raw/f6b32eea091da0d4d9c72e670c7135e8.png)
2. Switch on the “Origin-pull Authentication” button to enable origin-pull authorization for your bucket.
3. Click **Save** to activate CDN acceleration.
4. After clicking **Save**, you can see the default acceleration domain has been enabled, with the status of **CDN authentication** displayed at the bottom. Click **Authentication Configuration** to begin the authentication.
 ![](https://main.qcloudimg.com/raw/3b12f1a208662a170c9e829c88006ce3.png)
5. Go to the [CDN Console](https://console.cloud.tencent.com/cdn), and click **Domain Management** > **Manage** (for the domain you want) > **Security Configuration**. For detailed authentication configuration directions, see [Authentication Configuration Instruction](https://intl.cloud.tencent.com/document/product/228/35237).
