## Feature Description

This API is used to create a logset and return its ID.

## Request

#### Sample request

```shell
POST /logset HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/json

{"logset_name": "testname","period": 15}
```
#### Request line

```shell
POST /logset
```

#### Request header

There are only common response headers but no special response headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
|--------------|--------|------|---------|--------------------------------|
| logset_name  | string | body | Yes      | Logset name, which must be unique             |
| period       | int    | body | Yes      | Logset retention period in days. Maximum value: 90    |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{"logset_id": "xxxx-xx-xx-xx-xxxxxxxx"}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
|-------------|-----------|---------|-------------------------------|
| logset_id        | string     | Yes       | Logset ID                                                  |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
