## 1. API Description

This API (AttachClassicLinkVpc) is used to create a classiclink.
API request domain name: <font style="color:red">vpc.api.qcloud.com</font>

(1) The VPC and basic network devices must be in the same region.
(2) For the differences between VPCs and basic networks, see <a href="https://intl.cloud.tencent.com/doc/product/215/535#2.-.E7.A7.81.E6.9C.89.E7.BD.91.E7.BB.9C.E4.B8.8E.E5.9F.BA.E7.A1.80.E7.BD.91.E7.BB.9C" title="VPC and Basic Network">VPC Product Documentation - VPCs and Basic Networks.</a>

 

## 2. Input Parameters
 Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href="https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is AttachClassicLinkVpc.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | Yes | String | VPC ID assigned by the system, for example: vpc-dgd44d. Both the vpcId before upgrade and the upgraded unVpcId are supported. |
| instanceIds.n | Yes | Array | ID of the basic network CVM, for example: instanceIds.0=ins-5d8a23rs. You can query this ID through the cloud API <a href="https://intl.cloud.tencent.com/doc/api/229/831" title="View the List of Instances">DescribeInstances</a>. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/377/8946">Common Error Codes</a>. |
| message | String | Module error message, which depends on the API. |
| taskId | Int | Task ID. You can query the execution result by using taskId. For more information, see the <a href="https://intl.cloud.tencent.com/doc/api/245/%e6%9f%a5%e8%af%a2%e4%bb%bb%e5%8a%a1%e6%89%a7%e8%a1%8c%e7%bb%93%e6%9e%9c%e6%8e%a5%e5%8f%a3">API for Querying Task Execution Results</a>.|

## 4. Error Codes
 The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidInstance.NotFound | The CVM does not exist. In this case, verify that the instanceId that you entered is correct. To query the CVMs under the VPC, see <a href="https://intl.cloud.tencent.com/doc/api/229/831" title="View the List of CVM Instances">View the List of CVM Instances</a>. |
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. In this case, verify whether the resource information that you entered is correct. |
| InstanceLimitExceeded | The number of basic network devices interconnected with a VPC in the specified region exceeds the limit. To bind more basic network devices, contact customer service. For more information about VPC resource limits, see <a href="https://intl.cloud.tencent.com/doc/product/215/537" title="VPC Use Limits">VPC Use Limits</a>. |
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. In this case, verify whether the resource information that you entered is correct. |
| InstanceAlreadyLinked | The basic network CVM has been bound to another VPC, and one basic network CVM can only be interconnected with one VPC. For more information about VPC resource limits, see <a href="https://intl.cloud.tencent.com/doc/product/215/537" title="VPC Use Limits">VPC Use Limits</a>. |

## 5. Sample

Input
<pre>

  https://vpc.api.qcloud.com/v2/index.php?Action=AttachClassicLinkVpc
	&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
	&vpcId=vpc-2ari9m7h
	&instanceIds.0=ins-df454d
</pre>

Output
```

{
    "code": 0,
    "message": "",
		"taskId":135254
}

```

