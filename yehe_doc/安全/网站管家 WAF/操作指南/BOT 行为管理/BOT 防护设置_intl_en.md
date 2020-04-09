## Feature Overview
Bot protection configuration allows you to set bot protection policies based on the characteristics of bot session behaviors and take corresponding actions. Moreover, you can observe and analyze bot details and fine-tune the policies based on the provided session status details to ensure security of your website's core APIs and businesses. This feature supports setting two types of protection policies, namely, public policies and custom session policies.
### Public category
WAF provides protection against 12 public categories of bots with over 1,000 subcategories, such as search engine, speed tester, content aggregator, scanner, and website crawler. You can set protection actions (passing, monitoring, and blocking) for public bots as needed, and WAF will process bot requests that hit a public category policy accordingly.
### Custom session policy
WAF custom session policies allow you to set characteristics of protocols, IP intelligence, and custom sessions, all of which can be determined in multiple dimensions. You can set custom session policies and the processing actions (passing, monitoring, CAPTCHA, redirect, and blocking) based on your actual business needs and bot details, and WAF will process bot requests that hit a custom protection policy accordingly.
>Only WAF Enterprise and Ultimate editions support bot behavior management. WAF Advanced users are recommended to upgrade to the Enterprises or Ultimate edition.

## Instructions
### Enabling or disabling bot protection
Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/bot/strategy) and select **Bot Behavior Management** > **Bot Protection Settings** on the left sidebar to enter the bot policy settings page.
![](https://main.qcloudimg.com/raw/8745cf6f92bb41e4f2253c6513ee9ca8.png)
**Field description:**

- **Domain Name**: protected domain name added to WAF, i.e., the one in **Web Application Firewall** > **[Protection Settings](https://console.cloud.tencent.com/guanjia/waf/config)**. Sorting is supported.
- **Bot Traffic Analysis**: it is disabled by default, and you can enable it as needed.
>Only when the domain name's WAF service is activated can bot traffic analysis take effect.
- **WAF Status**: WAF service status as displayed in the protected domain name list in **Web Application Firewall** > **[Protection Settings](https://console.cloud.tencent.com/guanjia/waf/config)**.
- **Operation**: you can click **Protection Settings** to set a bot protection policy.

### Setting public category
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/bot/strategy) and select **Bot Behavior Management** > **Bot Protection Settings** on the left sidebar. Find the desired domain name and click **Protection Settings** in the "Operation" column on the right.
2. Enter the protection settings page and click **Public Category** to enter the corresponding list page.
![](https://main.qcloudimg.com/raw/58e1edabcc53ae75725d18867f9dd4a1.png)
**Parameter description:**
	- **Bot Category**: WAF supports bot identification in 12 public categories such as search engine, speed tester, content aggregator, scanner, and website crawler.
	- **Bot Subcategories**: number of subcategories in each category.
	- **Action**: action supported for the corresponding public bot category, which is "Monitor" by default. You can set it to "Pass" or "Block" in the "Operation" column on the right. You can view the blocking results in **[Attack Log](https://console.cloud.tencent.com/guanjia/waf/attack)** and view the IPs blocked in real time in **[IP Blocking Status](https://console.cloud.tencent.com/guanjia/ip/record)**.
	- **Operation**: action taken for the corresponding public bot category. For more information, please see [Action Category Description](#dzlx).
3. In the top-left corner, click **Copy** to copy the public bot category settings of the current domain name to another one whose original settings will be overridden.
![](https://main.qcloudimg.com/raw/10fff84ff41e5db0a3927dcfdab8eed3.png)

### Custom session policy
#### Protocol characteristics
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/bot/strategy) and select **Bot Behavior Management** > **Bot Protection Settings** on the left sidebar. Find the desired domain name and click **Protection Settings** in the "Operation" column on the right.
2. Enter the protection settings page and select **Custom Session Policy** > **Protocol Characteristics** to enter the corresponding list page.
![](https://main.qcloudimg.com/raw/55f2548f1daac0be5fd03551213153d9.png)
	- **Field description:**
		- **Policy Name**: protocol characteristics.
		- **Action**: default action of the protocol characteristics policy, which is "Monitor" by default. You can set its value in the "Operation" column on the right.
		- **Policy Status**: the policy is disabled by default.
		- **Modified at**: last time when the policy was modified.
		- **Operation**: you can click **Edit** to set the action, which can be "Pass", "Monitor", or "Block". For more information, please see [Action Category Description](#dzlx). You can view the blocking results in **[Attack Log](https://console.cloud.tencent.com/guanjia/waf/attack)** and view the IPs blocked in real time in **[IP Blocking Status](https://console.cloud.tencent.com/guanjia/ip/record)**.
	- **The following table lists the names of protocol characteristics policies**:
<table>
<tr><th>Protocol Characteristics Category</th><th>Policy Name</th></tr>
<tr><td rowspan="7">`User-Agent` category </td><td>`User-Agent` is empty or does not exist.</td></tr>
<tr><td>The `User-Agent` category is `BOT`.</td></tr>
<tr><td>The `User-Agent` category is `Unknown BOT`.</td></tr>
<tr><td>The `User-Agent` category is `HTTP Library`.</td></tr>
<tr><td>The `User-Agent` category is `Tools`.</td></tr>
<tr><td>The `User-Agent` category is `Framework`.</td></tr>
<tr><td>The User-Agent category is `Scanner`.</td></tr>
<tr><td rowspan="8">HTTP header</td><td>`Referer` is empty or does not exist.</td></tr>
<tr><td>`Referer` is abused (multiple UAs use the same `Referer`).</td></tr>
<tr><td>`Cookie` is abused (multiple UAs use the same `Cookie`).</td></tr>
<tr><td>`Cookie` is empty or does not exist.</td></tr>
<tr><td>`Connection` is empty or does not exist.</td></tr>
<tr><td>`Accept` is empty or does not exist.</td></tr>
<tr><td>`Accept-Language` is empty or does not exist.</td></tr>
<tr><td>`Accept-Enconding` is empty or does not exist.</td></tr>
<tr><td rowspan="2">HTTP protocol characteristics</td><td>The `HTTP HEAD` method is used.</td></tr>
<tr><td>The HTTP protocol version is 1.0 or below.</td></tr>
</table>

#### IP intelligence characteristics
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/bot/strategy) and select **Bot Behavior Management** > **Bot Protection Settings** on the left sidebar. Find the desired domain name and click **Protection Settings** in the "Operation" column on the right.
2. Enter the protection settings page and select **Custom Session Policy** > **IP Intelligence Characteristics** to enter the corresponding list page.
![](https://main.qcloudimg.com/raw/cfe58a8695dcac4016b30cc19ed23d9b.png)
	- **Field description:**
		- **Policy Name**: name of the IP intelligence policy field.
		- **Action**: default action of the intelligence characteristics policy, which is "Monitor" by default. You can set its value in the "Operation" column on the right.
		- **Policy Status**: the policy is disabled by default. You are recommended to enable the automated testing service of WAF which checks the health of your domain names.
		- **Modified at**: last time when the policy was modified.
		- **Operation**: you can click **Edit** to set the action, which can be "Pass", "Monitor", "CAPTCHA", or "Block". For more information, please see [Action Category Description](#dzlx).
>For the automated testing service used to check domain name health, do not set it to "Block".
	
	- **The following table lists the names of IP intelligence characteristics policies:**
<table>
<tr><th>IP Intelligence Category</th><th>Policy Name</th></tr>
<tr><td >Automated testing</td><td>Tencent Cloud WAF automated testing.</td></tr>
<tr><td rowspan="11">IDC-IP library</td><td>IDC-IP library - Tencent Cloud.</td></tr>
<tr><td>IDC-IP library - Alibaba Cloud.</td></tr>
<tr><td>IDC-IP library - Huawei Cloud.</td></tr>
<tr><td>IDC-IP library - Kingsoft Cloud.</td></tr>
<tr><td>IDC-IP library - UCloud.</td></tr>
<tr><td>IDC-IP library - Baidu Cloud.</td></tr>
<tr><td>IDC-IP library - JD Cloud.</td></tr>
<tr><td>IDC-IP library - QingCloud.</td></tr>
<tr><td>IDC-IP library - AWS.</td></tr>
<tr><td>IDC-IP library - Azure.</td></tr>
<tr><td>IDC-IP library - Google Cloud.</td></tr>
</table>

#### Customizing session characteristics
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/bot/strategy) and select **Bot Behavior Management** > **Bot Protection Settings** on the left sidebar. Find the desired domain name and click **Protection Settings** in the "Operation" column on the right.
2. Enter the protection settings page and select **Custom Session Policy** > **Custom Session Characteristics** to enter the corresponding list page.
![](https://main.qcloudimg.com/raw/9fe29dd854fd6fa35156e93d49cc4eea.png)
	- **Field description:**
		- **Number**: auto-incrementing policy number.
		- **Policy Name/Description**: policy name and description.
		- **Match Condition**: policy match conditions. Up to 10 match conditions can be added for one policy, which will be in "AND" relationship.
		- **Action**: action set when the policy is added. You can set its value in the "Operation" column on the right.
		- **Policy Status**: policy status set when the policy is added.
		- **Modified at**: last time when the policy was added or modified.
		- **Operation**: modification or deletion of the policy. You can click **Edit** to set the action, which can be "Pass", "Monitor", "CAPTCHA", "Redirect", or "Block". For more information, please see [Action Category Description](#dzlx).
3. Add custom session characteristics. Click **Add** in the top-right corner of the list to enter the custom session characteristics page.
![](https://main.qcloudimg.com/raw/eff73227445febfed7d08f00203079e1.png)

>Policy priority is subject to the action Category, which is: Pass > Monitor > Redirect > CAPTCHA > Block. For policies of the same action category, the later it is added, the higher its priority is.
>
	- **Field description:**
		- **Policy Name**: policy name.
		- **Policy Description**: policy description.
		- **Policy Status**: policy status, which is "Enabled" by default.
		- **Match Condition**: bot policy match conditions. Up to 10 match conditions can be added, which will be in "AND" relationship. You can hover your mouse over a match condition to view its description.
		- **Action:** action to be executed.
		<span id="dzlx"></span>
	- **Action category description:**
	<table>
<tr><th  >Action Category</th><th>Description</th></tr>
<tr><td>Pass</td><td>Session requests that match the set conditions will be allowed and will not be logged.</td></tr>
<tr><td>Monitor</td><td>Session requests that match the set conditions will be monitored. You can view more information of the monitored sessions in the custom bot details.</td></tr>
<tr><td>CAPTCHA</td><td>It is applicable only to access through browsers. Session requests that match the set conditions will be verified with a CAPTCHA; if the verification fails, they will be blocked; otherwise, they can normally access the domain name within the blocking period.</td></tr>
<tr><td>Redirect</td><td>Session requests that match the set conditions will be redirected to a specified URL of the current domain name within the specified blocking period.</td></tr>
<tr><td>Block</td><td>Session requests that match the set conditions will be blocked. You can set the blocking period to 5–10,080 minutes (7 days). you can view the blocking results in **<a href = "https://console.cloud.tencent.com/guanjia/waf/attack">Attack Log</a>** and view the IPs blocked in real time in **<a href = "https://console.cloud.tencent.com/guanjia/ip/record">IP Blocking Status</a>**.</td></tr>
</table>
	- **The match conditions for custom session characteristics are as follows:**
	<table>
<tr><th width=100px>Category</th><th width=150px>Filter Condition</th><th>Description</th></tr>
<tr><td rowspan="6">Session characteristics</td><td>Average session speed</td><td>Total number of session requests/session duration in requests/minute..</td></tr>
<tr><td>Session window speed</td><td>Session access speed in every 2 minutes (window) in requests/minute.</td></tr>
<tr><td>Total number of sessions</td><td>Total number of access requests in a bot session.</td></tr>
<tr><td>Session duration</td><td>Duration of the bot session.</td></tr>
<tr><td>`Robots.txt` existing in session</td><td>The session request wants to access the `Robots.txt` file.</td></tr>
<tr><td>Session in early morning</td><td>The session request is initiated between 2:00 AM and 5:00 AM.</td></tr>
<tr><td rowspan="3">IP characteristic</td><td>Access source IP</td><td>Access source IP.</td></tr>
<tr><td>IP category</td><td>IP category, which can be IDC or base station (ISP base station). When the IP type is IDC, there may be exceptions.</td></tr>
<tr><td>IP owner</td><td>IP owner information such as `tencent.com`, which can be queried in bot details and takes effect only if the IP category is IDC.</td></tr>
<tr><td rowspan="5">Request characteristics</td><td>Most frequently requested URL</td><td>The most frequently requested URL.</td></tr>
<tr><td>Proportion of repeated URLs</td><td>Proportion of repeated URLs in session requests, which ranges from 0 to 1. You should configure the parameter based on your actual business needs. A value that is too high or too low suggests an exception (which should be determined jointly based on the actual business conditions).</td></tr>
<tr><td>URL categories</td><td>Number of URLs in session requests after deduplication.</td></tr>
<tr><td>Most frequently requested parameter</td><td>The most frequently requested parameter, which may be a GET request parameter (`Query` content) or POST request parameter (`Body` content).</td></tr>
<tr><td>Proportion of repeated parameters</td><td>Proportion of repeated GET request parameters (`Query` content) or POST request parameters (`Body` content) in session requests, which ranges from 0 to 1. You should configure the parameter based on your actual business needs. A value that is too high or too low suggests an exception (which should be determined jointly based on the actual business conditions).</td></tr>
<tr><td rowspan="6">Cookie</td><td>Cookie existence</td><td>Used to check whether the HTTP header has a cookie in session requests.</td></tr>
<tr><td>Most frequently requested cookie</td><td>The most frequently requested cookie in session requests.</td></tr>
<tr><td>Proportion of repeated cookies</td><td>Proportion of repeated cookies in session requests, which ranges from 0 to 1.</td></tr>
<tr><td>Proportion of cookie existence</td><td>Proportion of requests with a cookie in all session requests, which ranges from 0 to 1.</td></tr>
<tr><td>Cookie abuse</td><td>Indicates that multiple different UAs use the same cookie.</td></tr>
<tr><td>Cookie categories</td><td>Number of cookies in session requests after deduplication.</td></tr>
<tr><td rowspan="6">Referer</td><td>Referer existence</td><td>Used to check whether the HTTP header has a referer in session requests.</td></tr>
<tr><td>Most frequently requested referer</td><td>The most frequent HTTP referer in session requests.</td></tr>
<tr><td>Proportion of repeated referers</td><td>Proportion of repeated referers in session requests, which is valid only for access through browsers and ranges from 0 to 1. A value that is too high suggests an exception (which should be determined jointly based on the actual business conditions).</td></tr>
<tr><td>Proportion of referer existence</td><td>Proportion of requests with a referer in session requests, which is valid only for access through browsers and ranges from 0 to 1. A value that is too low suggests an exception (which should be determined jointly based on the actual business conditions).</td></tr>
<tr><td>Referer abuse</td><td>Indicates that multiple different UAs use the same referer.</td></tr>
<tr><td>Referer categories</td><td>Number of referers in session requests after deduplication.</td></tr>
<tr><td rowspan="6">UA</td><td>UA existence</td><td>Used to check whether the HTTP header has UA in session requests.</td></tr>
<tr><td>Most frequently requested UA</td><td>The most frequent HTTP `User-Agent` value in session requests.</td></tr>
<tr><td>Proportion of UA existence</td><td>Proportion of requests with a UA in session requests, which ranges from 0 to 1. A value that is too low suggests an exception (which should be determined jointly based on the actual business conditions).</td></tr>
<tr><td>UA categories</td><td>Number of UAs in session requests after deduplication, which is valid only for non-proxy IPs. A value that is too high suggests an exception (which should be determined jointly based on the actual business conditions).</td></tr>
<tr><td>UA category</td><td><ul><li>Browser.</li>
<li>Mobile device.</li>
<li>Game console or TV.</li>
<li>Public bot.</li>
<li>Private bot.</li>
<li>Automated tool.</li>
<li>Unknown.</li>
<li>Public scanner.</li>
<li>Framework.</li>
<li>Programming language HTTP library.</li><ul></td></tr>
<tr><td>UA randomness index </td><td>Random distribution status, which ranges from 0 to 1. The higher the value, the more likely the request is exceptional.<br>Reference thresholds: a value above 0.6 suggests an exception; a value above 0.92 indicates a basically confirmed exception.</td></tr>
<tr><td rowspan="7">Other HTTP headers</td><td>`Accept` existence</td><td>The HTTP headers in the session requests will be checked for the `Accept` field.</td></tr>
<tr><td>`Accept-Language` existence</td><td>The HTTP headers in the session requests will be checked for the `Accept-Language` field.
</td></tr>
<tr><td>`Accept-Encoding` existence</td><td>The HTTP headers in the session requests will be checked for the `Accept-Encoding` field.</td></tr>
<tr><td>`Connectiton` existence</td><td>The HTTP headers in the session requests will be checked for the `Connectiton` field.</td></tr>
<tr><td>Request method proportion</td><td>Proportion of request method in the session requests.</td></tr>
<tr><td>HTTP protocol version proportion</td><td>Proportion of HTTP protocol version used in the session requests.
</td></tr>
<tr><td>Proportion of returned status code</td><td>Proportion of status codes returned by WAF in the session requests.
</td></tr>
<tr><td rowspan="7">Advanced characteristics</td><td>Prediction tag</td><td>It is the suspicious behavior predicated by the system. Not all sessions have a predication tag, which may be one of the following:
<ul><li>Suspicious irregular crawler.</li>
<li>Suspicious regular crawler.</li>
<li>Suspicious login with missing user value.</li>
<li>Suspicious login with missing user parameter.</li>
<li>Suspicious login with missing username and password.</li>
<li>Suspicious login with missing user login action.</li>
<li>Suspicious brute force attack.</li>
<li>Suspicious database comparison attack.</li>
<li>Suspicious unauthorized access to SMS APIs.</li> 
<li>Suspicious unauthorized access to CAPTCHA APIs.</li> 
<li>Suspicious malicious registration.</li> 
<li>Suspicious repeated API access</li> </ul></td></tr>
<tr><td>Bot score</td><td>Bot score of the session given by the intelligent bot analysis engine. The higher the score, the more likely the session is initiated by a bot. The reference value is 5.</td></tr>
<tr><td>AI engine detected</td><td>Result of AI behavior analysis model detection. If a result is detected by AI, the session is highly suspicious to be exceptional.</td></tr>
<tr><td>Public bot forgery</td><td>The session requests pretend to be those in public bot categories; for example, a request uses the UA of Baidu crawlers, but its IP does not belong to Baidu.</td></tr>
<tr><td>Sensitive API access</td><td>Used to determine whether sensitive APIs (such as SMS APIs, registration APIs, and login APIs) are accessed.</td></tr>
<tr><td>Time-series behavior exception index</td><td>An algorithm used to detect exceptional time-series behaviors. The smaller the index, the more likely the behavior is exceptional.<br>Reference value thresholds: a value below 0.5 suggests an exception; a value below 0.24 indicates a basically confirmed exception.</td></tr>
<tr><td>Time-series entropy exception index</td><td>An algorithm used to detect the time-series behavior entropy. The smaller the index, the more likely the session is exceptional. A value below 0.5 suggests an exception.</td></tr>
</table>
