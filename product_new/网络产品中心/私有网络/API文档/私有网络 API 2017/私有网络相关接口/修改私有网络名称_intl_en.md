## 1. API Description

This API (ModifyVpcAttribute) is used to modify VPCs.
API request domain name: <font style="color:red">vpc.api.qcloud.com</font>

Currently, only changing the name in VPC attributes is supported.

 

## 2. Input Parameters
 Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href=" https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is ModifyVpcAttribute.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | Yes | String | VPC ID assigned by the system. Both the vpcId before upgrade and the upgraded unVpcId are supported. |
| vpcName | Yes | String | VPC name, which is up to 60 characters. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/377/8946">Common Error Codes</a> on the “Error Codes” page. |
| message | String | Module error message description depending on API |

## 4. Error Codes
 Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href="https://intl.cloud.tencent.com/document/product/215/2107/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is ModifyVpcPeeringConnectionEx.

| Error code | Description |
|---------|---------|
| InvalidVpcName | Invalid VPC name, which is up to 60 characters. |
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC resource does not exist. In this case, verify whether the resource information that you entered is correct. |

## 5. Sample

Input
<pre>

  https://vpc.api.qcloud.com/v2/index.php?Action=ModifyVpcAttribute
  &<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
  &vpcId=vpc-2ari9m7h
  &vpcName=vpcName1
</pre>

Output
```

{
    "code": 0,
    "message": ""
}

```

