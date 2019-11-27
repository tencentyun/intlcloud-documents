## 1. API Description

This API (DescribeNatGateway) is used to query NAT gateways.
Domain name for API requests: `vpc.api.qcloud.com`


## 2. Input Parameters
The list below contains only the API request parameters. The common request parameters need to be added when a call is made. For more information, see the <a href="https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is DescribeNatGateway.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| natId | No | String | NAT gateway unified ID, for example: nat-xx454. |
| natName | No | String | NAT gateway name, supports fuzzy query. |
| vpcId | No | String | VPC ID or unified ID (recommended), for example: vpc-dfdg42d. |
| offset | No | Int | Offset of the initial line. The default is 0. |
| limit | No | Int | Number of lines per page. The default is 20 and the maximum is 50. |
| orderField | No | String | Sorts by a field. Sorting is not implemented by default.<br>Supported field: natId. |
| orderDirection | No | String | Ascending order (asc) or descending order (desc). The default is desc. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | String | Error message. |
| totalCount | Int | Total number of queried NAT gateways. |
| data.n | Array | Queried NAT gateway information array. |

**"data" is composed as follows:**

| Parameter name | Type | Description |
|---------|---------|---------|
| data.n.natId | String | Unified ID of the NAT gateway, for example: nat-xx454. |
| data.n.unVpcId | String | Unified ID of the VPC, for example: vpc-xgfd55d. |
| data.n.natName | String | NAT gateway name. |
| data.n.state | Int | Status of the NAT gateway, 0: Running, 1: Unavailable, 2: Service suspended due to overdue payment. |
| data.n.maxConcurrent | Int | Maximum gateway concurrent connections, values: 1,000,000 (small), 3,000,000 (medium), and 10,000,000 (large). |
| data.n.bandwidth | Int | The maximum public network outbound bandwidth of the gateway (in Mbps). |
| data.n.eipCount | String | Number of EIPs, for example: nat-xx454. |
| data.n.eipSet | Array | Complete EIP information of the gateway, for example: [183.60.249.11]. |
| data.n.createTime | String | Creation time of the NAT gateway, for example: 2016-06-21 12:01:23. |
| data.n.productionStatus | Int | Production status of the NAT gateway. 0: Creating; 1: Created successfully; 2: Creation failed; 3: Changing; 4: Change failed; 5: Deleting; 6: Deletion failed. |

## 4. Error Codes
 The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC resource does not exist. In this case, verify whether the resource information that you entered is correct. You can query the VPC through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| InvalidNatGatewayId.NotFound | Invalid NAT gateway. This error code indicates that the NAT gateway resource does not exist. In this case, verify whether the resource information that you entered is correct. You can query the NAT gateway through the API <a href="https://intl.cloud.tencent.com/doc/api/245/%e6%9f%a5%e8%af%a2NAT%e7%bd%91%e5%85%b3?viewType=preview" title="DescribeNatGateway">DescribeNatGateway</a>. |

## 5. Example
Input
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=DescribeNatGateway
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
&vpcId=vpc-8e0ypm3z
</pre>
Output
```
{
    "code":"0",
    "message":"",
    "totalCount":1,
    "data": [
        {
            "appId": "1351000042",
            "vpcId": "vpc-8e0ypm3z",
            "vpcName": "alblack.bbb1",
            "natId": "nat-dhfpwhtm",
            "natName": "apollan",
            "maxConcurrent": 0,
            "eipCount": 1,
            "createTime": "2016-06-21 12:01:23",
            "state": 1,
            "bandwidth": 90000,
            "productionStatus": 1,
            "eipSet": [
                "183.60.249.11"
            ]
        }
     ]
}
```

