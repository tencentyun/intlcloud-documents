## Feature Description

This API is used to obtain the details of a specified shipping policy.

## Request

### Request line

```
GET /deliverfunction
```

### Sample request

```
GET /deliverfunction?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```

### Request headers

No special request headers

### Request parameters

| Parameter | Type | Position | Required | Description |
|--------------|--------|------|--------|---------------------------|
| topic_id | string | query | Yes | ID of the topic queried |

## Response

### Sample response

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
    "topic_id": "yyyy-yy-yy-yy-yyyyyyyy",
    "names_pace": "test",
    "function_name": "myname",
    "qualifier": "$LATEST",
    "max_wait": 60,
    "max_size": 100,
    "effective" : true
  
}
```


### Response headers

No special response headers

### Response parameters

| Parameter | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| topic_id | string | Yes | ID of the topic to which shipping rules belong |
| name_space    | string | Yes      | Namespace               |
| function_name    | string | Yes      | Function name                 |
| qualifier | string  | Yes      | Function version                      |
| max_size | int | No      | Maximum number of messages shipped                 |
| max_wait  | int    | No     | Maximum shipping wait duration, in seconds          |
| effective  | bool  | Yes      |          Shipping switch            |
 
