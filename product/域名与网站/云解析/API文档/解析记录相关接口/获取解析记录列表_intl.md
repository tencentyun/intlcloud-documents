## 1. API Description
This API (RecordList) is used to obtain the resolution record of the domain name.
API request domain name: **cns.api.qcloud.com**

## 2. Input Parameters
The following list of request parameters lists only the API request parameters. The common request parameters need to be added when making a call. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/377/4153). Here, the Action field of this API is RecordList.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| domain | yes | String | The domain name to be operated (primary domain name without www, for example: qcloud.com) |
| offset | no | Int | Offset, 0 by default. For more information on the offset, see the relevant section in the API overview. |
| length | no | Int | Number of returns, 20 by default, up to 100. For more information on the limit, see the relevant section in the API overview. |
| subDomain | No | String | (Filter) filter by subdomain name |
| recordType | No | String | (Filter) filter by record type
| qProjectId | No | Int | (Filter) filter by project ID |

## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code; 0 - success, other values - failure. |
| message | String | Module error description; related to the API. |
| data | Array | The data returned by the API. |

The data field contains the information of the domain name and the number and details of resolution records.

"domain" is the domain name information, including:

| Parameter name | Type | Description |
|---------|---------|---------|
| id | String | Domain name ID |
| name | String | Domain name |
| punycode | String | Domain name after encoded with punycode |
| grade | String | Domain name level |
| owner | String | Domain name owner's email address |
| ext_status | String | Status information for domain name extension; "notexist", "dnserror" and "" represent "domain name not registered", "incorrect DNS settings" and "normal", respectively |
| ttl | Int | Default TTL value for the resolution records of the domain name |
| min_ttl | Int | Minimum TTL allowed by the current domain name |
| dnspod_ns | Array | NS address that should be set for the domain name |
| status | String | Domain name status; "enable", "pause", "spam" and "lock" represent "normal", "resolution paused", "blocked" and "locked", respectively |
| q_project_id | Int | ID of the project where the domain name is located |


"info" is the number of resolution records of the domain name, including:

| Parameter name | Type | Description |
|---------|---------|---------|
| sub_domains | String | Total number of resolution records |
| record_total | String | The actually returned number of records after filtered |

"records" contains detailed information for each resolution record, including:

| Parameter name | Type | Description |
|---------|---------|---------|
| id | Int | Resolution record ID
| ttl | Int | Record's TTL value |
| value | String | Record's value |
| enabled | Int | Record's running state, 1 - enabled, 0 - disabled |
| updated_on | String | Resolution record's last modified time |
| q_project_id | Int | ID of the project to which the resolution record belongs |
| name | String | Subdomain name |
| line | String | Line name of the resolution record |
| line_id | String | Line number of the resolution record |
| type | String | Resolution record type |
| remark | String | Resolution record remark |
| mx | Int | Priority of the MX record; 0 for non-MX records |


## 4. Examples
```
https://cns.api.qcloud.com/v2/index.php?
&<Common request parameter>
&Action=RecordList
&offset=0
&length=20
&domain=qq.com
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
			"name": "yizeroapitest.com",
			"punycode": "yizeroapitest.com",
			"grade": "DP_Free",
			"owner": "909619400@qq.com",
			"ext_status": "dnserror",
			"ttl": 600,
			"min_ttl": 600,
			"dnspod_ns": ["f1g1ns1.dnspod.net", "f1g1ns2.dnspod.net"],
			"status": "enable",
			"q_project_id": 0
		},
		"info": {
			"sub_domains": "4",
			"record_total": "4"
		},
		"records": [
            {
				"id": 281628246,
				"ttl": 86400,
				"value": "f1g1ns1.dnspod.net.",
				"enabled": 1,
				"status": "enabled",
				"updated_on": "2017-02-20 10:15:47",
				"q_project_id": 0,
				"name": "@",
				"line": "\u9ed8\u8ba4",
				"line_id": "0",
				"type": "NS",
				"remark": "",
				"mx": 0,
				"hold": "hold"
			},
            {
				"id": 281628247,
				"ttl": 86400,
				"value": "f1g1ns2.dnspod.net.",
				"enabled": 1,
				"status": "enabled",
				"updated_on": "2017-02-20 10:15:47",
				"q_project_id": 0,
				"name": "@",
				"line": "\u9ed8\u8ba4",
				"line_id": "0",
				"type": "NS",
				"remark": "",
				"mx": 0,
				"hold": "hold"
			},
            {
				"id": 281817767,
				"ttl": 600,
				"value": "119.29.18.115",
				"enabled": 1,
				"status": "enabled",
				"updated_on": "2017-02-20 20:00:39",
				"q_project_id": 0,
				"name": "www",
				"line": "\u9ed8\u8ba4",
				"line_id": "0",
				"type": "A",
				"remark": "",
				"mx": 0
			},
            {
				"id": 281817768,
				"ttl": 600,
				"value": "203.195.160.18",
				"enabled": 1,
				"status": "enabled",
				"updated_on": "2017-02-20 20:00:39",
				"q_project_id": 0,
				"name": "www",
				"line": "\u9ed8\u8ba4",
				"line_id": "0",
				"type": "A",
				"remark": "",
				"mx": 0
			}
		]
	}
}
```
