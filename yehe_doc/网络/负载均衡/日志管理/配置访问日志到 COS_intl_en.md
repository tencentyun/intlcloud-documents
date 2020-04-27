CLB supports configuring layer-7 (HTTP/HTTPS) access logs that can help you better understand client requests, troubleshoot issues, and analyze user behaviors. Currently, access logs can be stored in COS for download and analysis, and supported regions include Guangzhou, Shanghai, Beijing, and Hong Kong (China).

Access logs of CLB are mainly used to quickly locate and troubleshoot issues. The access logging feature includes log reporting, storage, and search:
- Log reporting provides best-effort service, that is, it prioritizes service forwarding over log reporting.
- Log storage and search provide SLA based on the storage service currently in use.

>
- Currently, log aggregation granularity is 1 hour, and log data transfer may have a delay.
- Currently, CLB supports storing and downloading access logs of public network layer-7 (HTTP/HTTPS) CLB instances but not layer-4 (TCP/UDP) or private network layer-7 CLB instances.
- The log service for CLB is free of charge. A free COS storage capacity of 50 GB is provided for individual users as specified in [Free Tier](https://intl.cloud.tencent.com/document/product/436/6240). If you have a high number of logs, please clean them up in a timely manner.
- In the regions that support storing access logs in COS, if the access logging feature is not enabled, Tencent Cloud will retain the logs for three days by default; otherwise, the retention period will be subject to the COS configuration. Access log cannot be configured in other regions.


## Enabling Access Logging
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2. Click the ID of the CLB instance to be configured to enter the "Basic Information" page.
3. In the "Log Access" module, edit "Store Logs in COS".
![](https://main.qcloudimg.com/raw/1b1dccd0d7a2232b49fc058442daef27.png)
4. In the pop-up box, enable access logging and select the destination COS bucket for storage. If you haven't created a bucket yet, please [create a bucket](https://console.cloud.tencent.com/cos4/bucket) and then select the new bucket.
![](https://main.qcloudimg.com/raw/1eb954e4a6d33090fc5901a87b930f6a.png)
5. Click **Submit** and a folder named `lb-id` will be automatically created in the bucket for request logs.
6. Then, click the bucket address to redirect to the log download page.
7. (Optional) If you want to disable access logging, you can edit "Store Logs in COS" again to disable it and submit in the pop-up window.

## Log Format and Variable Description
### Log format
```
[$stgw_request_id] [$time_local] [$protocol_type] [$server_addr:$server_port] [$server_name] [$remote_addr:$remote_port] [$status]  [$upstream_status] [$proxy_host] [$request] [$request_length] [$bytes_sent] [$http_host] [$http_user_agent] [$http_referer]
[$request_time] [$upstream_response_time] [$upstream_connect_time] [$upstream_header_time] [$tcpinfo_rtt] [$connection] [$connection_requests] [$ssl_handshake_time] [$ssl_cipher] [$ssl_protocol] [$ssl_session_reused]
```

### Log variable description

| Variable | Description |
| :-------- | :------ |
| time_local	| Access time and time zone, such as `01/Jul/2019:11:11:00 +0800` where `+0800` represents UTC+8, i.e., Beijing time. |
| protocol_type | Protocol type (HTTP/HTTPS/SPDY/HTTP2/WS/WSS). |
| server_addr:server_port | Destination IP and port of request. |
| server_name | Rule's `server_name`, i.e., server name. |
| remote_addr:remote_port	| Client IP and port. |
| status | Status code returned by CLB to client. |
| upstream_status | Status code returned by RS to CLB. |
| proxy_host | Stream ID. |
| request | Request line. |
| request_length | Number of bytes of request received from client. |
| bytes_sent | Number of bytes sent to client. |
| http_host	 | Request domain name. |
| http_user_agent | `user_agent` field of the HTTP header. |
| http_referer	 | HTTP request source. |
| request_time | Request processing time. The timing begins when the first byte is received from the client and stops when the last byte is sent to the client, i.e., the total time the whole process takes, where the client request reaches a CLB instance, the CLB instance forwards the request to an RS, the RS responds and sends data to the CLB instance, and finally the CLB instance forwards the data to the client. |
| upstream_response_time | The time that an entire backend request process takes. The timing begins when a CLB instance connects with an RS and stops when the RS receives the request and responds. |
| upstream_connect_time | The time it takes to establish a TCP connection with an RS. The timing begins when a CLB instance connects with an RS and stops when it sends the HTTP request. |
| upstream_header_time| The time it takes to receive an HTTP header from the RS. The timing begins when a CLB instance connects with an RS and stops when the HTTP response header is received from the RS. |
| tcpinfo_rtt | TCP connection RTT. |
| connection | Connection ID. |
| connection_requests | Number of requests on connection. |
| ssl_handshake_time	| The time that an SSL handshake takes. |
| ssl_cipher | SSL cipher suite. |
| ssl_protocol	| SSL protocol version. |
| ssl_session_reused | SSL session reuse. |	 
