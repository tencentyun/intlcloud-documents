## 1. API Description

This API (DescribeVpcClassicLink) is used to query the classiclink between a VPC and a basic network CVM.
API request domain name: <font style="color:red">vpc.api.qcloud.com</font>




## 2. Input Parameters
 Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href="https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is DescribeVpcClassicLink.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | No | String | VPC ID assigned by the system, for example: vpc-dgd5454. Both the vpcId before upgrade and the upgraded unVpcId are supported. |
| classicLinkId | No | String | Classiclink ID between a VPC and a basic network CVM, for example: vcx-opgnzgo9. |
| lanIp | No | String | CVM private IP address. |
| offset | No | Int | Offset of the initial line. The default is 0. |
| limit | No | Int | Number of lines per page. The default is 20 and the maximum is 50. |
| orderField | No | String | Sorts by a field. Sorting is not implemented by default. Supported field: createTime. |
| orderDirection | No | String | Ascending order (asc) or descending order (desc). The default is desc. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/377/8946">Common Error Codes</a>. |
| message | String | Module error message, which depends on the API. |
| totalCount | Int | Total number of returned Classiclinks. |
| data.n | Array | Returned details. |
| data.n.lanIp | String | Private IP address of the CVM. |
| data.n.unVpcId | String | Unified ID assigned by the system, for example: vpc-2ari9m7h. It is derived from vpcId. The system supports both IDs for compatibility, but the unified ID is recommended. |
| data.n.vpcId | String | VPC ID assigned by the system, for example: gz_vpc_15. |
| data.n.classicLinkId | String | Classiclink ID assigned by the system, for example: vcx-opgnzgo9. |
| data.n.createTime | String | Creation time, for example: 2016-01-21 14:59:37. |
| data.n.instanceId | String | Unified ID of a CVM, for example: ins-xxd51df. |
| data.n.instanceName | String | CVM name |

## 4. Error Codes
 The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidLanIp.NotFound | The CVM does not exist. In this case, verify that the lanIp that you entered is correct. To query the CVMs under the VPC, see <a href="https://intl.cloud.tencent.com/doc/api/229/831" title="View the List of CVM Instances">View the List of CVM Instances</a>. |
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC resource does not exist. In this case, verify whether the resource information that you entered is correct. |

## 5. Sample

Input
<pre>

  https://vpc.api.qcloud.com/v2/index.php?Action=DescribeVpcClassicLink
	&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
	&vpcId=vpc-2ari9m7h
	&classicLinkId=vcx-df454d
</pre>

Output
```

{
    "code": 0,
    "message": "",
		"totalCount":"1",
		"data":[
        {
            "lanIp":"10.232.18.145",
            "uniqVpcId":"vpc-8e0ypm3z",
            "vpcId":"gz_vpc_245",
            "classicLinkId":"vcx-opgnzgo9",
            "createTime":"2016-01-21 14:59:37",
            "instanceId":"ins-d1o128ru",
            "instanceName":"Not named"
        }
    ]
}

```

