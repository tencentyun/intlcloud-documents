This document describes how to configure WAF to protect APIs on API Gateway.

## Prerequisites

- You have activated [WAF](https://buy.cloud.tencent.com/buy/waf).
- You have published an API on API Gateway as instructed in [Step 1. Get the Access Permission](https://intl.cloud.tencent.com/document/product/628/34889).

## Directions

### Step 1. Bind a custom domain name in the API Gateway console
For more information about how to bind a custom domain name in the API Gateway console, see [Custom Domain Name and Certificate](https://intl.cloud.tencent.com/document/product/628/11791).
>!When a custom domain name is bound to API Gateway, the system will check whether you have configured CNAME and resolved it to the service subdomain name. Therefore, you need to configure CNAME and resolve the custom domain name to the subdomain name of API Gateway, modify the DNS record, and point the custom domain name to the WAF CNAME domain name.



### Step 2. Configure WAF
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Domain name list** on the left sidebar.
2. On the **Domain name list** page, select the target instance and click **Add domain name**.
![](https://qcloudimg.tencent-cloud.cn/raw/aa42bfb1313bf6634e409d1dca0b1b1c.png)
3. On the **Add domain name** page, configure relevant parameters and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/cdca55316408bbf99fcb9ee63ca130a3.png)
4. After the configuration is completed, the domain name connection status will become **No CNAME records added**.
![](https://qcloudimg.tencent-cloud.cn/raw/15f5f6878c3359cb9b4bff48f8ec2226.png)


### Step 3. Modify the CNAME record
1. Modify the CNAME record at your DNS service provider and resolve the custom domain name to the WAF domain name.
2. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview), select **Domain name list**, and you see the **Normal protection** flag.
![](https://qcloudimg.tencent-cloud.cn/raw/94b66dc5883894abadad27fda8265e0f.png)

