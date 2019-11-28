## 1. API Description

This API (CreateVpc) is used to create VPCs.

Domain name for API request: vpc.api.qcloud.com

1. The subnet mask of the smallest IP range that can be created is 28 (16 IP addresses), and that of the largest IP range is 16 (65,536 IP addresses). For more information, see the document about VPC IP ranges.
2. You can create a subnet while creating a VPC. When creating a subnet, you should also configure the subnet IP range and the availability zone in which the subnet resides. Subnet IP ranges in the same VPC cannot overlap with each other, and disaster recovery across different availability zones is allowed. For more information, see the document about VPC availability zones.
3. If you create a subnet while creating a VPC, the system will create a default route table and associate it with this subnet.
4. The number of VPCs that can be created in a region is also limited. For more information, see <a href="https://intl.cloud.tencent.com/doc/product/215/537" title="VPC Use Limits">VPC Use Limits</a>. To request more resources, please contact customer service. 

## 2. Input Parameters
 Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href="https://intl.cloud.tencent.com/document/product/215/4772" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is CreateVpc.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcName | Yes | String | VPC name, which cannot exceed 60 characters. |
| cidrBlock | Yes | String | VPC IP address range. Available values: 10.0.0.0/16, 172.16.0.0/16, 192.168.0.0/16, and their subnets. For more information, see the document about VPC IP ranges. |
| subnetSet.n | No | Array | Subnet information array. You can create subnets while creating a VPC. This parameter is optional. |
| subnetSet.n.subnetName | No | String | Subnet name, which cannot exceed 60 characters. |
| subnetSet.n.cidrBlock | No | String | Subnet IP range. It must fall within the VPC IP address range. Subnet IP address ranges must not overlap with each other within the same VPC. |
| subnetSet.n.zoneId | No | String | ID of the availability zone in which the subnet resides. You can set up disaster recovery across availability zones by choosing different availability zones for different subnets. For more information, see VPC Availability Zones</a>. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/215/4781#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81" title="Common Error Codes">Common Error Codes</a> on the “Error Codes” page.|
| message | String | Module error message, which depends on the API. |
| vpcId | String | vpcId assigned by the system, for example: gz_vpc_226. |
| unVpcId | String | Unified ID assigned by the system, for example: vpc-2ari9m7h. This ID is derived from the vpcId. The system supports both IDs for compatibility, but the unified ID is recommended. |
| vpcCreateTime | String | Creation time of the VPC, for example: 2015-11-06 11:33:52. |
| subnetSet.n | Array | Subnet information, which is returned when a subnet is added. |
| subnetSet.n.subnetId | String | Subnet ID assigned by the system, for example: subnetId_GZ_23. |
| subnetSet.n.unSubnetId | String | Unified subnet ID assigned by the system, for example: subnet-5gu2jxf4. This ID is derived from the vpcId. The system supports both IDs for compatibility. |
| subnetSet.n.routeTableId | String | ID of the default route table bound to the subnet, for example: gz_rtb_8751. |
| subnetSet.n.subnetName | String | Subnet name. |
| subnetSet.n.cidrBlock | String | Subnet IP range, for example: 192.168.0.0/25. |
| subnetSet.n.zoneId | String | ID of the availability zone (numeric-type parameter) in which the subnet resides, for example: 200001. |
| subnetSet.n.zone | String | ID of the availability zone (string-type parameter) in which the subnet resides, for example: ap-guangzhou-1. |
| routeTableSet.n | Array | Route table information. By default, a subnet is associated with the default route table. |
| routeTableSet.n.routeTableId | String | The route table ID assigned by the system, for example: gz_rtb_8751. |
| routeTableSet.n.routeTableType | Int | Route table type. 0: Ordinary route table; 1: Default route table. |
| routeTableSet.n.routeTableName | String | Route table name. |

## 4. Error Codes
 The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVpcName | Invalid VPC name. This name cannot exceed 60 characters. |
| InvalidVpcCidr | VPC CIDR is invalid. Available values for VPC CIDR: 10.0.0.0/16, 172.16.0.0/16, 192.168.0.0/16, and their subnets. For more information, see the document about VPC IP ranges. |
| VpcLimitExceeded | The limit of requested VPC resources for the specific region has been reached. To request more resources, contact customer service. For more information on VPC resource limits, see <a href="https://intl.cloud.tencent.com/doc/product/215/537" title="VPC Use Limits" >VPC Use Limits</a>. |
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. In this case, verify whether the resource information that you entered is correct. |

## 5. Sample

Input
<pre>
  https://vpc.api.qcloud.com/v2/index.php?Action=CreateVpc
  &<Common request parameters>
  &vpcName=bbbtest
  &cidrBlock=192.168.0.0/16
  &subnetSet.0.subnetName=wikitest
  &subnetSet.0.cidrBlock=192.168.1.0/24
  &subnetSet.0.zoneId=800001

</pre>

Output
```

{
    "code": 0,
    "message": "",
    "vpcId": "gz_vpc_266",
    "uniqVpcId": "vpc-2ari9m7h",
    "vpcCreateTime": "2015-11-06 11:33:52",
    "subnetSet": [
        {
            "subnetId": "gz_subnet_18720",
            "unSubnetId": "subnet-5gu2jxf4",
            "routeTableId": "gz_rtb_8751",
            "subnetName": "wikitest",
            "cidrBlock": "192.168.1.0/24",
            "zoneId": 800001
        }
    ],
    "routeTableSet": [
        {
            "routeTableId": "gz_rtb_8751",
            "routeTableType": 1,
            "routeTableName": "Default"
        }
    ]
}

```

