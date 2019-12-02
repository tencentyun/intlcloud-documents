## 1. API Description

This API (DeleteVpc) is used to delete VPCs.
API request domain name: <font style="color:red">vpc.api.qcloud.com</font>

(1) Before deleting a VPC, make sure that there are no resources in it, such as CVMs, cloud databases, NoSQL databases, VPN gateways, direct connect gateways, load balancers, peering connections, and basic network devices linked with it.
(2) The deletion of VPCs is irreversible. Please proceed with caution.

## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href="https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is DeleteVpc.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | Yes | String | VPC ID assigned by the system. Both the vpcId before upgrade and the upgraded unVpcId are supported. |

 

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/377/8946" title="Common Error Codes">Common Error Codes</a>.|
| message | String | Module error message, which depends on the API. |

## 4. Error Codes
 The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. In this case, verify whether the resource information that you entered is correct. |
| InvalidVpc.CannotDelete | A VPC that contains resources cannot be deleted.

## 5. Sample

Input
<pre>

  https://vpc.api.qcloud.com/v2/index.php?Action=DeleteVpc
	&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
  &vpcId=vpc-2ari9m7h
</pre>

Output
```

{
    "code": 0,
    "message": ""
}

```

