### How do I connect a domain name with WAF?
You can connect domain names to WAF in the [WAF Console](https://console.cloud.tencent.com/guanjia/tea-overview) as instructed in [Add a Domain Name](https://intl.cloud.tencent.com/document/product/627/35651).

### Does WAF support wildcard domain names?
Yes. You can add a wildcard domain name in the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview).
>?
>- When a wildcard domain is added to WAF, other Tencent Cloud users can still add subdomain names that match the wildcard domain name to WAF.
>- If you add both a wildcard and a precise domain name (e.g. `*.test.com` and `a.test.com`), policies of the precise domain name prevail.

### How long does it take to update the DNS resolution (protection) status of my domain name?
After you add the CNAME record at your DNS provider, status of the domain name on WAF is updated in 10 to 20 minutes. If you don’t see the update in 30 minutes, please check the CNAME configuration or [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=642&source=0&data_title=T-Sec-Web%E5%BA%94%E7%94%A8%E9%98%B2%E7%81%AB%E5%A2%99&level3_id=867&radio_title=%E6%8E%A7%E5%88%B6%E5%8F%B0%E9%97%AE%E9%A2%98&queue=15&scene_code=29995&step=2).

### Will the intermediate IP change?
The intermediate IP is subject to be changed by WAF. You will be notified by an SMS message, an email, or a message in Message Center if your intermediate IP address changes. You can check the effective intermediate IP o the [Domain Name List](https://console.cloud.tencent.com/guanjia/tea-domain) page of the WAF console.
![](https://qcloudimg.tencent-cloud.cn/raw/3d54e9333cfb490dfc1fd00bb13b5678.png)

### Will the SaaS WAF-connected VIP address change?
Yes. VIP address may change when WAF is maintaining and upgrading its in/cross-region disaster recovery capabilities. To ensure the service availability, WAF only supports configuring VIP addresses by adding the CNAME.

### Can I modify the SaaS WAF-connected VIP address?
No. A SaaS WAF-connected VIP address cannot be modified. If the associated domain name fails due to DDoS attacks, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=642&source=0&data_title=T-Sec-Web%E5%BA%94%E7%94%A8%E9%98%B2%E7%81%AB%E5%A2%99&level3_id=867&radio_title=%E6%8E%A7%E5%88%B6%E5%8F%B0%E9%97%AE%E9%A2%98&queue=15&scene_code=29995&step=2) for assistance.

### What are the requirements for connecting a domain name to WAF?
If the domain name points to a real server in the Chinese mainland, an ICP filling number is required. 
- If the domain name is not 
- If you have obtained an ICP filing for the domain name through another service provider, you must add Tencent Cloud as a service provider to the ICP filing.

>! If the instance to which you add the domain name is a SaaS WAF instance, you also need to add a CNAME record at the DNS service provider of the domain name. Set the record value to the CNAME allocated by WAF.

### What options does WAF offer for domain name origin-pull?
WAF performs origin-pull based on domain name or IP. You can choose which option to configure as you need. For more information, see [Add a Domain Name](https://www.tencentcloud.com/document/product/627/35651).

### How do I bind a CNAME to my domain name connected to WAF?
See [Step 3. Modify DNS Resolution](https://intl.cloud.tencent.com/document/product/627/35653).

### If I remove a domain name and add it back to WAF, does the CNAME change?
Yes. You can check the CNAME in the [Domain Name List page in the WAF console](https://console.cloud.tencent.com/guanjia/tea-domain).
![](https://qcloudimg.tencent-cloud.cn/raw/776ae20e26e6bffc200649ba9cfb518f.png)


### What is the forwarding domain name?
When you add a domain name to WAF, you must specify a forwarding domain name. It can be the CNAME of proxy or another domain name. The protocol type (HTTP or HTTPS) is not required.
