## 1. API Description
 This API is used to get the list of listeners by CLB instance IDs, listener protocol, or port. If no filter is specified, the default number (20) of listeners for the instance will be returned.

Domain name for API access: lb.api.qcloud.com

## 2. Request Parameters
   The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `DescribeLoadBalancerListeners`.

| Parameter | Required | Type | Description |
|-----|----|----|------------|
| loadBalancerId | Yes | String | Unique ID of the CLB instance, which can be queried via the <a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers</a> API. You can use `loadBalancerId` or `unLoadBalancerId`, we recommand using `unLoadBalancerId`. |
| listenerIds.n | No | String | ID of the CLB listener. |
| protocol | No | Int | Protocol type of the listener. 1: HTTP; 2: TCP; 3: UDP; 4: HTTPS. |
| loadBalancerPort | No | Int | Port of the CLB listener. |
| status | No | Int | Status of the CLB listener. This field will be ignored when `listenerIds.n` is specified.|


## 3. Response Parameters

| Parameter | Type | Description |
|------|-----|-------|
| code | Int | Common error code. 0: success; other values: failure. For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/11602#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81" title="Common Error Codes"> Common Error Codes</a>. |
| message | String | API-related module error message description. |
| codeDesc | String | Error code. For a successful operation, "Success" is returned. For a failed operation, a message describing the failure is returned. |
| totalCount | Int | Total number of CLB instances that meet the filter criteria. |
| listenerSet | Array | Returned array of listeners. |

Data structure of the returned `listener` array:

| Parameter | Type | Description |
|--------|-------|-------|
| unListenerId | String | ID of the CLB listener. |
| loadBalancerPort | Int | Listening port of the CLB instance. |
| instancePort | Int | Forwarding port of the listener’s backend. |
| listenerName | String | Listener name. |
| protocol | No | Int | Protocol type of the listener<br>. 1: HTTP; 2: TCP; 3: UDP; 4: HTTPS. |
| sessionExpire | Int | Session persistence duration.|
| healthSwitch | Int | Whether to enable the health check. 1: enable; 0: disable. |
| timeOut | Int | Response timeout. |
| intervalTime | Int | Interval between health checks. |
| healthNum | Int | Healthy threshold. |
| unhealthNum | Int | Unhealthy threshold. |
| httpHash | String | Polling method of the public network HTTP or HTTPS listener with static IP. Valid values: wrr (weighted round robin) ip_hash (forwarding the hash of the source IP to the real server). |
| httpCode | Int | Health check return code of the public network HTTP or HTTPS listener with static IP. |
| httpCheckPath | String | Health check path of the public network HTTP or HTTPS listener with static IP.|
| SSLMode | String | Verification method of public network HTTPS listener with static IP. |
| certId | String | Server certificate ID of the public network HTTPS listener with static IP. |
| certCaId | String | Client certificate ID of the public network HTTPS listener with static IP. |
| status | Int | Listener status. 0: creating. 1: running. |

## 4. Example

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


