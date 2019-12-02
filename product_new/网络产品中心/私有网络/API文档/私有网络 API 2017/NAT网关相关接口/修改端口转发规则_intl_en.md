## 1. API Description
This API (ModifyDnaptRule) is used to modify port forwarding rules for a NAT gateway.
Domain name for API requests: `vpc.api.qcloud.com`

Before using this API, please go to <a href="https://intl.cloud.tencent.com/doc/product/215/1682" title="NAT Gateway Description">NAT Gateway Description</a> to learn about the features of NAT gateways.

## 2. Input Parameters
The following request parameter list only provides API request parameters. Common request parameters are required when the API is called. For more information, see the [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/229/6976) page. The Action field for this API is ModifyDnaptRule.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | Yes | String | VPC ID, for example: vpc-8e0ypm3z. |
| natId | Yes | String | NAT gateway ID, for example: nat-dqbak2vy. |
| oldProto | Yes | String | Original protocol, optional values: tcp and udp. |
| oldEip | Yes | String | Original external IP address, namely the associated elastic IP address. |
| oldEport | Yes | String | Original external port number. |
| proto | No | String | New protocol, optional values: tcp and udp. |
| eip | No | String | New external IP address, namely the associated elastic IP address. |
| eport | No | String | New external port number. |
| pip | No | String | New internal IP address. |
| pport | No | String | New internal port number. |
| description | No | String | New rule description. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful, other values: Failed. |
| message | string | Error message. |

## 4. Error Codes
The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| 29151 | The length of the description exceeded the limit. |
| 29152 | Rule conflict occurred because the elastic IP address already exists. |
| 29153 | The internal IP address has not been bound to any instance. |
| -3325 | The elastic IP address does not exist. |
| -3326 | The internal IP address is not within the VPC. |
| -3327 | Rule conflict occurred because the internal IP address already exists. |
| -3328 | The maximum number of port forwarding rules has been reached. |
| -3344 | The internal IP address is not within the CVM. |

## 5. Example
Input
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=ModifyDnaptRule
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
&vpcId=vpc-d8vg6rev
&natId=nat-k6npdayk
&oldProto=tcp
&oldEip=139.199.232.178
&oldEport=303
&proto=tcp
&eip=139.199.232.178
&eport=304
&pip=10.90.90.11
&pport=304
&description=test
</pre>
Output
```
{
	"code": "0",
	"message": ""
}
```
