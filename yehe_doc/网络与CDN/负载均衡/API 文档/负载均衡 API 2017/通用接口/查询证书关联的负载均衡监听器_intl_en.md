## API Description
This API is used to query the information of the CLB instance associated with the certificate.
 
Domain name for API calls: `lb.api.qcloud.com`


## Request Parameters

The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `GetCertListWithLoadBalancer`.
 
| Parameter | Required | Type | Description |
|-|-|-|-|
|certIds.n | Yes | String | ID of the certificate to be queried. |


## Response Parameters
 
 
| Parameter | Type | Description |
|-------|---|---------------|
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/214/11602). |
| message | String | API-related module error message description. |
| codeDesc | String | Error code. For a successful operation, "Success" is returned. For a failed operation, a message describing the failure is returned. |
| certSet | Array | `key` is the certificate, and `value` is the information of the CLB instance and listener associated with the certificate. |

Data structure of the returned `certSet` array:

| Parameter | Type | Description |
|-|-|-|
| LBName | String | CLB instance name. |
|loadBalancerId | String | CLB instance ID. |
| Region | String | Region. |
| listener | Array | Listener information.|


Data structure of the returned `listener` array:

| Parameter | Type | Description |
|-|-|-|
| unListenerId | String | Listener ID. |
| listenerName | String | Listener name. |
| loadBalancerPort | Int | Listening port of the listener. |
| instancePort | Int | Service port of the listener's RS. |
| protocol | Int | Listener protocol. |
| sessionExpire | Int | Session persistence duration. |
| healthSwitch | Int | Whether the health check is enabled. |
| timeOut | Int | Response timeout. |
| intervalTime | Int | Interval between two health checks. |
| healthNum | Int | Healthy threshold. |
| unhealthNum | Int | Unhealthy threshold. |
| httpHash | No | String | Forwarding method of the CLB layer-7 listener. |
| scheduler | String | Forwarding method of the CLB layer-4 listener. |
| httpCode | Int | Return code for the health of HTTP and HTTPS listeners. |
| SSLMode | String | Verification mode of the HTTPS listener. |
| certId | String | New server certificate ID of the HTTPS listener. |
| certCaId | String | New client certificate ID of the HTTPS listener. |

## Example
 
Request
```
https://lb.api.qcloud.com/v2/index.php?Action=DescribeLoadBalancers
&<Common request parameters>
certIds.0=4b9fc92b
```

Response
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "certSet": {
        "4b9fc92b": [
            {
                "LBName": "ad",
                "loadBalancerId": "lb-ltkip4do",
                "region": "gz",
                "listener": [
                    {
                        "unListenerId": "lbl-6hkiqc6c",
                        "listenerName": "teaa",
                        "loadBalancerPort": 80,
                        "instancePort": 80,
                        "protocol": 4,
                        "SSLMode": "unidirectional",
                        "certId": "4b9fc92b",
                        "certCaId": "",
                        "sessionExpire": 0,
                        "healthSwitch": 1,
                        "timeOut": 6,
                        "intervalTime": 6,
                        "healthNum": 3,
                        "unhealthNum": 3,
                        "httpHash": "ip_hash",
                        "httpCode": 15
                    }
                ]
            },
            {
                "LBName": "ad",
                "loadBalancerId": "lb-ltkip4do",
                "region": "sh",
                "listener": [
                    {
                        "unListenerId": "lbl-6hkiqc6c",
                        "listenerName": "teaa",
                        "loadBalancerPort": 80,
                        "instancePort": 80,
                        "protocol": 4,
                        "SSLMode": "unidirectional",
                        "certId": "4b9fc92b",
                        "certCaId": "",
                        "sessionExpire": 0,
                        "healthSwitch": 1,
                        "timeOut": 6,
                        "intervalTime": 6,
                        "healthNum": 3,
                        "unhealthNum": 3,
                        "httpHash": "ip_hash",
                        "httpCode": 15
                    }
                ]
            }
        ]
    }
}

```

 
