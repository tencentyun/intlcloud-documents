## 1. API Description
This API (CreateSubnet) is used to create subnets.
API request domain name: <font style="color:red">vpc.api.qcloud.com</font> 

(1) You must create a VPC before creating a subnet.
(2) When the subnet is created, its IP address range cannot be changed. The subnet IP address range must fall within the VPC IP address range. They can be the same, in which case the VPC only has one subnet. We recommend that you set the subnet IP address range within the VPC IP address range to reserve IP address ranges for other subnets.
(3) The subnet mask of the smallest IP range that can be created is 28 (16 IP addresses), and that of the largest IP range is 16 (65,536 IP addresses).
(4) IP address ranges of different subnets must not overlap with each other within the same VPC.
(5) A subnet is automatically associated with the default route table once created.


## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href="https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is CreateSubnet.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | Yes | String | ID of VPC to which the subnet belongs, which can be the vpcId or unVpcId (recommended). You can query the ID through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| subnetSet.n | Yes | Array | Subnet information array. You can create subnets while creating a VPC. This field is optional. |
| subnetSet.n.subnetName | Yes | String | Subnet name, which cannot exceed 60 characters. |
| subnetSet.n.cidrBlock | Yes | String | Subnet IP address range, which must fall within the VPC IP address range. Subnet IP address ranges must not overlap with each other within the same VPC. |
| subnetSet.n.zoneId | Yes | String | ID of the availability zone in which the subnet resides. You can set up disaster recovery across availability zones by choosing different availability zones for different subnets. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/6091">VPC Availability Zones</a>. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/377/8946">Common Error Codes</a>. |
| message | String | Module error message, which depends on the API. |
| subnetSet.n | Array | Subnet information, which is returned when a subnet is added. |
| subnetSet.n.subnetId | String | Subnet ID assigned by the system, for example: subnetId_GZ_23. |
| subnetSet.n.unSubnetId | String | Unified subnet ID assigned by the system, for example: subnet-5gu2jxf4. It is derived from the subnet ID. The system supports both IDs for compatibility. |
| subnetSet.n.subnetName | String | Subnet name. |
| subnetSet.n.cidrBlock | String | Subnet IP address range, for example: 192.168.0.0/25. |
| subnetSet.n.routeTableId | String | ID of the default route table that is bound to the subnet, for example: gz_rtb_8751. |
| subnetSet.n.zoneId | String | ID of the availability zone in which the subnet resides, for example: 200001. |
| subnetSet.n.zone | String | ID of the availability zone in which the subnet resides, for example: ap-guangzhou-2. |

## 4. Error Codes
 The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. In this case, verify that the resource information that you entered is correct. You can query the VPC through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| InvalidSubnetName | Invalid subnet name. A valid subnet name cannot exceed 60 characters. |
| InvalidSubnetCidr | Subnet CIDR is invalid or does not fall within the VPC IP address range. Subnet CIDR value range: 10.0.0.0/16, 172.16.0.0/16, 192.168.0.0/16 and their subnets. |
| InvalidSubnet.Conflict | The subnet IP address range conflicts with other IP address ranges within the VPC. |
| SubnetLimitExceeded | The limit of requested subnet resources for the specific region has been reached. To request more resources, contact customer service. For more information about VPC resource limits, see <a href="https://intl.cloud.tencent.com/doc/product/215/537" title="VPC Use Limits">VPC Use Limits</a>. |
| InvalidZone.NotFound | Invalid availability zone ID. The availability zone that you entered does not exist or does not support VPCs. For more information, see VPC Availability Zones. |


## 5. Sample

Input
<pre>
  https://vpc.api.qcloud.com/v2/index.php?Action=CreateSubnet
	&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
  &vpcId=vpc-kd7d06of
  &subnetSet.0.subnetName=tttt
  &subnetSet.0.cidrBlock=10.0.200.0/24
  &subnetSet.0.zoneId=800001
</pre>

Output
```
{
    "code": 0,
    "message": "",
    "subnetSet": [
        {
            "subnetId": "gz_subnet_18748",
            "unSubnetId": "subnet-3lzrkspo",
            "routeTableId": "gz_rtb_359",
            "unRouteTableId": null,
            "subnetName": "tttt",
            "cidrBlock": "10.0.200.0\/24",
            "zoneId": 800001
        }
    ]
}

```

