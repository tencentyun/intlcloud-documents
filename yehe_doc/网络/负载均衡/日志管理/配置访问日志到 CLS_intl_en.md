CLB supports configuring layer-7 (HTTP/HTTPS) access logs that can help you better understand client requests, troubleshoot issues, and analyze user behaviors. Currently, access logs can be stored in CLS, reported at a minute granularity, and searched online by multiple rules.

Access logs of CLB are mainly used to quickly locate and troubleshoot issues. The access logging feature includes log reporting, storage, and search:
- Log reporting provides best-effort service, that is, it prioritizes service forwarding over log reporting.
- Log storage and search provide SLA based on the storage service currently in use.

>
>- Currently, access logs can be stored in CLS only for layer-7 protocols (HTTP/HTTPS) but not layer-4 protocols (TCP/UDP/TCP SSL).
- The access log service for CLB is free of charge, and you only need to pay for CLS usage.
- Currently, access logs can be stored in CLS in Chengdu and Toronto regions through the console or APIs. This feature is in beta test in Guangzhou, Beijing, and Shanghai regions. To try it out, please submit a [ticket](https://console.cloud.tencent.com/workorder/category) for application.
- Currently, [CLS](https://intl.cloud.tencent.com/document/product/614) is in beta test. To try it out, please submit a ticket for application.

## Enabling Access Logging
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2. Click the ID of the CLB instance to be configured to enter the "Basic Information" page.
3. In the "Log Access" module, edit "Cloud Log Service".
![](https://main.qcloudimg.com/raw/163c20ca7cb4326005c9ecf9fb43a39f.png)
4. In the pop-up box, enable access logging and select the destination logset and log topic for access log storage. If you haven't created a logset or log topic yet, please [create relevant resources](https://console.cloud.tencent.com/cls/logset) and then select them as the storage location.
![](https://main.qcloudimg.com/raw/33ccb8c1bcf3b200716a4a2f1751f0c1.png)
5. Click **Submit** and access logs will be collected into the corresponding topic.
6. Then, click the logset or log topic to redirect to the log search page in CLS.
7. (Optional) If you want to disable access logging, you can edit "Cloud Log Service" again to disable it and submit in the pop-up window.

## Searching for Access Logs
### Step 1. Configure log topic indexes
>The log topics must be configured with indexes; otherwise, no logs can be searched for.

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Logset** to enter the "Logset Management" page.
3. Click a logset ID to enter the logset details page.
4. On the logset details page, click a log topic ID to enter the log topic details page.
![](https://main.qcloudimg.com/raw/2ac7b3725bf4a598a4f9668ed3c80c1c.png)
5. On the log topic details page, select the **Index Configuration** tab. You can select some variables from the log variables and configure the index fields as needed. For more information on how to configure, please see [Enabling Index](https://intl.cloud.tencent.com/document/product/614/16981).
![](https://main.qcloudimg.com/raw/aff66a76b27f5ec0366028e1e9a6ed08.png)
6. The result of index configuration is as shown below:
![](https://main.qcloudimg.com/raw/a5c1dfd312827c8fd3945cb0945616fb.png)

### Step 2. Search for access logs
1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Log Search** to enter the "Search Analysis" page.
3. On the "Search Analysis" page, select a logset, log topic, and time range, and click **Search Analysis** to search for the access logs reported by CLB to CLS. For more information on the search syntax, please see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439).
![](https://main.qcloudimg.com/raw/57f74355eb469e59fca7efbe1994d9d0.png)

## Log Variable Description
<table class="table"><thead><tr><th>Variable</th><th>Description</th></tr></thead>
<tbody><tr><td>stgw_request_id</td><td>Request ID. </td></tr>
<tr><td>time_local</td><td>Access time and time zone, such as `01/Jul/2019:11:11:00 +0800` where `+0800` represents UTC+8, i.e., Beijing time. </td></tr>
<tr><td>protocol_type</td><td>Protocol type (HTTP/HTTPS/SPDY/HTTP2/WS/WSS).</td></tr>
<tr><td>server_addr</td><td>Destination IP of request.</td></tr>
<tr><td>server_port</td><td>Destination port of request.</td></tr>
<tr><td>server_name</td><td>Rule's `server_name`, i.e., server name.</td></tr>
<tr><td>remote_addr</td><td>Client IP.</td></tr>
<tr><td>remote_port</td><td>Client port.</td></tr>
<tr><td>status</td><td>Status code returned to client.</td></tr>
<tr><td>upstream_addr</td><td>RS address.</td></tr>
<tr><td>upstream_status</td><td>Status code returned by RS to CLB.</td></tr>
<tr><td>proxy_host</td><td>Stream ID.</td></tr>
<tr><td>request</td><td>Request line.</td></tr>
<tr><td>request_length</td><td>Number of bytes of request received from client.</td></tr>
<tr><td>bytes_sent</td><td>Number of bytes sent to client.</td></tr>
<tr><td>http_host</td><td>Request domain name.</td></tr>
<tr><td>http_user_agent</td><td>`user_agent` field of the HTTP header.</td></tr>
<tr><td>http_referer</td><td>HTTP request source.</td></tr>
<tr><td>request_time</td><td>Request processing time. The timing begins when the first byte is received from the client and stops when the last byte is sent to the client, i.e., the total time the whole process takes, where the client request reaches a CLB instance, the CLB instance forwards the request to an RS, the RS responds and sends data to the CLB instance, and finally the CLB instance forwards the data to the client.</td></tr>
<tr><td>upstream_response_time</td><td>The time that an entire backend request process takes. The timing begins when a CLB instance connects with an RS and stops when the RS receives the request and responds.</td></tr>
<tr><td>upstream_connect_time</td><td>The time it takes to establish a TCP connection with an RS. The timing begins when a CLB instance connects with an RS and stops when it sends the HTTP request.</td></tr>
<tr><td>upstream_header_time</td><td>The time it takes to receive an HTTP header from the RS. The timing begins when a CLB instance connects with an RS and stops when the HTTP response header is received from the RS.</td></tr>
<tr><td>tcpinfo_rtt</td><td>TCP connection RTT.</td></tr>
<tr><td>connection</td><td>Connection ID.</td></tr>
<tr><td>connection_requests</td><td>Number of requests on connection.</td></tr>
<tr><td>ssl_handshake_time</td><td>The time that an SSL handshake takes.</td></tr>
<tr><td>ssl_cipher</td><td>SSL cipher suite.</td></tr>
<tr><td>ssl_protocol</td><td>SSL protocol version.</td></tr>
<tr><td>vip_vpcid</td><td>VPC ID of CLB instance VIP.</td></tr></tbody></table>
