## Overview
The tamper protection feature is used to prevent exceptional display on a specified page caused by tampering.
>!The specified page is limited to static resources such as `.html`, `.shtml`, `.txt`,` .js`, `.css`, `.jpg`, and `.png`.
## Configuration Samples 
### Protecting your home page from being tampered
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia). In the left sidebar, select **Web Application Firewall**>**Defense settings**, and in the domain names list, select the domain name of the site you want to protect, e.g. `www.qcloudwaf.com`. In the Operation column on the right, click **Defense configuration**.
![](https://main.qcloudimg.com/raw/7f26451f8aef4c2ae76ac61ea0c67888.png)
2. If necessary, you can change the site domain name displayed at the top of the defense configuration page. Select the Tamper Resistance tab, and click **Add a Rule**.
![](https://main.qcloudimg.com/raw/3ec4494185c680b3754010f9a3bea75f.png)
3. In the Add Tamper Resistant Rule pop-up window, enter the rule name (e.g. homepage) and a full URL (e.g. `http://www.qcloudwaf.com/index.html`) for the rule, and click **Add** to save the rule.
![](https://main.qcloudimg.com/raw/efe6745893b7c840e4253393ba04969d.png)
4. The rule will take effect instantly. If a rule has been updated, click **Refresh** under **Operation** to display the updated rule.
![](https://main.qcloudimg.com/raw/adf66cf48928a5cea2671a746d317a4d.png)
