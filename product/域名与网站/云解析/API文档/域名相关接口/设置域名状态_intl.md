## 1. API Description
This API (SetDomainStatus) is used to set the status of the domain name, including "disabled" and "enabled".
API request domain name: **cns.api.qcloud.com**

## 2. Input Parameters
The following list of request parameters lists only the API request parameters. The common request parameters need to be added when making a call. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/377/4153). Here, the Action field of this API is SetDomainStatus.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| domain | yes | String | The domain name to be operated (primary domain name without www, for example: qcloud.com) |
| status | yes | String | Values include 'disable' (for disabling) and 'enable' (for enabling) |

## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code; 0 - success, other values - failure. |
| message | String | Module error description; related to the API. |


## 4. Examples
```
https://cns.api.qcloud.com/v2/index.php?
&<Common request parameter>
&Action=SetDomainStatus
&domain=qcloud.com
&status=enable
```


Below is a response example:
```
{
	"code": 0,
	"message": "",
	"codeDesc": "Success"
}
```
