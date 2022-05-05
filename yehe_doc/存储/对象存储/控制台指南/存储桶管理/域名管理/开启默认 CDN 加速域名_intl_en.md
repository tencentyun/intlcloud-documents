## Overview
This document describes how to enable a default CDN acceleration domain name.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5). Click **Bucket List** on the left sidebar to open the Bucket List page.
2. Click on the bucket for which to configure the domain name to enter the bucket configuration page.

3. Select **Domains and Transfer** > **Default CDN Acceleration Domain** on the left sidebar, click **Edit**, and toggle **Status** on to configure the following information:
 - **Acceleration Region**: Choose **Mainland China**, **Outside China mainland**, or **Global**, where the last means allowing global bucket acceleration across all regions.
 - **Origin Server Type**: **Default Endpoint** is selected by default. If you have enabled static website for the origin bucket and want to accelerate content delivery for the static website, select **Static Website Endpoint**.
		![](https://main.qcloudimg.com/raw/f6b32eea091da0d4d9c72e670c7135e8.png)
 - **Origin-pull Authentication**: For public-read buckets, you don't need to enable **Origin-pull Authentication**. For private-read buckets, enable [Origin-pull Authentication](#step1) after adding CDN service authorization.
>**Domain Management** is inaccessible if you have never used the CDN service. To activate it, go to the [CDN console](https://console.cloud.tencent.com/cdn).
4. Click **Save** to activate CDN acceleration.
>For private-read buckets, if both origin-pull authentication and CDN service authorization are enabled, signature is not required for access to origin server via CDN, and cached resources in CDN will be distributed over the public network, which will affect data security. Therefore, we recommend that you enable CDN authentication.


<span id="step1"></span>
#### Enabling origin-pull authentication

For a private-read bucket, authorize the CDN service before you can enable origin-pull authentication.
1. Click **Add CDN Service Authorization** in the **Default CDN Acceleration Domain** area, and follow the on-screen instructions to complete the authorization.
![](https://main.qcloudimg.com/raw/f6b32eea091da0d4d9c72e670c7135e8.png)
2. Toggle on **Origin-pull Authentication** to enable origin-pull authorization for your bucket.
3. Click **Save** to activate CDN acceleration.
4. After clicking **Save**, you can see the default acceleration domain has been enabled, with the status of **CDN authentication** displayed at the bottom. Click **Authentication Configuration** to begin the authentication.
 ![](https://main.qcloudimg.com/raw/3b12f1a208662a170c9e829c88006ce3.png)
5. Go to the [CDN console](https://console.cloud.tencent.com/cdn), and click **Domain Management** > **Manage** (for the domain you want) > **Security Configuration**. For detailed authentication configuration directions, see [Authentication Configuration Instruction](https://intl.cloud.tencent.com/document/product/228/35237).
