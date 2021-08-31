## API Description
 This API is used to modify basic configuration information of CLB instances based on your input parameters.
 
Domain name for API calls: `lb.api.qcloud.com`

## Request Parameters
 The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `ModifyLoadBalancerAttributes`.
<table class="t"><tbody><tr>
<th><b>Parameter</b></th>
<th><b>Required</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> loadBalancerId
<td> Yes
<td> String
<td> Unique ID of the CLB instance, which can be queried via the <a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers</a> API.
<tr>
<td> loadBalancerName
<td> No
<td> String
<td> Name of the CLB instance, which can contain 1-50 characters, including letters, Chinese, numbers, hyphen (-) or underscore (_).
<tr>
<td> domainPrefix
<td> No
<td> String
<td> Domain name prefix. The domain name of a CLB instance consists of the user-defined domain name prefix and the domain suffix in the configuration file to ensure the uniqueness.<br>Rule: 1-20 characters including lowercase letters, numbers, or hyphen (-). <br>This field cannot be specified for private network CLB instances.
</tbody></table>

 

## Response Parameters
 
<table class="t"><tbody><tr>
<th><b>Parameter</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> code
<td> Int
<td> Common error code. 0: success; other values: failure. For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/11602#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81" title="Common Error Codes">Common Error Codes</a>.
<tr>
<td> message
<td> String
<td>API-related module error message description.
<tr>
<td> codeDesc
<td> String
<td> Error code. For a successful operation, "Success" is returned. For a failed operation, a message describing the failure is returned.
<tr>
<td> requestId
<td> Int
<td> Request task ID. The API provides an asynchronous task. You can use this parameter to query the execution result of the task via the
<a href="https://intl.cloud.tencent.com/document/api/214/4007"> DescribeLoadBalancersTaskResult</a> API.
</tbody></table>

 

## Example
 
Request
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=ModifyLoadBalancerAttributes
&<<a href="https://intl.cloud.tencent.com/document/product/213/31574">Common request parameters</a>>
&loadBalancerId=lb-abcdefgh
&loadBalancerName=my-lb-name
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
