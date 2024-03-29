## 接口描述

DescribeLoadBalancersTaskResult 适用于负载均衡和传统型负载均衡，该接口是以请求任务 ID 作为入参，来查询该任务的执行结果。

接口访问域名：`lb.api.qcloud.com`

## 请求参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/214/11594) 页面。其中，此接口的 Action 字段为 DescribeLoadBalancersTaskResult。
	 
<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>必选</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> requestId
<td> 是
<td> Int
<td> 请求任务 ID，在具体的异步操作接口的返回值中提取。
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
<td>  模块错误信息描述，与接口相关。
<tr>
<td> codeDesc
<td> String
<td>  英文错误码，成功返回 Success，失败有相应的英文说明。
<tr>
<td> data
<td> Array
<td> 返回的数组
</tbody></table>

<b></th>Data结构：</b></th>
<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> status
<td> Int
<td> 任务的当前状态。
0：成功，1：失败，2：进行中。
</tbody></table>


## 示例
请求
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=DescribeLoadBalancersTaskResult
&<<a href="https://intl.cloud.tencent.com/document/api/213/6976">公共请求参数</a>>
&requestId=6356081
</pre>
返回
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "status": 0
    }
}
```
