## 1. API Description

This API (EnableVpcPeeringConnectionEx) is used to enable expired cross-region peering connections.
Domain name for API requests: <font style="color:red">vpc.api.qcloud.com</font>

If the receiver does not accept the request for a cross-account peering connection within seven days after the request is initiated, the peering connection expires. Upon expiration, the receiver will not be able to perform any action on the peering connection. The initiator can use this API to enable the peering connection and notify the peer to process the connection.

## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href="https://intl.cloud.tencent.com/document/product/215/2107/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is EnableVpcPeeringConnectionEx.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| peeringConnectionId | Yes | String | ID of the VPC peering connection, for example: pcx-6gw5wvmk. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | int | Error code. 0: Successful; other values: Failed. |
| message | string | Error message |
| taskId | int | Task ID. You can query the execution result by using taskId. For more information, see the <a href="https://intl.cloud.tencent.com/doc/api/245/%e6%9f%a5%e8%af%a2%e4%bb%bb%e5%8a%a1%e6%89%a7%e8%a1%8c%e7%bb%93%e6%9e%9c%e6%8e%a5%e5%8f%a3">API for Querying Task Execution Results</a>. |

## 4. Error Codes
  The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.
	
| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC does not exist. In this case, verify whether the resource information that you entered is correct. |
| InvalidPeeringConnection.NotFound | Invalid peering connection. This error code indicates that the peering connection does not exist. In this case, verify whether the resource information that you entered is correct. |

## 5. Example
Input
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=EnableVpcPeeringConnectionEx
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
&peeringConnectionId=pcx-6gw5wvmk
</pre>
Output
```
{
    "code":"0",
    "message":"",
    "taskId":1584
}
```

