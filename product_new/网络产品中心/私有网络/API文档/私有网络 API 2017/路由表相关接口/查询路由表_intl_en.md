## 1. API Description

This API (DescribeRouteTable) is used to query route tables.
Domain name for API requests: <font style="color:red">vpc.api.qcloud.com</font>


## 2. Input Parameters

The following request parameter list only provides API request parameters. Common request parameters are required when the API is called. For more information, see the <a href="https://intl.cloud.tencent.com/document/product/215/1372/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is DescribeRouteTable.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | No | String | ID of the VPC to which the subnet belongs, which can be the vpcId or unVpcId (recommended), for example vpc-0ox8fuhw. You can query the ID through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| routeTableId | No | String | Route table ID assigned by the system, which can be the routeTableId or unRouteTableId (recommended), for example rtb-rqndayhs. You can query the ID through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E8%B7%AF%E7%94%B1%E8%A1%A8" title="DescribeRouteTable">DescribeRouteTable</a>. |
| routeTableName | No | String | Route table name, supports fuzzy query. |
| offset | No | Int | Offset of the initial line. The default is 0. |
| limit | No | Int | Number of lines per page. The default is 20 and the maximum is 50. |
| orderField | No | String | Sorts by a field. Only createTime and routeTableName are supported currently. The default is createTime. |
| orderDirection | No | String | Ascending order (asc) or descending order (desc). The default is desc. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | String | Error message. |
| totalCount | Int | Total number of routes in the query result. |
| data.n | Array | Returned array. |
| data.n.vpcId | String | VPC ID assigned by the system, for example: gz_vpc_8849. |
| data.n.unVpcId | String | New VPC ID assigned by the system, for example: vpc-0ox8fuhw. This new ID is recommended. |
| data.n.routeTableId | String | Route table ID assigned by the system, for example: gz_rtb_8849. |
| data.n.unRouteTableId | String | New route table ID assigned by the system, for example: rtb-0ox8fuhw. The new ID is recommended. |
| data.n.routeTableName | String | Route table name. |
| data.n.routeTableType | Int | Type of the route table. 0: Ordinary route table; 1: Default route table. For more information about the differences between the two types of route tables, see <a href="" title="Route Table Overview">Route Table Overview</a>. |
| data.n.routeTableCreateTime | String | Creation time of the route table, for example: 2015-11-06 17:50:21. |
| data.n.subnetNum | Int | Number of associated subnets. |
| data.n.routeTableSet.n | Array | Information array of routing policies. |

routeTableSet information array of routing policies

| Parameter name | Type | Description |
|---------|---------|---------|
| routeTableSet.n.destinationCidrBlock | String | Destination IP range, for example: 112.20.51.0/24. The values within the VPC IP range cannot be used. |
| routeTableSet.n.nextType | String | Type of the next hop. Supported types: 0: Public gateway; 1: VPN gateway; 3: Direct connect gateway; 4: Peering connection; 7: sslvpn; 8: NAT gateway; 9: Ordinary CVM. |
| routeTableSet.n.nextHub | String | Address of the next hop. You simply need to specify gateway IDs (the new ID is recommended) of different next hop types, and the system will automatically match them to the next hop address.
| routeTableSet.n.unNextHub | String | Unique ID of next hop address, which is the the unique ID of the address of the next hop. We recommend using the unified ID. |
| routeTableSet.n.description | String | Route description. |

## 4. Error Codes
 The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. In this case, verify whether the resource information that you entered is correct. You can query the VPC through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| InvalidRouteTableId.NotFound | Invalid route table. This error code indicates that the route table ID does not exist. In this case, verify whether the resource information that you entered is correct. You can query this ID through the API <a href="http://cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E8%B7%AF%E7%94%B1%E8%A1%A8" title="DescribeRouteTable"> DescribeRouteTable</a>. |

## 5. Example

Input
<pre>
  https://vpc.api.qcloud.com/v2/index.php?Action=DescribeRouteTable
  &<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
  &vpcId=vpc-amhnnao5
  &routeTableName=tttt111
</pre>

Output
```

{
    "code": 0,
    "message": "",
    "totalCount": 114,
    "data": [
        {
            "vpcId": "gz_vpc_99",
            "unVpcId": "vpc-amhnnao5",
            "vpcName": "pan-vpc25",
            "vpcCidrBlock": "10.100.25.0\/24",
            "routeTableName": "tttt111",
            "routeTableId": "gz_rtb_8755",
            "unRouteTableId": "rtb-rqndayhs",
            "routeTableType": 0,
            "subnetNum": 1,
            "routeTableCreateTime": "2015-11-06 17:50:21",
            "routeSet": [
                {
                    "destinationCidrBlock": "Local",
                    "nextType": 2,
                    "nextHub": "Local"
                },
                {
                    "destinationCidrBlock": "121.0.0.0\/16",
                    "nextType": 1,
                    "nextHub": "548"
                }
            ]
        },
        {
            "vpcId": "gz_vpc_266",
            "unVpcId": "vpc-2ari9m7h",
            "vpcName": "bbbtest",
            "vpcCidrBlock": "192.168.0.0\/24",
            "routeTableName": "default,
            "routeTableId": "gz_rtb_8751",
            "unRouteTableId": "rtb-ggovmles",
            "routeTableType": 1,
            "subnetNum": 0,
            "routeTableCreateTime": "2015-11-06 11:33:52",
            "routeSet": [
                {
                    "destinationCidrBlock": "Local",
                    "nextType": 2,
                    "nextHub": "Local"
                }
            ]
        },
        {
            "vpcId": "gz_vpc_64",
            "unVpcId": "vpc-kd7d06of",
            "vpcName": "panpan-vpc1",
            "vpcCidrBlock": "10.0.0.0\/16",
            "routeTableName": "tttt",
            "routeTableId": "gz_rtb_8750",
            "unRouteTableId": "rtb-dy09eb46",
            "routeTableType": 0,
            "subnetNum": 0,
            "routeTableCreateTime": "2015-11-02 16:58:53",
            "routeSet": [
                {
                    "destinationCidrBlock": "Local",
                    "nextType": 2,
                    "nextHub": "Local"
                }
            ]
        },
        {
            "vpcId": "gz_vpc_265",
            "unVpcId": "vpc-ktom9wg5",
            "vpcName": "yunapitest",
            "vpcCidrBlock": "10.100.100.0\/24",
            "routeTableName": "default,
            "routeTableId": "gz_rtb_8747",
            "unRouteTableId": "rtb-fdyy7v1o",
            "routeTableType": 1,
            "subnetNum": 1,
            "routeTableCreateTime": "2015-10-30 16:10:49",
            "routeSet": [
                {
                    "destinationCidrBlock": "Local",
                    "nextType": 2,
                    "nextHub": "Local"
                }
            ]
        },
        {
            "vpcId": "gz_vpc_260",
            "unVpcId": "vpc-r4wc72kt",
            "vpcName": "oplogtest",
            "vpcCidrBlock": "10.100.180.0\/24",
            "routeTableName": "default,
            "routeTableId": "gz_rtb_8738",
            "unRouteTableId": "rtb-cfqwtvs4",
            "routeTableType": 1,
            "subnetNum": 1,
            "routeTableCreateTime": "2015-10-23 19:47:54",
            "routeSet": [
                {
                    "destinationCidrBlock": "Local",
                    "nextType": 2,
                    "nextHub": "Local"
                }
            ]
        },
        {
            "vpcId": "gz_vpc_180",
            "unVpcId": "vpc-cor5n2a5",
            "vpcName": "test",
            "vpcCidrBlock": "10.100.181.0\/24",
            "routeTableName": "default",
            "routeTableId": "gz_rtb_8730",
            "unRouteTableId": "rtb-hrjfw07c",
            "routeTableType": 1,
            "subnetNum": 1,
            "routeTableCreateTime": "2015-10-22 12:11:22",
            "routeSet": [
                {
                    "destinationCidrBlock": "Local",
                    "nextType": 2,
                    "nextHub": "Local"
                },
                {
                    "destinationCidrBlock": "10.0.0.0\/8",
                    "nextType": 3,
                    "nextHub": "4245"
                },
                {
                    "destinationCidrBlock": "10.100.2.0\/24",
                    "nextType": 3,
                    "nextHub": "4245"
                },
                {
                    "destinationCidrBlock": "172.0.0.0\/8",
                    "nextType": 3,
                    "nextHub": "4245"
                }
            ]
        },
        {
            "vpcId": "gz_vpc_248",
            "unVpcId": "vpc-ali73gtr",
            "vpcName": "pan-vpc180",
            "vpcCidrBlock": "10.100.180.0\/24",
            "routeTableName": "default,
            "routeTableId": "gz_rtb_8729",
            "unRouteTableId": "rtb-m5es14q4",
            "routeTableType": 1,
            "subnetNum": 1,
            "routeTableCreateTime": "2015-10-22 11:25:51",
            "routeSet": [
                {
                    "destinationCidrBlock": "Local",
                    "nextType": 2,
                    "nextHub": "Local"
                }
            ]
        },
        {
            "vpcId": "gz_vpc_231",
            "unVpcId": "vpc-erxok83l",
            "vpcName": "barry-uniqVpci",
            "vpcCidrBlock": "10.20.80.0\/24",
            "routeTableName": "apollolan121",
            "routeTableId": "gz_rtb_8724",
            "unRouteTableId": "rtb-5qaib2em",
            "routeTableType": 0,
            "subnetNum": 0,
            "routeTableCreateTime": "2015-10-19 19:50:38",
            "routeSet": [
                {
                    "destinationCidrBlock": "Local",
                    "nextType": 2,
                    "nextHub": "Local"
                }
            ]
        },
        {
            "vpcId": "gz_vpc_231",
            "unVpcId": "vpc-erxok83l",
            "vpcName": "barry-uniqVpci",
            "vpcCidrBlock": "10.20.80.0\/24",
            "routeTableName": "default,
            "routeTableId": "gz_rtb_8720",
            "unRouteTableId": "rtb-3jdtm2uk",
            "routeTableType": 1,
            "subnetNum": 1,
            "routeTableCreateTime": "2015-10-19 11:36:00",
            "routeSet": [
                {
                    "destinationCidrBlock": "Local",
                    "nextType": 2,
                    "nextHub": "Local"
                }
            ]
        },
        {
            "vpcId": "gz_vpc_174",
            "unVpcId": "vpc-gaep0rmx",
            "vpcName": "pan-vpc99",
            "vpcCidrBlock": "10.100.99.0\/24",
            "routeTableName": "default,
            "routeTableId": "gz_rtb_481",
            "unRouteTableId": "rtb-d1voj30m",
            "routeTableType": 1,
            "subnetNum": 1,
            "routeTableCreateTime": "2015-01-30 14:21:19",
            "routeSet": [
                {
                    "destinationCidrBlock": "Local",
                    "nextType": 2,
                    "nextHub": "Local"
                }
            ]
        }
    ]
}

```

