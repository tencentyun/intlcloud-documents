## Overview
This document only describes how to add a custom acceleration domain name and enable CDN acceleration on the COS Console. For more information on how to add a custom domain name using the CDN Console, see [Connecting Domain Names](https://intl.cloud.tencent.com/document/product/228/5734). 
>A maximum of 10 custom domain names can be added on the COS Console.

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5). Click **Bucket List** on the left sidebar to open the Bucket List page.
2. Click on the bucket for which to configure the domain name to enter the bucket configuration page.

3. Select **Domain and transmission management** > **Custom CDN Acceleration Domain**, click **Add domains** to configure the following options. 
**Domain**: Enter the custom domain name to be bound (e.g. `www.example.com`). Ensure that the domain name in Mainland China has obtained ICP filing, and a corresponding CNAME has been configured for the domain name with the DNS service provider. For more information, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).
**Acceleration Region**: supports CDN acceleration for Mainland China, Hong Kong, China, and overseas regions, and global acceleration for buckets across all regions.
**Origin Server Type**: You can select “Default origin server” or “Static website origin server”. Select the first option unless your bucket has enabled Static Website. If you want to use your custom acceleration domain name as static website, select “Static website origin server” here and enable Static Website on your bucket.
**Authentication**: Enable origin-pull authentication. For private-read buckets, enable **Origin-pull Authentication** to protect the origin server.
![](https://main.qcloudimg.com/raw/1278367aed8eada850c00fa4d5e18a4b.png)

>For private-read buckets, if both origin-pull authentication and CDN service authorization are enabled, signature is not required for accessing the origin via CDN, and cached resources in CDN will be distributed on the public network, which will affect the data security. Therefore, we recommend that you enable CDN authentication (Step 5).

4. After the configuration, click **Save** on the operation column on the right to add the domain name. After it is saved, the Enable button for CDN authentication appears in the **Authentication** column. You can click the button to enable the CDN authentication for custom domain name.
   **CDN Authentication:** timestamp authentication can be configured to prevent stealing by malicious users. You can enable the feature after adding the domain name.
5. Log in to [CDN Console](https://console.cloud.tencent.com/cdn/access). In the left sidebar, click **Domain Management**.
6. Locate the domain name you need to configure, click **Management** under Actions on the right to open the domain management page, and then click **Security Configuration** at the top. For more information, see [Authentication Configuration](https://intl.cloud.tencent.com/document/product/228/35237).

>After CDN acceleration is enabled for a domain name, anyone can directly access the origin server via the domain name. Therefore, if you need to keep your data private, be sure to protect your data in the origin server through **Authentication Configuration**.
