## 接口描述
DescribeLoadBalancerLog 接口用来查询 COS 中的负载均衡七层日志，适用于配置了 HTTP 与 HTTPS 协议监听器且开启了 COS 日志的公网负载均衡。

接口访问域名：`lb.api.qcloud.com`

接口说明：该接口只能查询 COS 日志，不支持查询 CLS 日志。如需查询 CLS 日志请参见 [搜索日志](https://intl.cloud.tencent.com/document/product/614/16875) ，该接口可以查询三天之内的负载均衡的转发日志，包括转发给后端 RS 的日志，以及由于后端 RS 异常，直接从负载均衡返回的日志，请求的时间间隔不超过一天。 

## 请求参数

 以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/214/11594) 页面。其中，此接口的 Action 字段为 DescribeLoadBalancerLog。
 
|参数名称|必选|类型|描述|
|-|-|-|-|
|loadBalancerId|是|String|负载均衡实例 ID，可通过 <a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers</a> 接口查询。|
|order|否|String|日志的按照时间戳的顺序，可选值 desc，asc，默认值 desc。|
|startTime|否|Int|查询日志的开始时间，Unix 时间戳（精度是秒）。默认为 endTime 的前5分钟。|
|endTime|否|Int|查询日志的截止时间，Unix 时间戳（精度是秒）。默认为当前时间戳。|
|offset|否|Int|日志的偏移量，取值范围 [0，10000]。|
|limit|否|Int|日志的条数，取值范围 [0，500]。|
|filter|否|Array|日志的过滤条件，key，value 的方式，**具体字段请参见下文 filter 数组 key 的可选值**。|


filter 数组 key 的可选值：

|参数名称|必选|类型|描述|
|-|-|-|-|
|status|否|Int|返回给客户端的状态码是 value 的日志。|
|status_not|否|Int|返回给客户端的状态码不是 value 的日志。|
|server_name|否|String|请求匹配的 host 是 value 的日志。|
|server_name_not|否|String|请求匹配的 host 不是 value 的日志。|
|http_host|否|String|请求的 host 是 value 的日志。|
|http_host_not|否|String|请求的 host 不是 value 的日志。|
|remote_addr|否|String|请求的客户端 IP 是 value 的日志。|
|remote_addr_not|否|String|请求的客户端 IP 不是 value 的日志。|
|request_time_less_than|否|String|请求处理的时间小于 value 值的日志，与 request_time_greater_than 同时传入有效。|
|request_time_greater_than|否|String|请求处理的时间大于 value 值的日志，request_time_less_than 同时传入有效。|




## 返回参数
 
 
|参数名称|类型|描述|
|-------|---|---------------|
|code|Int|公共错误码，0表示成功，其他值表示失败。详情请参见错误码页面的 [公共错误码](https://intl.cloud.tencent.com/document/product/214/11602)。|
|message|String|模块错误信息描述，与接口相关。|
|codeDesc|String|英文错误码，成功返回 Success，失败有相应的英文说明。|
|logInfo|Json|返回日志的信息。|

logInfo 的格式：

|参数名称|类型|描述|
|-|-|-|
|logList|Array|日志的数组。|
|total|Int|日志的总条数。|

logList 数据格式：

|序号|参数名称|类型|描述|
|-|-------|---|---------------|
| 1 | server_name |String| 规则的 server_name。 |
| 2 | request | String| 请求行。 |
| 3  | remote_addr | String| 客户端 IP。 |
| 4  | upstream_addr | String| 后端的 RS 信息。 |
| 5  | upstream_header_time | String| 从 RS 接收完 HTTP 头部所花费时间。 |
| 6  | connection_requests | Int| 连接上的请求个数。 |
| 7  | ssl_handshake_time|String|ssl 握手所花费时间。 |
| 8  | ssl_cipher| String|加密套件。|
| 9  | ssl_protocol	|String| ssl 协议版本。 |
| 10 | ssl_session_reused |String| ssl session 复用。|	
| 11|time_local|String|请求访问时间。|
| 12 |http_host|String|请求域名。|
| 13 |server_addr|String|请求的目的 IP。|
| 14 |bytes_sent|Int|发送客户端的字节数。|
| 15 |upstream_status|String|后端 RS 的状态。|
| 16 |protocol_type|String|协议类型（http/https/spdy/http2/ws/wss）。|
| 17 |request_time|Int| 请求处理时间。|
| 18 |upstream_connect_time|Int| 和 RS 建立 TCP 连接所花费时间，单位：秒。|
| 19 |request_length|Int| 从客户端收到的请求字节数。|
| 20 |tcpinfo_rtt|Int| TCP 连接的 rtt：微秒。|
| 21 |upstream_response_time|Int| 从 RS 接收应答所花费时间，单位：秒。|
|22|status|String| 请求返回的状态码，当后端没有机器时，该状态码为200。|
|23|http_user_agent|String|user_agent。 |



## 示例
 
请求
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=DescribeLoadBalancerLog
&<<a href="https://intl.cloud.tencent.com/document/api/213/6976">公共请求参数</a>>
&loadBalancerId=lb-7wdcqme9
&filter.0.key=status
&filter.0.value=200
&filter.1.key=server_name
&filter.1.value=www.qq.com
</pre>
返回
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
 
