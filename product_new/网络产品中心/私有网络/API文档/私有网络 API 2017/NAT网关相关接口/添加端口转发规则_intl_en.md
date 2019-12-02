## 1. API Description
This API (AddDnaptRule) is used to add NAT gateway port forwarding rules.
Domain name for API requests: `vpc.api.qcloud.com`

Before using this API, go to <a href="https://intl.cloud.tencent.com/doc/product/215/1682" title="About NAT Gateway" >About NAT Gateway</a> to learn about the features of NAT gateways.

## 2. Input Parameters
The following request parameter list only provides API request parameters. Common request parameters are required when the API is called. For more information, see the [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/229/6976) page. The Action field for this API is AddDnaptRule.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | Yes | String | VPC ID, for example: vpc-8e0ypm3z. |
| natId | Yes | String | NAT gateway ID, for example: nat-dqbak2vy. |
| proto | Yes | String | Protocol, available values: tcp and udp. |
| eip | Yes | String | External IP address, namely the associated EI.P |
| eport | Yes | String | External port number. |
| pip | Yes | String | Internal IP address. |
| pport | Yes | String | Internal port number. |
| description | No | String | Rule description. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | string | Error message. |

## 4. Error Codes
The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| 29151 | The length of rule description exceeded the limit. |
| 29152 | Rules conflict. The EIP already exists. |
| 29153 | The internal IP address has not been bound to any instance. |
| -3325 | The EIP does not exist. |
| -3326 | The internal IP address is not within the VPC. |
| -3327 | Rules conflict. The internal IP address already exists. |
| -3328 | The maximum number of port forwarding rules has been reached. |
| -3344 | The internal IP address is not within the CVM. |

## 5. Example
Input
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=AddDnaptRule
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
&vpcId=vpc-d8vg6rev
&natId=nat-k6npdayk
&proto=tcp
&eip=139.199.232.178
&eport=303
&pip=10.90.90.10
&pport=303
&description=aaa
</pre>
Output
```
{
	"code": "0",
	"message": ""
}
```
