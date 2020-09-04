## Overview
This document describes how to export service logs through the API Gateway console for data analysis and problem location.

## Directions
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index) and click **Service** in the left sidebar to access the service list page.
2. On the service list page, click a service name to access the service details page.
3. Click the **Service Log** tab.
4. Click the **Export** icon in the red box as shown in the following figure to export service logs.
![](https://main.qcloudimg.com/raw/792c521810aa4619707c44b30e4e351e.png)

>? 
>- The time range of the logs to be exported is consistent with the time range of the queried logs. You can modify the time range of the logs to be exported by modifying the time range of the queried logs.
>- The exported log file is a CSV file. The file name is in the following format: Service Log-service ID (start time - end time).


## Log Format
The format of exported service logs is as follows:
```
log_format  
'[$app_id][$env_name][$service_id][$http_host][$api_id][$uri][$scheme][rsp_st:$status][ups_st:$upstream_status]'
'[cip:$remote_addr][uip:$upstream_addr][vip:$server_addr][rsp_len:$bytes_sent][req_len:$request_length]' 
'[req_t:$request_time][ups_rsp_t:$upstream_response_time][ups_conn_t:$upstream_connect_time][ups_head_t:$upstream_header_time]'
'[err_msg:$err_msg][tcp_rtt:$tcpinfo_rtt][$pid][$time_local][req_id:$request_id]';
```
The following table describes the parameters.

| Parameter | Description |
|---------|---------|
| app_id | User ID. | 
| env_name | Environment name. |
| service_id | Service ID. |
| http_host | Domain name. |
| api_id | API ID. |
| uri | Request path. |
| scheme | HTTP/HTTPS protocol. |
| rsp_st | Request response status code. |
| ups_st | Backend business server's response status code (if the request is passed through to the backend, this variable will not be empty. If the request is blocked by the API Gateway, this variable will be displayed as `-`). |
| cip | Client IP. |
| uip | Backend business service (upstream) IP. |
| vip | VIP requested to be accessed. |
| rsp_len | Response length. |
| req_len | Request length. | 
| req_t | Total request and response time. |
| ups_rsp_t | Total backend response time (time between the connection establishment by the API Gateway and the backend response receipt). |
| ups_conn_t | Time when the backend business server is successfully connected to. |
| ups_head_t | Time when the backend response header arrives. |
| err_msg | Error message. |
| tcp_rtt | Client TCP connection information. Round Trip Time (RTT) consists of 3 parts: link propagation delay, end system processing delay, and queuing delay in the router cache. |
| pid | Process ID. |
| time_local | Time when the request is initiated. |
| req_id | Request ID. |
