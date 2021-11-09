Tencent Cloud WAF provides the following two types: SaaS WAF and CLB WAF, whose billable items, billing mode and price are identical basically. You can make your purchase based on the connection methods.

Tencent Cloud WAF only supports monthly subscription (prepaid). Any resource usage exceeds the quota is billed on a pay-per-use basis. Pay-as-you-go is not supported.

### Billing Mode

Tencent Cloud WAF adopts billing by basic packs and extra packs.

- Choose a yearly or monthly prepaid for your subscription.
- Extra pack: After purchasing a basic pack, you can get an extra domain pack, extra QPS pack and extra log services pack as needed.


### Basic pack pricing


|Edition|Premium|Enterprise|Ultimate|
|---|---|---|---|
|Price|550 USD|1,450 USD|4,250 USD|
|Scenario|Applicable to standardized protection for small and medium websites|Applicable to protection for small and medium website applications and customized protection for medium and large websites|Applicable to protection for large and super large website applications and customized protection for complex website applications, on the basis of AI technology and rule engine|
|OWASP Top 10 threats, such as SQL injection, cross-site scripting, cross-site request forgery and web shell trojan upload|Supported|Supported|Supported|
|Automatic update of protection rules against 0day vulnerabilities on cloud|Supported|Supported|Supported|
|AI-based online learning, including false positive/false negative submission, security model processing and online attack verification|-|-|Supported|
|Bot management, including identifying and protecting known bots, unknown bots and custom bots|-|Supported|Supported|
|Custom rule based on bot session features|-|20 rules per domain name|50 rules per domain name|
|Port|Protection for HTTP ports (ports 80 and 8080) and HTTPS ports (ports 443 and 8443)|Protection for non-standard HTTP and HTTPs ports (not limited to ports 80, 8080, 443 and 8443). Customizing non-standard ports is not supported.|Protection for non-standard HTTP and HTTPs ports (not limited to ports 80, 8080, 443 and 8443). Customizing non-standard ports is supported.|
|Regional blocking based on geographic locations|Supported|Supported|Supported|
|Emergency CC protection|Supported|Supported|Supported|
|Dedicated protection for a single IP|-|Supported|Supported|
|Custom bot protection rule based on features (of HTTP protocol, intelligence, custom session) |-|-|50 rules per domain name|
|Custom CC protection rule based on IPs and sessions |5 rules per domain name|20 rules per domain name|50 rules per domain name|
|Custom protection rule based on parameters (IP, URL, Referer, User-Agent, Cookie and Body)|10 rules per domain name|20 rules per domain name|50 rules per domain name|
|IP blocklist|1,000 blocked IPs can be set for a domain name|5,000 blocked IPs can be set for a domain name|20,000 blocked IPs can be set for a domain name|
|Webpage anti-tampering rule|10 rules per domain name|20 rules per domain name|50 rules per domain name|
|Data leakage prevention rule|5 rules per domain name|10 rules per domain name|20 rules per domain name|
|Wildcard domain name protection|Supported|Supported|Supported|
|Professional services|1 on 1 pre-sale consulting<br>After-sale service via submitting a ticket|24/7 online support|24/7 online support|
|QPS|2,500|5,000|10,000|
|Number of top-level domain names|2|3|4|
|Number of secondary domain names|20|30|40|

### Extra pack pricing

- Extra domain pack pricing

| Extra Domain Pack                                                   | Price       |
| ------------------------------------------------------------ | ---------- |
| An extra domain pack can protect a maximum of 10 domain names, including one top-level domain name and multiple secondary domain names | 285 USD/month |

- Extra QPS pack pricing

| Extra QPS Pack              | Price       |
| -------------------------- | ---------- |
| An extra QPS pack contains 1,000 QPS | 142 USD/month |




In case of insufficient account balance, the WAF service will be suspended one day after the account is in arrears, and the WAF resources will be released in 7 days. You can pay off the overdraft before the release of resources to resume defense service.

Prices published here are for reference only. Refer to your bills for final prices.