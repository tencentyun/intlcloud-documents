## 1. API Description

This API (DeleteVpcPeeringConnection) is used to delete intra-region peering connections.
Domain name for API requests: <font style="color:red">vpc.api.qcloud.com</font>

(1) Either of the peers can delete the peering connection at any time. The peering connection is invalid upon deletion.
(2) When the peering connection is deleted, the routing entry containing this connection in the route table will also be deleted.

## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href=" https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is DeleteVpcPeeringConnection.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| peeringConnectionId | Yes | String | ID of the VPC peering connection, for example: pcx-0jtgah4s. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | String | Error message. |

## 4. Error Codes
  The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. In this case, verify whether the resource information that you entered is correct. |
| InvalidPeeringConnection.NotFound | Invalid peering connection. This error code indicates that the peering connection does not exist. In this case, verify whether the resource information that you entered is correct. |

## 5. Example
Input
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=DeleteVpcPeeringConnection
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
&peeringConnectionId=pcx-0jtgah4s
</pre>

Output
```
{
    "code":"0",
    "message":""
}
```

