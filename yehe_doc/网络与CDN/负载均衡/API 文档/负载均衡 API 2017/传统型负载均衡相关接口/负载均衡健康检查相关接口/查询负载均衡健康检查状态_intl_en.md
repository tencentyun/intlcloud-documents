## API Description
 This API is used to query the health check parameters for CLB instances.
 
Domain name for API calls: `lb.api.qcloud.com`

## Request Parameters
The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `DescribeLBHealthStatus`.
	 
<table class="t"><tbody><tr>
<th><b>Parameter</b></th>
<th><b>Required</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> loadBalancerId
<td> Yes
<td> String
<td>CLB instance ID, which can be queried via the<a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers"> DescribeLoadBalancers </a>API.
<tr>
<td> listenerId
<td> No
<td> String
<td> CLB listener ID, which can be queried via the<a href="https://intl.cloud.tencent.com/document/api/214/1260" title=" DescribeLoadBalancerListeners"> DescribeLoadBalancerListeners</a> API.
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
<td> data
<td> Array
<td> Returned array.
</tbody></table>

**Data structure of the `data` array:**

<table class="t"><tbody><tr>
<th><b>Parameter</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> ip
<td> String
<td> Private IP of the CVM.
<tr>
<td> protocol
<td> String
<td> Protocol.
<tr>
<td> port
<td> Int
<td> Port of the CVM.
<tr>
<td> vport
<td> Int
<td> Listening port of the CLB instance.
<tr>
<td> healthStatus
<td> Int
<td> Health check result. 1: healthy; 0: unhealthy.
</tbody></table>
 

## Example

Sample request
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=DescribeLBHealthStatus
&<<a href="https://intl.cloud.tencent.com/document/product/213/31574">Common request parameters</a>>
&loadBalancerId=lb-abcdefgh
</pre>
Sample response
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
 
