## Overview
This document only describes how to add a custom acceleration domain name and enable CDN acceleration in the COS console. For more information on how to add a custom domain name using the CDN console, see [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734). 
>A maximum of 10 custom domain names can be added in the COS console.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5). Click **Bucket List** on the left sidebar to open the Bucket List page.
2. Click on the bucket for which to configure the domain name to enter the bucket configuration page.

3. Select **Domains and Transfer** > **Custom CDN Acceleration Domain**, and click **Add Domain** to configure the following options. 
**Domain Name**: Enter the custom domain name to be bound (e.g. `www.example.com`). Ensure that the domain name for content delivery in the Chinese mainland has obtained ICP filing, and a corresponding CNAME has been configured for the domain name with the DNS service provider. For more information, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).
**Acceleration Region**: Supports CDN acceleration for the Chinese mainland, outside the Chinese mainland, and global regions.
**Origin Server Type**: Select **Default Endpoint** or **Static Website Endpoint**. Select the first option unless your bucket has enabled static website. If you want to use your custom acceleration domain name as static website, select **Static Website Endpoint** here and enable static website on your bucket.
**Authentication**: Enable origin-pull authentication. For private-read buckets, enable **Origin-pull Authentication** to protect the origin server.
![](https://main.qcloudimg.com/raw/1278367aed8eada850c00fa4d5e18a4b.png)

>For private-read buckets, if both origin-pull authentication and CDN service authorization are enabled, signature is not required for accessing the origin via CDN, and cached resources in CDN will be distributed on the public network, which will affect the data security. Therefore, we recommend that you enable CDN authentication (Step 5).

4. After the configuration, click **Save** in the **Operation** column on the right to add the domain name. After it is saved, the Enable button for CDN authentication appears next to **CDN Authentication**. You can click the button to enable the CDN authentication for the custom domain name.
   **CDN Authentication:** Timestamp authentication can be configured to prevent stealing by malicious users. You can enable the feature after adding the domain name.
5. Log in to the [CDN console](https://console.cloud.tencent.com/cdn/access) and select **Domain Management** on the left sidebar.
6. Locate the domain name you need to configure, click **Manage** under **Operation** on the right to open the domain management page, and then click **Security Configuration** at the top. For more information, see [Authentication Configuration](https://intl.cloud.tencent.com/document/product/228/35237).

>After CDN acceleration is enabled for a domain name, anyone can directly access the origin server via the domain name. Therefore, if you need to keep your data private, be sure to protect your data in the origin server through **Authentication Configuration**.
