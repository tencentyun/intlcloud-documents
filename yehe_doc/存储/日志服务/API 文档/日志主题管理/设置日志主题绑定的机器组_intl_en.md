## Feature Description

This API is used to set the server group information bound to a log topic.

## Request

#### Sample request

```sh
PUT /topic/machinegroup?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <Authorization String>
Content-Type: application/json
{  
	"machine_groups": ["xxxxxx-xx-xx-xx-yyyyyyyy"]
}
```

#### Request line

```sh
PUT /topic/machinegroup
```

#### Request header

There are only common request headers but no special request headers. 

#### Request parameters

| Field Name | Type | Location | Required | Description |
| -------------- | ----------------- | ----- | -------- | ---------------------------- |
| topic_id       | string            | query | Yes       | Configured log topic ID            |
| machine_groups | JsonArray (string) | body  | Yes       | Array of server group IDs bound to log topic |

## Response

#### Sample response

```sh
HTTP/1.1 200 OK
Content-Length: 0
```

#### Response header

There are only common response headers but no special response headers. 

#### Response parameters

None.

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
