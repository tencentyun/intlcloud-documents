## 接口描述
ModifyLoadBalancerBackends 接口用来修改绑定到负载均衡实例的云服务器权重。通过修改权重来调节请求转发的规则。
 
接口访问域名：`lb.api.qcloud.com`


## 请求参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/214/11594) 页面。其中，此接口的 Action 字段为 ModifyLoadBalancerBackends。
	 
<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>必选</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> loadBalancerId
<td> 是
<td> String
<td>  负载均衡实例 ID，可通过 <a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers</a> 接口查询。
<tr>
<td> backends.n.instanceId
<td> 是
<td> String
<td> 云服务器的唯一 ID，可通 <a href="https://intl.cloud.tencent.com/document/api/213/831" title="DescribeInstances">DescribeInstances</a> 接口返回字段中的 unInstanceId 字段获取；<br>此接口支持同时输入多台主机的实例 ID ( 如：要输入两台主机，则设置 backends.0.instanceId&backends.1.instanceId）。
<tr>
<td> backends.n.weight
<td> 是
<td> Int
<td> 绑定的云服务器的权重，取值范围 0-100，默认 10。
</tbody></table>

 

## 返回参数
 
<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> code
<td> Int
<td>公共错误码，0 表示成功，其他值表示失败。详见错误码页面的 <a href="https://intl.cloud.tencent.com/document/product/214/11602#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81" title="公共错误码">公共错误码</a>。
<tr>
<td> message
<td> String
<td>  模块错误信息描述，与接口相关。
<tr>
<td> codeDesc
<td> String
<td>  英文错误码，成功返回 Success，失败有相应的英文说明。
<tr>
<td> requestId
<td> Int
<td>请求任务 ID。该接口为异步任务，可根据本参数调用 
<a href="https://intl.cloud.tencent.com/document/api/214/4007">DescribeLoadBalancersTaskResult</a> 接口来查询任务操作结果。
</tbody></table>

 

## 示例
 
请求
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=ModifyLoadBalancerBackends
&<<a href="https://intl.cloud.tencent.com/document/api/213/6976">公共请求参数</a>>
&loadBalancerId=lb-abcdefgh
&backends.0.instanceId=ins-6789test
&backends.0.weight=10
&backends.1.instanceId=ins-1234test
&backends.1.weight=6
</pre>
返回
```

{
  "code" : 0,
  "message" : "",
  "codeDesc": "Success",
  "requestId" : 1234
}

```

