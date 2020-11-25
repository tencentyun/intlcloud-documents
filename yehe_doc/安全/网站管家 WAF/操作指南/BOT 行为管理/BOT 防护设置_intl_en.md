## Overview

Bot protection configuration allows you to set bot protection policies based on the characteristics of bot session behaviors and take corresponding actions. You can also observe and analyze bot details and fine-tune the policies based on the provided session status details to ensure the security of your website's core APIs and businesses. This feature supports two types of protection policies, public policies and custom session policies.

### Public categories

WAF provides protection against 12 public categories of bots with over 1,000 subcategories, such as search engine, speed tester, content aggregator, scanner, and website crawler. You can set protection actions (passing, monitoring, and blocking) for public bots as needed, and WAF will process bot requests that hit a public category accordingly.

### Custom session policies

WAF custom session policies allow you to set features of protocols, IP intelligence, and custom sessions, each of which can be determined in multiple dimensions. You can set custom session policies and the processing actions (passing, monitoring, CAPTCHA, redirect, and blocking) based on your actual business needs and bot details, and WAF will process bot requests that hit a custom protection policy accordingly.

>! Only WAF Enterprise and Ultimate Editions support bot behavior management. We recommended WAF Advanced users upgrade to the Enterprises or Ultimate Edition.


## Instructions

### Enabling or disabling bot protection


Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/bot/strategy) and choose **Bot Behavior Management** -> **Bot Protection Settings** on the left sidebar to go to the bot policy settings page.
![](https://main.qcloudimg.com/raw/8745cf6f92bb41e4f2253c6513ee9ca8.png)
**Field description:**

- **Domain Name:** protected domain name that is added to WAF in [**Web Application Firewall** -> **Defense settings**](https://console.cloud.tencent.com/guanjia/waf/config). Sorting is supported.

- **BOT Switch:** disabled by default. You can enable it as needed.

>! BOT Switch takes effect only when WAF Switch is enabled.

- **WAF Switch:** the WAF switch status, which is displayed in the protected domain name list in [**Web Application Firewall** -> **Defense settings**](https://console.cloud.tencent.com/guanjia/waf/config).

- **Operation:** click **Defense settings** to set a bot protection policy.


### Setting public categories

1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/bot/strategy) and choose **Bot Behavior Management** > **Bot Protection Settings** on the left sidebar. Find the target domain name and click **Defense settings** in the **Operation** column on the right.

2. On the **Defense settings** page, click **Public Type** to enter the corresponding list page.

![](https://main.qcloudimg.com/raw/58e1edabcc53ae75725d18867f9dd4a1.png)

**Field description:**

	- **Categories:** WAF can identify 12 public bot categories, including search engine, speed tester, content aggregator, scanner, and website crawler.
	
	- **Number of BOT Classes:** number of BOT subcategories in each category.
	
	- **Action:** the action supported by the corresponding public bot category, which is "Monitor" by default. You can set it to "Pass" or "Block" in the "Operation" column on the right. You can view the blocking results in [Attack Log](https://console.cloud.tencent.com/guanjia/log/attack) and view the IP addresses blocked in real time in [IP Blocking Status](https://console.cloud.tencent.com/guanjia/ip/record).
	
	- **Operation:** the action taken for the corresponding public bot category. For more information, see [Action Category Description](#dzlx).
	
3. In the upper-left corner, click Copy to copy the public bot category settings of the current domain name to another one whose original settings will be overridden.



### Custom session policies

#### Protocol features

1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/bot/strategy) and choose **Bot Behavior Management** > **Bot Protection Settings** on the left sidebar. Find the target domain name and click **Defense settings** in the **Operation** column on the right.
2. On the **Defense settings** page, choose **Custom Session Policy** > **Protocol Features** to go to the corresponding list page.

![](https://main.qcloudimg.com/raw/55f2548f1daac0be5fd03551213153d9.png)
	- **Field description:**
	
		- **Rule Name:** protocol feature.
		
		- **Action:** the default action of the protocol feature policy, which is "Monitor" by default. You can set its value in the **Operation** column on the right.
		
		- **Rule Switch:** disabled by default.
		
		- **Modification Time:** the last time the policy was modified.
		
		- **Operation:** click **Edit** to set the action, which can be "Pass", "Monitor", or "Block". For more information, see [Action Category Description](#dzlx). You can view the blocking results in [Attack Log](https://console.cloud.tencent.com/guanjia/log/attack) and view the IP addresses blocked in real time in [IP Blocking Status](https://console.cloud.tencent.com/guanjia/ip/record).
		
	- **The following table lists the names of protocol feature policies.**
	
<table>
	
<tr><th>Protocol Feature Category</th><th>Policy Name</th></tr>

<tr><td rowspan="7">User-Agent</td><td>User-Agent is empty or does not exist.</td></tr>

<tr><td>User-Agent is BOT.</td></tr>

<tr><td>User-Agent is Unknown BOT.</td></tr>

<tr><td>User-Agent is HTTP Library.</td></tr>

<tr><td>User-Agent is Tools.</td></tr>

<tr><td>User-Agent is Framework.</td></tr>

<tr><td>User-Agent is Scanner.</td></tr>

<tr><td rowspan="8">HTTP header</td><td>Referer is empty or does not exist.</td></tr>

<tr><td>Referer abuse (multiple UAs use the same Referer).</td></tr>

<tr><td>Cookie abuse (multiple UAs use the same Cookie).</td></tr>

<tr><td>Cookie is empty or does not exist.</td></tr>

<tr><td>Connection is empty or does not exist.</td></tr>

<tr><td>Accept is empty or does not exist.</td></tr>

<tr><td>Accept-Language is empty or does not exist.</td></tr>

<tr><td>Accept-Encoding is empty or does not exist.</td></tr>

<tr><td rowspan="2">HTTP features</td><td>The HTTP HEAD method is used.</td></tr>

<tr><td>The HTTP version is 1.0 or earlier.</td></tr>

</table>


#### IP intelligence features

1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/bot/strategy) and choose **Bot Behavior Management** -> **Bot Protection Settings** on the left sidebar. Find the target domain name and click **Defense settings** in the "Operation" column on the right.
2. On the Defense settings page, select **Custom Session Policy** > **IP Intelligence Characteristics** to enter the corresponding list page.

![](https://main.qcloudimg.com/raw/cfe58a8695dcac4016b30cc19ed23d9b.png)
	- **Field description:**
	
		- **Rule Name:** IP intelligence policy.
		
		- **Action:** the default action of the intelligence feature policy, which is "Monitor" by default. You can set its value in the "Operation" column on the right.
		
		- **Rule Switch:** disabled by default. We recommend that you enable the switch to automatically check the health of your domain names in Tencent Cloud WAF.
		
		- **Modification Time:** the last time the policy was modified.
		
		- **Operation:** click **Edit** to set the action, which can be "Pass", "Monitor", "CAPTCHA", or "Block". For more information, see [Action Category Description](#dzlx).
		
>! This is used to automatically check the health of your domain names. Do not set it to "Block".

	- **The following table lists the names of IP intelligence feature policies.**
	
<table>
	
<tr><th>IP Intelligence Category</th><th>Policy Name</th></tr>

<tr><td >Automated testing</td><td>Automated testing provided by Tencent Cloud WAF.</td></tr>

<tr><td rowspan="11">IDC-IP library</td><td>IDC-IP library - Tencent Cloud.</td></tr>

<tr><td>IDC-IP library - Alibaba Cloud.</td></tr>

<tr><td>IDC-IP library - Huawei Cloud.</td></tr>

<tr><td>IDC-IP library - Kingsoft Cloud.</td></tr>

<tr><td>IDC-IP library - Ucloud.</td></tr>

<tr><td>IDC-IP library - Baidu Cloud.</td></tr>

<tr><td>IDC-IP library - JD Cloud.</td></tr>

<tr><td>IDC-IP library - QingCloud.</td></tr>

<tr><td>IDC-IP library - AWS.</td></tr>

<tr><td>IDC-IP library - Azure.</td></tr>

<tr><td>IDC-IP library - Google Cloud.</td></tr>

</table>


#### Custom session features

1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/bot/strategy) and choose **Bot Behavior Management** -> **Bot Protection Settings** on the left sidebar. Find the target domain name and click **Defense settings** in the "Operation" column on the right.
2. On the **Defense settings** page, choose **Custom Session Policy** > **Custom Session Features** to go to the corresponding list page.

![](https://main.qcloudimg.com/raw/9fe29dd854fd6fa35156e93d49cc4eea.png)
	- **Field description:**
	
		- **SN:** the policy number, which automatically increases.
		
		- **Rule name/Description:** the policy name and description.
		
		- **Condition:** policy match conditions. Up to 10 match conditions can be added for one policy, which are connected by the "AND" relationship.
		
		- **Action:** the action that is set when the policy is added. You can set its value in the "Operation" column on the right.
		
		- **Rule Switch:** policy switch status, which is set when the policy is added.
		
		- **Modification Time:** the last time the policy was added or modified.
		
		- **Operation:** modification or deletion of the policy. Click **Edit** to set the action, which can be "Pass", "Monitor", "CAPTCHA", "Redirect", or "Block". For more information, see [Action Category Description](#dzlx).
		
3. Add custom session features. Click **Add** in the upper-right corner of the list to go to the **Add custom session features** page.

![](https://main.qcloudimg.com/raw/eff73227445febfed7d08f00203079e1.png)
>? Policy priority is determined by the action category in the order: Pass > Monitor > Redirect > CAPTCHA > Block. For policies of the same action category, the more recently a policy was added, the higher its priority.


	- **Field description:**
	
		- **Rule Name:** the policy name.
		
		- **Rule Description:** the policy description.
		
		- **Rule Switch:** enabled by default.
		
		- **Condition:** conditions for matching BOT policies. Up to 10 match conditions can be set, which are connected by the “AND” relationship. When you hover the curse over a match condition, you can view its description.
		
		- **Action**: the action to be taken.
		
		<span id="dzlx"></span>
		
	- **Action Category Description:**
	
	<table>
	
<tr><th  >Category</th><th>Description</th></tr>

<tr><td>Pass</td><td>Session requests that match the set conditions will be allowed and will not be logged.</td></tr>

<tr><td>Monitor</td><td>Session requests that match the set conditions will be monitored. You can view more information on the monitored sessions in the custom bot details.</td></tr>

<tr><td>CAPTCHA</td><td>This is applicable only to access through browsers. Session requests that match the set conditions will be verified through a CAPTCHA. If they fail verification, they will be blocked. Otherwise, they can normally access the domain name within the penalty period.</td></tr>

<tr><td>Redirect</td><td>Session requests that match the set conditions will be redirected to a specified URL of the current domain name within the specified penalty period.</td></tr>

<tr><td>Block</td><td>Session requests that match the set conditions will be blocked. You can set the penalty period to 5 to 10,080 minutes (7 days). You can view the blocking results in the [<a href = "https://console.cloud.tencent.com/guanjia/log/attack">Attack Log</a>], and view the IP addresses blocked in real time in [<a href = "https://console.cloud.tencent.com/guanjia/ip/record">IP Blocking Status</a>].</td></tr>

</table>

	- **The following table lists the match conditions for custom session features:**
	
	<table>
	
<tr><th width=100px>Category</th><th width=150px>Filter Condition</th><th>Description</th></tr>

<tr><td rowspan="6">Session features</td><td>Average Speed</td><td>Total Session Requests/Session Duration in requests/minute.</td></tr>

<tr><td>Window Speed</td><td>Session access frequency for every 2-minute interval (window) in requests/minute.</td></tr>

<tr><td>Total Sessions</td><td>Total number of access requests in a bot session.</td></tr>

<tr><td>Session Duration</td><td>Duration of the bot session.</td></tr>

<tr><td>Robots.txt</td><td>The session request wants to access the `Robots.txt` file.</td></tr>

<tr><td>Session in early morning</td><td>The session request is initiated between 2:00 AM and 5:00 AM.</td></tr>

<tr><td rowspan="3">IP features</td><td>Access real IP</td><td>Access real IP.</td></tr>

<tr><td>IP Type</td><td>IP type, which can be IDC or base station (ISP base station). When the IP type is IDC, exceptions may occur.</td></tr>

<tr><td>IP Owner</td><td>IP owner information such as `tencent.com`, which can be queried in bot details and is valid only if the IP type is IDC.</td></tr>

<tr><td rowspan="5">Request features</td><td>Most Requested URL</td><td>The most frequently requested URL.</td></tr>

<tr><td>URL Duplicate Rate</td><td>Proportion of repeated URLs in session requests, which ranges from 0 to 1. Set this parameter based on your actual business needs. A value that is too high or too low suggests an exception (which must be determined based on the actual business conditions).</td></tr>

<tr><td>URL Class</td><td>Number of URLs in session requests after deduplication.</td></tr>

<tr><td>Most Requested Parameter</td><td>The most frequently requested parameter, which may be a GET request parameter (`Query` content) or POST request parameter (`Body` content).</td></tr>

<tr><td>Parameter Duplicate Rate</td><td>Proportion of repeated GET request parameters (`Query` content) or POST request parameters (`Body` content) in session requests, which ranges from 0 to 1. Set this parameter based on your actual business needs. A value that is too high or too low suggests an exception (which must be determined based on the actual business conditions).</td></tr>

<tr><td rowspan="6">COOKIE</td><td>COOKIE Existence</td><td>Used to check whether the HTTP headers fo session requests have cookies.</td></tr>

<tr><td>Most Requested COOKIE</td><td>The most frequently requested cookie in session requests.</td></tr>

<tr><td>COOKIE Duplicate Rate</td><td>Proportion of repeated cookies in session requests, which ranges from 0 to 1.</td></tr>

<tr><td>COOKIE Existence Rate</td><td>Proportion of requests with a cookie among all session requests, which ranges from 0 to 1.</td></tr>

<tr><td>COOKIE Abuse</td><td>Multiple different UAs use the same cookie.</td></tr>

<tr><td>COOKIE Class</td><td>Number of cookies in session requests after deduplication.</td></tr>

<tr><td rowspan="6">Referer</td><td>Referer Existence</td><td>Used to check whether the HTTP header has a referer in session requests.</td></tr>

<tr><td>Most Requested Referer</td><td>The most frequent HTTP referer in session requests.</td></tr>

<tr><td>Referer Duplicate Rate</td><td>Proportion of repeated referers in session requests, which is valid only for access through browsers and ranges from 0 to 1. A value that is too high suggests an exception (which must be determined based on the actual business conditions).</td></tr>

<tr><td>Referer Existence Rate</td><td>Proportion of requests with a referer in session requests, which is valid only for access through browsers and ranges from 0 to 1. A value that is too low suggests an exception (which must be determined based on the actual business conditions).</td></tr>

<tr><td>Referer Abuse</td><td>Multiple different UAs use the same referer.</td></tr>

<tr><td>Referer Class</td><td>Number of referers in session requests after deduplication.</td></tr>

<tr><td rowspan="6">UA</td><td>UA Existence</td><td>Used to check whether the HTTP headers of session requests have UAs.</td></tr>

<tr><td>Most Requested UA</td><td>The most frequent HTTP `User-Agent` value in session requests.</td></tr>

<tr><td>UA Existence Rate</td><td>Proportion of requests with a UA among session requests, which ranges from 0 to 1. A value that is too low suggests an exception (which must be determined based on the actual business conditions).</td></tr>

<tr><td>UA Class</td><td>Number of UAs in session requests after deduplication, which is valid only for non-proxy IP addresses. A value that is too high suggests an exception (which must be determined based on the actual business conditions).</td></tr>

<tr><td>UA Type</td><td><ul><li>Browser.</li>
	
<li>Mobile device.</li>

<li>Game console or TV.</li>

<li>Public bot.</li>

<li>Private bot.</li>

<li>Automated tool.</li>

<li>Unknown.</li>

<li>Public scanner.</li>

<li>Framework.</li>

<li>Programming language HTTP library.</li><ul></td></tr>

<tr><td>UA Randomness Index</td><td>The random distribution status, which ranges from 0 to 1. The higher the value, the more likely the request is exceptional. <br>Reference thresholds: a value above 0.6 suggests an exception; a value above 0.92 is almost certainly an exception.</td></tr>

<tr><td rowspan="7">HTTP Header</td><td>Accept Existence</td><td>The HTTP headers in session requests will be checked for the `Accept` field.</td></tr>

<tr><td>Accept-Language Existence</td><td>The HTTP headers in session requests will be checked for the `Accept-Language` field.
	
</td></tr>

<tr><td>Accept-Encoding Existence</td><td>The HTTP headers in session requests will be checked for the `Accept-Encoding` field.</td></tr>

<tr><td>Connection Existence</td><td>The HTTP headers in session requests will be checked for the `Connectiton` field.</td></tr>

<tr><td>Request Method Rate</td><td>Proportion of session requests with request methods.</td></tr>

<tr><td>HTTP Version Rate</td><td>Proportion of session requests that use HTTP versions.
	
</td></tr>

<tr><td>Returned Status Code Rate</td><td>Proportion of session requests with status codes returned by WAF.
	
</td></tr>
<tr><td rowspan="7">Advanced Features</td><td>Prediction Tag</td><td>Suspicious behavior predicted by the system. Not all sessions have a prediction tag. A prediction tag can indicate the following:
	
<ul><li>Suspected illegal crawler.</li>
	
<li>Suspected regular crawler.</li>

<li>Suspected login without user value.</li>

<li>Suspected login without user parameter.</li>

<li>Suspected login without username and password.</li>

<li>Suspected login without user login action.</li>

<li>Suspected brute force attack.</li>

<li>Suspected credential stuffing attack.</li>

<li>Suspected unauthorized access to SMS APIs.</li> 

<li>Suspected unauthorized access to CAPTCHA APIs.</li> 

<li>Suspected malicious registration.</li> 

<li>Suspected repeated API access</li></ul></td></tr>

<tr><td>Score</td><td>Bot score for the session given by the intelligent bot analysis engine. The higher the score, the more likely the session is initiated by a bot. The reference value is 5.</td></tr>

<tr><td>AI Model Checkout</td><td>Result of AI behavior analysis model detection. If the AI model flags a request, this suggests an exception.</td></tr>

<tr><td>Public BOT Forging</td><td>Session requests pretend to be in public bot categories. For example, a request uses the UA of a Baidu crawler, but its IP address does not belong to Baidu.</td></tr>

<tr><td>Access to Sensitive API</td><td>Used to determine whether sensitive APIs (such as SMS APIs, registration APIs, and login APIs) are accessed.</td></tr>

<tr><td>Index Exception for Time-series Behavior</td><td>An algorithm used to detect abnormal time-series behaviors. A smaller index suggestions a higher probability of an exception. <br>Reference value thresholds: a value below 0.5 suggests an exception; a value below 0.24 is almost certainly an exception.</td></tr>

<tr><td>Index Exception of Sequential Entropy</td><td>An algorithm used to detect the time-series behavior entropy. A smaller index suggests a higher probability of exception. The reference value threshold is 0.5. A value below 0.5 suggests an exception.</td></tr>

</table>
