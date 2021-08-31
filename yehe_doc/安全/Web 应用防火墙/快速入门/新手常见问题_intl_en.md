## Connection
### Can I use WAF for servers outside Tencent Cloud?

WAF can be connected with servers in data centers outside Tencent Cloud. It protects servers in any public networks, including but not limited to Tencent Cloud and clouds and IDCs of other vendors. 
>!ICP filing issued by the MIIT is required for all connected domain names in Chinese mainland.

### Does WAF support HTTPS protection?

WAF fully supports HTTPS services. You just need to upload an SSL certificate and private key as instructed or select a Tencent Cloud-hosted certificate to make WAF protect HTTPS traffic.

### How many intermediate IPs can be set for one protected domain name in WAF?
Up to 20 intermediate IPs can be set for one protected domain name in WAF.

### Does WAF support health check?
Health check is enabled in WAF by default. WAF checks the health status of all real server IPs. If a real server IP does not respond, WAF will stop forwarding requests to it until it is restored to normal status.

### Does WAF support session persistence?
WAF supports session persistence, which is enabled by default.

### How long does it take for configuration changes in the WAF Console to take effect?

In general, a configuration change takes effect within 10 seconds.

### Do both SaaS and CLB WAF support SSL two-way authentication?
SaaS WAF does not support SSL two-way authentication, but CLB WAF does.

## Domain Name

### How do I connect a domain name?
You can connect a domain name in the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/config). For more information, please see [Step 1. Add a Domain Name](https://intl.cloud.tencent.com/document/product/627/35651).

### Can I change the VIP address of my domain name?
No, you can't change it in principle. However, if an exception occurs to your WAF service, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=642&source=0&data_title=T-Sec-Web%E5%BA%94%E7%94%A8%E9%98%B2%E7%81%AB%E5%A2%99&level3_id=867&radio_title=%E6%8E%A7%E5%88%B6%E5%8F%B0%E9%97%AE%E9%A2%98&queue=15&scene_code=29995&step=2) for application, and we will switch it to another working VIP address for you.
### What options does WAF offer for domain name forwarding?
WAF performs forwarding based on domain name or IP. You can choose an option to configure as needed. For more information, please see [Step 1. Add a Domain Name](https://intl.cloud.tencent.com/document/product/627/35651).
### How do I bind a CNAME record to my domain name connected to WAF?
Please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121) for how to bind CNAME at your DNS service provider.
### Will the logging feature still be available once WAF is disabled in the domain name list?
Once WAF is disabled, all its protection features become unavailable, and the traffic forwarding mode starts to run instead, with no logs recorded.
### Will the CNAME change if my domain name is deleted and added again?
No, it won't. You can go to the WAF Console, click your domain name in the [Domain Name List](https://console.cloud.tencent.com/guanjia/waf/config), and view the CNAME in "Basic Settings".
