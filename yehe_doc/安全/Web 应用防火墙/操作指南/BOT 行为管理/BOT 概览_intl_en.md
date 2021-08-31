## Feature Overview
The bot behavior management feature of WAF can differentiate between friendly and malicious bots and crawlers and implement corresponding management policies such as letting through the traffic of search engine bots, blocking the traffic of malicious item information crawlers, delaying responses, or adopting different response time periods. This feature reduces resource consumption, information leakage, and failed marketing caused by malicious bots and crawlers on the one hand and ensures normal operations of friendly ones (such as search engine bots and advertising programs) on the other hand.
On the bot overview page, you can quickly get to know the information of bots for the top 5–10 domain names, view the bot type, action, and request trend through thumbnails, and stay up to date with the access proportion and trend of bots for each domain name.
## Instructions
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/bot2/overview) and select **Bot Behavior Management** > **Bot Overview** on the left sidebar to view the bot behavior overview.
2. The overview page displays the bot overview for the top 5 domain names by default. If you want to view more domain names, click the "Rank" drop-down list in the top-right corner to select more domain names (such as top 10).
![](https://main.qcloudimg.com/raw/d52559e8e83f3b6541b024249051f47a.png)
**Statistics item description:**
	- **Number of Bots**: the number of bots detected by WAF for a domain name is displayed by bot type (unknown, custom, and public) with the access source IP as the statistical dimension.
	- **Rank**: the bots of the top 5 domain names are displayed by default, and you can view up to 10 domain names. If you want to view more domain names, please go to the [Bot Details](https://console.cloud.tencent.com/guanjia/bot2/record/overview) page.
3. View the overview of a domain name. Bot overview provides an overview of bots for up to 10 domain names, which allows you to quickly view the bot type, action, and request trend for each domain name. You can click a domain name in the top-left corner to view its detailed statistics.
![](https://main.qcloudimg.com/raw/bc2db5a9552f67e21ab95ce1cc7bd99e.png)
**Statistics item description:**
	- **Bot Type**: the quantities and proportions of bots in different types (unknown, public, and custom) detected for the domain name are displayed.
	- **Bot Action**: the quantities and proportions of actions in different types (CAPTCHA verification, redirect, blocking, and monitoring) detected for the domain name are displayed.
	- **Bot Request Trend**: the trends in total requests and bot requests are displayed.
