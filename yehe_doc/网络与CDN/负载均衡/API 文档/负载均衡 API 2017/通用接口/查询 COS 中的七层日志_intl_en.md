## API Description
This API is used to query the CLB layer-7 log in COS. It is applicable to public network CLB instances with HTTP or HTTPS listener configured and COS log enabled.

Domain name for API calls: `lb.api.qcloud.com`

Note that this API only supports querying COS log, but not CLS log. To query the CLS log, call the [Searching for Log](https://intl.cloud.tencent.com/document/product/614/16875) API, which can be used to query the forwarding logs of a CLB instance over the last three days, including logs forwarded to the RS and those directly returned from the CLB due to RS exception. Interval between requests shall be within one day. 

## Request Parameters

 The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see the [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `DescribeLoadBalancerLog`.

| Parameter | Required | Type | Description |
|-|-|-|-|
|loadBalancerId | Yes | String | CLB instance ID, which can be queried via the <a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers</a> API. |
| order | No | String | Log sequence by timestamp. Valid values: desc and asc. Default value: desc.|
|startTime | No | Int | Time when you start querying logs using Unix timestamp (accurate to seconds). The default is 5 minutes earlier than `endTime`. |
|endTime | No | Int | Time when you finish querying logs using Unix timestamp (accurate to seconds). The default is the current timestamp. |
| offset | No | Int | Log offset. Value range: [0,10000].|
| limit | No | Int | Number of logs. Value range: [0,500].|
|filter | No | Array | Filter condition of logs in key-value pairs. **See the valid values for the key of `filter` array below for supported fields.**|


Valid values for the key of `filter` array:

| Key | Required | Type | Description |
|-|-|-|-|
| status | No | Int | Logs with the status code matching `value` are returned to the client. |
| status_not | No | Int | Logs except those with the status code matching `value` are returned to the client. |
| server_name | No | String | Logs with the domain name in the CLB rules matching `value` are returned. |
| server_name_not | No | String | Logs except those with the domain name in the CLB rules matching `value` are returned. |
| http_host | No | String | Logs with the domain name of http request matching `value` are returned. |
| http_host | No | String | Logs except those with the domain name of http request matching `value` are returned. |
| remote_addr | No | String | Logs with the request client IP matching `value` are returned. |
| remote_addr_not | No | String | Logs except those with the request client IP matching `value` are returned. |
| request_time_less_than | No | String | Logs with the request processing time less than `value` are returned. This parameter must be passed in along with `request_time_greater_than`. |
| request_time_greater_than | No | String | Logs with the request processing time greater than `value` are returned. This parameter must be passed in along with `request_time_less_than`. |




## Response Parameters


| Parameter | Type | Description |
|-------|---|---------------|
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/214/11602). |
| message | String | API-related module error message description. |
| codeDesc | String | Error code. For a successful operation, "Success" is returned. For a failed operation, a message describing the failure is returned. |
| logInfo | Json | Information of the log returned. |

`logInfo` format:

| Parameter | Type | Description |
|-|-|-|
| logList | Array | Log array. |
| total | Int | Total number of logs. |

`logList` data format:

| No. | Parameter | Type | Description |
|-|-------|---|---------------|
| 1 | server_name | String | Domain name configured in the CLB layer-7 rules. |
| 2 | request | String | Request line. |
| 3 | remote_addr | String | Client IP. |
| 4 | upstream_addr | String | RS information. |
| 5 | upstream_header_time | String | The time it takes to receive an HTTP header from the RS. |
| 6 | connection_requests | Int | Number of connection requests. |
| 7 | ssl_handshake_time | String | The time that an SSL handshake takes. |
| 8 | ssl_cipher | String | SSL cipher suite. |
| 9 | ssl_protocol | String | SSL protocol version. |
| 10 | ssl_session_reused | String | SSL session reuse. |
| 11 | time_local | String | Request access time. |
| 12 | http_host | String | Request domain name. |
| 13 | server_addr | String | Request destination IP. |
| 14 | bytes_sent | Int | Number of bytes sent to the client. |
| 15 | upstream_status | String | RS status. |
| 16 | protocol_type | String | Protocol type (http/https/spdy/http2/ws/wss). |
| 17 | request_time | Int | Request processing time. |
| 18 | upstream_connect_time | Int | The time it takes to establish a TCP connection with an RS, in seconds. |
| 19 | request_length | Int | Number of bytes of the request received from the client. |
| 20 | tcpinfo_rtt | Int | TCP connection RTT, in milliseconds. |
| 21 | upstream_response_time | Int | The time it takes to receive a response from an RS, in seconds. |
| 22 | status | String | Status code returned by the request. Status code “200” will be returned if no RS exists. |
| 23 | http_user_agent | String | The user_agent used in the HTTP request header. |



## Example

Request
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=DescribeLoadBalancerLog
&<<a href="https://intl.cloud.tencent.com/document/product/213/31574">Common request parameters</a>>
&loadBalancerId=lb-7wdcqme9
&filter.0.key=status
&filter.0.value=200
&filter.1.key=server_name
&filter.1.value=www.qq.com
</pre>
Response
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "logInfo": {
        "logList": [
            {
                "server_name": "www.qq.com",
                "request": "GET / HTTP/1.1",
                "remote_addr": "119.28.138.187",
                "upstream_addr": "-",
                "upstream_header_time": "-",
                "connection_requests": 1,
                "ssl_cipher": "-",
                "remote_port": "40554",
                "time_local": "02/Nov/2017:12:03:13 +0800",
                "http_host": "115.159.132.241",
                "server_addr": "115.159.132.241",
                "bytes_sent": 239,
                "upstream_status": "-",
                "protocol_type": "http",
                "ssl_handshake_time": "-",
                "request_time": 0,
                "upstream_connect_time": "-",
                "request_length": 79,
                "ssl_session_reused": "-",
                "tcpinfo_rtt": 38000,
                "upstream_response_time": "-",
                "ssl_protocol": "-",
                "status": "200"
            }
        ],
        "total": 3918
    }
}

```

