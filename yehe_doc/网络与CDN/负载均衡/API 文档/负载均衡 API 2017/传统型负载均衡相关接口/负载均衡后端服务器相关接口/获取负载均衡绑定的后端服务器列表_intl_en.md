## API Description
This API is used to query the list of CVMs bound to the CLB instance by instance ID.
 
 Domain name for API calls: `lb.api.qcloud.com`

## Request Parameters
The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `DescribeLoadBalancerBackends`.

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
</tbody></table>

 

## Response Parameters
 
<table class="t"><tbody><tr>
<th><b>Parameter</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> code
<td> Int
<td> Common error code. 0: success; other values: failure. For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/11602" title="Common Error Codes">Common Error Codes</a>. |
<tr>
<td> message
<td> String
<td> API-related module error message description. |
<tr>
<td> codeDesc
<td> String
<td> Error code. For a successful operation, "Success" is returned. For a failed operation, a message describing the failure is returned.
<tr>
<td> totalCount
<td> Int
<td> Total number of CVMs bound to this CLB instance.
<tr>
<td> backendSet
<td> Array
<td> Array of real servers returned.
</tbody></table>

</b></th>Structure of the `backendSet` array:</b></th>
<table class="t"><tbody><tr>
<th><b>Parameter</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> instanceId
<td> String
<td> CVM instance ID.
<tr>
<td> unInstanceId
<td> String
<td>CVM instance ID. This parameter supports all operations of `instanceId`. We recommend using it.
<tr>
<td> weight
<td> Int
<td> Weight of the CVM instance.
<tr>
<td> instanceName
<td> String
<td> Name of the CVM instance.
<tr>
<td> lanIp
<td> String
<td> Private IP of the CVM instance.
<tr>
<td> wanIpSet
<td> Array
<td> Public IP of the CVM instance.
<tr>
<td> instanceStatus
<td> Int
td> Status of the CVM instance.<br>1: failed; 2: running; 3: creating; 4: shut down; 5: returned; 6: returning; 7: restarting; 8: starting; 9: shutting down; 10: resetting password; 11: formatting; 12: creating image; 13: setting bandwidth; 14: reinstalling system; 19: upgrading; 21: hot migrating
</tbody></table>

 

## Example
 
Request
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=DescribeLoadBalancerBackends
&<<a href="https://intl.cloud.tencent.com/document/product/213/31574">Common request parameters</a>>
&loadBalancerId=lb-byhpduqt
</pre>
Response
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "totalCount": 1,
    "backendSet": [
        {
            "instanceId": "qcvmed9e93b0bb2784b043c983761e624639",
            "unInstanceId": "ins-9o9ex9s0",
            "instanceName": "test_k8s_1",
            "lanIp": "10.104.222.152",
            "wanIpSet": [
                "193.112.93.144"
            ],
            "instanceStatus": 4,
            "weight": 44
        }
    ]
}

```
 
