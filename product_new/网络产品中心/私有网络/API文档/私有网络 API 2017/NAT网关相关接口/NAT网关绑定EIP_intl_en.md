## 1. API Description

This API (EipBindNatGateway) is used to bind the EIP to a NAT gateway.
Domain name for API requests: <font style="color:red">vpc.api.qcloud.com</font>

## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href=" https://intl.cloud.tencent.com/doc/api/229/6976" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is EipBindNatGateway.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| natId | Yes | String | Unified ID of the high-availability gateway, for example: nat-df5dfd. |
| vpcId | Yes | String | ID or unified ID (recommended) of the VPC, for example: vpc-dfd5dfgd. |
At least one of the two input parameters assignedEipSet and autoAllocEipNum must be passed in, for example, assignedEipSet.0=183.23.0.0.1. |
| autoAllocEipNum | No | Int | Number of EIPs in a new request. Value range: [0, 3]. Either assignedEipSet or autoAllocEipNum must be passed in. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | String | Error message |
| taskId | Int | Task ID. You can query the execution result by using the taskId. For more information, see the <a href="https://intl.cloud.tencent.com/doc/api/245/%e6%9f%a5%e8%af%a2%e4%bb%bb%e5%8a%a1%e6%89%a7%e8%a1%8c%e7%bb%93%e6%9e%9c%e6%8e%a5%e5%8f%a3">API for Querying Task Execution Results</a>. |

## 4. Error Codes
 The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC resource does not exist. In this case, verify whether the resource information that you entered is correct. You can query the VPC through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| InvalidNatGatewayId.NotFound | Invalid NAT gateway. This error code indicates that the NAT gateway resource does not exist. In this case, verify whether the resource information that you entered is correct. You can query the NAT gateway through the API <a href="https://intl.cloud.tencent.com/doc/api/245/%e6%9f%a5%e8%af%a2NAT%e7%bd%91%e5%85%b3?viewType=preview" title="DescribeNatGateway">DescribeNatGateway</a>. |

## 5. Example
Input
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=EipBindNatGateway
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
&natId=nat-8pbrkzh6
&vpcId=314
&autoAllocEipNum=1
</pre>
Output
```
{
    "code":"0",
    "message":"",
    "taskId":16167
}
```

