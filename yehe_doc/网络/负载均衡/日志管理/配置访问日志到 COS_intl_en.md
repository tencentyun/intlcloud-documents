>!The feature of storing access logs in COS will stop accepting new enablement requests after 00:00:00, May 15, 2020 (00:00:00, April 26, 2020 for the Guangzhou region) and will be officially disused after 00:00:00, June 30, 2020. Please use the upgraded feature of [storing access logs in CLS](https://intl.cloud.tencent.com/document/product/214/35063).

CLB supports configuring layer-7 (HTTP/HTTPS) access logs that can help you better understand client requests, troubleshoot issues, and analyze access data. Currently, access logs can be stored in COS for download and analysis, and supported regions include Guangzhou, Shanghai, Beijing, Hong Kong (China), Shanghai Finance, and Shanghai Finance.

Access logs of CLB are mainly used to quickly locate and troubleshoot issues. The access logging feature includes log reporting, storage, and search:
- Log reporting provides best-effort service, that is, it prioritizes service forwarding over log reporting.
- Log storage and search provide SLA based on the storage service currently in use.

>?
>- Currently, log aggregation granularity is 1 hour, and log data transfer may have a delay.
>- Currently, CLB supports storing and downloading access logs of public network layer-7 (HTTP/HTTPS) CLB instances but not layer-4 (TCP/UDP) or private network layer-7 CLB instances.
>- The log service for CLB is free of charge. A free COS storage capacity of 50 GB is provided for individual users as specified in [Free Tier](https://intl.cloud.tencent.com/document/product/436/6240). If you have a high number of logs, please clean them up in a timely manner.
>- In the regions that support storing access logs in COS, if the access logging feature is not enabled, Tencent Cloud will retain the logs for three days by default; otherwise, the retention period will be subject to the COS configuration. Access log cannot be configured in other regions.


## Enabling Access Log Storage in COS
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2. On the "CLB Instance" list page, click the ID of the CLB instance to be configured to enter the "Basic Information" page.
3. In the "Access Log" module, edit "Store Logs in COS".
4. Enable access logging in the pop-up window and select a destination COS bucket. If you have not created any COS bucket yet, you can [create a bucket](https://console.cloud.tencent.com/cos4/bucket) and select it for log storage.
![](https://main.qcloudimg.com/raw/1eb954e4a6d33090fc5901a87b930f6a.png)
5. Click **Submit** and a folder named `lb-id` will be automatically created in the bucket for request logs.
6. Then, click the bucket address to enter the log download page.

## Disabling Access Log Storage in COS
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2. On the "CLB Instance" list page, click the ID of the CLB instance to be configured to enter the "Basic Information" page.
3. In the "Access Log" module, edit "Store Logs in COS".
4. In the pop-up box, disable access log and click **Submit**.
 The configuration result is as follows. Log storage in COS cannot be enabled again after it is disabled. 

## Log Format and Variable Description
### Log format
```
[$stgw_request_id] [$time_local] [$protocol_type] [$server_addr:$server_port] [$server_name] [$remote_addr:$remote_port] [$status]  [$upstream_status] [$proxy_host] [$request] [$request_length] [$bytes_sent] [$http_host] [$http_user_agent] [$http_referer]
[$request_time] [$upstream_response_time] [$upstream_connect_time] [$upstream_header_time] [$tcpinfo_rtt] [$connection] [$connection_requests] [$ssl_handshake_time] [$ssl_cipher] [$ssl_protocol] [$ssl_session_reused]
```

### Log variable description

| Variable | Description |
| :-------- | :------ |
|stgw_request_id  |	Request ID. |
| time_local	|  Access time and time zone, such as "01/Jul/2019:11:11:00 +0800" where "+0800" represents UTC+8, i.e., Beijing time. |
| protocol_type | Protocol type (HTTP/HTTPS/SPDY/HTTP2/WS/WSS). |
| server_addr:server_port  | Destination IP and port of request. |
| server_name | Rule's `server_name`, i.e., server name. |
| remote_addr:remote_port	| Client IP and port. |
| status | Status code returned by CLB to client. |
| upstream_status | Status code returned by RS to CLB instance. |
| proxy_host | Stream ID. |
| request | Request line. |
| request_length | Number of bytes of request received from client. |
|bytes_sent | 	Number of bytes sent to client. |
|http_host	 | Request domain name. |
|http_user_agent | 	`user_agent` field of the HTTP header. |
|http_referer	 | HTTP request source. |
| request_time | Request processing time. The timing begins when the first byte is received from the client and stops when the last byte is sent to the client, i.e., the total time the whole process takes, where the client request reaches a CLB instance, the CLB instance forwards the request to an RS, the RS responds and sends data to the CLB instance, and finally the CLB instance forwards the data to the client. |
| upstream_response_time | The time that an entire backend request process takes. The timing begins when a CLB instance connects with an RS and stops when the RS receives the request and responds. |
| upstream_connect_time 	| The time it takes to establish a TCP connection with an RS. The timing begins when a CLB instance connects with an RS and stops when it sends the HTTP request. |
| upstream_header_time	| The time it takes to receive an HTTP header from the RS. The timing begins when a CLB instance connects with an RS and stops when the HTTP response header is received from the RS. |
| tcpinfo_rtt | TCP connection RTT. |
| connection | Connection ID. |
| connection_requests | Number of connection requests. |
| ssl_handshake_time 	| The time that an SSL handshake takes. |
| ssl_cipher | SSL cipher suite. |
| ssl_protocol	| SSL protocol version. |
| ssl_session_reused | SSL SESSION reuse. |	 

