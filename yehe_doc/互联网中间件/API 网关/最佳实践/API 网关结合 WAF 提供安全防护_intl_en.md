## Overview
Tencent Cloud Web Application Firewall (WAF) is an AI-based one-stop web service protection solution.
This document describes how to integrate WAF to the API Gateway to protect your APIs.

## Prerequisites

- You have activated [Web Application Firewall](https://intl.cloud.tencent.com/product/waf).
- You have published APIs using the API Gateway.

## Directions

### Step 1. Bind a custom domain name in the API Gateway console

For more information about how to bind a custom domain name in the API Gateway console, refer to [Custom Domain Name and Certificate](https://intl.cloud.tencent.com/document/product/628/11791).
<img src="https://main.qcloudimg.com/raw/fb4621332105ad78229c43d150c8fe91.png">

>! When a custom domain name is bound to the API Gateway console, the system will check whether you have configured CNAME and resolved it to the service subdomain name. Be sure to first configure CNAME and resolve it to the subdomain name of the API Gateway, modify the CNAME record, and point the custom domain name to the WAF domain name.

### Step 2. Configure WAF

1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/config).
2. Click **Web Application Firewall** -> **Defense settings** in the left sidebar to access the domain name list page.
3. Click **Add domains** at the top of the **Domain Name List** module.
4. Enter the **Real Server Address** and the subdomain name of the API Gateway, and complete the other configurations.
<img src="https://main.qcloudimg.com/raw/47455694ca1ad24bb0f0b4125a759f7a.png">
5. Click **Save**. The domain name should now be in the “CNAME record not configured” status.
<img src="https://main.qcloudimg.com/raw/c0cc86b0eb8ae0d294a71a79b1265be6.png">


### Step 3. Modify the CNAME record

1. Modify the CNAME record and resolve the custom domain name to the WAF domain name.
2. Log in to WAF console and click **Web Application Firewall** -> **Defense settings** in the left sidebar to access the domain name list page.
3. Click the refresh icon in the **Protection status** column. The status should change to **Normal protection**.
