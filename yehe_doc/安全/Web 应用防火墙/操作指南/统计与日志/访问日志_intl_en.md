## Feature Overview
Access logging is used to record access logs of domain names protected by WAF. It allows you to query and download access logs generated in the last 30 days and retain them for up to 180 days. After enabling this feature, you can query and download access logs as needed to meet your security compliance and OPS requirements.
>!
>- To use access logging, you need to [purchase an extra log services pack](https://intl.cloud.tencent.com/document/product/627/11730) and enable access logging as instructed in [Directions](#sysm). Only after this feature is enabled for a domain name can its access requests be logged by WAF.
>- To disable access logging, you can cancel renewal for the billing item at [Renewals](https://console.cloud.tencent.com/account/renewal).

## Directions[](id:sysm)
### Enabling access logging
Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/config), select **Instant Management** > **Domain Name Connection** on the left sidebar, and then click **Enable** for domain names you choose on the Domain Name List. 
![](https://qcloudimg.tencent-cloud.cn/raw/2fbe9fd1743f9368529ec6b9eff37171.png)

### Viewing a log
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/overview). On the left sidebar, select **Log Services** > **Access Logs**.
2. Click the drop-down list in the top left corner of the page to select domain names, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/42a77d62f290d2b298e3ed9d38763143.png)
3. The usage capacity is displayed in top right corner. For more details about WAF billing, click **Learn More**.
4. To view usage capacity and set the retention period at the same time, click **Storage Configuration**, and then click **Save** to save your setting.
>?The retention period ranges from 1 to 30 days.

### Querying a log
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/overview). On the left sidebar, select **Log Services** > **Access Logs**.
2. Search logs by using quick search, filters, or statements.
 - Quick search: supports quick searches based on the query period.
   
 - Search by filter: Select fields and operators, enter the filed values, and click **OK**. You can select multiple fields.

3. Search by statement: supports professional searches by statement and enables you to run more complex log queries. Enter the required information, and then click ![](https://main.qcloudimg.com/raw/de2de3ad90917a2dba3259716cb87963.png).

**Search statement**

<table>
<thead>
<tr>
<th align="left">Reserved Character</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">AND</td>
<td align="left">"AND" logical operator, such as <code>level:ERROR AND pid:1234</code></td>
</tr>
<tr>
<td align="left">OR</td>
<td align="left">"OR" logical operator, such as <code>level:ERROR OR level:WARNING</code></td>
</tr>
<tr>
<td align="left">NOT</td>
<td align="left">"NOT" logical operator, such as <code>level:ERROR NOT pid:1234</code></td>
</tr>
<tr>
<td align="left">TO</td>
<td align="left">"TO" logical operator, such as <code>request_time:[0.1 TO 1.0]</code></td>
</tr>
<tr>
<td align="left">""</td>
<td align="left">Double quotation mark, which quotes a phrase, such as <code>name:"john Smith"</code></td>
</tr>
<tr>
<td align="left">：</td>
<td align="left">Colon, which is used for key-value search, such as <code>level:ERROR</code></td>
</tr>
<tr>
<td align="left">*</td>
<td align="left">Wildcard, which is used to replace zero, one, or more characters, such as <code>host:www.test*.com</code></td>
</tr>
<tr>
<td align="left">?</td>
<td align="left">Wildcard, which is used to replace one character, such as <code>host:www.te?t.com</code></td>
</tr>
<tr>
<td align="left">()</td>
<td align="left">Parentheses, which is used to group clauses to form sub queries and control the logic operations, such as <code>(ERROR OR WARNING) AND pid:1234</code></td>
</tr>
<tr>
<td align="left">&gt;</td>
<td align="left"> Range operator, which indicates the left operand is greater than the right operand, such as <code>status:&gt;400</code></td>
</tr>
<tr>
<td align="left">&gt;=</td>
<td align="left">Range operator, which indicates the left operand is greater than or equal to the right operand, such as <code>status:&gt;=400</code></td>
</tr>
<tr>
<td align="left">&lt;</td>
<td align="left">Range operator, which indicates the left operand is less than the right operand, such as <code>status:&lt;400</code></td>
</tr>
<tr>
<td align="left">&lt;=</td>
<td align="left">Range operator, which indicates the left operand is less than or equal to the right operand, such as <code>status:&lt;=400</code></td>
</tr>
<tr>
<td align="left">[]</td>
<td align="left">Range operator, which includes the upper and lower boundary values, such as <code>age:[20 TO 30]</code></td>
</tr>
<tr>
<td align="left">{}</td>
<td align="left">Range operator, which excludes the upper and lower boundary values, such as <code>age:{20 TO 30}</code></td>
</tr>
<tr>
<td align="left">\</td>
<td align="left">Escape character. An escaped character represents the literal meaning of the character, such as <code>url:\/images\/favicon.ico</code>. You can also use <code>""</code> to wrap special characters as a whole, e.g., <code>url:"/images/favicon.ico"</code>. For details about the difference between these two search methods, see <a href="https://intl.cloud.tencent.com/document/product/614/39594">Configuring Indexes</a>.</td>
</tr>
<tr>
<td align="left">+</td>
<td align="left">Logical operator (similar to AND). The term <code>+A</code> indicates <code>A</code> must exist, such as <code>+level:ERROR +pid:1234</code>.</td>
</tr>
<tr>
<td align="left">-</td>
<td align="left">Logical operator (similar to NOT). The term <code>-A</code> indicates <code>A</code> does not exist, such as <code>+level:ERROR -pid:1234</code>.</td>
</tr>
<tr>
<td align="left">&amp;&amp;</td>
<td align="left">Logical operator (similar to AND), such as <code>level:ERROR &amp;&amp; pid:1234</code></td>
</tr>
<tr>
<td align="left">!</td>
<td align="left">Logical operator (similar to NOT), such as <code>level:ERROR !pid:1234</code></td>
</tr>
<tr>
<td align="left">/</td>
<td align="left">Regular expression identifier in the format of <code>/${regExp}/</code>, e.g., <code>/[mb]oat/</code> returns results containing <code>moat</code> or <code>boat</code>.</td>
</tr>
<tr>
<td align="left">_exists_</td>
<td align="left"><code>_exists_:key</code> returns results where the `key` value is not empty, e.g., <code>_exists_:userAgent</code> returns results where the <code>userAgent</code> value is not empty.</td>
</tr>
<tr>
<td align="left">~</td>
<td align="left">Fuzzy search, e.g., <code>level:errro~</code> returns results where <code>level</code> contains <code>error</code>.</td>
</tr>
</tbody></table>

>!
> - The operators are case-sensitive. For example, `AND` and `OR` represent logical search operators, while `and` and `or` are regarded as common words.
> - When multiple search statements are connected with spaces, they are regarded as in the `OR` logic. For example, `warning error` indicates to return results containing the `warning` keyword or `error` keyword.
> - The following special characters must be escaped: +, -, &&, ||, !, ( ), { }, [ ], ^, ", ~, *, ?, :, \
> - Before performing a `key:value` search, make sure the key is configured in the index configuration of the log topic.
> - Use () to group search conditions and clarify the precedency when using the "AND" and "OR" operators, such as `(ERROR OR WARNING) AND pid:1234`.


### Displaying logs
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/overview). On the left sidebar, select **Log Services** > **Access Logs**.
2. Click **Filed Name** to display top five logs that match the filed.
3. Click ![](https://main.qcloudimg.com/raw/f85fc295aaf54ed8855edb882bb1ce06.png) on the left of the date that the log is generated to view filed details. If you want to view details in JSON format, click **JSON**.

**JSON field description**
<table>
<thead>
<tr>
<th><strong>Field</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody><tr>
<td>domain</td>
<td>Wildcard domain name</td>
</tr>
<tr>
<td>request_time</td>
<td>Time that the client takes to send a request to WAF and receive a response</td>
</tr>
<tr>
<td>uuid</td>
<td>Unique identifier of an HTTP request</td>
</tr>
<tr>
<td>schema</td>
<td>Request protocol: HTTP or HTTPS</td>
</tr>
<tr>
<td>method</td>
<td>Client request method</td>
</tr>
<tr>
<td>url</td>
<td>Request URI, which resides between "/" and "?" in the client’s request path</td>
</tr>
<tr>
<td>host</td>
<td>Client domain name</td>
</tr>
<tr>
<td>http_user_agent</td>
<td>Request UA</td>
</tr>
<tr>
<td>headers</td>
<td>HTTP request header</td>
</tr>
<tr>
<td>upstream_status</td>
<td>Status code returned to WAF from the real server</td>
</tr>
<tr>
<td>status</td>
<td>Status code returned to the client from WAF</td>
</tr>
<tr>
<td>body_bytes_sent</td>
<td>Response body size</td>
</tr>
<tr>
<td>upstream_response_time</td>
<td>Time that WAF takes to receive the client request from the real server</td>
</tr>
<tr>
<td>ip_info.country</td>
<td>Country/Region</td>
</tr>
<tr>
<td>ip_info.city</td>
<td>City</td>
</tr>
<tr>
<td>ip_info.province</td>
<td>Province</td>
</tr>
<tr>
<td>ip_info.operator</td>
<td>ISP</td>
</tr>
<tr>
<td>ip_info.ip_type</td>
<td>IP type</td>
</tr>
<tr>
<td>ip_info.idc</td>
<td>IDC data center</td>
</tr>
<tr>
<td>ip_info.longtitude</td>
<td>Longitude</td>
</tr>
<tr>
<td>ip_info.dimensionality</td>
<td>Latitude</td>
</tr>
</tbody></table>
4. Display the filtered log content in the list mode or field mode.
 - Field mode: This is the default display mode. You can change to the other mode by clicking the icon in the top right corner.

 - List mode: Click ![](https://main.qcloudimg.com/raw/1c901122eac1bd6e8f21815d777551b7.png) to change to list view.

**Field description**
<table>
<thead>
<tr>
<th><strong>Field</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody><tr>
<td>msec</td>
<td>Timestamp of when the request is sent</td>
</tr>
<tr>
<td>schema</td>
<td>Request protocol: HTTP or HTTPS</td>
</tr>
<tr>
<td>method</td>
<td>Client request method</td>
</tr>
<tr>
<td>host</td>
<td>Client domain name</td>
</tr>
<tr>
<td>url</td>
<td>Request URI, which resides between "/" and "?" in the client’s request path</td>
</tr>
<tr>
<td>query</td>
<td>HTTP Query String. The maximum length is 1 KB.</td>
</tr>
<tr>
<td>body</td>
<td>Request body data</td>
</tr>
<tr>
<td>http_referer</td>
<td>Page source</td>
</tr>
<tr>
<td>http_user_agent</td>
<td>Request UA</td>
</tr>
<tr>
<td>http_x_forwarded_for</td>
<td>All the proxies that pass the request</td>
</tr>
<tr>
<td>cookie</td>
<td>Request cookie. The maximum length is 1 KB.</td>
</tr>
<tr>
<td>upstream_status</td>
<td>Status code returned to WAF from the real server</td>
</tr>
<tr>
<td>upstream_response_time</td>
<td>Time that WAF takes to receive the client request from the real server</td>
</tr>
<tr>
<td>upstream_addr</td>
<td>Upstream server IP</td>
</tr>
<tr>
<td>status</td>
<td>Status code returned to the client from WAF</td>
</tr>
<tr>
<td>upstream_status</td>
<td>Status code returned to WAF from the real server</td>
</tr>
<tr>
<td>upstream_response_length</td>
<td>Response length returned from the upstream server</td>
</tr>
<tr>
<td>edition</td>
<td>WAF versions: `sparta-waf`, `clb-waf`, `cdn-waf</td>
</tr>
</tbody></table>

### Downloading access logs
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/overview). On the left sidebar, select **Log Services** > **Access Logs**.
2. Click ![](https://main.qcloudimg.com/raw/789f18df056dbc4e37f5a325b613ca70.png) to enter the download page. Click **OK** to create a download task.
>?	
>- You cannot create more than one download task simultaneously.
>- Up to 1 million logs can be downloaded at a time. To download more logs, it is recommended that you create multiple tasks to download them in batches.
>- If you select a wildcard domain name (for example, *.abc.com), logs of all associated subdomain names such as those suffixed with .abc.com will also be downloaded.
>- Up to five download tasks can be created.


3. On the download page, click **View Task** to view the download details, such as the task number, creation time, and total number of logs.

**Log field description**
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>domain</td>
<td>Wildcard domain name</td>
</tr>
<tr>
<td>bytes_sent</td>
<td>Response size, including response headers (in bytes) and downstream bandwidth</td>
</tr>
<tr>
<td>method</td>
<td>Client request method</td>
</tr>
<tr>
<td>request_time</td>
<td>Time that the client takes to send a request to WAF and receive a response</td>
</tr>
<tr>
<td>http_connection</td>
<td>HTTP request header Connection</td>
</tr>
<tr>
<td>upstream_connect_time</td>
<td>Time that WAF takes to send the client request to the real server</td>
</tr>
<tr>
<td>uuid</td>
<td>Unique identifier of an HTTP request</td>
</tr>
<tr>
<td>upstream_addr</td>
<td>Upstream server IP</td>
</tr>
<tr>
<td>host</td>
<td>Client domain name</td>
</tr>
<tr>
<td>upstream_response_length</td>
<td>Response length returned from the upstream server</td>
</tr>
<tr>
<td>schema</td>
<td>Request protocol: HTTP or HTTPS</td>
</tr>
<tr>
<td>http_user_agent</td>
<td>Request UA</td>
</tr>
<tr>
<td>headers</td>
<td>HTTP request header</td>
</tr>
<tr>
<td>url</td>
<td>Request URI, which resides between "/" and "?" in the client’s request path</td>
</tr>
<tr>
<td>http_x_forwarded_for</td>
<td>All the proxies that pass the request</td>
</tr>
<tr>
<td>http_referer</td>
<td>Page source</td>
</tr>
<tr>
<td>body</td>
<td>Request body data</td>
</tr>
<tr>
<td>remote_addr</td>
<td>Requester IP</td>
</tr>
<tr>
<td>cookie</td>
<td>Request cookie. The maximum length is 1 KB.</td>
</tr>
<tr>
<td>bot_client_ip</td>
<td>Client IP, which is typically the same as `remote_addr`</td>
</tr>
<tr>
<td>request_length</td>
<td>Request length</td>
</tr>
<tr>
<td>http_accept</td>
<td>HTTP request header Accept</td>
</tr>
<tr>
<td>status</td>
<td>Status code returned to the client from WAF</td>
</tr>
<tr>
<td>protocol</td>
<td>HTTP protocol, such as 1.1、1.0 and 2.0</td>
</tr>
<tr>
<td>msec</td>
<td>Timestamp of when the request is sent</td>
</tr>
<tr>
<td>pipe</td>
<td>Nginx built-in variable</td>
</tr>
<tr>
<td>content_type</td>
<td>HTTP request header Content-Type</td>
</tr>
<tr>
<td>time_local</td>
<td>Nginx readable local time string</td>
</tr>
<tr>
<td>upstream_response_time</td>
<td>Time that WAF takes to receive the client request from the real server</td>
</tr>
<tr>
<td>server_addr</td>
<td>WAF private IP</td>
</tr>
<tr>
<td>edition</td>
<td>WAF versions: `sparta-waf`, `clb-waf`, `cdn-waf`</td>
</tr>
<tr>
<td>upstream_status</td>
<td>Status code returned to WAF from the real server</td>
</tr>
<tr>
<td>body_bytes_sent</td>
<td>Response body size</td>
</tr>
<tr>
<td>query</td>
<td>HTTP Query String. The maximum length is 1 KB.</td>
</tr>
</tbody></table>
