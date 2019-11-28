## 1. API Description
This API (DeleteDnaptRule) is used to delete NAT gateway port forwarding rules.
Domain name for API requests: `vpc.api.qcloud.com`

Before using this API, please go to <a href="https://intl.cloud.tencent.com/doc/product/215/1682" title="About Gateway" >About NAT Gateway</a> to learn about the features of NAT gateways.

## 2. Input Parameters
The following request parameter list only provides API request parameters. Common request parameters are required when the API is called. For more information, see the [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/229/6976) page. The Action field for this API is DeleteDnaptRule.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | Yes | String | VPC ID, for example: vpc-8e0ypm3z. |
| natId | Yes | String | NAT gateway ID, for example: nat-dqbak2vy. |
| dnatList | Yes | Array | List of port forwarding rules to be deleted. |
| dnatList.N.proto | Yes | String | Protocol; available values: tcp and udp. |
| dnatList.N.eip | Yes | String | External IP address, namely the associated EIP. |
| dnatList.N.eport | Yes | String | External port number. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | string | Error message. |

## 4. Error Codes
This API has no business logic error codes. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

## 5. Example
Input
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=DeleteDnaptRule
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
&vpcId=vpc-d8vg6rev
&natId=nat-k6npdayk
&dnatList.0.proto=tcp
&dnatList.0.eip=139.199.232.178
&dnatList.0.eport=303
</pre>
Output
```
{
    "code":"0",
    "message":""
}
```
