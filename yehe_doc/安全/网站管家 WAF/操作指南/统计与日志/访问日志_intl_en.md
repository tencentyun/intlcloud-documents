## Feature Overview
The access log feature is used to record access logs of domain names protected by WAF. It allows you to query and download access logs generated in the last 30 days and retain them for up to 180 days. After enabling this feature, you can query and download access logs as needed to meet your security compliance and OPS requirements.
>To use the access log feature, you need to [purchase the security log service package](https://intl.cloud.tencent.com/document/product/627/11730) and enable access log as instructed in [Instructions](#sysm). Only after access log is enabled for a domain name can its access requests be logged by WAF.

<span id ="sysm"></span>
## Instructions
### Enabling access log
Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/config) and select **Web Application Firewall** > **Protection Setting** on the left sidebar to enter the protection settings page. Select a desired domain name and click **Enable Access Log**. 
![](https://main.qcloudimg.com/raw/0d6ec65518d8c4beabe3bc6ccfb283c2.png)

### Querying access logs
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/config) and select **Security Overview** on the left sidebar to enter the security overview page. Select **Access Log** > **Log Query** and select a desired domain name to view its access logs.
![](https://main.qcloudimg.com/raw/8747d77ac8d40fa3a2daa51ebca513f6.png)
2. You can click <img src="https://main.qcloudimg.com/raw/81e64100ad0ed8422617c10b08fee09f.png"  style="margin:0;"> in the top-right corner as shown above. On the "Customize List Field" page, select the fields to be displayed in the list as shown below:
![](https://main.qcloudimg.com/raw/2becf70cc2f40a89a2d417b480e68be5.png)
3. Query the access logs. You can use multiple keywords separated by carriage return. After entering the keywords of the corresponding fields, click **Query** to search for logs.
![](https://main.qcloudimg.com/raw/9166164f1d6ecaa33222df10000b22ee.png)
 >
>- Access logs can be queried by key-value (kv) pairs where up to 7 keys are supported. In `value`, you can enter multiple keywords of log data for easier search, which are case-insensitive and separated by separators (default separators include !@#%^&*()-_="', <>/?|\;:\n\t\r[]{}).
>- Access log supports fuzzy query. You can use certain fuzzy keywords to query logs as described below:

| Metacharacter | Description |
|---------|---------|
| *	 | Fuzzy query of keywords that can match zero, single, or multiple random characters. `*` cannot be used as the first character. For example, if you enter `abc*`, all logs beginning with `abc` will be returned. |
| ?	 | Fuzzy query of keywords that can match a single character at a specific position. For example, if you enter `ab?c`, logs that begin with `ab`, end with `c`, and contain only one character between `ab` and `c` will be returned. |


Log query field description:

| Field Name | Description |
|---------|---------|
| Access source IP | Source IP of client request. |
| Access URI	| URI accessed by client. |
| Referer	| Source URL information of client's access request to server. |
| Cookie	| Cookie information carried in client's access request to server. |
| User-Agent	| Information such as browser type and OS ID in client's request to server. |
| X-Forworder-For	| Used to identify the original IP address of client accessing web server through HTTP proxy or load balancer. |
| WAF response code	| Response status code returned by WAF to client. |
| Real server response code	| Response status code returned by real server to WAF. |
| Body	| Body information carried in client's access request to server. |

### Downloading access logs
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/config) and select **Security Overview** on the left sidebar to enter the security overview page. Select **Access Log** > **Log Query** and click the download icon in the top-right corner to create a download task.
![](https://main.qcloudimg.com/raw/7d0fe9615ddb279f90124f64b3f20a59.png)

>
- Only one download task can be created within a certain time period. Please be patient.
- Up to 10,000 logs can be downloaded at a time. If you want to download more logs, you are recommended to download them in multiple batches or [contact us](https://intl.cloud.tencent.com/support) for assistance.
- If you select a wildcard domain name (e.g., `*.abc.com`), logs of all associated subdomain names such as those suffixed with `.abc.com` will also be downloaded.

2. Click **Query Download Task**, select the desired download task, and click **Download** to download the log file to your local file system.
![](https://main.qcloudimg.com/raw/0dfe2da477191d8f6576c1691e1cc336.png)
Log file field description:

| Download Field | Description |
|---------|---------|
| time | Access time. |
|host	| Client request domain name. |
|client	| Client's source IP.|
|ipinfo_nation	| Country/region information of client's source IP. |
|ipinfo_province	| District information of client's source IP. |
|schema	| Client request protocol. |
|method	| Client request method. |
|url	| Content between the first "/" and "?" after domain name in complete path of client request. |
|query	| Content after "?" in complete path of client request, which is also called query string. |
|cookie	| Cookie information carried in client's access request to server. |
|referer	| Source URL information of client's access request to server. |
|user-agent	| Information such as browser type and OS ID in client's request to server. |
|x-forwarded-for	| Used to identify the original IP address of client accessing web server through HTTP proxy or load balancer. |
|status	| Response status code returned by WAF to client. |
|upstream_status	| Response status code returned by real server to WAF. |
|upstream	| Intermediate IP and port after a client request passes through WAF. |
|upstream_connect_time	| The time it takes for a client request to arrive at the real server from WAF. |
|upstream_response_time	| The time it takes for a client request to arrive at WAF from the real server. |
|request_time	| The time it takes for a client request to arrive at WAF and return from WAF. |
