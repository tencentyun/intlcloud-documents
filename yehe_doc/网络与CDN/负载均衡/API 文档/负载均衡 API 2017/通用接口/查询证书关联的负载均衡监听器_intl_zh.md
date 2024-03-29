## 接口描述
GetCertListWithLoadBalancer 接口用来查询证书关联的负载均衡信息。
 
接口访问域名：`lb.api.qcloud.com`


## 请求参数

以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/214/11594) 页面。其中，此接口的 Action 字段为 GetCertListWithLoadBalancer。
 
|参数名称|必选|类型|描述|
|-|-|-|-|
|certIds.n|是|String|要查询的证书 ID。|


## 返回参数
 
 
|参数名称|类型|描述|
|-------|---|---------------|
|code|Int|公共错误码，0表示成功，其他值表示失败。详见错误码页面的 [公共错误码](https://intl.cloud.tencent.com/document/product/214/11602)。|
|message|String|模块错误信息描述，与接口相关。|
|codeDesc|String|英文错误码，成功返回 Success，失败有相应的英文说明。|
|certSet|Array|证书为 key，value 为证书关联的负载均衡以及监听器的信息。|

返回的 certSet 数组内容：

|参数名称|类型|描述|
|-|-|-|
|LBName|String|负载均衡服务名称。|
|loadBalancerId|String|负载均衡实例的 ID。|
|region|String|地域。|
|listener|Array|监听器信息。|


返回的 listener 数组内容

|参数名称|类型|描述|
|-|-|-|
|unListenerId|String|监听器的 ID。|
|listenerName|String|监听器名称。|
|loadBalancerPort|Int|监听器的监听端口。|
|instancePort|Int|监听器的后端服务器服务端口。|
|protocol|Int|监听器的协议。|
|sessionExpire|Int|会话保持时间。|
|healthSwitch|Int|是否开启健康检查。|
|timeOut|Int|响应超时时间。|
|intervalTime|Int|检查间隔。|
|healthNum|Int|健康阈值。|
|unhealthNum|Int|不健康阈值。|
|httpHash|String|负载均衡七层监听器转发的方式。|
|scheduler|String|负载均衡四层监听器转发的方式。|
|httpCode|Int|对于 HTTP、HTTPS 协议的监听器，以该返回码来判断健康与否。|
|SSLMode|String|HTTPS 协议监听器的认证类型。|
|certId|String|HTTPS 协议监听器新的服务端证书 ID。|
|certCaId|String|HTTPS 协议监听器新的客户端证书 ID。|

## 示例
 
请求
```
https://lb.api.qcloud.com/v2/index.php?Action=DescribeLoadBalancers
&<公共请求参数>
certIds.0=4b9fc92b
```

返回
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

 
