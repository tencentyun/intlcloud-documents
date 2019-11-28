## 1. API Description

This API (DetachClassicLinkVpc) is used to delete the classiclink between a VPC and a basic network CVM.
API request domain name: <font style="color:red">vpc.api.qcloud.com</font>

 

## 2. Input Parameters
 Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href="https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is DetachClassicLinkVpc.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | Yes | String | VPC ID assigned by the system. Both the vpcId before upgrade and the upgraded unVpcId are supported. |
| instanceIds.n | Yes | Array | ID of basic network CVM, for example: instanceIds.0=ins-df221dd. You can query this ID through the cloud API <a href="https://intl.cloud.tencent.com/doc/api/229/831" title="View the List of Instances">DescribeInstances</a>. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/377/8946">Common Error Codes</a>. |
| message | String | Module error message, which depends on the API. |
| taskId | Int | Task ID. You can query the execution result by using taskId. For more information, see the <a href="https://intl.cloud.tencent.com/doc/api/245/%e6%9f%a5%e8%af%a2%e4%bb%bb%e5%8a%a1%e6%89%a7%e8%a1%8c%e7%bb%93%e6%9e%9c%e6%8e%a5%e5%8f%a3">API for Querying Task Execution Results</a>. |

## 4. Error Codes
 The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidInstance.NotFound | The CVM does not exist. In this case, verify whether the instanceId that you entered is correct. To query the CVMs under the VPC, see <a href="https://intl.cloud.tencent.com/doc/api/229/831" title="View the List of CVM Instances">View the List of CVM Instances</a>. |
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. In this case, verify whether the resource information that you entered is correct. |

## 5. Sample

Input
<pre>

  https://vpc.api.qcloud.com/v2/index.php?Action=DetachClassicLinkVpc
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

