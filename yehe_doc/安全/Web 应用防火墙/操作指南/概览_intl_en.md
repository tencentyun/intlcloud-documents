The Overview page allows you to get an overall picture of the security status of your domain name.

## Security Overview
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Overview** on the left sidebar. Then open the **Security Overview** tab.
2. Select a domain name to view data that measures the security status of the domain name.
![](https://qcloudimg.tencent-cloud.cn/raw/23dfbc23419f0245f479ef3af9c08a5d.png)

## Instance Overview
To view expired instances under your account, select a domain name and click **Include x instances**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/81f0cdb46e064821cc004276b9269b3c.png)

## Rule Updates
By clicking **See more** in the rule updates section, you can view WAF supported rules in detail.
![](https://qcloudimg.tencent-cloud.cn/raw/54962f9ed88750627ca66efa4a273313.png)


## Attacks Overview
#### All domain names
1. When "All domain names" is selected, all attack data are displayed. You can also set a time range to display data you want to see.
![](https://qcloudimg.tencent-cloud.cn/raw/83aa0ad35a197fd6cb27c3b660dbf224.png)
2. At the lower part of the page, you can view the following information including top 5 domain names by web attacks, top 5 attacker IPs, and top 5 domain names by CC attacks.
![](https://qcloudimg.tencent-cloud.cn/raw/fbab1ef15352085f9fe3f17b23fa3f37.png)

**Field description:**
 - Top 5 domain names by web attacks: It displays five domain names that suffer web attacks most frequently.
 - Top 5 attacker IPs: It displays five IPs that initiate attacks most frequently.
 - Top 5 domain names by CC attacks: It displays five domain names that suffer CC attacks most frequently.
 - Top 5 requester IPs: It displays five IPs that send access requests most frequently.
 - Distribution of attacker IPs: It displays how the attacker IPs distribute across regions.
 - Types of attacks (%): It displays the distribution of the attack types.
 - Types of browsers (%): It displays the distribution of the browser types.



#### Single domain name
1. When a specific domain name is selected, the corresponding attack data is displayed. You can also set a time range to display data you want to see.
![](https://qcloudimg.tencent-cloud.cn/raw/e0d1d9f2c98d03468dfe0b6e02f88f3f.png)
2. At the lower part of the page, you can view the following information including top 5 attacker IPs, top 5 requester IPs and distribution of attacker IPs.
![](https://qcloudimg.tencent-cloud.cn/raw/37feb6d131391509a6ddf03eb9be6bdd.png)

**Field description:**
 - Top 5 attacker IPs: It displays five IPs that initiate attacks most frequently.
 - Top 5 requester IPs: It displays five IPs that send access requests most frequently.
 - Distribution of attacker IPs: It displays how the attacker IPs distribute across regions.
 - Types of attacks (%): It displays the distribution of the attack types.
 - Types of browsers (%): It displays the distribution of the browser types.

## Overview of Security Analysis
- Basic security analysis: It displays the number of web attacks on the selected domain name during the specified period.
![](https://qcloudimg.tencent-cloud.cn/raw/e2da627fcd6fc8a8cbdd34f497504493.png)
- Application operation analysis: It displays the QPS and bandwidth of the selected domain name on the left, and top 5 slowest pages and top 5 most visited pages on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/1b5157b79a67dd09b4fa4bc270ce850a.png)
- Application security analysis: It displays the bot information of the selected domain name during the specified period. To view more details, you can click [View bot traffic analysis](https://console.cloud.tencent.com/guanjia/tea-flowanalysis).
![](https://qcloudimg.tencent-cloud.cn/raw/faca16583c5cc20ac85c54ece1d59ce1.png)
