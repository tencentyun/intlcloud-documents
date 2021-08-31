## API Description

This API is used to unbind one or multiple CVM instances from a CLB instance.
 
API domain name: `lb.api.qcloud.com`

## Request Parameters
The list below contains only the API request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field of this API is `DeregisterInstancesFromLoadBalancer`.
	 
 
<table class="t"><tbody><tr>
<th><b>Parameter Name</b></th>
<th><b>Required</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> loadBalancerId
<td> Yes
<td> String
<td>  CLB instance ID, which can be queried through the <a href="https://intl.cloud.tencent.com/document/api/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers</a> API.
<tr>
<td> backends.n.instanceId
<td> Yes
<td> String
<td> Unique ID of CVM instance, which can be obtained through the `unInstanceId` (recommended) or `instanceId` field returned by the <a href="https://intl.cloud.tencent.com/document/api/213/%E6%9F%A5%E7%9C%8B%E5%AE%9E%E4%BE%8B%E5%88%97%E8%A1%A8" title="DescribeInstances">DescribeInstances</a> API. You can enter the IDs of multiple CVM instances (for example, for two CVM instances, enter `backends.0.instanceId&backends.1.instanceId`).
</tbody></table>

 

## Response Parameters
 
<table class="t"><tbody><tr>
<th><b>Parameter Name</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> code
<td> Int
<td> Common error code. 0: success; other values: failure. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/214/11602" title="Common Error Codes">Common Error Codes</a>.
<tr>
<td> message
<td> String
<td>  Module error message related to the API.
<tr>
<td> codeDesc
<td> String
<td>  Error code. For a successful operation, "Success" will be returned. For a failed operation, a message describing the failure will be returned.
<tr>
<td> requestId
<td> Int
<td>  Request task ID. This API is an async task. You can call the 
<a href="https://intl.cloud.tencent.com/document/api/214/4007">DescribeLoadBalancersTaskResult</a> API to query the task operation result based on this parameter.
</tbody></table>

 

## Sample
 
Request
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=DeregisterInstancesFromLoadBalancer
&<<a href="https://intl.cloud.tencent.com/document/product/213/31574">Common request parameters</a>>
&loadBalancerId=lb-abcdefgh
&backends.0.instanceId=ins-1234test
&backends.1.instanceId=ins-6789test
</pre>
Return
```
{
  "code" : 0,
  "message" : "",
  "codeDesc": "Success",
  "requestId" : 1234
}
```
 


