## 1. API Description

This API (DescribeVpcEx) is used to query the list of VPCs.
API request domain name: <font style="color:red">vpc.api.qcloud.com</font>

When no parameter is input for this API, the information of the first 20 VPCs in default order is returned.

 

## 2. Input Parameters
 Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href="https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is DescribeVpcEx.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | No | String | VPC ID assigned by the system. Both the the vpcId before upgrade and the upgraded unVpcId are supported. |
| vpnName | No | String | VPC name, supports fuzzy search. |
| offset | No | Int | Offset of the initial line. The default is 0. |
| limit | No | Int | Number of lines per page. The default is 20. |
| orderField | No | String | Sorts by a field. createTime and vpcName are supported. The default is createTime. |
| orderDirection | No | String | Ascending order (asc) or descending order (desc). The default is desc. |

 

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/377/8946">Common Error Codes</a>. |
| message | String | Module error message, which depends on the API. |
| totalCount | Int | Total number of the developer's VPCs. |
| data.n | Array | VPC information array. |
| data.n.vpcId | String | vpcId assigned by the system, for example: gz_vpc_266. |
| data.n.unVpcId | String | New vpcID assigned by the system, for example: vpc-5gu2jxf4. This ID is derived from the VPC ID. The new vpcId is recommended. |
| data.n.vpcName | String | VPC name. |
| data.n.cidrBlock | String | VPC IP range, for example: 192.168.0.1/24. |
| data.n.subnetNum | Int | Number of subnets under the VPC. |
| data.n.routeTableNum | Int | Number of route tables under the VPC. |
| data.n.vpnGwNum | Int | Number of VPN gateways under the VPC. |
| data.n.vpcPeerNum | Int | Number of peering connections under the VPC. |
| data.n.vpcDeviceNum | Int | Number of CVMs under the VPC. |
| data.n.classicLinkNum | Int | Number of basic network devices that are interconnected with the VPC. |
| data.n.vpgNum | Int | Number of direct connect gateways under the VPC. |
| data.n.natNum | Int | Number of NAT gateways under the VPC. |
| data.n.createTime | String | Creation time of the VPC. |
| data.n.isDefault | Bool | Whether the current VPC is the default VPC. |

## 4. Error Codes
 The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC resource does not exist. In this case, verify whether the resource information that you entered is correct. |

## 5. Sample

Input
<pre>
  https://vpc.api.qcloud.com/v2/index.php?Action=DescribeVpcEx
	&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
	&vpcId=vpc-2ari9m7h
	&offset=0
	&limit=1
	&orderDirection=desc
</pre>

Output
```

{
    "code": 0,
    "message": "",
		"totalCount":10,
		"data":[
        {
            "vpcId":"gz_vpc_245",
            "unVpcId":"vpc-8e0ypm3z",
            "vpcName":"alblack.bbb",
            "cidrBlock":"10.0.0.0/24",
            "subnetNum":0,
            "routeTableNum":5,
            "vpnGwNum":3,
            "vpcPeerNum":5,
            "vpcDeviceNum":0,
            "classicLinkNum":1,
            "vpgNum":0,
            "natNum":0,
            "createTime":"2015-08-24 15:05:16"
        }
   ]
}

```

