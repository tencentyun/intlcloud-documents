## Overview
WAF logs information on cyberattacks by default, which includes the time, source IP, type, and details of attacks. You can set filters to query logs as needed and download the query results.
## Instructions
### Querying attack logs
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/attack) and choose **Web Application Firewall** -> **Attack Log** on the left sidebar. On the **Attack Log** page, click **Log Search**, select the target domain name in the drop-down list at the top, set search criteria as needed, and click **Search** to view the corresponding attack logs.
![](https://main.qcloudimg.com/raw/b0f782b0ce530ec81cc0106b74366a40.png)
**Search criteria description:**
	- Domain name: select the target domain name in the domain name drop-down list.
	- Attack time: it is `Last 1 hour` by default. You can search attack logs of up to 30 days.
	- Risk grade: it is `All risk grades` by default. You can select `Major`, `Medium`, or `Minor`.
	- Action: it is `All actions` by default. You can select `Observation` or `Block`.
	- Rule ID: enter the target rule ID, which can be found in the log entries.
	- Attack source IP: enter the attack source IP that you want to search.
2. Click the <img src="https://main.qcloudimg.com/raw/81e64100ad0ed8422617c10b08fee09f.png"  style="margin:0;"> button at the upper-right corner. In the **Custom fields** dialog box, select the fields to be displayed in the list, as shown in the following figure.
![](https://main.qcloudimg.com/raw/aa47909f3d383b7434672ee9dad93be3.png)
3. View the attack details. Select the target log entry and click **details** in the "Operation" column on the right to view the attack details.
![](https://main.qcloudimg.com/raw/bd5c505a0f08c540e7447540ac01b4b3.png)
4. On the log details page, view the corresponding fields.
![](https://main.qcloudimg.com/raw/22e19c007e25ea977b978861c73e10d4.png)

**Log details field description:**
- **Basic Info**

| Field | Description |
|---------|---------|
| Domain Name | Domain name accessed by the client. |
| Attack type | Attack types currently supported by `WAF`, which is "All" by default. |
| Attack Count | Number of attacks from the same attack source IP address and of the same type, calculated once every 10 seconds. |
| Attack source IP | Source IP address of a client attack.|
| Rule ID | ID of the rule that triggers a protection policy. If an attack is detected by the AI engine, the rule ID will be 0. |
| Rule Name | Name of the rule that triggers a protection policy, which is empty for the rule engine and AI engine. |
| Request method | Method of the attack requests used in a client attack. |
| Risk grade | Level of risk caused by the client attack. |
| Attack time | Time of the client attack. |
| Source | Source matching information of the client attack, such as the source IP address. |
| Action | Action triggered by the client attack. |
| Request URI | Content of the request URI. |
| Attack Content | Content of the client attack. |

- **Attack IP Details**

| Field | Description |
|---------|---------|
| Region | Abbreviation of the country/region where the source IP address was purchased. |
| IP Owner | Owner of the purchased source IP address. |
| Country | Country/region where attack source IP address is registered. |
| Province | Province where the attack source IP address is registered. |
| City | City where the attack source IP address is registered. |
| Carrier | ISP to which the attack source IP address belongs. |
| Longitude | Longitude of the attack source IP address. |
| Latitude | Latitude of the attack source IP address. |

- **Details**

| Field | Description |
|---------|---------|
| Protocol Version | HTTP version information of the attack source IP address. |
| User-Agent | Information such as browser type and OS ID in the requests from the attack source IP address to a server. |

### Downloading attack logs
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/attack) and select **Web Application Firewall** -> **Attack Log** on the left sidebar. On the **Attack Log** page, click **Log Search** and click the download icon in the upper-right corner to create a download task.
![](https://main.qcloudimg.com/raw/643c9c502e1c9242dce8103a5285199d.png)
>!
	- Only one download task can be created within a certain time period.
	- Up to 10,000 logs can be downloaded at a time. If you want to download more logs, we recommend that you download them in multiple batches or [contact us](https://intl.cloud.tencent.com/support) for assistance.
	- If you select a wildcard domain name (e.g., `*.abc.com`), logs of all associated subdomain names such as those suffixed with `.abc.com` will also be downloaded.

2. Click the **Download Task** tab, select a target download task, and click **Download** in the **Operation** column on the right to download the log file to your local file system.
![](https://main.qcloudimg.com/raw/76f01f3181f1039decf4b848b66ab483.png)
>! As the log file is in CSV format and encoded in UTF-8, it is incompatible with Excel. If opened in Excel, the attack type will appear as garbled text. Please use compatible editors such as WPS or Sublime to open it.
>
** Log file field description:**

| Download Field | Description |
|---------|---------|
| attack_time | Time of the client attack. |
| rule_id | ID of the rule triggered by the client attack. |
| count | Number of attacks from the same attack source IP address and of the same type, calculated once every 10 seconds. |
| status | Action taken. 0: observation; 1: block. |
| domain | Information of the domain name targeted by the client attack. |
| attack_ip | IP address of the client attack. |
| attack_type | Type of the client attack. |
| args_name | Location of the attack in the client request, such as request parameter, URI, or IP. |
| attack_content | Content of the client attack. |
| uri | URI information for the client attack. |
| method | Method of the attack requests used in the client attack. |
| user_agent | User_Agent information of the client. |

