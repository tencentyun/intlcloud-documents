## Overview
This article shows you how to turn on a custom accelerated domain name. The steps are as follows.

### Procedure
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5). Click **Bucket List** on the left sidebar to open the Bucket List page.
2. Click the bucket for which you need to set a domain name to go the COS configuration page, as shown below:
![](https://main.qcloudimg.com/raw/e7864a63d1a7a1c1cde36d186b067c97.png)
3. Click **Domain Name Management** at the top, click **Edit** in the **Default Accelerated Domain Name**, set the current status of the default accelerated domain name to **Enabled**, and configure as follows:
 - **Origin Server Type**: The origin server type usually defaults to **Default Origin Server**, but if you have enabled static website for the origin server bucket and want to accelerate content delivery for the static website, select **Static Website Origin Server**.
![](https://main.qcloudimg.com/raw/f6b32eea091da0d4d9c72e670c7135e8.png)
 - **Origin-pull Authentication**: For public-read buckets, you don't need to enable **Origin-pull Authentication**. For private-read buckets, enable [Origin-pull Authentication](#step1) after adding CDN service authorization.
 > If you have never used Tencent Cloud CDN service, you need to go to CDN Console to activate CDN service before you can access **Domain Name Management**.
4. Click **Save** to acactivate CDN acceleration.
> For private-read buckets, if both origin-pull authentication and CDN service authorization are enabled, signature is not required for the access to origin server via CDN, and cached resources in CDN will be distributed on the public network, which will affect the data security. Therefore, it is recommended to enable CDN authentication.

<span id="step1"></span>
#### Enabling origin-pull authentication
1. For private-read buckets, **Origin-pull Authentication** needs to be enabled provided that CDN service authorization is added.
2. Enable **Origin-pull Authentication** on the bucket domain name management page. (CDN service authorization must be added before it is enabled.)
![](https://main.qcloudimg.com/raw/f6b32eea091da0d4d9c72e670c7135e8.png)
3. Click **Save** to activate CDN acceleration.
4. After clicking **Save**, you can see the default accelerated domain name is under deployment. The status of **CDN authentication** is displayed at the bottom. Click **Authentication Configuration** to configure authentication, as shown below:
![](https://main.qcloudimg.com/raw/3b12f1a208662a170c9e829c88006ce3.png)
5. You can go to CDN authentication configuration page from [CDN Console](https://console.cloud.tencent.com/cdn) by clicking **Domain Management** -> **Management** for the domain name -> **Security Configuration**. 


