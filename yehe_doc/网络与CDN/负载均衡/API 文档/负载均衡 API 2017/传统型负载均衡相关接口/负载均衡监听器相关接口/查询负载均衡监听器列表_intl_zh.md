## 接口描述
DescribeLoadBalancerListeners 接口可根据负载均衡器 ID，监听器的协议或者端口作为过滤条件获取监听器列表。

接口访问域名：`lb.api.qcloud.com`

## 请求参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/214/11594) 页面。其中，此接口的 Action 字段为 DescribeLoadBalancerListeners。
 
|参数名称|必选|类型|描述|
|-----|----|----|------------|
|loadBalancerId|是|String|负载均衡实例 ID，可通过 <a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers</a> 接口查询。|
|listenerIds.n|否|String|负载均衡监听器 ID。|
|protocol|否|Int|监听器协议类型<br>1：HTTP，2：TCP，3：UDP，4：HTTPS。|
|loadBalancerPort|否|Int|负载均衡监听器端口。|
|status|否|Int|负载均衡监听器的状态，当输入负载均衡监听器 ID 来查询时，忽略该字段。|


## 返回参数
 
|参数名称|类型|描述|
|------|-----|-------|
|code|Int|公共错误码，0表示成功，其他值表示失败。详见错误码页面的 <a href="https://intl.cloud.tencent.com/document/product/214/11602" title="公共错误码">公共错误码</a>。|
|message|String|模块错误信息描述，与接口相关。|
|codeDesc|String|英文错误码，成功返回 Success，失败有相应的英文说明。|
|totalCount|Int|满足过滤条件的负载均衡监听器总数。|
|listenerSet|Array|返回的监听器数组。|

返回的 listenerSet 数组结构

|参数名称|类型|描述|
|--------|-------|-------|
|listenerId|String|负载均衡监听器 ID。|
|unListenerId|String|负载均衡监听器 ID。|
|loadBalancerPort|Int|负载均衡器监听端口。|
|instancePort|Int|监听器后端转发端口。|
|listenerName|String|监听器的名字。|
|protocol|Int|监听器协议类型<br>1：HTTP，2：TCP，3：UDP，4：HTTPS。|
|sessionExpire|Int|会话保持时间。|
|healthSwitch|Int|是否开启了检查：1（开启）、0（关闭）。|
|timeOut|Int|响应超时时间。|
|intervalTime|Int|检查间隔。|
|healthNum|Int|健康阈值。|
|unhealthNum|Int|不健康阈值。|  
|httpHash|String|传统型公网属性的负载均衡的 HTTP、HTTPS 协议监听器的转发方式。|
|scheduler|String|传统型公网属性的负载均衡 UDP、TCP 协议监听器的转发方式。|
|httpCode|Int|传统型公网属性的负载均衡的 HTTP、HTTPS 协议监听器的健康检查返回码。具体可参考 [创建监听器](https://intl.cloud.tencent.com/document/product/214/1255) 中对该字段的解释。|
|httpCheckPath|String|传统型公网属性的负载均衡的 HTTP、HTTPS 协议监听器的健康检查路径。|
|SSLMode|String|传统型公网属性的负载均衡 HTTPS 协议监听器的认证方式。|
|certId|String|传统型公网属性的负载均衡 HTTPS 协议监听器服务端证书 ID。|
|certCaId|String|传统型公网属性的负载均衡 HTTPS 协议监听器客户端证书 ID。|
|status|Int|监听器的状态，0表示创建中，1表示运行中。|

## 示例
 
请求
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=DescribeLoadBalancerListeners
&<<a href="https://intl.cloud.tencent.com/document/api/213/6976">公共请求参数</a>>
&loadBalancerId=lb-abcdefgh
&listenerIds.0=lbl-6hkiqc6c
&listenerIds.1=lbl-6wv071ba
</pre>

返回
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
