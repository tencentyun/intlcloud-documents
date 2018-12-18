## 1. API Description
This API (DomainCreate) is used to add a domain name.
API request domain name: **cns.api.qcloud.com**

## 2. Input Parameters
The following list of request parameters lists only the API request parameters. The common request parameters need to be added when making a call. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/377/4153). Here, the Action field of this API is DomainCreate.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| domain | yes | String | The domain name to be added (primary domain name without www, for example: qcloud.com) |
| projectId | No | Int | Project ID; if left blank, the "default project" is used |

## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code; 0 - success, other values - failure. |
| message | String | Module error description; related to the API. |
| data | Array | The data returned by the API. |

If the addition succeeds, a data field will be returned containing the domain name information.

Here, the domain field is the basic information returned after the addition succeeds:

| Parameter name | Type | Description |
|---------|---------|---------|
| id | String | Domain name ID |
| punycode | String | Domain name after encoded with punycode |
| domain | String | Domain name |

## 4. Examples
```
https://cns.api.qcloud.com/v2/index.php?
&<Common request parameter>
&Action=DomainCreate
&domain=qcloud.com
&projectId=0
```


Below is a response example:
```
{
	"code": 0,
	"message": "",
	"codeDesc": "Success",
	"data": {
		"domain": {
			"id": "55309561",
			"punycode": "qcloud.com",
			"domain": "qcloud.com"
		}
	}
}
```
