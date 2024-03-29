## 接口描述
 ModifyLoadBalancerListener 接口用来修改负载均衡监听器的属性。
 
接口访问域名：`lb.api.qcloud.com`


## 请求参数

以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/214/11594) 页面。其中，此接口的 Action 字段为 ModifyLoadBalancerListener。
 
|参数名称|必选|类型|描述|
|-----|------|--------|-----------|
|loadBalancerId|是|String|负载均衡实例 ID，可通过 <a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers</a> 接口查询。|
|listenerId|是|String|负载均衡监听器 ID，可通过 <a href="https://intl.cloud.tencent.com/document/product/214/1260" title=" DescribeLoadBalancerListeners"> DescribeLoadBalancerListeners</a> 接口查询。|
|listenerName|否|String|监听器名称。|
|sessionExpire|否|Int|会话保持时间，0表示关闭，可选值：30-3600。|
|healthSwitch|否|Int|是否开启健康检查：1（开启）、0（关闭）。|
|timeOut|否|Int|响应超时时间，可传值为 2-60 秒；<br>公网属性负载均衡 HTTP、HTTPS 协议的监听器响应超时时间暂不能设置。|
|intervalTime|否|Int|检查间隔，可选值：5-300。默认值5。|
|healthNum|否|Int|健康阈值，可选值：2-10。|
|unhealthNum|否|Int|不健康阈值，可选值：2-10。|
|scheduler|否|String|负载均衡监听器转发的方式，该值不可以与 httpHash 同时传入。公网属性负载均衡（监听器为TCP、UDP）才支持此字段，可传值：wrr、least_conn。分别表示按权重轮询、最小连接数。|
|httpHash|否|String|负载均衡监听器转发的方式。公网属性负载均衡（监听器为 HTTP、HTTPS）才支持此字段，可传值：wrr、ip_hash，least_conn<br>分别表示按权重轮询、根据源 IP 进行哈希出一个值转发到后端机器、最小连接数， 默认为 wrr。|
|httpCode|否|Int|对于 HTTP、HTTPS 协议的监听器，以该返回码来判断健康与否。可选值：1~31，默认31。<br>1表示返回值 1xx 表示健康，2表示返回 2xx 表示健康，4表示返回 3xx 表示健康，8表示返回 4xx 表示健康，16表示返回 5xx 表示健康。若返回多种表示健康，则将相应的值累加。|
|httpCheckPath|否|String|公网属性负载均衡 HTTP、HTTPS 协议的监听器，健康检查的路径，默认/，必须以/开头。|
|SSLMode|否|String|公网属性负载均衡 HTTPS 协议监听器的认证类型，unidirectional：单向认证，mutual：双向认证。|
|certId|否|String|公网属性负载均衡 HTTPS 协议监听器新的服务端证书 ID。|
|certCaId|否|String|公网属性负载均衡 HTTPS 协议监听器新的客户端证书 ID。|
|certCaContent|否|String|公网属性负载均衡 HTTPS 协议监听器新的客户端证书内容。|
|certCaName|否|String|公网属性负载均衡 HTTPS 协议监听器新的客户端证书名称。|
|certContent|否|String|公网属性负载均衡 HTTPS 协议监听器新的服务端证书内容。|
|certKey|否|String|公网属性负载均衡 HTTPS 协议监听器新的服务端证书的密钥。|
|certName|否|String|公网属性负载均衡 HTTPS 协议监听器新的服务端证书的名称。|


## 返回参数
 
 
|参数名称|类型|描述|
|-------|---|---------------|
|code|Int|公共错误码，0表示成功，其他值表示失败。详见错误码页面的 [公共错误码](https://intl.cloud.tencent.com/document/product/214/11602)。|
|message|String|模块错误信息描述，与接口相关。|
|codeDesc|String|英文错误码，成功返回 Success，失败有相应的英文说明。|
|requestId|Int|请求任务 ID，可根据 [DescribeLoadBalancersTaskResult](https://intl.cloud.tencent.com/document/api/214/4007) 接口查询操作状态。|

## 示例
 
请求
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=ModifyLoadBalancerListener
&<<a href="https://intl.cloud.tencent.com/document/api/213/6976">公共请求参数</a>>
loadBalancerId=lb-ltkip4do
&listenerId=lbl-6hkiqc6c
&SSLMode=unidirectional
</pre>
返回
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "requestId": 18642
}

```
 
