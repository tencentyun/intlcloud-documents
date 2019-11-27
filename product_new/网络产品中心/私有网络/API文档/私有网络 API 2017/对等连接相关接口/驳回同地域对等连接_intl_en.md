## 1. API Description

This API (RejectVpcPeeringConnection) is used to reject intra-region peering connections.
API request domain name: <font style="color:red">vpc.api.qcloud.com</font>
This API is used by the receiver to reject the request for intra-region peering connection from another account.

## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href=" https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is RejectVpcPeeringConnection.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| peeringConnectionId | Yes | String | ID of VPC peering connection, for example: pcx-8g675gr8. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | String | Error message. |

## 4. Error Codes
  The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.
	
| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC resource does not exist. In this case, verify whether the resource information that you entered is correct. |
| InvalidPeeringConnection.NotFound | Invalid peering connection. This error code indicates that the peering connection does not exist. In this case, verify whether the resource information that you entered is correct. |

## 5. Sample
Input
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=RejectVpcPeeringConnection
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
&peeringConnectionId=pcx-8g675gr8
</pre>
Output
```
{
    "code":"0",
    "message":""
}
```

