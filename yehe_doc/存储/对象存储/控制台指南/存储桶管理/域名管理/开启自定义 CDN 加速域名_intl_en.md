## Overview

This document only describes how to add a custom acceleration domain name and enable CDN acceleration in the COS console. For more information on how to add a custom domain name in the CDN console, see [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734). 

>? Up to ten custom domain names can be added in the COS console.
>

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the **Bucket List** page.
2. Click the target bucket to enter the **Bucket Configuration** page.
3. Click **Domains and Transfer** > **Custom CDN Acceleration Domain** on the left, click **Add Domain**, and configure the following options:
>? If you have enabled **Custom Domain** in the legacy console, you will see **Custom Domain** instead of **Custom CDN Acceleration Domain** displayed in the current console.
>
![](https://main.qcloudimg.com/raw/1278367aed8eada850c00fa4d5e18a4b.png)
  - **Domain Name**: Enter the target custom domain name (such as `www.example.com`). Make sure that an ICP filing has been obtained and a CNAME record has been configured at the DNS service provider for the entered domain. For more information, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121). If the custom CDN acceleration domain you are connecting is in the following situations, you need to verify your domain ownership as instructed in [Domain Name Ownership Verification](https://intl.cloud.tencent.com/document/product/228/42693).
     - The domain name is being connected for the first time.
     - The domain name has been connected by another user.
     - The domain name is a wildcard domain name.
  - **Acceleration Region**: CDN acceleration is supported for the Chinese mainland, outside the Chinese mainland, as well as global acceleration for buckets across all regions.
  - **Origin Server Type**: Select **Default Endpoint** or **Static Website Endpoint**. Select the first option unless your bucket has enabled static website. If you want to use your custom acceleration domain name as static website, select **Static Website Endpoint** here and enable static website for your bucket.
  - **Authentication**: Enable origin-pull authentication. For private-read buckets, enable **Origin-pull Authentication** to protect the origin.
>!For private-read buckets, if both origin-pull authentication and CDN service authorization are enabled, then signature is not required for access to the origin through CDN, and cached resources in CDN will be delivered over the public network, which will affect the data security. Therefore, we recommend you enable CDN authentication as instructed in step 5.
  - **Automatic CDN Cache Purge**: After this feature is enabled, when a file in the COS bucket is updated, the CDN cache will be automatically purged. You can go to the **Function Service** section in the COS console to configure this feature as instructed in [Setting CDN Cache Purge](https://intl.cloud.tencent.com/document/product/436/37273).
  - **HTTPS Certificate**: To add an HTTPS certificate for the custom domain name, go to the [CDN console](https://console.cloud.tencent.com/cdn/certificate).
4. After the configuration, click **Save** in the **Operation** column on the right to add the domain name. After it is saved, the **Enable** button for **CDN Authentication** will appear in the **Authentication** column. You can click the button to enable CDN authentication for the custom domain name.
**CDN Authentication:** Timestamp authentication can be configured to prevent stealing by malicious users. You can enable the feature after adding the domain name.
> !After CDN acceleration is enabled for a domain name, anyone can directly access the origin at the domain name. Therefore, if you want to keep your data private, be sure to protect your data on the origin through **Authentication Configuration**.
5. Log in to the [CDN console](https://console.cloud.tencent.com/cdn/access) and click **Domain Management** on the left sidebar.
6. Locate the target domain name and click **Manage** in the **Operation** column on the right to enter the domain management page. Click **Access control** > **Authentication Configuration**. For more information, see [Instruction](https://intl.cloud.tencent.com/document/product/228/35237).


