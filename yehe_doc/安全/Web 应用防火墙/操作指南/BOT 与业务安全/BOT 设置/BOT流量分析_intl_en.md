## Overview
Bot traffic management identifies friendly and malicious bots, and take appropriate traffic management strategies. It can allow traffic from search engine bots, ignore traffic from malicious bots crawling product information, slow down its response or take different response strategies, and deal with resource consumption, information leakage and ineffective marketing caused by malicious bot crawling. Meanwhile, it protects friendly bot programs (such as search engines and advertising programs).

With rich data provided by this module, bot traffic analysis can quickly analyze how domain names are affected by bots in terms of the following metrics: types of bots, types of actions, distribution of bot scores, top statistics by bot requests, and vulnerable URLs.


## Directions
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Bot Traffic Analysis** on the left sidebar.
2. On the page that appears, click **All domain names** in the upper-left corner.
3. If you select a specific domain name, then click **View configuration**. You will be redirected to the bot and application security page.
![](https://qcloudimg.tencent-cloud.cn/raw/c408ef612fc3ff0be613c067ad18ddc6.png)
4. Specify a date or use the filter to search data of a specific domain name.
    - By specifying a date, you can search data of a specific domain name within the specified period.
        ![](https://qcloudimg.tencent-cloud.cn/raw/adbe8d2f6643d3cf631329fd808d07fe.png)
    - By setting the filter, you can add conditions to filter out data you need.
    ![](https://qcloudimg.tencent-cloud.cn/raw/9187c911de28baefa8f6a49902d2c722.png)
5. In the Requests section, you can view requests that are identified as different types of bots and the bot session scores.
   - According to the action and score you configure, requests sent to a website are scored and categorized.
    ![](https://qcloudimg.tencent-cloud.cn/raw/2af9fc64262416e63eb99c7943d6a05f.png)
	- The bot session scores chart shows you how bot requests distribute and the bot scores given, and lets you take appropriate actions to combat malicious bots.
![](https://qcloudimg.tencent-cloud.cn/raw/a13160ec3631114f53957999d651386f.png)
6. In the Actions section, you can view the actions taken on the requests at different times and the proportion of actions.
![](https://qcloudimg.tencent-cloud.cn/raw/ce7ad19c08f2115e4233ab3afa9f0ae7.png)
7. Top 5 exceptional requests shows you top 5 requests within the specified period that are considered abnormal based on bot features detected. You can click **Filter** or **Exclude** to display data you need.
![](https://qcloudimg.tencent-cloud.cn/raw/6fb31ce907c2981bd192adb8115c917e.png)
8. Top 5 by request count shows you top 5 data within the specified period based on the bot features detected. You can click **Filter** or **Exclude** to display data you need.
![](https://qcloudimg.tencent-cloud.cn/raw/e5bd32d5d1836201d5751924c724c82c.png)
9. You can also view a list of URLs that are the most vulnerable to bots and the actions taken to combat bots. The data in the list will be collected every 5 minutes.
![](https://qcloudimg.tencent-cloud.cn/raw/e9d5351d7852eeab0080bfd5a3c3b7a8.png)

**Field description**
 - Access source: Source of the access request.
 - Session ID: ID of the session.
 - Region: Location of the access source.
 - Domain name: Accessed domain name.
 - Request path: URI of the access request.
 - Action: Action taken by the bot traffic management module.
 - Number of accesses: Number of sessions.
 - Hit module: Modules that are hit.
 - Bot score: Bot score of the access request.
 - Bot tag: Bot tag of the access request.
 - Threat intelligence: It provides collected data that is used to analyze attack behaviors.
 - Intelligent analysis modules: Modules that analyze access requests are hit.
 - Type of exceptions: Types of exceptions detected.
 - Logging time: Time that the bot accesses.
 - Operation:

   - View logs: It allows you to view access logs.
>? To view access logs, you need to subscribe to the [access logging](https://intl.cloud.tencent.com/document/product/627/47799) service.

![](https://qcloudimg.tencent-cloud.cn/raw/9b97c37a32856783a40156cfe3e68af9.png)

   - View details: It allows you to view details of a specific bot feature.
   - Add to blocklist: It allows you to add a specific access source IP to the blocklist.
![](https://qcloudimg.tencent-cloud.cn/raw/f6e349dcf87510c4ba4e00ad6f643d65.png)

 

