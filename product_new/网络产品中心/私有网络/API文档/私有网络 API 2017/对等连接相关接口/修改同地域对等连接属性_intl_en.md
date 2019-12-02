## 1. API Description

This API (ModifyVpcPeeringConnection) is used to modify the attributes of an intra-region peering connection.
Domain name for API requests: <font style="color:red">vpc.api.qcloud.com</font>

## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href="https://intl.cloud.tencent.com/document/product/215/2107/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is ModifyVpcPeeringConnection.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| peeringConnectionId | Yes | String | ID of the VPC peering connection, for example: pcx-krmzap90. |
| peeringConnectionName | Yes | String | Peering connection name, which is up to 60 characters. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | String | Error message. |

## 4. Error Codes
  The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidPeeringConnectionName | Invalid peering connection name. This name cannot exceed 60 characters. |
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC resource does not exist. In this case, verify whether the resource information that you entered is correct. |
| InvalidPeeringConnection.NotFound | Invalid peering connection. This error code indicates that the peering connection resource does not exist. In this case, verify whether the resource information that you entered is correct. |

## 5. Example
Input
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=ModifyVpcPeeringConnection
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
&peeringConnectionId=pcx-krmzap90
&peeringConnectionName=uuuuuuu
</pre>
Output
```
{
    "code":"0",
    "message":""
}
```

