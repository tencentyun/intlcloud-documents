## Overview

This document describes how to bind the custom domain name to the bucket. You can access the files in the bucket via the custom domain name.

>? Up to 20 custom domain names can be added via the COS console. If you need to apply for a higher quota, [contact us](https://intl.cloud.tencent.com/contact-sales).
>

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5). 
2. In the left sidebar, click **Bucket List** to go to the bucket list page.
3. Click the bucket for which you need to set a domain name to go to the bucket configuration page.
4. In the left sidebar, choose **Domains and Transfer** -> **Custom Endpoint**, and click **Add Domain**.
5. If your custom domain name has been filed with MIIT, and resolution has been added on the [DNS console](https://console.cloud.tencent.com/cns/domains), you can enter the custom domain name in the **Domain Name** input box, and click **Save**.
    ![](https://main.qcloudimg.com/raw/d0c76b2e57cd6a1b6d395bd7d4d21216.png)
6. If you have not added resolution for your custom domain name, add your custom domain name by following the steps below.
  a. Log in to the [DNS console](https://console.cloud.tencent.com/cns/domains), click **Domain Name Resolution List** in the left sidebar to go to the **All Domains** page. Click **Add Resolution** to go to the **Add Resolution** dialog box.
  b. Enter the domain name, select the default project from **Project Options**, and click **OK** to save. **Select the default project from Project Options if there is no special requirement.**

    ![](https://main.qcloudimg.com/raw/e56eb87f45433d0b0cab1b51bccdcbc6.jpg)
  c. After the domain name is added successfully, click the domain name to enter the resolution record management page. Click **Add Record** to go to the **Add Record** dialog box.
  d. Enter the host record as prompted, select **CNAME** for **Record Type** and **Default** for **Line Type**, enter your bucket domain name in **Record Value**, leave **TTL** as is, and click **Save**.

    ![](https://main.qcloudimg.com/raw/0d1bc007db4643f4b52852594f62e34c.jpg)
  e. After the resolution is added, it takes about 10 minutes to take effect. Then you can complete relevant configurations as described in Step 3.
