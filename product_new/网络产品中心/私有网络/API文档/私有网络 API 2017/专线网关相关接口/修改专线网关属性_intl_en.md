## 1. API Description

This API (ModifyDirectConnectGateway) is used to modify the attributes of direct connect gateways.
Domain name for API requests: <font style="color:red">vpc.api.qcloud.com</font>

Currently, only changing the name in the attributes of a direct connect gateway is supported.

## 2. Input Parameters
The list below contains only the API request parameters. The common request parameters need to be added when a call is made. For more information, see the <a href="https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is ModifyDirectConnectGateway.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | Yes | String | VPC ID assigned by the system, for example: vpc-7t9nf3pu. |
| directConnectGatewayId | Yes | String | Direct connect gateway ID assigned by the system, for example: dcg-7t9nf3pu. |
| directConnectGatewayName | Yes | String | Direct connect gateway name, which must be a combination of 1-25 uppercase and lowercase letters, numbers, and underscores. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | String | Error message |
| taskId | Int | Task ID. You can query the execution result by using the taskId. For more information, see the API for Querying Task Execution Results. |

## 4. Error Codes
  The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.
 
| Error code | Description |
|---------|---------|
| InvalidDirectConnectGatewayName | Invalid direct connect gateway name. A valid name should be a combination of 1-60 uppercase and lowercase letters, numbers, and underscores. |
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC resource does not exist. In this case, verify whether the resource information that you entered is correct. |
| InvalidDirectConnectGateway.NotFound | Invalid direct connect gateway. This error code indicates that the direct connect gateway does not exist. In this case, verify whether the resource information that you entered is correct. |

## 5. Example
Input
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=ModifyDirectConnectGateway
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
&vpcId=vpc-dfgg190
&directConnectGatewayId=dcg-ddf14d
&directConnectGatewayName=Direct connect gateway 1
</pre>
Output
```
{
    "code":"0",
    "message":"",
    "taskId":16284
}
```

