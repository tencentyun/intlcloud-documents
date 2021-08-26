## Overview
Custom rules allow for controlling the access from public network users by combining and matching HTTP message sections such as request path, GET parameters, POST parameters, Referer, and User-Agent. This feature enables Tencent Cloud users to respond flexibly with a combination of rules to easily block various attacks from the Internet.
>!
>- Each custom rule can set up to 5 conditions for section control.
>- Conditions in each custom rule are evaluated using a logical AND, that is, the rule does not take effect unless all the conditions are matched.
>- For each custom rule to be matched, you can configure two consequential actions: block and allow.

## Sample Case
### Case 1: Banning specific IP addresses from access to a designated site
To ban specific IP addresses from access to a designated site, the webmaster can perform configuration with the following steps:
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia), and click **Web Application Firewall** > **Defense settings** on the left sidebar. In the domain name list, select the domain name of the site you want to protect. In the **Operation** column on the right, click **Defense configuration** to enter the details page, and select **Custom Rule**>**Add a Rule**.
 ![](https://main.qcloudimg.com/raw/28061aeb403c4a3a816ec05eae98a6a0.png)
2. Enter the name of the rule (e.g. “001”), select an option (such as “source IP”) for **Field**, select “matched” for **Condition**, and enter the source IP (e.g. `192.168.1.1`) banned from access for **Content**. Then select an action (e.g. “block”), and click **Confirm** to save the rule.
![](https://main.qcloudimg.com/raw/631c07e4f425fa7309aa7de35f07c52c.png)
>? WAF custom rules allow you to use masks to control access requests from source IPs within a range. We can enter a specific IP address range (e.g. `10.10.10.10/24`) in **Content**.
3. Now the rule will take effect immediately, and block all HTTP access requests from specific source IPs.
![](https://main.qcloudimg.com/raw/866f2674fe97dae364bca13742d0a00c.png)

### Case 2: Banning public network users from access to specified Web resources 
If the webmaster does not want a public network user to access specified Web resources, such as administration backend `/admin.html`, he or she can enter the "Edit Custom Rule" page and configure the following: select "Request Path" for **Field**, select "equals to" for **Condition**, enter `/admin.html` in **Content**, select "block" for **Action**, and click **Confirm**.
![](https://main.qcloudimg.com/raw/35982e6ab392d2f60e8e6827022a9886.png)

### Case 3: Banning an external site from hot-linking certain resources 
To block hotlink attacks by external sites, such as `www.test.com`, the webmaster can use custom rules to capture and block the Referer in a hotlink request. The configuration is as follows: select "Referer" for **Field**, select "includes" for **Condition**, enter `www.test.com` in **Content**, select "Block" for **Action**, and click **Confirm**.
![](https://main.qcloudimg.com/raw/8c0a309be63f91061751beaf4ff48389.png)
<a href="https://intl.cloud.tencent.com/document/product/627/11710" target="_blank">Previous: Tamper Protection</a>


### Case 4: Copying rules to target domain names
You can copy the rule you configured to other domain names by using the copy operation.
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia) and select **Web Application Firewall** > **Defense settings** > **Custom Rule** on the left sidebar.
2. On the **Custom Rule** page, select rules as needed and click **Copy**.
3. In the pop-up window, select a domain name and click **Copy** to copy the rules to the target domain name.
