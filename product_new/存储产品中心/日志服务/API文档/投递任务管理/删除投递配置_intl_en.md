## Feature Description

This API is used to delete a shipping configuration.

## Request

### Sample request

```
DELETE /shipper?shipper_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>

```
### Request line

```
DELETE /shipper
```
### Request header

There are only common request headers but no special request headers.

### Request parameters

| Field Name | Type | Location | Required | Description |
|--------------|--------|------|---------|--------------------------------|
| shipper_id   | string | query| Yes      | ID of the shipping configuration to be deleted                |

## Response

### Sample response

```
HTTP/1.1 200 OK
Content-Length: 0

```

### Response header

There are only common response headers but no special response headers.

### Response parameters

None.

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
