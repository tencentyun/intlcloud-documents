如无特别说明，每次请求的返回值中，都会包含下面的字段：
## 接口描述
 DeleteLoadBalancers 接口用来删用户指定的一个或者多个负载均衡实例。
接口访问域名：`lb.api.qcloud.com`

 
## 请求参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/214/11594) 页面。其中，此接口的 Action 字段为 DeleteLoadBalancers。
<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>必选</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> loadBalancerIds.n
<td> 是
<td> String
<td>  负载均衡实例 ID，可通过 <a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers </a> 接口查询。
</tbody></table>

 

## 返回参数
 
<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> code
<td> Int
<td> 公共错误码，0表示成功，其他值表示失败。详见错误码页面的 <a href="https://intl.cloud.tencent.com/document/product/214/11602" title="公共错误码">公共错误码</a>。
<tr>
<td> message
<td> String
<td> 模块错误信息描述，与接口相关。
<tr>
<td> codeDesc
<td> String
<td> 英文错误码。
<tr>
<td> requestId
<td> Int
<td>请求任务 ID，该接口为异步任务，可根据本参数调用 
<a href="https://intl.cloud.tencent.com/document/api/214/4007">DescribeLoadBalancersTaskResult </a> 接口来查询任务操作结果。
</tbody></table>

## 示例
 
请求
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=DeleteLoadBalancers
&<<a href="https://intl.cloud.tencent.com/document/api/213/6976">公共请求参数</a>>
&loadBalancerIds.0=lb-abcdefgh
</pre>
返回
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "requestId": 6356502
}
```

 
