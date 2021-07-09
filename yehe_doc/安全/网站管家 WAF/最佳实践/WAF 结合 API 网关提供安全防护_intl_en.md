
This document describes how to configure WAF to protect the security of APIs in API Gateway.

## Prerequisites

- You have activated [WAF](https://buy.cloud.tencent.com/buy/waf).
- You have published the API in API Gateway as instructed in [Getting Started](https://intl.cloud.tencent.com/document/product/628/34889).

## Directions

### Step 1. Bind a custom domain name in the API Gateway Console

Bind a custom domain name in the API Gateway Console as instructed in [Custom Domain Name and Certificate](https://intl.cloud.tencent.com/document/product/628/11791).
>!When you bind the custom domain name in API Gateway, the system will verify whether the domain name is resolved (through a CNAME record) to a subdomain name of the API Gateway service. Therefore, you should resolve the custom domain name (through a CNAME record) to a subdomain name of the service first, bind it, and then modify the CNAME record to point it to the CNAME domain name of WAF.
>
<img src="https://main.qcloudimg.com/raw/fb4621332105ad78229c43d150c8fe91.png">



### Step 2. Configure WAF

1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/config).
2. Select **Web Application Firewall** > **Protection Settings** on the left sidebar to enter the protection settings page.
3. Click **Add Domain** above the domain name list to enter the domain name configuration page.
4. On the "Domain Configuration" page, fill in the relevant fields based on the actual conditions. Here, select "Domain Name" as the real server address, enter the subdomain name of the API Gateway service, and click **Save**.
5. After the configuration is completed, the domain name access status will become "CNAME record not configured".
<img src="https://main.qcloudimg.com/raw/c0cc86b0eb8ae0d294a71a79b1265be6.png">


### Step 3. Modify the CNAME record

1. Modify the CNAME record at your DNS provider and point the custom domain name to the CNAME domain name of WAF.
2. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/config) and select **Web Application Firewall** > **Protection Settings** to enter the protection settings page.
3. In the domain name list, click the refresh button next to the access status, and you can see that the access status becomes "Normal protection". At this point, the access configuration is completed.
