## API Description
 This API is used to delete listener(s) of a CLB instance.
 
Domain name for API calls: `lb.api.qcloud.com`

## Request Parameters
The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `DeleteLoadBalancerListeners`.
 
<table class="t"><tbody><tr>
<th><b>Parameter</b></th>
<th><b>Required</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> loadBalancerId
<td> Yes
<td> String
<td> CLB instance ID, which can be queried via the <a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers</a> API.
<tr>
<td> listenerIds.n
<td> Yes
<td> String
<td> ID of the CLB listener to delete, which can be queried via the<a href="https://intl.cloud.tencent.com/document/product/214/1260" title=" DescribeLoadBalancerListeners"> DescribeLoadBalancerListeners</a> API.

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
<td> Request task ID. The API provides an asynchronous task. You can use this parameter to query the execution result via the 
<a href="https://intl.cloud.tencent.com/document/api/214/4007"> DescribeLoadBalancersTaskResult</a> API.
</tbody></table>

## Example
 
Request
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=DeleteLoadBalancerListeners
&<<a href="https://intl.cloud.tencent.com/document/product/213/31574">Common request parameters</a>>
&loadBalancerId=lb-abcdefgh
&listenerIds.0=lbl-rbuzrm5d
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

 
