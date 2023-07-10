## Feature Description

This API is used to get the information of the machine groups bound to a log topic.

## Request

### Sample request

```
GET /topic/machinegroup?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <Authorization String>
```

### Request line

```
GET /topic/machinegroup
```

### Request header

There are only common request headers but no special request headers. 

### Request parameters

| Field Name | Type | Location | Required | Description |
| -------- | ------ | ----- | -------- | ---------------- |
| topic_id       | string            | query | Yes       | ID of the log topic to be queried            |

## Response

### Sample response

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

There are only common response headers but no special response headers. 

### Response parameters

| Field Name | Type | Required | Description |
| -------------- | --------- | -------- | ------------------------ |
| machine_groups | JsonArray | Yes       | Array of machine groups bound to log topic |

`machine_groups` is in the following format:

| Field Name | Type | Required | Description |
| ---------- | ------ | -------- | ------------ |
| group_id   | string | Yes      | Machine group ID                  |
| group_name | string | Yes      | Machine group name                    |

### Error codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
