## 1. API Description 
This API (DescribeVpcLimit) is used to query the use limits of VPCs.

Domain name: `vpc.api.qcloud.com`

API name: `DescribeVpcLimit`

## 2. Request Parameters
| Parameter | Required | Type | Description |
| -------- | ------ | ------ | ------- |
| type.n | Yes | String | VPC feature type. |

**Feature type**

| Feature type | Description |
| -------- | ----------------------- |
| 0 | Number of VPCs that can be created by each developer. |
| 1 | Number of subnets that can be created for each VPC. |
| 2 | Number of route tables that can be created for each VPC. |
| 3 | Number of policies that can be added for each route table. |
| 4 | Number of VPN gateways that can be created for each VPC. |
| 5 | Number of peer gateways that can be created by each developer. |
| 7 | Number of VPN tunnels that can be created for each peer gateway. |
| 8 | Number of tunnels that can be created for each VPNGW. |
| 15 | Number of network ACLs that can be created for each VPC. |
| 17 | Number of inbound rules that can be added for each network ACL. |
| 18 | Number of outbound rules that can be added for each network ACL. |
| 20 | Number of valid peering connections that can be created for each VPC. |
| 22 | Number of Classiclinks (between basic network CVMs and VPCs) that can be created for each VPC. |
| 32 | Number of SNATs that can be created for each direct connect gateway. |
| 34 | Number of DNATs that can be created for each direct connect gateway. |
| 36 | Number of DNAPTs that can be created for each direct connect gateway. |
| 38 | Number of SNAPTs that can be created for each direct connect gateway. |
| 44 | Address pool size that can be set for each SSLVPN. |
| 51 | Number of SSLVPNs that can be created for each VPC. |
| 55 | Number of NATs that can be created for each VPC. |
| 56 | Number of public IP addresses that can be purchased for each NAT. |
| 57 | Number of ENIs that can be created for each VPC. |

## 3. Response Parameters
| Parameter | Type | Description |
| -------- | ------ | --------------- |
| code | Int | Error code</br>0: Successful</br>Other values: Failed. |
| message | String | Error message. |
| data | Array | Returned array. |

**data is composed as follows:**

| Parameter | Type | Description |
| -------- | ------ | --------------- |
| data.limit | Array | Limit information. |

## 4. Code Example 
**Request example**
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=DescribeVpcLimit
&type.0=1
&type.1=2
&<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>
</pre>
**Response example**
```
{
    "code": 0,
    "message": "",
    "data": {
        "limit": {
            "1": 10,
            "2": 10
        }
    }
}
```
