
## Overview
This document describes how to validate a domain when you apply for a certificate or add a domain in the certificate management console and the domain validation mode is DNS validation.

## Directions

### Step 1. View validation information[](id:details)
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview).
2. Select a certificate in the **Validating** state. On the **Validate Domain** page displayed, obtain the host record and record value. See the figure below.
>?Take note of the host record and record value before you go to step 2 to add a DNS record.
>
![](https://qcloudimg.tencent-cloud.cn/raw/1010a2309189d79dfeefdc3399b4e81c.png)

### Step 2. Add a DNS record
>!The following operations apply only to domain names hosted with Tencent Cloud. For domain names hosted with other platforms, go to the corresponding **DNS service provider** for DNS. To query DNS service providers, go to [DNS.TECH](https://dns.tech/).
>
1. Obtain the host record and record value, which can be obtained on the **Validate Domain** page, as described in step 1.
2. Log in to the [DNSPod console](https://www.dnspod.com/) to view the domain name for which a certificate has been applied, and then click **DNS** in the **Operation** column to go to the **Record Management** page. See the figure below.
![](https://qcloudimg.tencent-cloud.cn/raw/e713a12f2ccae8d85a411d772802a6f3.png)
3. Click **Add Record** and add a DNS record depending on the certificate type.
>?Only the CNAME and TXT types of DNS records are supported, and they are applicable for certificates of different brands. Please select the DNS record type as needed.
>
<dx-tabs>
::: TrustAsia and WoTrus Certificates
For TrustAsia and WoTrus certificates, enter a DNS record of the CNAME type. See the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/f0ec90c0cf4e2322d40001c0c188ce95.png)
 - **Host**: enter the host record obtained in [step 1](#details).
 - **Type**: select **CNAME**.
 - **Split Zone**: select **Default**. Otherwise, the corresponding CA will not be able to review the DNS record.
 - **Value**: enter the record value obtained in [step 1](#details).
 - **MX Priority**: leave it empty.
 - **TTL**: it refers to the time to live. The smaller the value is, the less the time cost for record changes to take effect globally. The default value is 600 seconds.
:::
::: Certificates of Other Brands
For certificates of other brands, enter a DNS record of the TXT type. See the figure below.
![](https://qcloudimg.tencent-cloud.cn/raw/1afca1c98a4481c5e7b81587ca1630e2.png)
 - **Host**: enter the host record obtained in [step 1](#details).
 - **Type**: select **TXT**.
 - **Split Zone**: select **Default**. Otherwise, the corresponding CA will not be able to review the DNS record.
 - **Value**: enter the record value obtained in [step 1](#details).
 - **MX Priority**: leave it empty.
 - **TTL**: it refers to the time to live. The smaller the value is, the less the time cost for record changes to take effect globally. The default value is 600 seconds.
:::
</dx-tabs>
4. Click **Save**.
5. After the record is added, the system periodically checks for the record value. If the record value is detected and matches the specified value, the domain ownership verification will be completed. Please wait for the CA's review.
>?
>- DNS usually takes effect within **10 minutes to 24 hours**. The actual time depends on the ISP refresh time.
>- After the certificate is issued or the domain name information is approved, you can manually clear the DNS record.





