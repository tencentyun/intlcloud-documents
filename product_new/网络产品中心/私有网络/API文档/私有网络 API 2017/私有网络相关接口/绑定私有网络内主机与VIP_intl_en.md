## 1. API Description

This API (AssociateVip) is used to bind VPC CVMs with a VIP, that is, to bind a preassigned private VIP to the specified CVMs to produce the master and slave servers.

<font style="color:red">We do not recommend using this API because its functions can be replaced by ENIs.</font>

For more information about the methods for calling the new API and relevant use cases, see [Build Highly Available Master/Slave Clusters in VPCs with keepalived >>](https://intl.cloud.tencent.com/document/product/215/20186).

API request domain name: <font style="color:red">vpc.api.qcloud.com</font>

(1) Contact online customer service to apply for a VIP.
(2) The CVMs must be in a VPC.

 

## 2. Input Parameters
 Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href=" https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is AssociateVip.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | Yes | String | VPC ID assigned by the system, for example: vpc-2ari9m7h. Both the vpcId before upgrade and the upgraded unVpcId are supported. |
| vipId | Yes | Int | VIP ID, for example: 12. You need to contact the online customer service to apply for a VIP ID. |
| lanIp | Yes | String | Private IP address of the CVM, for example: 10.0.0.1. For more information about querying CVM IP addresses, see <a href="https://intl.cloud.tencent.com/doc/api/229/%E6%9F%A5%E7%9C%8B%E5%AE%9E%E4%BE%8B%E5%88%97%E8%A1%A8" title="View the List of Instances">View the List of Instances</a>. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/377/8946">Common Error Codes</a>. |
| message | String | Module error message, which depends on the API. |

## 4. Error Codes
 The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVipId.NotFound | The vipId does not exist. This error code indicates that the VIP needs to be assigned manually. If you forget your vipId or you are trying to bind for the first time, contact the online customer service to retrieve your vipId or apply for a new one. |
| InvalidLanIp.NotFound | The CVM does not exist. In this case, verify that the lanIp that you entered is correct. To query the CVMs under the VPC, see <a href="https://intl.cloud.tencent.com/doc/api/229/831" title="View the List of CVM Instances">View the List of CVM Instances</a>. |
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC resource does not exist. In this case, verify whether the resource information that you entered is correct. |

## 5. Sample

Input
<pre>

  https://vpc.api.qcloud.com/v2/index.php?Action=AssociateVip
	&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
  &vpcId=vpc-2ari9m7h
	&vipId=1
	&lanIp=10.0.0.2
</pre>

Output
```

{
    "code": 0,
    "message": ""
}

```

