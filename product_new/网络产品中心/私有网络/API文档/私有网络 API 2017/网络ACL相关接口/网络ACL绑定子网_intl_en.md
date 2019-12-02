## 1. API Description

This API (CreateSubnetAclRule) is used to associate a network ACL with subnets.
API request domain name: <font style="color:red">vpc.api.qcloud.com</font> 


## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href=" https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is CreateSubnetAclRule.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | Yes | String | ID of the VPC to which the subnet belongs, which can be the vpcId or unVpcId (recommended), for example vpc-erxok83l. You can query the ID through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| networkAclId | Yes | String | Network ACL ID assigned by the system, for example: acl-e9dbyl8s. You can query the ID through the API <a href="https://intl.cloud.tencent.com/doc/api/245/1441" title="DescribeNetworkAcl">DescribeNetworkAcl</a>. |
| subnetIds.n | Yes | Array | List of subnet IDs assigned by the system, for example: subnet-i6mdq6ra. Both the subnetId and unSubnetId are supported. unSubnetId is recommended. You can query the list through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E5%AD%90%E7%BD%91%E5%88%97%E8%A1%A8" title="DescribeSubnetEx">DescribeSubnetEx</a>. |

 

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | String | Error message. |


## 4. Error Codes
  The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. In this case, verify whether the resource information that you entered is correct. You can query the VPC through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| InvalidNetworkAclID.NotFound | Invalid network ACL ID. This error code indicates that the Network ACL ID does not exist. In this case, verify whether the resource information that you entered is correct. You can query this ID through the API <a href="https://intl.cloud.tencent.com/doc/api/245/1441" title="DescribeNetworkAcl">DescribeNetworkAcl</a>. |

## 5. Sample

Input
<pre>
  https://vpc.api.qcloud.com/v2/index.php?Action=CreateSubnetAclRule
  &<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
  &vpcId=vpc-erxok83l
  &networkAclId=acl-e9dbyl8s
  &subnetIds.0=subnet-i6mdq6ra

</pre>

Output
```

{
    "code": 0,
    "message": ""
}

```

