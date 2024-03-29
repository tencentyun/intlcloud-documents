## 接口描述
 ModifyLoadBalancerAttributes 接口可以根据您的输入参数来修改负载均衡实例的基本配置信息。
 
接口访问域名：`lb.api.qcloud.com`

## 请求参数
 以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见 [公共请求参数](https://intl.cloud.tencent.com/document/product/214/11594) 页面。其中，此接口的 Action 字段为 ModifyLoadBalancerAttributes。
<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>必选</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> loadBalancerId
<td> 是
<td> String
<td> 负载均衡实例唯一 ID，可通过 <a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers</a> 接口查询。
<tr>
<td> loadBalancerName
<td> 否
<td> String
<td> 负载均衡实例名称，规则：1-50 个英文、汉字、数字、连接线“-”或下划线“_”。
<tr>
<td> domainPrefix
<td> 否
<td> String
<td> 域名前缀，负载均衡实例的域名由用户输入的域名前缀与配置文件中的域名后缀一起组合而成，保证是唯一的域名。<br>规则：1-20 个小写英文字母、数字或连接线“-”。<br>内网类型的负载均衡实例不能配置该字段。
</tbody></table>

 

## 返回参数
 
<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> code
<td> Int
<td> 公共错误码，0 表示成功，其他值表示失败。详见错误码页面的 <a href="https://intl.cloud.tencent.com/document/product/214/11602#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81" title="公共错误码">公共错误码</a>。
<tr>
<td> message
<td> String
<td> 模块错误信息描述，与接口相关。
<tr>
<td> codeDesc
<td> String
<td> 英文错误码，成功返回 Success，失败有相应的英文说明。
<tr>
<td> requestId
<td> Int
<td>请求任务 ID，该接口为异步任务，可根据本参数调用
<a href="https://intl.cloud.tencent.com/document/api/214/4007">DescribeLoadBalancersTaskResult</a> 接口来查询任务操作结果。
</tbody></table>

 

## 示例
 
请求
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=ModifyLoadBalancerAttributes
&<<a href="https://intl.cloud.tencent.com/document/api/213/6976">公共请求参数</a>>
&loadBalancerId=lb-abcdefgh
&loadBalancerName=my-lb-name
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
