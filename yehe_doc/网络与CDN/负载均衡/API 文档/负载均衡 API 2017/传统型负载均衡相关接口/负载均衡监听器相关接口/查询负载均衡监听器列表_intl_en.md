## API Description
This API is used to query the list of listeners by CLB ID, listener protocol or port.

Domain name for API calls: `lb.api.qcloud.com`

## Request Parameters
The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see the [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `DescribeLoadBalancerListeners`.
 
| Parameter | Required | Type | Description |
|-----|----|----|------------|
| loadBalancerId | Yes | String | CLB instance ID, which can be queried via the <a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers</a>API. |
| listenerIds.n | No | String | CLB listener ID. |
| protocol | No | Int | Protocol type of the listener.<br>1: HTTP; 2: TCP; 3: UDP; 4: HTTPS. |
| loadBalancerPort | No | Int | Port of the CLB listener. |
| status | No | Int | Status of the CLB listener. This field will be ignored when `listenerIds.n` is specified.|


## Response Parameters
 
| Parameter | Type | Description |
|------|-----|-------|
| code | Int | Common error code. 0: success; other values: failure. For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/11602" title="Common Error Codes">Common Error Codes</a>. |
| message | String | API-related module error message description. |
| codeDesc | String | Error code. For a successful operation, "Success" is returned. For a failed operation, a message describing the failure is returned. |
| totalCount | Int | Total number of CLB listeners that meet the filter condition. |
| listenerSet | Array | Listener array returned. |

Structure of the `listenerSet` array returned

| Parameter | Type | Description |
|--------|-------|-------|
| listenerId | String | CLB listener ID. |
| unListenerId | String | CLB listener ID. |
| loadBalancerPort | Int | Listening port of the CLB listener. |
| instancePort | Int | Forwarding port of the listener. |
| listenerName | String | Listener name. |
| protocol | Int | Protocol type of the listener.<br>1: HTTP; 2: TCP; 3: UDP; 4: HTTPS. |
| sessionExpire | Int | Session persistence duration. |
| healthSwitch | Int | Whether to enable the health check. 1: enable; 0: disable. |
| timeOut | Int | Response timeout. |
| intervalTime | Int | Interval between health checks. |
| healthNum | Int | Healthy threshold. |
| unhealthNum | Int | Unhealthy threshold. |  
| httpHash | String | Forwarding method of the HTTP or HTTPS listener of a public network classic CLB instance. |
| scheduler | String | Forwarding method of the UDP or TCP listener of a public network classic CLB instance. |
|httpCode | Int | Return code for health check of the HTTP or HTTPS listener of a public network classic CLB instance. For more information about this field, see its explanation in the [CreateLoadBalancerListeners](https://intl.cloud.tencent.com/document/product/214/1255) API. |
| httpCheckPath | String | Health check path of the HTTP or HTTPS listener of a public network classic CLB instance. |
| SSLMode | String | Verification method of the HTTPS listener of a public network classic CLB instance. |
| certId | String | Server certificate ID of the HTTPS listener of a public network classic CLB instance. |
| certCaId | String | Client certificate ID of the HTTPS listener of a public network classic CLB instance. |
| status | Int | Listener status. 0: creating; 1: running. |

## Example
 
Request
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=DescribeLoadBalancerListeners
&<<a href="https://intl.cloud.tencent.com/document/product/213/31574">Common request parameters</a>>
&loadBalancerId=lb-abcdefgh
&listenerIds.0=lbl-6hkiqc6c
&listenerIds.1=lbl-6wv071ba
</pre>

Response
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "listenerSet": [
        {	
			"listenerId": "lbl-6hkiqc6c",
            "loadBalancerPort": 80,
            "instancePort": 80,
            "protocol": 4,
            "status": 1,
            "listenerName": "teaa",
            "unListenerId": "lbl-6hkiqc6c",
            "sessionExpire": 1000,
            "healthSwitch": 1,
            "timeOut": 6,
            "intervalTime": 6,
            "healthNum": 3,
            "unhealthNum": 3,
            "httpCode": 15,
            "httpCheckPath": "/",
            "httpHash": "ip_hash",
            "SSLMode": "mutual",
            "certId": "4b9fc92b",
            "certCaId": "ee4c5590"
        },
        {
			"listenerId": "lbl-6hkiqc6c",
            "loadBalancerPort": 777,
            "instancePort": 798,
            "protocol": 4,
            "status": 1,
            "listenerName": "",
            "unListenerId": "lbl-6wv071ba",
            "sessionExpire": 0,
            "healthSwitch": 1,
            "timeOut": 2,
            "intervalTime": 5,
            "healthNum": 3,
            "unhealthNum": 3,
            "httpCode": 31,
            "httpCheckPath": "/",
            "httpHash": "wrr",
            "SSLMode": "mutual",
            "certId": "e2b6d555",
            "certCaId": "dcda0a22"
        }
    ],
    "totalCount": 2
}

```
