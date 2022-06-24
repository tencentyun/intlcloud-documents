## Overview
Access control rules allow you to control access from public network users by matching HTTP message sections such as request path, GET parameters, POST parameters, Referer, and User-Agent. This feature enables Tencent Cloud users to respond flexibly with a combination of rules to easily block various cyber attacks.
>?
>- Each rule can contain up to 5 conditions.
>- Conditions in each rule are evaluated using a logical AND, that is, the rule does not take effect unless all the conditions are matched.
>- Each rule supports four actions: Block, CAPTCHA, Observe, and Redirect.
    - Block: Enables WAF to block access requests that hit the specified rule.
    - CAPTCHA: Enables WAF to verify access requests that hit the specified rule.
    - Observe: Enables WAF to observe access requests that hit the specified rule.
    - Redirect: Enables WAF to redirect access requests that hit the specified rule.
>- Priority: The value range is 1-100. A smaller number represents higher priority.

## Example
### Example 1: Banning specific IP addresses from access to a designated site
To ban specific IP addresses from access to a designated site, the webmaster can perform configuration with the following steps:
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia) and click **Configuration Center** > **Basic Security** on the left sidebar.
2. On the basic security page, select the target domain name in the top-left corner and click **Access control**.
![](https://qcloudimg.tencent-cloud.cn/raw/d5aceac7ddc0eadff36998e0106e2b88.png)
3. On the access control page, click **Add rule**, and the rule adding window will pop up.
4. Enter the name of the rule (e.g. "001"), select an option (such as "source IP") for **Field**, select “Match” for **Logical operator**, and enter the source IP (e.g. `192.168.1.1`) banned from access for **Content**. Then select an action (e.g. "Block"), and click **OK** to save the rule.
![](https://qcloudimg.tencent-cloud.cn/raw/16e6aa2b05f04de88e6168cc3c205840.png)
>? WAF access control rules allow you to use masks to control access requests from source IPs within a range. We can enter a specific IP address range (e.g. `10.10.10.10/24`) in **Content**.

5. Now, the rule will take effect immediately, and block all HTTP access requests from specific source IPs.
![](https://qcloudimg.tencent-cloud.cn/raw/7295e1ccf9b405af4b9c3a8fd1ef288e.png)

### Example 2: Banning public network users from access to specified Web resources
If the webmaster does not want a public network user to access specified web resources, such as administration backend `/admin.html`, he or she can  configure as follows: select "Request Path" for **Field**, select "Equal to" for **Condition**, enter `/admin.html` in **Content**, select "Block" for **Action**, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/2147dc3ed5069794d1b307f7f7573037.png)

### Example 3: Banning an external site from hot-linking certain resources
To block hotlink attacks by external sites, such as `www.test.com`, the webmaster can use access control rules to capture and block the Referer in a hotlink request. The configuration is as follows: select "Referer" for **Field**, select "Include" for **Condition**, enter `www.test.com` in **Content**, select "Block" for **Action**, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/033592a232297bf2456a8a5d8f3470e7.png)


### Example 4: Copying rules to target domain names
You can copy the rule you configured to other domain names by using the copy operation.
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia) and click **Configuration Center** > **Basic Security** on the left sidebar.
2. On the basic security page, select the target domain name in the top-left corner and click **Access control**.
![](https://qcloudimg.tencent-cloud.cn/raw/f2918f4f96c070037924950d7107aeb9.png)
2. On the access control page, select the required policy, click **Copy**, and the custom policy copy window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/dd92a4ecafb7a31df61d91f304b163e3.png)
3. In the pop-up window, select a domain name and click **OK** to copy the rules to the target domain name.
![](https://qcloudimg.tencent-cloud.cn/raw/63ff21947bc2aa3c5c036bde99d245ed.png)
