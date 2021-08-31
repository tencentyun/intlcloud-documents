This document describes how to add domain names in WAF.
## Directions
To apply WAF protection for a specified domain name, the domain name needs to be added to WAF first. This document takes `waf.qcloudwaf.com` as the sample domain name for directions.
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/config), and select **Web Application Firewall** -> **Defense Settings** on the left sidebar.
2. Click **Add domains** to enter the **Domain Configuration** page.
![](https://main.qcloudimg.com/raw/9e14c97169bacf7fca99411c5278457b.png)
 - **Domain configuration**
     1. Enter `waf.qcloudwaf.com` in the **Domain Name** field.
     2. Select the protocol and port as needed. For example, select HTTP and port 80, or select HTTPS and port 443.
     3. You can select HTTP or HTTPS as the HTTPS origin-pull method.
     >? The origin-pull port can be specified only when HTTP is selected as the origin-pull method. The origin-pull port for HTTPS is consistent with the opened port.
     4. You can select a Tencent Cloud-hosted certificate or your own certificate.
     5. In the **Real Server Address** field, enter the real origin server IP address of the target website, i.e., the public IP address of the real server.   
 - **Other configurations**
 If you have connected your domain name to an intermediate proxy device before WAF is used, tick **Yes**; otherwise, tick **No**.
1. Click **Save** to complete the configuration. Then, you can view the domain name in the domain name list.
2. Click the domain name to enter its details page, you can then view the CNAME that WAF assigned to the website.
 ![](https://main.qcloudimg.com/raw/9541ea01c087959b5f2882ca846faa02.png)
>?WAF assigns a unique CNAME to each domain name added to WAF irrespective of whether the domain name is of the first-level or second-level.

## Subsequent Operations
After adding a domain name, you can proceed:
- [Step 2. Perform Local Testing](https://intl.cloud.tencent.com/document/product/627/35652)
- [Step 3. Modify DNS Resolution](https://intl.cloud.tencent.com/document/product/627/35653)
- [Step 4. Set a Security Group](https://intl.cloud.tencent.com/document/product/627/35654)
