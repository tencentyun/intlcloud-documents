## 1. API Description

This API (DeleteRouteTable) is used to delete route tables.
Domain name for API requests: <font style="color:red">vpc.api.qcloud.com</font> 


## 2. Input Parameters

The following request parameter list only provides API request parameters. Common request parameters are required when the API is called. For more information, see the <a href="https://intl.cloud.tencent.com/document/product/215/1372/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is DeleteRouteTable.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | Yes | String | ID of the VPC to which the subnet belongs, which can be the vpcId or unVpcId (recommended), for example vpc-rqndayhs. You can query this ID through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| routeTableId | Yes | String | The route table ID assigned by the system, which can be routeTableId or unRouteTableId (recommended), for example rtb-rqndayhs. You can query this ID through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E8%B7%AF%E7%94%B1%E8%A1%A8" title="DescribeRouteTable">DescribeRouteTable</a>. |

 

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | String | Error message. |

## 4. Error Codes
  The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. In this case, verify whether the resource information that you entered is correct. You can query the VPC through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| InvalidRouteTableId.NotFound | Invalid route table. This error code indicates that the route table ID does not exist. In this case, verify whether the resource information that you entered is correct. You can query this ID through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E8%B7%AF%E7%94%B1%E8%A1%A8" title="DescribeRouteTable">DescribeRouteTable</a>. |

## 5. Example

Input
<pre>
  https://vpc.api.qcloud.com/v2/index.php?Action=DeleteRouteTable
  &<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
  &vpcId=vpc-amhnnao5
  &routeTableId=rtb-4ahe1qy2
</pre>

Output
```
{
    "code": 0,
    "message": ""
}

```

