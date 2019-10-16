CLB supports storage of request logs. You can store such logs to COS and download them for analytics. Currently, the layer-7 (HTTP/HTTPS) logging feature is available in Guangzhou, Shanghai, Beijing, Hong Kong (China), Shanghai Finance, and Beijing Finance regions. CLB does not support layer-4 (TCP/UDP) log storage or download.

## Activating Logging
1. On the **CLB instance details** page, activate the log access feature.
![](https://main.qcloudimg.com/raw/bac871f6bb89869bea69d8f71c2879fc.png)
2. Select the corresponding bucket in the COS, under which to automatically create a folder named `lb-id` for the request logs. Then, click the bucket address to redirect to the log download page.
![](https://main.qcloudimg.com/raw/e006dc215ffc6f54d226b3835f53019c.png)
> If you haven't created a COS bucket, see [Creating a Bucket](https://console.cloud.tencent.com/cos4/bucket) and select the corresponding storage location.

## Restrictions and Billing
- The current log convergence granularity is 1 hour.
- CLB currently supports storage and download of layer-7 (HTTP/HTTPS) logs but not layer-4 (TCP/UDP) logs.
- Log data transmission may have a delay.
- Logging is currently free of charge. A free storage capacity of 50 GB is provided for individual users as specified in [Free Quotas](http://intl.cloud.tencent.com/document/product/436/6240). If you have massive amounts of logs, please clean them up in a timely manner.
- If the log access feature is not activated, Tencent Cloud will keep the logs for three days by default; otherwise, the storage period will be subject to the COS configuration.

## Log Format and Variable Descriptions
### Log Format
```
[$stgw_request_id] [$time_local] [$protocol_type] [$server_addr:$server_port] [$server_name] [$remote_addr:$remote_port] [$status]  [$upstream_status] [$proxy_host] [$request] [$request_length] [$bytes_sent] [$http_host] [$http_user_agent] [$http_referer]
[$request_time] [$upstream_response_time] [$upstream_connect_time] [$upstream_header_time] [$tcpinfo_rtt] [$connection] [$connection_requests] [$ssl_handshake_time] [$ssl_cipher] [$ssl_protocol] [$ssl_session_reused]
```

## Log Variable Descriptions

| Number | Variable Name | Description |
| :-------- | :-------- | :------ |
| 1 | time_local	| Access time and time zone, such as "01/Jul/2019:11:11:00 +0800" where "+0800" represents UTC+8, i.e., Beijing time. |
| 2 | protocol_type | Protocol type (HTTP/HTTPS/SPDY/HTTP2/WS/WSS) |
| 3 | server_addr:server_port | Destination IP and port of a request. |
| 4 | server_name | Rule's `server_name`, i.e., server name. |
| 5 | remote_addr:remote_port 	| Client ip:port. |
| 6 | status | Status code returned by CLB to the client. |
| 7 | upstream_status | Status code returned by RS to CLB. |
| 8 | proxy_host | Upstream ID. |
| 9 | request | Request line. |
| 10 | request_length | Number of bytes of the request received by the client. |
| 11 |bytes_sent | 	Number of bytes of the request sent to the client. |
| 12 |http_host	 | Request domain name. |
| 13 |http_user_agent |	user_agent. |
| 14 |http_referer	 | HTTP request source. |
| 15 | request_time| Request processing time (from the first byte received by the client until the last byte sent to it, i.e., the total time it takes for the client request to reach CLB, for CLB to forward the request to RS, for RS response data to arrive at CLB, and for CLB to forward the data to the client). |
| 16 | upstream_response_time | Time that an entire backend request takes (from when CONNECT RS starts until RS receives the response). |
| 17 | upstream_connect_time| Time it takes to establish a TCP connection to RS (from when CONNECT RS starts until CLB starts sending HTTP requests to RS) |
| 18 | upstream_header_time	| Times it takes for RS to receive an HTTP header (from when CONNECT RS starts until RS receives the HTTP response header). |
| 19 | tcpinfo_rtt | TCP connection RTT. |
| 20 | connection | Connection ID. |
| 21 | connection_requests | Number of connection requests. |
| 22 | ssl_handshake_time	| Time that an SSL handshake takes. |
| 23 | ssl_cipher | Encryption suite. |
| 24 | ssl_protocol	| SSL protocol version. |
| 25 | ssl_session_reused |SSL SESSION reuse. |	 
