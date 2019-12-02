## 1. API Description

This API (ModifyNetworkAclEntry) is used to configure ACL rules.
API request domain name: <font style="color:red">vpc.api.qcloud.com</font>

You can configure both inbound and outbound network ACL policies.

## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href=" https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is ModifyNetworkAclEntry.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | Yes | String | ID of the VPC to which the subnet belongs, which can be vpcId or unVpcId (recommended), for example vpc-jk7weyp2. You can query the ID through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| networkAclId | Yes | String | Network ACL ID assigned by the system, for example: acl-jk7weyp2. You can query the ID through the API <a href="https://intl.cloud.tencent.com/doc/api/245/1441" title="DescribeNetworkAcl">DescribeNetworkAcl</a>. |
| ruleDirection | Yes | Int | Network ACL direction. 1: Inbound; 0: Outbound. |
| networkAclEntrySet.n | Yes | Array | Information array of network ACL policies. |
| networkAclEntrySet.n.desc | Yes | String | Comments. |
| networkAclEntrySet.n.ipProtocol | Yes | String | Protocol, such as TCP. |
| networkAclEntrySet.n.cidrIp | Yes | String | Source IP address or source IP range, for example: 10.20.3.0 or 10.0.0.2/24. IP or CIDR is supported. |
| networkAclEntrySet.n.portRange | Yes | String | Source port number or port range, for example: 80 or 90-100. |
| networkAclEntrySet.n.action | Yes | Int | Policy. 0: Allow; 1: Reject. |

 

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | String | Error message |

## 4. Error Codes
  The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. In this case, verify whether the resource information that you entered is correct. You can query the VPC through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| InvalidNetworkAclID.NotFound | Invalid Network ACL ID. This error code indicates that the Network ACL ID does not exist. In this case, verify whether the resource information that you entered is correct. You can query this ID through the API <a href="https://intl.cloud.tencent.com/doc/api/245/1441" title="DescribeNetworkAcl">DescribeNetworkAcl</a>. |
| NetworkAclInLimitExceeded | The number of created network ACL inbound rules exceeds its limit. To request more resources, contact our customer service. For more information about VPC resource limits, see <a href="https://intl.cloud.tencent.com/doc/product/215/537" title="VPC Use Limits">VPC Use Limits</a>. |
| NetworkAclOutLimitExceeded | The number of created network ACL outbound rules exceeds its limit. To request more resources, contact our customer service. For more information about VPC resource limits, see <a href="https://intl.cloud.tencent.com/doc/product/215/537" title="VPC Use Limits">VPC Use Limits</a>. |

## 5. Sample

Input
<pre>
  https://vpc.api.qcloud.com/v2/index.php?Action=ModifyNetworkAclEntry
  &<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
  &vpcId=vpc-erxok83l
  &networkAclId=acl-jk7weyp2
  &ruleDirection=1
  &networkAclEntrySet.0.desc=test
  &networkAclEntrySet.0.ipProtocol=all
  &networkAclEntrySet.0.cidrIp=0.0.0.0/0
  &networkAclEntrySet.0.portRange=ALL
  &networkAclEntrySet.0.action=1
</pre>

Output
```

{
    "code": 0,
    "message": ""
}

```

