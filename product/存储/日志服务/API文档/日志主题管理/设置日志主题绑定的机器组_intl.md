## Description

This API is used to set the server groups bound to a log topic.

## Request

### Request example

```
PUT /topic/machinegroup?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <Authorization String>
Content-Type: application/json
{  
	"machine_groups": ["xxxxxx-xx-xx-xx-yyyyyyyy"]
}
```

### Request line

```
PUT /topic/machinegroup
```

### Request header

No special request header is used except for the common header. 

### Request parameters

| Field Name | Type | Location | Required | Description |
| -------------- | ----------------- | ----- | -------- | ---------------------------- |
| topic_id | string | query | Yes | ID of the log topic to be set |
| machine_groups | JsonArray(string) | body | Yes | Array of IDs of server groups bound to a log topic |

## Response

### Response example

```
HTTP/1.1 200 OK
Content-Length: 0
```

### Response header

No special response header is used except for the common response header. 

### Response parameters

None.

### Error codes

For more information, see [Error Codes](https://cloud.tencent.com/document/product/614/12402).

