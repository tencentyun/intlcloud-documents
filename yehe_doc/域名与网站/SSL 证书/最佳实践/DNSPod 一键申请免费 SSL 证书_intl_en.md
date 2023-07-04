## Overview

The DNSPod console allows you to quickly apply for a free SSL certificate.
This document describes how to quickly apply for one.

## Prerequisites

You have registered a domain at your registrar.

## Directions

>?
> 
>  You can skip steps 1 and 2 if your domain has been hosted in the DNSPod console.
> 


### Step 1. Add a domain in the DNSPod console
1. Log in to the [DNSPod console](https://console.dnspod.cn/dns/list) and go to the **My Domains** page.

2. On the **My Domains** page, click **Add Domain**.

3. In the displayed input box, enter the target second-level domain and click **OK**.
   

   >?
   > 
   >   - DNSPod does not support adding subdomains other than second-level domains. For example, it supports the second-level domain `dnspod.cn` but not the third-level domain `bbs.dnspod.cn`.
   >   - If you are prompted that the domain has been added by another user, see [Domain Retrieval](https://docs.dnspod.cn/dns/5f4889498ae73e11c5b01c12/).


### Step 2. Modify the DNS server of the domain

If "DNS Servers Not Correctly Set" is prompted for the added domain, you need to change the DNS server of the domain to that of DNSPod to allow for DNS query and hosting in DNSPod.
>?
> 
> - DNSPod will query the corresponding settings document based on your registrar information. You can click the prompt box and view the settings document to complete the change.
> - If the settings document is unavailable or cannot be queried, we recommend that you contact your registrar.
> - If your domain is registered at Tencent Cloud and under the current DNSPod account, you can click **One-Click Modification** to quickly change to the correct DNS server.


### Step 3. Quickly apply for a free SSL certificate
1. Select the target domain and click **SSL** in the **Operation** column.

2. In the **Apply for SSL certificate** pop-up window, select **Free SSL Certificate** and click **Apply (Free)** as shown below:
   

   >?
   > 
   > Only second-level domains and their subdomains are supported for a free certificate. If you need to use a wildcard domain, get a paid SSL certificate.
   > 

 

3. DNSPod will validate your domain automatically, and you only need to wait for the certificate issue.
   

   >?
   > 
   > Tencent Cloud will complete the SSL certificate review within one business day and notify you of the result through SMS, email, and Message Center.
   > 
