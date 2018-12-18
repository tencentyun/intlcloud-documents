## 1. API Description
This API (RecordModify) is used to modify a resolution record.
API request domain name: **cns.api.qcloud.com**

## 2. Input Parameters
The following list of request parameters lists only the API request parameters. The common request parameters need to be added when making a call. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/377/4153). Here, the Action field of this API is RecordModify.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| domain | yes | String | The domain name to be operated (primary domain name without www, for example: qcloud.com) |
| recordId | Yes | Int | Resolution record ID, which can be viewed in the id field in the response of the RecordList API
| subDomain | Yes | String | Subdomain name, for example: www |
| recordType | Yes | String | Record type; values include "A", "CNAME", "MX", "TXT", "NS", "AAAA" and "SRV"
| recordLine | yes | String | Line name of the record, for example: "default" |
| value | yes | String | Record value, for example: IP:192.168.10.2, CNAME: cname.dnspod.com., MX: mail.dnspod.com.
| ttl | No | Int | TTL value; range: 1-604800; the minimum value varies for different domain name levels; 600 by default
| mx | No | Int | MX priority; range: 0-50; required when record type is MX

## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code; 0 - success, other values - failure. |
| message | String | Module error description; related to the API. |
| data | Array | The data returned by the API. |

If the modification succeeds, a data field will be returned containing the record information.

Here, the record field is the basic information returned after the modification succeeds:

| Parameter name | Type | Description |
|---------|---------|---------|
| id | String | Resolution record ID |
| name | String | Subdomain name |
| value | String | Record value |
| status | String | Resolution record status |
| weight | Int | Weight of the resolution record; null by default |

## 4. Examples
```
https://cns.api.qcloud.com/v2/index.php?
&<Common request parameter>
&Action=RecordModify
&domain=qcloud.com
&recordId=281628246
&subDomain=www
&recordType=CNAME
&recordLine= Default
&value=cloud.tencent.com
```

Below is a response example:
```
{
	"code": 0,
	"message": "",
	"codeDesc": "Success",
	"data": {
		"record": {
			"id": 282529938,
			"name": "yizeronew1487857638",
			"value": "112.112.21.21",
			"status": "enable",
			"weight": null
		}
	}
}
```
