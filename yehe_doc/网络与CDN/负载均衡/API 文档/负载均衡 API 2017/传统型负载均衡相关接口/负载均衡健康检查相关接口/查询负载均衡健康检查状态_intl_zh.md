## 接口描述
 DescribeLBHealthStatus 接口用来查询负载均衡实例的健康检查相关参数。
 
接口访问域名：`lb.api.qcloud.com`

## 请求参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/214/11594) 页面。其中，此接口的 Action 字段为 DescribeLBHealthStatus。
	 
<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>必选</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> loadBalancerId
<td>是
<td> String
<td> 负载均衡实例 ID，可通过 <a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers"> DescribeLoadBalancers </a> 接口查询。
<tr>
<td> listenerId
<td> 否
<td> String
<td> 负载均衡监听器 ID, 可通过 <a href="https://intl.cloud.tencent.com/document/api/214/1260" title=" DescribeLoadBalancerListeners"> DescribeLoadBalancerListeners</a> 接口查询。
</tbody></table>
 

##  返回参数
 
<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> code
<td> Int
<td> 公共错误码，0表示成功，其他值表示失败。详情请参见 <a href="https://intl.cloud.tencent.com/document/product/214/11602" title="公共错误码">公共错误码</a>。
<tr>
<td> message
<td> String
<td>  模块错误信息描述，与接口相关。
<tr>
<td> codeDesc
<td> String
<td>  英文错误码，成功返回 Success，失败有相应的英文说明。
<tr>
<td> data
<td> Array
<td> 返回的数组。
</tbody></table>

**Data数组结构：**

<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> ip
<td> String
<td> 云服务器内网 IP。
<tr>
<td> protocol
<td> String
<td> 协议。
<tr>
<td> port
<td> Int
<td> 云服务器端口。
<tr>
<td> vport
<td> Int
<td> 负载均衡监听端口。
<tr>
<td> healthStatus
<td> Int
<td> 健康检查结果，1表示健康，0表示不健康。
</tbody></table>
 

## 示例

请求示例
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=DescribeLBHealthStatus
&<<a href="https://intl.cloud.tencent.com/document/api/213/6976">公共请求参数</a>>
&loadBalancerId=lb-abcdefgh
</pre>
返回示例
```
{
  "code":0,
  "message" : "",
  "codeDesc": "Success",
  "data":[
	     {
			"ip":"10.2.3.0",
			"protocol":"TCP",
			"port":8001,
			"vport":8001,
			"healthStatus":0
	     }
	]
}
```
 
