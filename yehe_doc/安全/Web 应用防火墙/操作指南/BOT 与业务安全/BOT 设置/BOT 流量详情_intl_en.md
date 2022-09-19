## Overview
With data provided by the bot traffic management module, bot traffic analysis quickly analyzes the bot impacts on domain names in terms of bot feature metrics, including the types of bots, proportion of actions, bot score distribution, top data by request count and URLs that may be affected. You can click **View details** to view the bot details of an access source, and its access characteristics and exceptions detected.

The bot traffic details section displays the bot traffic details of top 10 access sources. You can also view their session access information and logs if session settings are configured, and the information of these access sources/IPs by retrieval.


## Prerequisites
You have subscribed to the [bot traffic management](https://intl.cloud.tencent.com/document/product/627/47799) service and enabled bot traffic analysis.

## Directions
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-flowanalysis) and select **Bot Traffic Analysis** on the left sidebar. Open the **Bot traffic details** tab.
2. On the page displayed, click the drop-down list in the upper-left corner and select a domain name.
3. Specify a date or use the filter to search top 10 access sources of all domain names or a specific domain name. Then click **View logs** of the access source you want to view.
![](https://qcloudimg.tencent-cloud.cn/raw/a1daa51d16c11b69a86df1a2f2f149b9.png)
4. To view traffic details of an access source, click **View details** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/85c3657b10a44d8c612903697013ef16.png)

### Viewing access overview
The bot traffic details page shows you the estimated risk value of the access source and the information of the hit policy, and allows you to take measures such as adding the access source to the allowlist/blocklist and creating custom rules targeting the access source.
![](https://qcloudimg.tencent-cloud.cn/raw/46f468f7e80da3afe9a728b07685a2d7.png)

**Field description:**
 - IP address and tag: It displays the IP address of an access source and the hit tag that identifies the bot category.
 - Last request: It displays the score of the last access request from the access source and the risk level.
 - Session count: It displays the number of continuous sessions on the website accessed occurred in the last access request.
 - Access address: It displays the domain name of the access source.
 - Exception feature: It displays modules that detect exceptional features of the access source.
 - Hit modules: It displays modules that take actions to combat bots.
 - Policy ID: It is the ID of a hit policy.
 - View access logs: It redirects you to the access logs page where you can view the access details of the access source.
 - Add to allowlist: It allows you to add the access source to the allowlist.
 - Add to blocklist: It allows you to add the access source to the blocklist.
 - Add custom rules:  It allows you to add custom rules targeting the access source.

### Viewing bot scores
In the bot score distribution and bot action distribution sections, you can view the distribution of bot scores and bot actions within the selected period, helping you determine the risk level of the access source.

### Viewing bot information
The bot traffic details page also displays information of the automated access source including the features of the bot and access request, threat intelligence and AI evaluation information, bot flow statistics and sessions. Using this data, you can quickly identify exceptions in the access request and take measures against the bot.
![](https://qcloudimg.tencent-cloud.cn/raw/990be3be63bb580eb818cb4121388ed9.png)
![](https://qcloudimg.tencent-cloud.cn/raw/2b9da02cb298891e8da49ea36e78f4db.png)

#### Basic session information
On the basic session information tab, you can view the information of the access source IP and session separately.

![](https://qcloudimg.tencent-cloud.cn/raw/5c86dd786034e4d085000af79c6e2d84.png)


**Field description:**
- IP information
 - Access source IP: IP address of an access source.
 - City: City where the access source is located.
 - Region: Country where the access source is located.
 - IP type: IP type of the access source.
 - IP owner: IP owner of the access source.
- Session information
 - Session average speed: The average session speed of the access source in the latest session, which is calculated by the total number of session requests/session duration. Unit: times/minute.
 - Total sessions: The total number of sessions of the access source in the latest session.
 - Whether Robots.txt exists: Whether the access source has accessed the Robots.txt file, which is often accessed by bot sessions.
 - Session duration: Amount of time the latest session initiated by the access source.

#### Request feature information
 On the request feature information tab, you can view the information of the request features, Cookie, User-Agent, Referer, and Query in the session request.
![](https://qcloudimg.tencent-cloud.cn/raw/f78f5726a52647ac86397ce35aa9ff1c.png)


 **Field description:**
<table>
<thead>
<tr>
<th>Type</th>
<th>Metric</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
 <td  rowspan=6 >Request feature information</td>
<td>Percentage of repeated URLs</td>
<td>Percentage of the repeated URLs in a session request. The value range is 0-1. Set this parameter based on your actual business needs. A value that is too high or too low suggests an exception (which must be determined based on the actual business conditions).</td>
</tr>
<tr>
 <td>Total URL types</td>
<td>Number of deduplicated URLs in a session request.</td>
</tr>
<tr>
 <td>Minimum URL depth</td>
<td>Minimum directory levels of URLs in a session request.</td>
</tr>
<tr>
 <td>Maximum URL depth</td>
<td>Maximum directory levels of URLs in a session request.</td>
</tr>
<tr>
 <td>Average URL depth</td>
<td>Average directory levels of URLs in a session request.</td>
</tr>
<tr>
 <td>Total URLs</td>
<td>Total number of URLs visited in a session request (including duplicates).</td>
</tr>
<tr>
 <td  rowspan=6 >Cookie information</td>
<td>Whether Cookie is abused</td>
<td>Different types of UAs use the same Cookie.</td>
</tr>
<tr>
 <td>Cookie exist</td>
<td>Whether the Cookie exists in all session requests.</td>
</tr>
<tr>
 <td>Percentage of repeated Cookies</td>
<td>Percentage of the repeated Cookies in a session request. The value ranges from 0-1.</td>
</tr>
<tr>
 <td>Cookie validity</td>
<td>Percentage of the Cookies that can be parsed in a session request.</td>
</tr>
<tr>
 <td>Most used Cookie</td>
<td>Most used Cookies in a session request.</td>
</tr>
<tr>
 <td>Percentage of the most used Cookies</td>
<td>Percentage of the most used Cookies in a session request.</td>
</tr>
<tr>
 <td  rowspan=8 >User-Agent information</td>
<td>User-Agent type</td>
<td>User-Agent type of the request user in a session request.</td>
</tr>
<tr>
 <td>User-Agent exist</td>
<td>Whether User-Agent exists in a session request.</td>
</tr>
<tr>
 <td>User-Agent randomness index</td>
<td>Random distribution of User-Agents in a session request. When the reference value threshold exceeds 0.6, an exception is suspected; when it exceeds 0.92, an exception is basically confirmed.</td>
</tr>
<tr>
 <td>User-Agent type</td>
<td>Number of deduplicated User-Agents in a session request, which is valid only for non-proxy IPs. A value that is too high suggests an exception (which must be determined based on the actual business conditions).</td>
</tr>
<tr>
 <td>User-Agent existence rate</td>
<td>Existence rate of UAs in a session request, which ranges from 0 to 1. A value too small may be suspected as an exception (which must be determined based on the actual business conditions).</td></tr>
</tr>
<tr>
 <td>Most used User-Agent</td>
<td>Most used value of the HTTP User-Agent in a session request.</td>
</tr>
<tr>
 <td>Percentage of the most used User-Agents</td>
<td>Percentage of the most used HTTP User-Agent values ​in a session request.</td>
</tr>
<tr>
 <td>User-Agent similarity rate</td>
<td>Similarity between the most used value and the rest in a session request.</td>
</tr>
<tr>
 <td  rowspan=6 >Referer information</td>
<td>Percentage of repeated Referers</td>
<td>Percentage of repeated Referers in a session request, which is valid only for access through browsers and ranges from 0 to 1. A value that is too high suggests an exception (which must be determined based on the actual business conditions).</td>
</tr>
<tr>
 <td>Referer exist</td>
<td>Existence rate of Referers in a session request, which ranges from 0 to 1. A value too small may be suspected as an exception. It's available for browser access.</td>
</tr>
<tr>
 <td>Referer existence rate</td>
<td>Existence rate of Referers in a session request, which ranges from 0 to 1. A value too small may be suspected as an exception. It's available for browser access.</td>
</tr>
<tr>
 <td>Whether Referer is abused</td>
<td>Different types of UAs use the same Referer.</td>
</tr>
<tr>
 <td>Most used Referer</td>
<td>Most used value of the HTTP Referer in a session request.</td>
</tr>
<tr>
 <td>Percentage of the most used Referers</td>
<td>Percentage of the most used HTTP Referer values in a session request.</td>
</tr>
<tr>
 <td  rowspan=2 >Query information</td>
<td>Percentage of repeated Query parameters</td>
<td>Percentage of repeated GET request parameters (`Query` content) or POST request parameters (`Body` content) in a session request, which ranges from 0 to 1. Set this parameter based on your actual business needs. A value that is too high or too low suggests an exception (which must be determined based on the actual business conditions).</td>
</tr>
<tr>
<td>Total query parameter types</td>
<td>Most used parameters in a session request, which may be GET request parameters (`Query` content) or POST request parameters (`Body` content).</td>
</tr>
</tbody></table>

#### Threat intelligence
The threat intelligence tab displays the known information that matches the current access source IP/session ID, such as the IDC details of the access source.
- IDC details: If the information of the access source includes the IDC, the IDC information will be displayed.
- Threat Intelligence: If the IP information of the access source is matched, the matched tag and its definition will be displayed.

#### AI evaluation
The AI evaluation tab displays the following feature metrics detected exceptionally and the corresponding probability values, including information of Cookie, User-Agent, Referer, and Query. If a metric's value larger than 0, this metric is considered exceptional.

![](https://qcloudimg.tencent-cloud.cn/raw/d3799fbd7a34c1e0ee8415d7b8759ee5.png)
#### Bot flow statistics
The bot flow statistics tab displays the feature metrics detected exceptionally, and the corresponding values estimated, as well as the reference values.

![](https://qcloudimg.tencent-cloud.cn/raw/6294dca3e66fefeae3bf1f31407a2190.png)
 **Field description:**

| Metric           | Description                                                     |
| ------------------ | ------------------------------------------------------------ |
| Session average speed   | This metric indicates that the session average speed is considered exceptional, and gives a probability threshold to confirm the exception. |
| User-Agent type | This metric indicates that the User-Agent type is considered exceptional, and gives a probability threshold to confirm the exception. |
| URL type        | This metric indicates that the URL type is considered exceptional, and gives a probability threshold to confirm the exception. |
| Session duration   | This metric indicates that the session duration is considered exceptional, and gives a probability threshold to confirm the exception. |
| Total session count     | This metric indicates that the total session count is considered exceptional, and gives a probability threshold to confirm the exception. |

#### Session management
The session management tab displays the IP addresses accessed by the current session, the number of accesses by each IP address, and the access logs of the current session ID.
>? When session settings are configured, the session management tab will be displayed.

![](https://qcloudimg.tencent-cloud.cn/raw/3cb900c31c4c3dce16ea13d1367ecec8.png)
