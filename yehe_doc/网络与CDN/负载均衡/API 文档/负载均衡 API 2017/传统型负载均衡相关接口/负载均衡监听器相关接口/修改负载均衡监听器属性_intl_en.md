## API Description
 This API is used to modify the attributes of CLB listeners.
 
Domain name for API calls: `lb.api.qcloud.com`


## Request Parameters

The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `ModifyLoadBalancerListener`.
 
| Parameter | Required | Type | Description |
|-----|------|--------|-----------|
| loadBalancerId | Yes | String | CLB instance ID, which can be queried via the <a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers</a> API. |
| loadBalancerId | Yes | String | CLB listener ID, which can be queried via the <a href="https://intl.cloud.tencent.com/document/product/214/1260" title=" DescribeLoadBalancerListeners"> DescribeLoadBalancerListeners</a> API. |
| listenerName | No | String | Listener name. |
| sessionExpire | No | Int | Session persistence duration. 0: disable. Value range: 30-3600. |
| healthSwitch | No | Int | Whether to enable health check.1: enable; 0: disable. |
| timeOut | No | Int | Response timeout. Value range: 2-60 seconds;<br>This parameter cannot be specified for public network CLB listener with HTTP or HTTPS protocol. |
| intervalTime | No | Int | Interval between health checks. Value range: 5-300 seconds. Default value: 5. |
| healthNum | No | Int | Healthy threshold. Value range: 2-10. |
| unhealthNum | No | Int | Unhealthy threshold. Value range: 2-10. |
| scheduler | No | String | Forwarding method of the CLB listener. This field cannot be passed in together with `httpHash`. Only public network CLB listeners with TCP or UDP protocol support this field. Valid values: wrr (weighted round robin), least_conn (least connection). |
| httpHash | No | String | Forwarding method of the CLB listener. Only public network CLB listener with HTTP or HTTPS protocol support this field. Valid values: wrr (weighted round robin), ip_hash (forwarding the hash of the source IP to the real server), least_conn (least connection).<br>Default value: wrr. |
| httpCode | No | Int | Return code for the health check of HTTP or HTTPS CLB listeners. Valid range: 1-31. Default value: 31.<br>1 represents a return code of 1xx (healthy). 2 represents a return code of 2xx (healthy). 4 represents a return code of 3xx (healthy). 8 represents a return code of 4xx (healthy). 16 represents a return code of 5xx (healthy). If there are multiple codes that can show the healthy status, enter the accumulated value corresponding to such codes. |
| httpCheckPath | No | String | Health check path for the public network CLB listener with HTTP or HTTPS protocol. Default is /. It must start with /. |
| SSLMode | No | String | Verification mode of the public network CLB listener with HTTPS protocol. unidirectional: unidirectional verification; mutual: mutual verification. |
| certId | No | String | New server certificate ID of the public network CLB listener with HTTPS protocol. |
| certCaId | No | String | New client certificate ID of the public network CLB listener with HTTPS protocol. |
| certCaContent | No | String | New client certificate content of the public network CLB listener with HTTPS protocol. |
| certCaName | No | String | New client certificate name of the public network CLB listener with HTTPS protocol. |
| certContent | No | String | New server certificate content of the public network CLB listener with HTTPS protocol. |
| certKey | No | String | New server certificate key of the public network CLB listener with HTTPS protocol. |
| certName | No | String | New server certificate name of the public network CLB listener with HTTPS protocol. |


## Response Parameters
 
 
| Parameter | Type | Description |
|-------|---|---------------|
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/214/11602). |
| message | String | API-related module error message description. |
| codeDesc | String | Error code. For a successful operation, "Success" is returned. For a failed operation, a message describing the failure is returned. |
| requestId | Int | Request task ID. You can use this field to query the operation status via the [DescribeLoadBalancersTaskResult](https://intl.cloud.tencent.com/document/api/214/4007) API. |

## Example
 
Request
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=ModifyLoadBalancerListener
&<<a href="https://intl.cloud.tencent.com/document/product/213/31574">Common request parameters</a>>
loadBalancerId=lb-ltkip4do
&listenerId=lbl-6hkiqc6c
&SSLMode=unidirectional
</pre>
Response
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "requestId": 18642
}

```
 
