## Overview

This document describes how to bind a custom domain name to a bucket. You can access the files in the bucket via the custom domain name.

>? Up to 20 custom domain names can be added in the COS console. To add more, [contact us](https://intl.cloud.tencent.com/contact-sales).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5). 
2. Click **Bucket List** on the left sidebar.
3. Click the bucket for which you need to set a domain name to go to the bucket configuration page.
4. Click **Domains and Transfer** > **Custom Endpoint** on the left sidebar, click **Add Domain**, and configure the following items:

  - **Domain Name**: Enter the target custom domain name (such as `www.example.com`). Make sure that an ICP filing has been obtained, a DNS record has been added in the [Domains console](https://console.cloud.tencent.com/cns/domains), and a CNAME record has been configured at the DNS service provider for the entered domain name. For more information, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121). If the custom CDN acceleration domain you are connecting is in the following situations, you need to verify your domain ownership as instructed in [Domain Name Ownership Verification](https://intl.cloud.tencent.com/document/product/228/42693).
     - The domain name is being connected for the first time.
     - The domain name has been connected by another user.
     - The domain name is a wildcard domain name.
  - **Origin Server Type**: Select **Default Endpoint** or **Static Website Endpoint**. Select the first option unless your bucket has enabled static website. If you want to use your custom domain name as static website, select **Static Website Endpoint** here and enable static website for your bucket.
  - **HTTPS Certificate**: After the domain name is saved, you can choose to bind a certificate. For detailed instructions, see [Certificate Installation](https://www.tencentcloud.com/document/product/1007/36568).
  >?
  >- HTTPS certificate hosting for custom origin server domain names of COS is supported in public cloud regions in the Chinese mainland and in Singapore. If no HTTPS certificate is available for your domain name, click [Apply for Free Certificate](https://console.cloud.tencent.com/ssl).
  >- HTTPS certificate hosting currently is not supported in other regions. If you need to use HTTPS certificates, see [Method 2](https://intl.cloud.tencent.com/document/product/436/11142).
