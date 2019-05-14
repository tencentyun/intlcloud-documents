## Description

This API is used to get the information of server groups bound to a log topic.

## Request

### Request example

```
GET /topic/machinegroup?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <Authorization String>
```

### Request line

```
GET /topic/machinegroup
```

### Request header

No special request header is used except for the common header. 

### Request parameters

| Field Name | Type | Location | Required | Description |
| -------- | ------ | ----- | -------- | ---------------- |
| topic_id | string | query | Yes | ID of the log topic to be queried |

## Response

### Response example

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123
{
	"machine_groups": [
	{
		"group_id": "xxxx-xx-xx-xx-yyyyyyyy",
		"group_name": "testname"},    
		{"group_id": "xxxx-xx-xx-xx-zzzzzzzz", 
		"group_name": "testname1"}
	]
}
```

### Response header

No special response header is used except for the common response header. 

### Response parameters

| Field Name | Type | Required | Description |
| -------------- | --------- | -------- | ------------------------ |
| machine_groups | JsonArray | Yes | Array of server groups bound to a log topic |

machine_groups is composed as follows:

| Field Name | Type | Required | Description |
| ---------- | ------ | -------- | ------------ |
| group_id | string | Yes | Server group ID |
| group_name | string | Yes | Server group name |

### Error codes

For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).

