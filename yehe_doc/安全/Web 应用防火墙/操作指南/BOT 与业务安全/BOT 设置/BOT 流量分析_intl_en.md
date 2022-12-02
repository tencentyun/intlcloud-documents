## Background
The bot traffic management feature can differentiate between friendly and malicious bots and crawlers and implement corresponding management policies such as letting through the traffic of search engine bots, blocking the traffic of malicious item information crawlers, delaying responses, or adopting different response time periods. This feature reduces resource consumption, information leakage, and failed marketing caused by malicious bots and crawlers on the one hand and ensures normal operations of friendly ones (such as search engine bots and advertising programs) on the other hand.

With bot traffic analysis, you can collect data from bot traffic management and quickly understand how a selected domain name with bot traffic analysis enabled is affected by bots. You can also view the bot classification trend, action trend, bot score distribution, top statistics by request count, and list of URLs vulnerable to attacks.


## Directions
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Bot traffic analysis** on the left sidebar.
2. On the **Bot traffic analysis** page, click the **All domain names** drop-down list in the top-left corner and select the target domain name.
3. Select **Not all domain names** and click **View configuration** in the top-left corner to enter the **Bot and application security** page for the corresponding domain name.
![](https://qcloudimg.tencent-cloud.cn/raw/4d30708ce91fb5be36346543dda18d29.png)
4. On the **Bot traffic analysis** page, search for the protection data of a domain name by **Time** or **Filter**.
    - You can search for the bot protection effect data of a domain name in the specified time period.
     ![](https://qcloudimg.tencent-cloud.cn/raw/5dda8e94571305f5f92fb9a3f247d07c.png)
    - Click **Filter** to display the bot traffic analysis filter.
    ![](https://qcloudimg.tencent-cloud.cn/raw/238cecfe5b5b8c9c051ec3bfa08868b6.png)
5. In the **Requests** section, you can view the bot requests and bot session scores of the current domain name (you can select a global domain name).
   - Bot requests chart: Group different bot scores into different ranges according to the configured action and tag, score and tag each traffic request accessing the website, and display the result on the chart.
    ![](https://qcloudimg.tencent-cloud.cn/raw/2af9fc64262416e63eb99c7943d6a05f.png)
	- Bot session scores: It's a chart displaying the bot traffic risk distribution in a domain name of the current user, including the access traffic trend. You can set bot scores accordingly. The higher the scores, the larger the impact of the bots.
![](https://qcloudimg.tencent-cloud.cn/raw/a13160ec3631114f53957999d651386f.png)
6. Click **Actions** to view the actions on traffic of the current domain name (or a global domain name) by bot traffic management and its percentage to the actions on all the request traffic.
![](https://qcloudimg.tencent-cloud.cn/raw/ce7ad19c08f2115e4233ab3afa9f0ae7.png)
7. The **Top 5 exceptional requests** section displays the top 5 key-value pairs and quantity of abnormal bot features in a certain time period. The statistical chart is subject to the filter and the time of the traffic trend comparison chart. Click **Bar chart** to view the key-value pair information. Click **Filter** or **Exclude** to quickly add a filter.
![](https://qcloudimg.tencent-cloud.cn/raw/6fb31ce907c2981bd192adb8115c917e.png)
8. The **Top 5 by request count** section displays the top 5 key-value pairs and number of bot features in a certain time period. The statistical chart is subject to the filter and the time of the traffic trend comparison chart. Click **Bar chart** to view the key-value pair information. Click **Filter** or **Exclude** to quickly add a filter.
![](https://qcloudimg.tencent-cloud.cn/raw/e5bd32d5d1836201d5751924c724c82c.png)
8. The affected asset statistical list displays the URLs most affected by bots and the actions performed by bot traffic management. The entries are aggregated once every five minutes.
![](https://qcloudimg.tencent-cloud.cn/raw/e9d5351d7852eeab0080bfd5a3c3b7a8.png)
**Field description**
 - **Access source**: Source of the access request.
 - **Session**: A single connection establishment session.
 - **Region**: Geographical location of the access request.
 - **Domain name**: Access domain name.
 - **Request path**: URI of the access request.
 - **Action**: Action performed by bot traffic management.
 - **Access count**: Number of sessions.
 - **Detected module**: Hit modules.
 - **Bot score**: Bot score of the current access request in the aggregated dimension.
 - **Bot tag**: Bot tag hit by the current access request in the aggregated dimension.
 - **Threat intelligence module**: Match tag hit by the current bot in the threat intelligence module.
 - **Analysis of hits**: Displays the exceptions in the current access request that hit the bot analytics module in the aggregated dimension.
 - **Type of exceptions**: Displays the exceptions discovered by the bot flow statistics module in the aggregated dimension.
 - **Logging time**: Time when bot access is discovered.
 - **Operation**:
   - View logs: Click **View logs** to view the access log of a bot.
>? To view access logs, you need to subscribe to the [access logging](https://intl.cloud.tencent.com/document/product/627/47799) service.

![](https://qcloudimg.tencent-cloud.cn/raw/9b97c37a32856783a40156cfe3e68af9.png)
   - View details: Click **View details** to view the feature details of a bot.
   - Add to blocklist: Click **Add to blocklist**, configure parameters, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/f6e349dcf87510c4ba4e00ad6f643d65.png)

 

