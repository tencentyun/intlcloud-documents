## Overview
API Gateway records the client access logs, which can help you better understand client requests, troubleshoot issues, and analyze user behaviors.
API Gateway provides a basic log dashboard in the console, where you can directly view and search for logs. It also allows you to ship logs to [CLS](https://console.cloud.tencent.com/cls) for multidimensional statistical analysis.

## Directions
### Step 1. Create a logset and log topic[](id:step1)
To configure access logs in CLS, you need to first create a logset and log topic.
You can directly proceed to [step 2](#step2) if you have already created a logset and log topic.
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway) and click **Tool** > **Log delivery** on the left sidebar.
2. On the **Access Logs** page, select a region for the logset, and then click **Create Logset** in the **Logset Information** section.
3. In the pop-up **Create Logset** dialog box, set the retention period and click **Save**.
>?You can only create a single logset named "apigw_logset" in each region.
4. Click **Create Log Topic** in the **Log Topic** section of the **Access Logs** page.
5. In the pop-up window, select a dedicated API Gateway instance to add to the list on the right, and then click **Save**.
>?
>- API Gateway logs are shipped at the instance level. Only dedicated instances can ship logs to CLS, while shared instances can't.
>- In the **Operation** column on the right of the log topic list, you can click **Manage** to edit the added dedicated API Gateway instance.
>- Each API Gateway instance can be added to only one log topic.
>- Multiple log topics can be created in a logset. You can store logs of different dedicated API Gateway instances in different log topics.
6. (Optional) To disable logging, just click **Disable**.

### Step 2. View access logs[](id:step2)
Without any manual configurations, API Gateway has been automatically configured with index search by access log variable. You can directly query access logs through search and analysis.
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway) and click **Tool** > **Log delivery** on the left sidebar.
2. Select a log topic, and click **Search** in the operation column to redirect to the **Search Analysis** page in the [CLS console](https://console.cloud.tencent.com/cls/search).
3. On the **Search Analysis** page, enter the search syntax in the input box, select a time range, and then click **Search Analysis** to search for access logs reported by API Gateway to CLS.
>?See [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/37803) for more information on search syntax.

## Log Format Description
A shipped service log is in the following format:
```LOG
log_format  
'[$app_id][$env_name][$service_id][$http_host][$api_id][$uri][$scheme][rsp_st:$status][ups_st:$upstream_status]'
'[cip:$remote_addr][uip:$upstream_addr][vip:$server_addr][rsp_len:$bytes_sent][req_len:$request_length]' 
'[req_t:$request_time][ups_rsp_t:$upstream_response_time][ups_conn_t:$upstream_connect_time][ups_head_t:$upstream_header_time]'
'[err_msg:$err_msg][tcp_rtt:$tcpinfo_rtt][$pid][$time_local][req_id:$request_id]';
```
The parameters are as detailed below:

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
| ups_st | Backend business server response status code (if the request is passed through to the backend, this variable will not be empty. If the request is blocked in API Gateway, this variable will be displayed as `-`). |
| cip | Client IP. |
| uip |     Backend business service (upstream) IP.
| vip | VIP requested to be accessed. |
| rsp_len | Response length. |
| req_len | Request length. | 
| req_t | Total request response time. |
| ups_rsp_t | Total backend response time (time between connection establishment by API Gateway and backend response receipt). |
| ups_conn_t | Time when the backend business server is successfully connected to. |
| ups_head_t | Time when the backend response header arrives. |
| err_msg | Error message. |
| tcp_rtt | Client TCP connection information. RTT (Round Trip Time) consists of three parts: link propagation delay, end system processing delay, and queuing delay in router cache. |
| pid | Process ID. |
| time_local | Request time. |
| req_id | Request ID. |

## Notes
- API Gateway logs are shipped at the instance level. Only dedicated instances can ship logs to CLS, while shared instances can't.
- Shipping API Gateway access logs to CLS is now free of charge. You only need to pay for the CLS service.
- This feature is only supported in CLS available regions. See [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).
