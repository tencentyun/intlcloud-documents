## API Description
This API is used to bind one or more CVMs to a CLB instance.
 
Domain name for API calls: `lb.api.qcloud.com`


## Request Parameters
 
The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `RegisterInstancesWithLoadBalancer`.

<table class="t"><tbody><tr>
<th><b>Parameter</b></th>
<th><b>Required</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> loadBalancerId
<td> Yes
<td> String
<td> CLB instance ID, which can be queried via the<a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers"> DescribeLoadBalancers </a>API.
<tr>
<td> backends.n.instanceId
<td> Yes
<td> String
<td> Unique ID of the CVM, which can be obtained from the “unInstanceId” field in the response of the<a href="https://intl.cloud.tencent.com/document/product/213/33258" title="DescribeInstances"> DescribeInstances </a>API.<br>This API supports entering multiple CVM instance IDs at a time. For example, if you want to specify two CVMs, enter backends.0.instanceId&backends.1.instanceId.
<tr>
<td> backends.n.weight
<td> No
<td> Int
<td> Weight of the CVM. Value range: 0-100. Default value: 10.
</tbody></table>

 

## Response Parameters
 
<table class="t"><tbody><tr>
<th><b>Parameter</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> code
<td> Int
<td> Common error code. 0: success; other values: failure. For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/11602" title="Common Error Codes">Common Error Codes</a>.
<tr>
<td> message
<td> String
<td> API-related module error message description.
<tr>
<td> codeDesc
<td> String
<td> Error code. For a successful operation, "Success" is returned. For a failed operation, a message describing the failure is returned.
<tr>
<td> requestId
<td> Int
<td>Request task ID. The API provides an asynchronous task. You can use this parameter to query the operation result via the
<a href="https://intl.cloud.tencent.com/document/product/214/4007"> DescribeLoadBalancersTaskResult </a>API.
</tbody></table>

 

## Example
 
Request
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=RegisterInstancesWithLoadBalancer
&<<a href="https://intl.cloud.tencent.com/document/product/213/31574">Common request parameters</a>>
&loadBalancerId=lb-abcdefgh
&backends.0.instanceId=ins-1234test
&backends.0.weight=10
&backends.1.instanceId=ins-5678test
&backends.1.weight=6
</pre>
Response
```
{
  "code" : 0,
  "message" : "",
  "codeDesc": "Success",
  "requestId" : 1234
}
```


 

