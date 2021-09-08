### How do I connect a domain name?
You can connect a domain name using the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/config). For more information, see [Add a Domain Name](https://intl.cloud.tencent.com/document/product/627/35651).
### Does WAF support connecting wildcard domain names?
Yes. You can connect a wildcard domain name in the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/config/add).
>?
>- If a wildcard domain name, such as `*.test.com`, is already connected to Tencent Cloud, then any of its sub-domain names cannot be connected to another account.
>- If the wildcard domain name `*.test.com` is already connected to your account, then wildcard domain names in formats such as `*.a.test.com` cannot be connected to this account.
>- If you add both a wildcard and a precise domain name (e.g. `*.test.com` and `a.test.com`), WAF first uses the protection policies configured for the precise domain name.

### How long does it take to update the DNS resolution (protection) status of my domain name?
Verify that CNAME configuration for your website domain name is correct. Once you add a CNAME record in DNS, please wait 10-20 minutes for the protection status to be updated. If you have waited over 30 minutes, and the protection status has not been updated yet, you can contact us for help by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=642&source=0&data_title=T-Sec-Web%E5%BA%94%E7%94%A8%E9%98%B2%E7%81%AB%E5%A2%99&level3_id=867&radio_title=%E6%8E%A7%E5%88%B6%E5%8F%B0%E9%97%AE%E9%A2%98&queue=15&scene_code=29995&step=2).

### Will WAF notify me when the intermediate IP address of my domain name is changed?
In principle, the intermediate IP address of your domain name is not changed. If it happens, we will notify you by SMS, email or Message Center. You can view your intermediate IP address in the [Domain Name List](https://console.cloud.tencent.com/guanjia/waf/config) of the console.
![](https://main.qcloudimg.com/raw/d0d8ce06b25775d61cfada695a016135.png)

### What are the requirements for connecting a domain name to WAF?
The business content on your real server must be legal, and you can modify the DNS resolution properly. Otherwise, you will not be able to connect your domain name to WAF.

### What options does WAF offer for domain name origin-pull?
WAF performs origin-pull based on domain name or IP. You can choose which option to configure as you need. For more information, see [Add a Domain Name](https://intl.cloud.tencent.com/document/product/627/35651).
### How do I bind a CNAME to my domain name connected to WAF?
See [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121) for how to bind CNAME with your DNS service provider.

### Will the CNAME change if my domain name is deleted and added again?
No, it won’t. You can go to the WAF Console, click your domain name in the [Domain Name List](https://console.cloud.tencent.com/guanjia/waf/config), and view the CNAME in **Basic Settings**.
![](https://main.qcloudimg.com/raw/dde2826c8364d1a8eb580466782471fc.png)

### Can I change the VIP address of my domain name?
No, you can’t change it, in principle. However, if an exception occurs to your WAF service, you may contact us quickly by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=642&source=0&data_title=T-Sec-Web%E5%BA%94%E7%94%A8%E9%98%B2%E7%81%AB%E5%A2%99&level3_id=867&radio_title=%E6%8E%A7%E5%88%B6%E5%8F%B0%E9%97%AE%E9%A2%98&queue=15&scene_code=29995&step=2) so that we can switch it to another working VIP address for you.

### How to enter a forwarding domain name when adding a domain name to WAF?
You can enter a CNAME address from other proxies or any other domain name as forwarding domain name. The domain name you entered and the one you added to WAF cannot be identical, and the protocol type (HTTP or HTTPS) can be left empty.
