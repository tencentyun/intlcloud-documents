### How do I connect a domain name?
You can connect a domain name using the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/config). For more information, see [Add a Domain Name](https://intl.cloud.tencent.com/document/product/627/35651).
### Does WAF support connecting wildcard domain names?
Yes. 
>?
>- If you have configured a wildcard domain name in WAF, contact us quickly to help process it by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=642&source=0&data_title=T-Sec-Web%E5%BA%94%E7%94%A8%E9%98%B2%E7%81%AB%E5%A2%99&level3_id=981&radio_title=IP%E7%AE%A1%E7%90%86&queue=15&scene_code=31050&step=2). The wildcard domain name configuration will then be available for you in WAF, which automatically matches the corresponding sub-domain names.
>- If a wildcard domain name, such as `*.test.com`, is already connected to Tencent Cloud, then any of its sub-domain names cannot be connected to another account.
>- If the wildcard domain name `*.test.com` is already connected to your account, then wildcard domain names in formats such as `*.a.test.com` cannot be connected to this account.
>- If you add both a wildcard and a precise domain name (e.g. `*.test.com` and `a.test.com`), WAF first uses the protection policies configured for the precise domain name.

### How long does it take to update the DNS resolution (protection) status of my domain name?
Verify that CNAME configuration for your website domain name is correct. Once you add a CNAME record in DNS, please wait 10-20 minutes for the protection status to be updated. If you have waited over 30 minutes, and the protection status has not been updated yet, you can contact us for help by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=642&source=0&data_title=T-Sec-Web%E5%BA%94%E7%94%A8%E9%98%B2%E7%81%AB%E5%A2%99&level3_id=867&radio_title=%E6%8E%A7%E5%88%B6%E5%8F%B0%E9%97%AE%E9%A2%98&queue=15&scene_code=29995&step=2).

### Will WAF notify me when the intermediate IP address of my domain name is changed?
In principle, the intermediate IP address of your domain name is not changed. If it happens, we will notify you by SMS, email or Message Center. You can view your intermediate IP address in the [Domain Name List] (https://console.cloud.tencent.com/guanjia/waf/config) of the console.

### What are the requirements for connecting a domain name to WAF?
The business content on your real server must be legal, and you can modify the DNS resolution properly. Otherwise, you will not be able to connect your domain name to WAF.

### What options does WAF offer for domain name origin-pull?
WAF performs origin-pull based on domain name or IP. You can choose which option to configure as you need. For more information, see [Add a Domain Name](https://intl.cloud.tencent.com/document/product/627/35651).
### How do I bind a CNAME to my domain name connected to WAF?
See [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121) for how to bind CNAME with your DNS service provider.
### Will the logging feature still be available once WAF is disabled for the domain name list?
Once WAF is disabled, all its protection features are unavailable, and only the traffic forwarding mode starts to run instead, with no logs recorded.
### Will the CNAME change if my domain name is deleted and added again?
No, it won’t. You can go to the WAF Console, click your domain name in the [Domain Name List](https://console.cloud.tencent.com/guanjia/waf/config), and view the CNAME in **Basic Settings**.

### Can I change the VIP address of my domain name?
No, you can’t change it, in principle. However, if an exception occurs to your WAF service, you may contact us quickly by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=642&source=0&data_title=T-Sec-Web%E5%BA%94%E7%94%A8%E9%98%B2%E7%81%AB%E5%A2%99&level3_id=867&radio_title=%E6%8E%A7%E5%88%B6%E5%8F%B0%E9%97%AE%E9%A2%98&queue=15&scene_code=29995&step=2) so that we can switch it to another working VIP address for you.
### What should I do if the VIP address of my WAF-protected domain name is blocked due to DDoS?
WAF provides anti-DDoS Basic capabilities (2 G) for VIP addresses by default. In case of an urgent need to resume your business for a VIP address blocked by anti-DDoS Basic, you can:
- Log in to the [DDoS Protection Console](https://console.cloud.tencent.com/ddos/unblock/list), and unblock the VIP address manually. You are allowed to do so three times each month.
- Or buy a [Anti-DDoS Pro](https://console.cloud.tencent.com/ddos/ddos-pro/protection-config) instance, and bind it to your WAF-protected VIP address.

You are allowed to remove blocking manually only three times per month. The system resets the count of blocking removals at zero o'clock on the 1st day of every month, and the remaining number of allowed removals from last month is not carried over to this month.

### How do I connect a CDN domain name to WAF?
To connect a CDN domain name, simply use the CNAME address that WAF assigned for your domain name as CDN origin server. The content is pulled from the origin as traffic flows through the architecture “user > CDN > WAF > CLB > real server”. Meanwhile, you can log in to the WAF Console, and select **Yes** for *Proxy** in the [Add domains](https://console.cloud.tencent.com/guanjia/waf/config/add) page. Then, WAF obtains the real IP of your client for protection based on the XFF field in HTTP headers.

### How do I add a real server domain name to WAF?
To add a real server domain name to WAF, enter the CNAME or other domain name different from the protection domain names. You may leave the protocol (HTTP or HTTPs) empty.
