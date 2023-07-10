## Overview

This document describes how to enable the default CDN acceleration domain name.

>!Starting from May 9, 2022, COS will stop supporting default CDN acceleration domain names for buckets that have never used them. This change will not affect buckets that are using or once used default CDN acceleration domain names. However, we recommend you switch to custom CDN acceleration domain names instead. For more information on custom CDN acceleration domain names, see [Enabling Custom CDN Acceleration Domain Name](https://intl.cloud.tencent.com/document/product/436/31506).


## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the target bucket to enter the **Bucket Configuration** page.
4. On the left sidebar, select **Domains and Transfer** > **Default CDN Acceleration Domain** and click **Edit**.
5. Enable **Default CDN Acceleration Domain** and configure the following options:
 - **Acceleration Region**: CDN acceleration is supported for the Chinese mainland, outside the Chinese mainland, as well as global acceleration for buckets across all regions.
 - **Origin Type**: The origin type usually defaults to **Default Endpoint**, but if you have enabled static website for the origin bucket and want to accelerate content delivery for the static website, select **Static Website Endpoint**.
![](https://main.qcloudimg.com/raw/f6b32eea091da0d4d9c72e670c7135e8.png)
 - **Origin-pull Authentication**: For public-read buckets, you don't need to enable origin-pull authentication. For private-read buckets, you need to [enable origin-pull authentication](#step1) after adding CDN service authorization.
>? **Domain Management** is inaccessible if you have never used the CDN service. To activate it, go to the [CDN console](https://console.cloud.tencent.com/cdn).
>
4. Click **Save**.
>! For private-read buckets, if both origin-pull authentication and CDN service authorization are enabled, signature is not required for access to the origin through CDN, and cached resources in CDN will be delivered over the public network, which will affect the data security. Therefore, we recommend you enable CDN authentication.
>

<span id="step1"></span>

#### Enabling origin-pull authentication

For a private-read bucket, authorize the CDN service before you can enable origin-pull authentication.

1. On the **Default CDN Acceleration Domain** configuration page, click **Add CDN Service Authorization** and proceed as prompted.
![](https://main.qcloudimg.com/raw/f6b32eea091da0d4d9c72e670c7135e8.png)
2. Toggle on **Origin-pull Authentication** to enable origin-pull authentication for your bucket.
3. Click **Save**.
After clicking **Save**, you can see the default CDN acceleration domain name has been enabled, with the status of **CDN Authentication** displayed at the bottom. Click **Authentication Configuration** to begin the configuration.
![](https://main.qcloudimg.com/raw/3b12f1a208662a170c9e829c88006ce3.png)
For more information on how to configure CDN authentication, see the **Authentication Configuration** section in [Instruction](https://intl.cloud.tencent.com/document/product/228/35237).
