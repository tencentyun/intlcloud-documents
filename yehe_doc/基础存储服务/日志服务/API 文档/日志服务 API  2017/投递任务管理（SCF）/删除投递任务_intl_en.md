## Feature Description

This API is used to delete the shipping configuration.

## Request

### Request line

```
DELETE /deliverfunction
```

### Sample request

```
DELETE /deliverfunction?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
```

### Request headers

No special request headers

### Request parameters

| Parameter | Type | Position | Required | Description |
|--------------|--------|------|---------|--------------------------------|
| topic_id | string | query | Yes | ID of the topic whose shipping task is to be deleted |

## Response

### Sample response

```
HTTP/1.1 200 OK
Content-Length: 0
```

### Response headers

No special response headers

### Response parameters

None

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/42832).

