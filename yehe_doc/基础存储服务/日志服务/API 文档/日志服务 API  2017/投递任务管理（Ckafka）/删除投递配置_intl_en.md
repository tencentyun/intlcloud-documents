## Feature Description

This API is used to delete the shipping configuration.

## Request

### Request line

```
DELETE /consumer
```

### Sample request

```
DELETE /consumer?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```

### Request headers

No special request headers

### Request parameters

| Parameter | Type | Position | Required | Description |
|--------------|--------|------|---------|--------------------------------|
| topic_id | string | query | Yes | ID of the log topic associated with the shipping task |


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
