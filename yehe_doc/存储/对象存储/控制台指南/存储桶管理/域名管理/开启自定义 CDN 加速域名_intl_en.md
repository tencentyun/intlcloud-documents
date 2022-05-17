## Overview

This document only describes how to add a custom acceleration domain name and enable CDN acceleration in the COS console. For more information on how to add a custom domain name in the CDN console, see [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734). 

>?Up to ten custom domain names can be added in the COS console.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the **Bucket List** page.
2. Click the target bucket to enter the **Bucket Configuration** page.
3. Click **Domains and Transfer** > **Custom CDN Acceleration Domain** on the left and click **Add Domain** to configure the following options. (If you have enabled **Custom Domain** in the legacy COS console, **Custom Domain** will be displayed in the new console instead of **Custom CDN Acceleration Domain**.)
   **Domain Name**: Enter the target custom domain name (such as `www.example.com`). Make sure that an ICP filing has been obtained and a CNAME record has been configured at the DNS service provider for the entered domain. For more information, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121). If the custom CDN acceleration domain you are connecting is in the following situations, you need to verify your domain ownership as instructed in [Domain Name Ownership Verification](https://intl.cloud.tencent.com/document/product/228/42693).
     - The domain name is being connected for the first time.
     - The domain name has been connected by another user.
     - The domain name is a wildcard domain name.
   **Acceleration Region**: CDN acceleration is supported for the Chinese mainland, Hong Kong (China), outside the Chinese mainland, and global acceleration for buckets across all regions.
   **Origin Type**: **Default Endpoint** or **Static Website Endpoint**. It is **Default Endpoint** unless you have enabled **Static Website** for your bucket. To use your custom acceleration domain name as static website, select **Static Website Endpoint** and enable **Static Website** for your bucket.
   **Authentication**: Enable origin-pull authentication. For private-read buckets, enable **Origin-pull Authentication** to protect the origin.
   ![](https://main.qcloudimg.com/raw/1278367aed8eada850c00fa4d5e18a4b.png)

> !For private-read buckets, if both origin-pull authentication and CDN service authorization are enabled, then signature is not required for access to the origin through CDN, and cached resources in CDN will be delivered over the public network, which will affect the data security. Therefore, we recommend you enable CDN authentication as instructed in step 5.

4. After completing the configuration, click **Save** in the **Operation** column on the right. After it is saved, the **Enable** button for **CDN Authentication** will appear in the **Authentication** column. You can click the button to enable CDN authentication for custom domain names.
   **CDN Authentication:** Timestamp authentication can be configured to prevent stealing by malicious users. You can enable the feature after adding the domain name.
5. Log in to the [CDN console](https://console.cloud.tencent.com/cdn/access). On the left sidebar, click **Domain Management**.
6. Locate the target domain name, click **Manage** in the **Operation** column on the right to open the **Domain Management** page, and then click **Security Configuration** at the top. For more information, see [Instruction](https://intl.cloud.tencent.com/document/product/228/35237).

> !After CDN acceleration is enabled for a domain name, anyone can directly access the origin through the domain name. Therefore, if you want to keep your data private, be sure to protect your data on the origin through **Authentication Configuration**.
