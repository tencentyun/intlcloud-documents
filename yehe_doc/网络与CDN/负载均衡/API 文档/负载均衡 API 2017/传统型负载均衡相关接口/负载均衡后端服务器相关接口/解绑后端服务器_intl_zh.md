## 接口描述

DeregisterInstancesFromLoadBalancer 接口用来将一台或多台云服务器从负载均衡实例上解绑。
 
接口访问域名：`lb.api.qcloud.com`

## 请求参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/214/11594) 页面。其中，此接口的 Action 字段为 DeregisterInstancesFromLoadBalancer。
	 
 
<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>必选</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> loadBalancerId
<td> 是
<td> String
<td>  负载均衡实例 ID，可通过 <a href="https://intl.cloud.tencent.com/document/api/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers</a> 接口查询。
<tr>
<td> backends.n.instanceId
<td> 是
<td> String
<td> 云服务器的唯一 ID，可通过 <a href="https://intl.cloud.tencent.com/document/api/213/%E6%9F%A5%E7%9C%8B%E5%AE%9E%E4%BE%8B%E5%88%97%E8%A1%A8" title="DescribeInstances">DescribeInstances</a>  接口返回字段中的 unInstanceId、instanceId 获取（建议使用 unInstanceId）；此接口支持同时输入多台主机的实例 ID ( 如：要输入两台主机，则设置 backends.0.instanceId&backends.1.instanceId )。
</tbody></table>

 

##  返回参数
 
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
<td>  模块错误信息描述，与接口相关。
<tr>
<td> codeDesc
<td> String
<td>  英文错误码，成功返回 Success，失败有相应的英文说明。
<tr>
<td> requestId
<td> Int
<td>  请求任务 ID，该接口为异步任务，可根据本参数调用 
<a href="https://intl.cloud.tencent.com/document/api/214/4007">DescribeLoadBalancersTaskResult</a> 接口来查询任务操作结果。
</tbody></table>

 

## 示例
 
请求
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=DeregisterInstancesFromLoadBalancer
&<<a href="https://intl.cloud.tencent.com/document/api/213/6976">公共请求参数</a>>
&loadBalancerId=lb-abcdefgh
&backends.0.instanceId=ins-1234test
&backends.1.instanceId=ins-6789test
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
 


