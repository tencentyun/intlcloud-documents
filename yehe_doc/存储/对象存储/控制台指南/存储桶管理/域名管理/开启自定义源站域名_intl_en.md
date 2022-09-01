## Overview

This document describes how to bind a custom domain name to a bucket. Then, you can access files in the bucket at the custom domain name.

>? Up to 20 custom domain names can be added in the COS console. To add more, [contact us](https://intl.cloud.tencent.com/contact-sales).
>

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5). 
2. Click **Bucket List** on the left sidebar.
3. Click the target bucket to enter the **Bucket Configuration** page.
4. Click **Domains and Transfer** > **Custom Endpoint** on the left sidebar and click **+Add Domain**.
5. If your custom domain name has been filed with MIIT, and a DNS record has been added in the [DNS console](https://console.cloud.tencent.com/cns/domains), you can enter the custom domain name in the **Domain Name** input box, and click **Save**. Then, you can choose to upload a certificate.

6. If you have not added a DNS record for your custom domain name, add your custom domain name by following the steps below.
  1. Log in to the [DNS console](https://console.cloud.tencent.com/cns/domains), click **DNS Record List** on the left sidebar to enter the **All Domains** page. Click **Add Record**.
  2. Enter the custom domain name, **select the default project (recommended if you don't have special requirements)**, and click **OK** to save.


  3. After the domain name is added successfully, click it to enter the DNS record management page. Click **Add Record**.
  4. Enter the host record as prompted, select **CNAME** for **Record Type** and **Default** for **Split Zone**, enter your bucket domain name in **Record Value**, leave **TTL** as-is, and click **Save**.


  5. After the record is added, it takes about ten minutes to take effect. Then, you can configure relevant options as described in step 3.
