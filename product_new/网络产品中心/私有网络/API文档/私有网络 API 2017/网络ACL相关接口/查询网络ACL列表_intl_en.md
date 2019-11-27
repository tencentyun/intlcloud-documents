## 1. API Description

This API (DescribeNetworkAcl) is used to query the list of network ACLs.
API request domain name: <font style="color:red">vpc.api.qcloud.com</font>


## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href=" https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is DescribeNetworkAcl.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | No | String | ID of the VPC to which the subnet belongs, which can be the vpcId or unVpcId (recommended), for example vpc-0ox8fuhw. You can query this ID through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| networkAclId | No | String | Network ACL ID assigned by the system, for example: acl-0ox8fuhw. You can query this ID through the API <a href="https://intl.cloud.tencent.com/doc/api/245/1441" title="DescribeNetworkAcl">DescribeNetworkAcl</a>. |
| offset | No | Int | Offset of the initial line. The default is 0. |
| limit | No | Int | Number of lines per page. The default is 10 and the maximum is 50. |
| orderField | No | String | Sorts by a field. Only createTime and subnetName are supported currently. The default is createTime. |
| orderDirection | No | String | Ascending order (asc) or descending order (desc). The default is desc. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | String | Error message. |
| totalCount | Int | Total number of network ACLs in the returned result. |
| data.n | Array | Returned array. |
| data.n.vpcId | String | VPC ID assigned by the system, for example: gz_vpc_8849. |
| data.n.unVpcId | String | New VPC ID assigned by the system, for example: vpc-0ox8fuhw. This new ID is recommended. |
| data.n.networkAclId | String | Network ACL ID assigned by the system, for example: acl-e9dbyl8s. |
| data.n.networkAclName | String | Network name. |
| data.n.subnetNum | Int | Number of bound subnets. |
| data.n.createTime | String | Creation time of a network ACL, for example: 2015-11-06 20:55:12. |
| data.n.networkAclEntrySet | Array | Information array of network ACL policies. |


**networkAclEntrySet is composed as follows:**

| Parameter name | Type | Description |
|---------|---------|---------|
| networkAclEntrySet.Ingress.n | Array | Network ACL inbound rules. |
| networkAclEntrySet.ingress.n.desc | String | Comments. |
| networkAclEntrySet.ingress.n.ipProtocol | String | Protocol, for example: TCP. |
| networkAclEntrySet. Ingress.n.cidrIp | String | Source IP address or source IP range, for example: 10.20.3.0 or 10.0.0.2/24. IP or CIDR is supported. |
| networkAclEntrySet.ingress.n.portRange | String | Source port number or port range, for example: 80 or 90-100. |
| networkAclEntrySet.ingress.n.action | Int | Policy. 1: Allow; 0: Reject. |
| networkAclEntrySet.egress.n | Array | Network ACL outbound rules. |
| networkAclEntrySet.egress.n.desc | String | Comments. |
| networkAclEntrySet.egress.n.ipProtocol | String | Protocol, for example: TCP. |
| networkAclEntrySet.egress.n.cidrIp | String | Source IP address or source IP range, for example: 10.20.3.0 or 10.0.0.2/24. IP or CIDR is supported. |
| networkAclEntrySet.egress.n.portRange | String | Source port number, which can be a single port or a range of ports. For example: 80 or 90-100. |
| networkAclEntrySet.egress.n.action | Int | Policy. 1: Allow; 0: Reject. |

## 4. Error Codes
  The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. In this case, verify whether the resource information that you entered is correct. You can query the VPC through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| InvalidNetworkAclID.NotFound | Invalid Network ACL ID. This error code indicates that the Network ACL ID does not exist. In this case, verify whether the resource information that you entered is correct. You can query this ID through the API <a href="https://intl.cloud.tencent.com/doc/api/245/1441" title="DescribeNetworkAcl">DescribeNetworkAcl</a>. |

## 5. Sample

Input
<pre>
  https://vpc.api.qcloud.com/v2/index.php?Action=DescribeNetworkAcl
  &<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
  &vpcId=vpc-erxok83l
  &networkAclId=acl-jk7weyp2

</pre>

Output
```

{
    "code": 0,
    "message": "",
    "totalCount": 3,
    "data": [
        {
            "vpcId": "gz_vpc_231",
            "unVpcId": "vpc-erxok83l",
            "networkAclName": "tttssass",
            "networkAclId": "acl-e9dbyl8s",
            "vpcName": "barry-uniqVpci",
            "vpcCidrBlock": "10.20.80.0\/24",
            "subnetNum": 0,
            "createTime": "2015-11-06 20:55:12",
            "networkAclEntrySet": {
                "egress": [
                    {
                        "desc": "",
                        "ipProtocol": "all",
                        "cidrIp": "0.0.0.0\/0",
                        "portRange": "ALL",
                        "action": 1
                    }
                ],
                "ingress": [
                    {
                        "desc": "",
                        "ipProtocol": "all",
                        "cidrIp": "0.0.0.0\/0",
                        "portRange": "ALL",
                        "action": 1
                    }
                ]
            }
        },
        {
            "vpcId": "gz_vpc_265",
            "unVpcId": "vpc-ktom9wg5",
            "networkAclName": "barrytt",
            "networkAclId": "acl-cva92t60",
            "vpcName": "yunapitest",
            "vpcCidrBlock": "10.100.100.0\/24",
            "subnetNum": 0,
            "createTime": "2015-11-04 10:37:07",
            "networkAclEntrySet": {
                "egress": [
                    {
                        "desc": "",
                        "ipProtocol": "all",
                        "cidrIp": "0.0.0.0\/0",
                        "portRange": "ALL",
                        "action": 1
                    }
                ],
                "ingress": [
                    {
                        "desc": "",
                        "ipProtocol": "all",
                        "cidrIp": "0.0.0.0\/0",
                        "portRange": "ALL",
                        "action": 1
                    }
                ]
            }
        },
        {
            "vpcId": "gz_vpc_76",
            "unVpcId": "vpc-03vihbk9",
            "networkAclName": "dddddUniq",
            "networkAclId": "acl-7gvd06dq",
            "vpcName": "pan-vpc2",
            "vpcCidrBlock": "10.100.2.0\/24",
            "subnetNum": 0,
            "createTime": "2015-10-22 18:23:29",
            "networkAclEntrySet": {
                "egress": [
                    {
                        "desc": "",
                        "ipProtocol": "all",
                        "cidrIp": "0.0.0.0\/0",
                        "portRange": "ALL",
                        "action": 1
                    }
                ],
                "ingress": [
                    {
                        "desc": "",
                        "ipProtocol": "all",
                        "cidrIp": "0.0.0.0\/0",
                        "portRange": "ALL",
                        "action": 1
                    }
                ]
            }
        }
    ]
}

```

