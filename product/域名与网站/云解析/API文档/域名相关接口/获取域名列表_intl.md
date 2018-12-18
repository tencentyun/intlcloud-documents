## 1. API Description
This API (DomainList) is used to obtain the domain names under the account.
API request domain name: **cns.api.qcloud.com**

## 2. Input Parameters
The following list of request parameters lists only the API request parameters. The common request parameters need to be added when making a call. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/377/4153). Here, the Action field of this API is DomainList.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| offset | no | Int | Offset, 0 by default. For more information on the offset, see the relevant section in the API overview. |
| length | no | Int | Number of returns, 20 by default, up to 100. For more information on the limit, see the relevant section in the API overview. |
| keyword | No | String | (Filter) filter domain name by keyword |
| qProjectId | No | Int | (Filter) filter by project ID |

## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code; 0 - success, other values - failure. |
| message | String | Module error description; related to the API. |
| data | Array | The data returned by the API. |

The "data" parameter contains the quantity and list of domain names under the account.

Description of the "info" parameter

| Parameter name | Type | Description |
|---------|---------|---------|
| domain_total | Int | Total number of domain names under the account |

"domains" contains detailed information for each domain name, including:

| Parameter name | Type | Description |
|---------|---------|---------|
| domain_total | Int | Total number of domain names under the account |
| id | Int | Domain name ID |
| status | String | Domain name status; "enable", "pause", "spam" and "lock" represent "normal", "resolution paused", "blocked" and "locked", respectively |
| group_id | String | ID of the domain name group |
| searchengine_push | String | Prioritized push for search engine; yes - enabled, no - disabled |
| is_mark | String | Whether the domain name is marked with an asterisk; yes - yes, no - no |
| ttl | String | Default TTL value for the resolution records of the domain name |
| cname_speedup | String | enable - enabled, disable - disabled |
| remark | String | Domain name remark |
| created_on | String | Domain name's added time |
| updated_on | String | Domain name's last modified time |
| q_project_id | Int | ID of the project where the domain name is located |
| punycode | String | Domain name after encoded with punycode |
| ext_status | String | Status information for domain name extension; "notexist", "dnserror" and "" represent "domain name not registered", "incorrect DNS settings" and "normal", respectively |
| src_flag | String | Tag for the source for the domain name; QCLOUD - Tencent Cloud DNS, DNSPOD - DNSPod |
| name | String | Domain name |
| grade | String | Domain name level |
| grade_title | String | Level of the domain name |
| is_vip | String | Whether it is a VIP domain name; yes- yes, no - no |
| owner | String | Domain name owner's email address |
| records | String | Number of resolution records under the domain name |
| min_ttl | Int | Minimum TTL allowed by the current domain name |

## 4. Examples
```
https://cns.api.qcloud.com/v2/index.php?
&<Common request parameter>
&Action=DomainList
&offset=0
&length=10
```


Response example; code 0 indicates success
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "info": {
            "domain_total": 18
        },
        "domains": [
            {
                "id": 53980930,
                "status": "enable",
                "group_id": "1",
                "searchengine_push": "no",
                "is_mark": "no",
                "ttl": "600",
                "cname_speedup": "disable",
                "remark": "",
                "created_on": "2017-02-08 18:05:22",
                "updated_on": "2017-02-08 18:05:22",
                "q_project_id": 0,
                "punycode": "yizero.wang",
                "ext_status": "dnserror",
                "src_flag": "QCLOUD",
                "name": "yizero.wang",
                "grade": "DP_Free",
                "grade_title": "New free package",
                "is_vip": "no",
                "owner": "100000@qq.com",
                "records": "2",
                "min_ttl": 600
            }
        ]
    }
}
```

