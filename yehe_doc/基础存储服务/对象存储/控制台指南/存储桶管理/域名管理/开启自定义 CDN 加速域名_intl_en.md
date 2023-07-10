## Overview

This document only describes how to add a custom acceleration domain name and enable CDN acceleration in the COS console. For more information on how to add a custom domain name by using the CDN console, see [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/32978). 


## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5). Click **Bucket List** on the left sidebar to open the Bucket List page.
2. Click the bucket you need to set a domain name to go to the bucket configuration page.
3. Click **Domains and Transfer** > **Custom CDN Acceleration Domain** on the left and click **Add Domain** to perform the configurations below.
>? If you have enabled **Custom Domain** in the previous console, you will see **Custom Domain** still displayed, with Custom CDN Acceleration Domain not displayed in the current console.
>

  - **Domain Name**: Enter the target custom domain name (such as `www.example.com`). Make sure that an ICP filing has been obtained and a CNAME record has been configured at the DNS service provider for the entered domain. For more information, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121). If the custom CDN acceleration domain you are connecting is in the following situations, you need to verify your domain ownership as instructed in [Domain Name Ownership Verification](https://intl.cloud.tencent.com/document/product/228/42693).
     - The domain name is being connected for the first time.
     - The domain name has been connected by another user.
     - The domain name is a wildcard domain name.
  - **Acceleration Region**: CDN acceleration is supported for regions in the Chinese mainland, outside the Chinese mainland, and globally, with global acceleration for buckets across all regions.
  - **Origin Server Type**: Select **Default Endpoint** or **Static Website Endpoint**. Select the first option unless your bucket has enabled static website. If you want to use your custom CDN acceleration domain name as static website, select **Static Website Endpoint** here and enable static website for your bucket.
  - **Authentication**: Enable origin-pull authentication. For private-read buckets, enable **Origin-pull Authentication** to protect the origin server.
>! For private-read buckets, if both origin-pull authentication and CDN service authorization are enabled, signature is not required for accessing the origin via CDN, and cached resources in CDN will be distributed on the public network, which will affect the data security. Therefore, we recommend you enable CDN authentication (Step 5).
  - **Automatic CDN Cache Purge**: After this feature is enabled, when a file in the COS bucket is updated, the CDN cache will be automatically purged. You can go to the **Function Service** section in the COS console to configure this feature as instructed in [Setting CDN Cache Purge](https://intl.cloud.tencent.com/document/product/436/37273).
  - **HTTPS Certificate**: To add an HTTPS certificate for the custom domain name, go to the [CDN console](https://console.cloud.tencent.com/cdn/certificate).
4. After the configuration, click **Save** in the **Operation** column on the right to add the domain name. After it is saved, the Enable button for CDN authentication appears next to **Authentication**. You can click the button to enable the CDN authentication for the custom domain name.
**CDN Authentication:** Timestamp authentication can be configured to prevent stealing by malicious users. You can enable the feature after adding the domain name.
> ! After CDN acceleration is enabled for a domain name, anyone can directly access the origin via the domain name. Therefore, if you need to keep you data private, be sure to protect your data in the origin through **Authentication Configuration**.
5. Log in to the [CDN console](https://console.cloud.tencent.com/cdn/access) and click **Domain Management** on the left sidebar.
6. Locate the domain name you need to configure and click **Manage** under **Operation** on the right to open the domain management page. Click **Access control** at the top, and then locate **Authentication Configuration**. For details, see [Instruction](https://intl.cloud.tencent.com/document/product/228/35237).


