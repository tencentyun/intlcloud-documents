## 1. API Description
This API (RecordDelete) is used to delete the resolution record.
API request domain name: **cns.api.qcloud.com**

## 2. Input Parameters
The following list of request parameters lists only the API request parameters. The common request parameters need to be added when making a call. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/377/4153). Here, the Action field of this API is RecordDelete.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| domain | yes | String | Domain name where the resolution record resides |
| recordId | Yes | Int | Resolution record ID |


## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code; 0 - success, other values - failure. |
| message | String | Module error description; related to the API. |


## 4. Examples
```
https://cns.api.qcloud.com/v2/index.php?
&<Common request parameter>
&Action=RecordDelete
&domain=qcloud.com
&recordId=371266
```


Below is a response example:
```
{
	"code": 0,
	"message": "",
	"codeDesc": "Success"
}
```
