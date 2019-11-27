## 1. API Description

This API (DescribeSubnetEx) is used to query the list of subnets.
API request domain name: <font style="color:red">vpc.api.qcloud.com</font> 


## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href="https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is DescribeSubnetEx.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | No | String | ID of the VPC to which the subnet belongs, which can be the vpcId or unVpcId (recommended), for example vpc-kd7d06of. You can query this ID through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| subnetId | No | String | Subnet ID assigned by the system, which can be the subnetId or unSubnetId (recommended), for example subnet-3lzrkspo. |
| subnetName | No | String | Subnet name, supports fuzzy query. |
| zoneIds | No | Array | Availability zone ID. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/6091">Regions and Availability Zones</a>. |
| offset | No | Int | Offset of the initial line. The default is 0. |
| limit | No | Int | Number of lines per page. The default is 20. |
| orderField | No | String | Sorts by a field. createTime and subnetName are supported. The default is createTime. |
| orderDirection | No | String | Ascending order (asc) or descending order (desc). The default is desc. |
| getAclIdFlag | No | Int | Whether to query the associated ACLID. 1: Return the associated ACLID; 0: Do not return the associated ACLID. Default: 0. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | String | Error message |
| totalCount | Int | Total number of subnets |
| data | Array | Returned array |
| data.n.vpcId | String | vpcId assigned by the system, for example: gz_vpc_266. |
| data.n.unVpcId | String | New vpcID assigned by the system, for example: vpc-5gu2jxf4. This ID is derived from the VPC ID. The new vpcId is recommended. |
| data.n.subnetId | String | Subnet ID assigned by the system, for example: subnetId_GZ_23. |
| data.n.unSubnetId | String | New subnet ID assigned by the system, for example: subnet-5gu2jxf4. This ID is derived from the subnet ID. The new subnet ID is recommended. |
| data.n.subnetName | String | Subnet name |
| data.n.cidrBlock | String | Subnet IP range, for example: 192.168.0.0/25. |
| data.n.routeTableId | String | ID of the default route table bound to the subnet, for example: gz_rtb_8751. |
| data.n.zoneId | String | ID of the availability zone in which the subnet resides, for example: 200001. |
| data.n.zone | String | ID of the availability zone in which the subnet resides, for example: ap-guangzhou-2. |
| data.n.networkAclId | String | ID of the network ACL bound to the subnet, for example: acl-e9dbyl8s. 0 is returned if no ACL is bound to the subnet. For more information, see <a href="https://intl.cloud.tencent.com/doc/api/245/1441" title="Network ACL-Related APIs">Network ACL-Related APIs</a>. |
| data.n.vpcDevices | Int | Number of CVMs within the subnet. |
| data.n.totalIPNum | Int | Number of IP addresses within the subnet. |
| data.n.availableIPNum | Int | Number of available IP addresses within the subnet. |
| data.n.broadcast | Bool | Whether broadcasting is enabled. true: Enabled; false: Disabled. |
| data.n.isDefault | Bool | Whether the current VPC is the default VPC. |

## 4. Error Codes
The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. In this case, verify whether the resource information that you entered is correct. You can query the VPC through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| InvalidSubnet.NotFound | Invalid subnet. This error code indicates that the subnet resource does not exist. In this case, verify whether the resource information that you entered is correct. You can query the subnet through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E5%AD%90%E7%BD%91%E5%88%97%E8%A1%A8" title="DescribeSubnetEx">DescribeSubnetEx</a>. |

## 5. Sample

Input
<pre>
  https://vpc.api.qcloud.com/v2/index.php?Action=DescribeSubnetEx
  &<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
  &subnetName=tttt
</pre>

Output

```
{
    "code": 0,
    "message": "",
    "totalCount": 1,
    "data": [
        {
            "vpcId": "gz_vpc_64",
            "unVpcId": "vpc-kd7d06of",
            "vpcName": "panpan-vpc1",
            "vpcCidrBlock": "10.0.0.0\/16",
            "subnetId": "gz_subnet_18748",
            "unSubnetId": "subnet-3lzrkspo",
            "subnetName": "tttt",
            "subnetCreateTime": "2015-11-13 12:06:26",
            "routeTableId": "gz_rtb_359",
            "unRouteTableId": "rtb-85alck92",
            "routeTableName": "222",
            "cidrBlock": "10.0.200.0\/24",
            "zoneId": 800001,
            "zone": "ap-guangzhou-2",
            "vpcDevices": 0,
            "networkAclId": 0,
            "totalIPNum": 253,
            "availableIPNum": 253,
            "broadcast":false
        }
    ]
}
```

