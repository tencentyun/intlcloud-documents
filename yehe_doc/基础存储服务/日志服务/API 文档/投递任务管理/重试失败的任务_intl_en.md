## Feature Description

This API is used to retry a failed shipping task.

## Request


#### Sample request

```shell
PUT /task HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
  "shipper_id": "xxxxxx-xx-xx-xx-xxxxxxxx",
  "task_id": "xxxxxx-xx-xx-xx-xyyyyyyy"
}
```

#### Request line

```shell
PUT /task
```
#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
|--------------|--------|------|---------|--------------------------------|
| shipper_id   | string | body | Yes      | Shipping rule ID                     |
| task_id      | string | body | Yes      | Shipping task ID                     |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Length: 0
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

None.

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
