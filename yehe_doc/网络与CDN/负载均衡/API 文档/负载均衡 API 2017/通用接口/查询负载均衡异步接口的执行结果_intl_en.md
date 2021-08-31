## API Description

This API is used to query the execution result of a task with request task ID as the input parameter for Cloud Load Balancer and classic CLB.

Domain name for API calls: `lb.api.qcloud.com`

## Request Parameters
The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `DescribeLoadBalancersTaskResult`.
	 
<table class="t"><tbody><tr>
<th><b>Parameter</b></th>
<th><b>Required</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> requestId
<td> Yes
<td> Int
<td>Request task ID, which is obtained from the returned value of an asynchronous API.
</tbody></table>


## Response Parameters

<table class="t"><tbody><tr>
<th><b>Parameter</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> code
<td> Int
<td>Common error code. 0: success; other values: failure. For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/11602" title="Common Error Codes">Common Error Codes</a>.
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

<b></th>`Data` structure:</b></th>
<table class="t"><tbody><tr>
<th><b>Parameter</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> status
<td> Int
<td> Current task status.
0: successful; 1: failed; 2: in progress.
</tbody></table>


## Example
Request
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=DescribeLoadBalancersTaskResult
&<<a href="https://intl.cloud.tencent.com/document/api/213/6976">Common request parameters</a>>
&requestId=6356081
</pre>
Response
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
