CLB supports configuring layer-7 (HTTP/HTTPS) access logs that can help you better understand client requests, troubleshoot issues, and analyze user behaviors. Currently, access logs can be stored in CLS, reported at a minute granularity, and searched online by multiple rules.

Access logs of CLB are mainly used to quickly locate and troubleshoot issues. The access logging feature includes log reporting, storage, and search:
- Log reporting provides best-effort service, that is, it prioritizes service forwarding over log reporting.
- Log storage and search provide SLA based on the storage service currently in use.

>?
>- Currently, access logs can be stored in CLS only for layer-7 protocols (HTTP/HTTPS) but not layer-4 protocols (TCP/UDP/TCP SSL).
- Storing CLB access logs to CLS is now free of charge. You only need to pay for the CLS service.
- This feature is only supported in CLS available regions. See [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).



## Method 1: Single-Instance Access Logging
### Step 1. Enable access log storage in CLS
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3), and click **Instance Management** on the left sidebar.
2. Click the CLB instance ID to open the **Instance Management** page.
3. Click the pencil icon in the **Access Log (Layer-7)** module on the **Basic Information** page.
![](https://main.qcloudimg.com/raw/b3f9b4276b4ff2f28ac184478ce7964c.png)
4. In the pop-up **Modify CLS Log Storage Location** window, enable logging and select the destination logset and log topic for access log storage, and then click **Submit**. If you haven't created a logset or log topic yet, please [create relevant resources](https://console.cloud.tencent.com/cls/logset) and then select them as the storage location.
![](https://main.qcloudimg.com/raw/33386c84ae812881548d1b621fbe6a70.png)
>?You are recommended to use a log topic marked with "CLB" in the clb_logset logset. The differences between a log topic marked with "CLB" and a common one are:
>- CLB log topics can automatically create an index, while a common log topic requires manual index creation.
>- A dashboard is provided for CLB log topics by default, but needs to be manually configured for a common log topic.
6. Click the logset or log topic to redirect to the log search page in CLS.
7. (Optional) To disable logging, click the pencil icon to open **Modify CLS Log Storage Location** window, and disable it.

### Step 2. Configure log topic indexes
>?If the access log is configured for a single instance, you must configure the index for the log topic; otherwise, no logs can be found.
>
The recommended indexes are as follows:

| Key-Value Index    | Field Type | Delimiter |
| :---------- | :------- | :----- |
| server_addr | text     | No delimiter required     |
| server_name | text     | No delimiter required     |
| http_host   | text     | No delimiter required     |
| status      | long     | -     |
| vip_vpcid   | long     | -     |

The steps are as follows:
1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls), and click **Log Topic** on the left sidebar.
2. Click the target log topic ID on the "Log Topic" page.
3. On the log topic details page, select the **Index Configuration** tab, and click **Edit** to add indexes. See [Configuring Index](https://intl.cloud.tencent.com/document/product/614/39594) for more information on index configuration.
![](https://main.qcloudimg.com/raw/38b22da412497a25ac9d6d304766d1ac.png)
4. The result of index configuration is as shown below:
![](https://main.qcloudimg.com/raw/6e2393e34cd06c5d073faba88d34110f.png)

### Step 3. View access logs
1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls) and click **Search and Analysis** on the left sidebar.
2. On the **Search Analysis** page, select a logset, log topic, and time range, and click **Search Analysis** to search for the access logs reported by CLB to CLS. See [Legacy CLS Search Syntax](https://intl.cloud.tencent.com/document/product/614/37882) for more information on search syntax.
![](https://main.qcloudimg.com/raw/e15271ea2d1ffac0e735eb254224a5e5.png)

## Method 2: Batch configure access logging

### Step 1. Create logsets and log topics[](id:step2)
To configure access logs in CLS, you need to first creat a logset and log topic.
You can directly jump to [Step 2](#step3) if you have created a logset and log topic.
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb) and select **Access Logs** on the left sidebar.
2. On the **Access Logs** page, select a region for the logset, and then click **Create Logset** in the "Logset Information" section.
3. In the pop-up **Create Logse**" dialog box, set the retention period and click **Save**.
>?You can only create a single logset named "clb_logset" in each region.
4. Click **Create Log Topic** in the **Log Topic** section of the "Access Logs" page.
5. In the pop-up window, select a CLB instance to add to the list on the right, and then click **Save**.
>?
>- When creating a log topic, you can add a CLB instance as needed. To add one, select a log topic in the list and click **Manage** in the operation column. Each CLB instance can only be added to one log topic.
>- A logset can contain multiple log topics. You can categorize CLB logs into various log topics which will be marked with "CLB".
>
6. (Optional) To disable logging, just click **Disable**.

### Step2. View access logs[](id:step3)
Without any manual configurations, CLB has been automatically configured with index search by access log valuable. You can directly query access logs through search and analysis.
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb) and select **Access Logs** on the left sidebar.
2. Select a log topic, and click **Search** in the operation column to redirect to the **Search Analysis** page in the [CLS Console](https://console.cloud.tencent.com/cls/search).
3. On the **Search Analysis** page, enter the search syntax in the input box, select a time range, and then click **Search Analysis** to search for access logs reported by CLB to CLS.
>?See [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439) for more information on search syntax.


## Log Format and Variable Description
### Log format
```
[$stgw_request_id] [$time_local] [$protocol_type] [$server_addr:$server_port]  [$server_name] [$remote_addr:$remote_port] [$status] [$upstream_addr] [$upstream_status] [$proxy_host] [$request] [$request_length] [$bytes_sent] [$http_host] [$http_user_agent] [$http_referer] [$request_time] [$upstream_response_time] [$upstream_connect_time] [$upstream_header_time] [$tcpinfo_rtt] [$connection] [$connection_requests] [$ssl_handshake_time] [$ssl_cipher] [$ssl_protocol] [$vip_vpcid] [$uri] [$server_protocol]
```

### Field type
Currently, CLS supports the following three field types:

| Name   | Type Description                 |
| :----- | :----------------------- |
| text   | Text type                 |
| long   | Integer type (Int 64)   |
| double | Floating point type (64 bit) |

## Log variable description
<table class="table"><thead><tr><th>Variable</th><th>Description</th></tr></thead>Field Type</th></tr></thead>
<tbody><tr><td>stgw_request_id</td><td> Request ID. </td></tr>text</td></tr>
<tr><td>time_local</td><td> Access time and time zone, such as "01/Jul/2019:11:11:00 +0800" where "+0800" represents UTC+8, i.e., Beijing time.</td><td>text</td></tr>
<tr><td>protocol_type</td><td> Protocol type (HTTP/HTTPS/SPDY/HTTP2/WS/WSS).</td><td>text</td></tr>
<tr><td>server_addr</td><td>CLB VIP. </td><td>text</td></tr>
<tr><td>server_port</td><td>CLB VPort, i.e., the listening port.</td><td>long</td></tr>
<tr><td>server_name</td><td> `server_name` of a rule, i.e., the domain name configured in a CLB listener.</td><td>text</td></tr>
<tr><td>remote_addr</td><td> Client IP.</td><td>text</td>
<tr><td>remote_port</td><td> Client port.</td><td>long</td></tr>
<tr><td>status</td><td> Status code returned to client. </td><td>long</td></tr>
<tr><td>upstream_addr</td><td> RS address.</td><td>text</td>
<tr><td>upstream_status</td><td> Status code returned by RS to CLB. </td><td>text</td></tr>
<tr><td>proxy_host</td><td> Stream ID. </td><td>text</td>
<tr><td>request</td><td> Request line. </td><td>text</td></tr>
<tr><td>request_length</td><td> Number of bytes of request received from client.</td><td>long</td></tr>
<tr><td>bytes_sent</td><td> Number of bytes sent to client.<td>long</td></tr>
<tr><td>http_host</td><td> Request domain name, i.e., the host of the HTTP header.</td><td>text</td></tr>
<tr><td>http_user_agent</td><td> `user_agent` field of the HTTP header.</td><td>text</td></tr>
<tr><td>http_referer</td><td> HTTP request source. </td><td>text</td></tr>
<tr><td>request_time</td><td> Request processing time. The timing begins when the first byte is received from the client and stops when the last byte is sent to the client, i.e., the total time the whole process takes, where the client request reaches a CLB instance, the CLB instance forwards the request to an RS, the RS responds and sends data to the CLB instance, and finally the CLB instance forwards the data to the client.</td><td>double</td></tr>
<tr><td>upstream_response_time</td><td> The time that an entire backend request process takes. The timing begins when a CLB instance connects with an RS and stops when the RS receives the request and responds.<td>double</td></tr>
<tr><td>upstream_connect_time</td><td> The time it takes to establish a TCP connection with an RS. The timing begins when a CLB instance connects with an RS and stops when it sends the HTTP request.</td><td>double</td></tr>
<tr><td>upstream_header_time</td><td> The time it takes to receive an HTTP header from the RS. The timing begins when a CLB instance connects with an RS and stops when the HTTP response header is received from the RS.</td><td>double</td></tr>
<tr><td>tcpinfo_rtt</td><td> TCP connection RTT. </td><td>long</td></tr>
<tr><td>connection</td><td> Connection ID. </td><td>long</td></tr>
<tr><td>connection_requests</td><td> Number of requests on connection. </td><td>long</td></tr>
<tr><td>ssl_handshake_time</td><td> The time that an SSL handshake takes. </td><td>double</td></tr>
<tr><td>ssl_cipher</td><td> SSL cipher suite.</td><td>text</td></tr>
<tr><td>ssl_protocol</td><td> SSL protocol version.</td><td>text</td></tr>
<tr><td>vip_vpcid</td><td>VPC ID of a CLB VIP; the `vip_vpcid` of a public network CLB instance is `-1`.</td><td>long</td></tr>
<tr><td>request</td><td> Request method. Only POST and GET requests are supported.</td><td>text</td></tr>
<tr><td>uri</td><td> Resource Identifier.</td><td>text</td></tr>
<tr><td>server_protocol</td><td>Protocol used for CLB.</td><td>text</td></tr>
</tbody></table>

### Default search log valuable
The following fields can be found in logsets with "CLB" by default:
<table class="table"><thead><tr><th>Index Field</th><th>Description</th></tr>Field Type</th></tr></thead>
<tbody>
<tr><td>time_local</td><td> Access time and time zone, such as "01/Jul/2019:11:11:00 +0800" where "+0800" represents UTC+8, i.e., Beijing time.</td><td>text</td></tr>
<tr><td>protocol_type</td><td> Protocol type (HTTP/HTTPS/SPDY/HTTP2/WS/WSS).</td><td>text</td></tr>
<tr><td>server_addr</td><td>CLB VIP. </td><td>text</td></tr>
<tr><td>server_name</td><td> `server_name` of a rule, i.e., the domain name configured in a CLB listener.</td><td>text</td></tr>
<tr><td>remote_addr</td><td> Client IP.</td><td>text</td>
<tr><td>status</td><td> Status code returned to client. </td><td>long</td></tr>
<tr><td>upstream_addr</td><td> RS address.</td><td>text</td>
<tr><td>upstream_status</td><td> Status code returned by RS to CLB. </td><td>text</td></tr>
<tr><td>request_length</td><td> Number of bytes of request received from client.</td><td>long</td></tr>
<tr><td>bytes_sent</td><td> Number of bytes sent to client.<td>long</td></tr>
<tr><td>http_host</td><td> Request domain name, i.e., the host of the HTTP header.</td><td>text</td></tr>
<tr><td>request_time</td><td> Request processing time. The timing begins when the first byte is received from the client and stops when the last byte is sent to the client, i.e., the total time the whole process takes, where the client request reaches a CLB instance, the CLB instance forwards the request to an RS, the RS responds and sends data to the CLB instance, and finally the CLB instance forwards the data to the client.</td><td>double</td></tr>
<tr><td>upstream_response_time</td><td> The time that an entire backend request process takes. The timing begins when a CLB instance connects with an RS and stops when the RS receives the request and responds.<td>double</td></tr>
</tbody></table>
