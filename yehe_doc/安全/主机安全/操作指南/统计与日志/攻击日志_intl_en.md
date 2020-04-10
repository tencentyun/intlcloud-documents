## Feature Overview
WAF logs information of web attacks by default, which includes the time, source IP, type, and details of attacks. You can set filters to query logs as needed and download the query results.
## Instructions
### Querying attack logs
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/attack) and select **Web Application Firewall** > **Attack Details** on the left sidebar to enter the attack log query page. Click **Log Query**, select the desired domain name in the drop-down list at the top, set query criteria as needed, and click **Query** to view the corresponding attack logs.
![](https://main.qcloudimg.com/raw/b0f782b0ce530ec81cc0106b74366a40.png)
**Query criteria description:**
	- Domain name: you can select the desired domain name in the domain name drop-down list.
	- Time: it is 1 hour by default. You can query attack logs within the last 30 days.
	- Risk level: it is "All" by default. You can select "High", "Medium", or "Low".
	- Executed action: it is "All" by default. You can select "Observe" or "Block".
	- Policy ID: you can enter the desired policy ID (which can be viewed in log entries).
	- Attack source IP: you can enter the attack source IP to query its related logs.
2. Click <img src="https://main.qcloudimg.com/raw/81e64100ad0ed8422617c10b08fee09f.png"  style="margin:0;"> in the top-right corner on the attack log page. In the pop-up "Customize List Field" window, select the fields to be displayed in the list as shown below:
![](https://main.qcloudimg.com/raw/aa47909f3d383b7434672ee9dad93be3.png)
3. View the attack details. Select the desired log entry and click **Details** in the "Operation" column on the right to view the attack details.
![](https://main.qcloudimg.com/raw/bd5c505a0f08c540e7447540ac01b4b3.png)
4. Enter the log details page to view the corresponding fields.
![](https://main.qcloudimg.com/raw/1909e910299b36acc2012d73b6823960.png)

**Log details field description:**
- **Basic Information**

| Field Name | Description |
|---------|---------|
| Domain Name	| Domain name accessed by client. |
| Attack Type	| Attack types currently supported by WAF, which is "All" by default. |
| Aggregated Attacks |	Number of attacks from the same attack source IP and in the same type that are aggregated once every 10 seconds. |
| Attack Source IP |	Source IP of attack against client. |
| Hit Rule ID | ID of the rule that triggers a protection policy. If an attack is detected by the AI engine, the rule ID will be 0. |
| Hit Rule Name	| Name of the rule that triggers a protection policy, which is empty for the rule engine and AI engine.|
| Request Method |	Method of attack request to client. |
| Risk Level |	Level of risk caused by attack against client. |
| Attack Time	| Time when the client is attacked. |
| Matched Source |	Matched source of attack against client, such as source IP. |
| Executed Action |	Action triggered by attack against client. |
| Request URI |	Content of request URI. |
| Attack Content	| Content of attack against client. |

- **Attack Source IP Details**

| Field Name | Description |
|---------|---------|
| Region |	Abbreviation of the country/region where the source IP is purchased. |
| IP Owner	| Owner of purchased source IP. |
| Country/Region |	Name of country/region of attack source IP. |
| District	| District of attack source IP. |
| City |	City of attack source IP. |
| ISP |	ISP of attack source IP. |
| Longitude	| Longitude of attack source IP. |
| Latitude |	Latitude of attack source IP. |

- **Details**

| Field Name | Description |
|---------|---------|
| Protocol Version | HTTP protocol version information of attack source IP. |
| User-Agent | Information such as browser type and OS ID in attack source IP's request to server. |

### Downloading attack logs
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/attack) and select **Web Application Firewall** > **Attack Details** on the left sidebar to enter the attack log query page. Click **Log Query** and click the download icon in the top-right corner to create a download task.
![](https://main.qcloudimg.com/raw/643c9c502e1c9242dce8103a5285199d.png)
>
	- Only one download task can be created within a certain time period. Please be patient.
	- Up to 10,000 logs can be downloaded at a time. If you want to download more logs, you are recommended to download them in multiple batches or [contact us](https://intl.cloud.tencent.com/support) for assistance.
	- If you select a wildcard domain name (e.g., `*.abc.com`), logs of all associated subdomain names such as those suffixed with `.abc.com` will also be downloaded.

2. Click the **Download Task** tab, select a desired download task, and click **Download** in the "Operation" column on the right to download the log file to your local file system.
![](https://main.qcloudimg.com/raw/76f01f3181f1039decf4b848b66ab483.png)
>As the log file is in CSV format and encoded in UTF-8, if opened in Excel, incompatibility will occur, and the attack type will become garbled text. Please use compatible editors such as WPS or Sublime to open it.
>
**Log file field description:**

| Download Field | Description |
|---------|---------|
| attack_time |	Client attack event. |
| rule_id	| ID of rule triggered by attack against client.|
| count	| Number of attacks from the same attack source IP and in the same type that are aggregated once every 10 seconds. |
| status	| Executed action. 0: observing; 1: blocking. |
|domain	| Information of client's attacked domain name. |
| attack_ip	| IP of attack against client. |
| attack_type |	Type of attack against client. |
| args_name	| Attacked object in client request, such as request parameter, URI, or IP. |
| attack_content |	Content of attack against client. |
| uri	| Information of client's attacked URI. |
| method	| Method of attack request to client. |
| user_agent	| Information of client's `User_Agent`. |

