## Feature Description

This API is used to create a shipping task.

## Request

### Request line

```
POST /deliverfunction
```

### Sample request

```
POST /deliverfunction HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
    "topic_id": "yyyy-yy-yy-yy-yyyyyyyy",
    "names_pace": "test",
    "function_name": "myfunction",
    "qualifier": "$LATEST",
    "max_wait": 60,
    "max_size": 100
}
```

### Request headers

No special request headers

### Request parameters

| Parameter | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| topic_id | string | Yes | ID of the topic to which shipping rules belong |
| name_space    | string | Yes      | Namespace               |
| function_name     | string | Yes      | Shipping function name                 |
| qualifier | string  | Yes      | Function version                      |
| max_size | int | No      | Maximum number of messages shipped                 |
| max_wait  | int    | No     | Maximum shipping wait duration, in seconds          |


## Response

### Sample response

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
```

### Response headers

No special response headers

### Response parameters

None

