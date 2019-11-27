## 1. API Description
This API (CreateVpcPeeringConnection) is used to create intra-region peering connections.
Domain name for API requests: <font style="color:red">vpc.api.qcloud.com</font>

(1) Regional peering connection is used to establish connectivity between VPCs within the same region. The segments of both VPCs that need to interconnected cannot overlap. For more information, see <a href="https://intl.cloud.tencent.com/doc/product/215/1685" title="Peering Connections">About Peering Connection</a>.
(2) Cross-account peering connections take effect only when the receiver accepts the request. The connections within the same account take effect immediately.
(3) There is no limit on the traffic of intra-region peering connections.
(4) Intra-region peering connections are available for free.

## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API.For more information, see the <a href=" https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is CreateVpcPeeringConnection.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | Yes | String | VPC ID, which can be the vpcId or unVpcId (recommended). You can query this ID through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| peerVpcId | Yes | String | VPC ID of the receiver, which can be the vpcId or unVpcId (recommended). You can query this ID through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| peerUin | Yes | String | Receiver's uin. |
| peeringConnectionName | Yes | String | Peering connection name, which cannot exceed 60 characters. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | String | Error message. |
| peeringConnectionId | String | Peering connection ID assigned by the system, for example: pcx-6gw5wvmk. |

## 4. Error Codes
 The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidPeeringConnectionName | Invalid peering connection name. This name cannot exceed 60 characters. |
| PeeringConnectionVpcConflict | A conflict occured between VPC segments in peering connection. |
| PeeringConnectionLimitExceeded | The limit of requested peering connection resources for the specific region has been reached. To request more resources, contact customer service. For more information about VPC resource limits, see <a href="https://intl.cloud.tencent.com/doc/product/215/537" title="VPC Use Limits">VPC Use Limits</a>. |
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. In this case, verify whether the resource information that you entered is correct. |

## 5. Example
Input
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=CreateVpcPeeringConnection
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
&vpcId=gz_vpc_226
&peerVpcId=gz_vpc_89
&peerUin=2407912486
&peeringConnectionName=tses
</pre>
Output
```
{
    "code":"0",
    "message":"",
    "peeringConnectionId":"pcx-6gw5wvmk"
}
```

