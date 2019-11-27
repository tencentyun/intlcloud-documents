## API Description
This API is used to create cross-region peering connections.
Domain name: `vpc.api.qcloud.com`
API name: `CreateVpcPeeringConnectionEx`
- Cross-region peering connections are used to establish connectivity between VPCs in two different regions. The IP address ranges of both VPCs that need to be interconnected cannot overlap.
- Cross-account peering connections take effect only when the receiver accepts the request. Peering connections between VPCs in the same account take effect immediately.
- You can set a bandwidth for cross-region interconnection. For any changes made after the creation of the peering connection, contact customer service.
- For more information about the regions, bandwidth limits, and billing methods supported for cross-regional peering connections, see [About Peering Connection](https://intl.cloud.tencent.com/doc/product/215/1685).

## Request Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/229/6976) page. The Action field for this API is `CreateVpcPeeringConnectionEx`.

| Parameter | Required | Type | Description |
| ----- | ---- | ------ | ---------------------------------------- |
| vpcId | Yes | String | VPC ID, which can be the vpcId or unVpcId (recommended). </br>You can query this ID through the API [DescribeVpcEx API](http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8). |
| peerVpcId | Yes | String | VPC ID of the receiver, which can be the vpcId or unVpcId (recommended). </br>You can query this ID through the API [DescribeVpcEx API](http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8). |
| peerUin | Yes | String | The receiver's unique account ID on Tencent Cloud. You can ask the receiver to check this ID in the personal information area of the User Center. For more information, see the [Operation Guide](https://intl.cloud.tencent.com/document/product/215/5000#.E6.9F.A5.E7.9C.8B.E5.AF.B9.E7.AB.AF.E8.B4.A6.E5.8F.B7id21). |
| peeringConnectionName | Yes | String | Peering connection name, which cannot exceed 60 characters. |
| peerRegion | Yes | String | Receiver's region. For more information about the supported regions, see [About Regions](https://intl.cloud.tencent.com/document/product/215/4927#.E5.9C.B0.E5.9F.9F.EF.BC.88region.EF.BC.895). |
| bandwidth | Yes | String | Upper limit of bandwidth for the peering connection (in Mbps). There is no limit by default. </br>For more information about the limit, see [About Peering Connections](https://intl.cloud.tencent.com/document/product/215/5000#.E5.90.8C.E5.9C.B0.E5.9F.9F.E5.AF.B9.E7.AD.89.E8.BF.9E.E6.8E.A5-.E5.92.8C-.E7.A7.81.E6.9C.89.E7.BD.91.E7.BB.9C.E8.B7.A8.E5.9C.B0.E5.9F.9F.E5.AF.B9.E7.AD.89.E8.BF.9E.E6.8E.A5.EF.BC.88.E5.8D.B3.EF.BC.9A.E7.A7.81.E6.9C.89.E7.BD.91.E7.BB.9C.E8.B7.A8.E5.9C.B0.E5.9F.9F.E4.BA.92.E8.81.94.EF.BC.893). |
| type | No | Int | Interconnection type. The default is 1.</br>1: Peering connection between VPCs</br>2: Peering connection between a VPC and a BM network. |

## Response Parameters

| Parameter name | Type | Description |
| ------- | ------ | ---------------------------------------- |
| code | Int | Error code.</br>0: Successful</br>Other values: Failed. |
| message | String | Error message. |
| taskId | Int | Task ID. You can query the execution result by using taskId.</br>For more information, see the [API for Querying Task Execution Results](https://intl.cloud.tencent.com/doc/api/245/%e6%9f%a5%e8%af%a2%e4%bb%bb%e5%8a%a1%e6%89%a7%e8%a1%8c%e7%bb%93%e6%9e%9c%e6%8e%a5%e5%8f%a3). |


## Error Codes
The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
| ------------------------------ | ---------------------------------------- |
| InvalidPeeringConnectionName | Invalid peering connection name. </br>This name cannot exceed 60 characters. |
| PeeringConnectionVpcConflict | A conflict occured between VPC IP ranges in peering connection. |
| PeeringConnectionLimitExceeded | The limit of requested peering connection resources for the specific region has been reached. To request more resources, contact customer service. </br>For more information about VPC resource limits, see [VPC Use Limits](https://intl.cloud.tencent.com/doc/product/215/537). |
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. </br>In this case, verify whether the resource information that you entered is correct. |


## Sample Code
**Request example**
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=CreateVpcPeeringConnectionEx
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
&vpcId=gz_vpc_226
&peerVpcId=gz_vpc_89
&peerUin=2407912486
&peeringConnectionName=tses
&peerRegion=gz
&bandwidth=20
</pre>

**Response example**
```
{
    "code":"0",
    "message":"",
    "taskId":112245
}
```
