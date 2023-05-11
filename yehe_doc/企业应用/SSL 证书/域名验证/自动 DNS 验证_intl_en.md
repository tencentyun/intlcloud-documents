## Overview

This document describes how to validate a domain through automatic DNS validation when you apply for a certificate or add a domain in the SSL Certificate Service console.

>!
> 
> Automatic DNS validation is supported for multi-year international standard certificates only. For more information, see [Available Multi-Year International Standard Certificates](https://www.tencentcloud.com/document/product/1007/53630).
> 


## Directions

### Step 1. View validation information
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview). In the left sidebar, click **My Profile** to go to the **My Profile** page.

2. On the **My Profile** page, click the name of the organization for which domain information is to be validated. Then you can view the information of administrators that have been applied for.

3. Click the target administrator name to enter the **Review Information** page.

4. Click the **Domain Information* tab, select the target domain, and click **View Validation**.

5. On the **Validate Domain** page, add a DNS record as prompted and within the specified period of time.


### Step 2. Add a DNS record

>!
> 
> The following operations apply only to domains hosted with Tencent Cloud. For those hosted with other platforms, go to the corresponding DNS service provider.
> 

1. Get the **host** and **record value** as shown in the figure in substep 5 in **Step 1. View validation information**.

2. Log in to the [DNSPod console](https://console.cloud.tencent.com/cns) to view the target domain and click **DNS** in the **Operation** column to enter the **Record Management** page.

3. Click **Add Record** to add a CNAME record.

  - **Host**: Enter the obtained host.

  - **Record Type**: Select **CNAME**.

  - **Split Zone**: Make sure that it is **Default**, or resolution may fail for some users.

  - **Record Value**: Enter the obtained record value.

  - **MX Priority**: leave it empty.

  - **TTL**: it refers to the time to live. The smaller the value is, the less the time cost for record changes to take effect globally. The default value is 600 seconds.

4. Click **Save**.

5. After adding the record successfully, wait for the CA to scan and review it. If it can be found and matches the specified value, the review is completed.
   

>?
>   - DNS usually takes effect within **10 minutes to 24 hours**. The actual time depends on the ISP refresh time.
>   - Do not delete or modify the configured CNAME record; otherwise, the proxy will not work.
>   - Do not configure the TXT record for a domain if the CNAME record is already configured; otherwise, domain validation may fail.
>   - If anything goes wrong during this process, [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).

6. On the **Validate Domain** page, click **Validate** to check whether the CNAME record has been added successfully.
