## Feature Description

This API is used to modify a logset.

## Request

#### Sample request

```shell
PUT /logset HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/json

{"logset_id": "xxxx-xx-xx-xx-xxxxxxx","logset_name": "testname","period": 15}
```

#### Request line

```shell
PUT /logset
```

#### Request header

There are only common response headers but no special response headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
|--------------|--------|------|---------|--------------------------------|
| logset_id    | string     | body | Yes   | ID of the logset to be modified                                    |
| logset_name  | string | body | No      | Logset name, which must be unique             |
| period       | int    | body | No      | Logset retention period in days. Maximum value: 90    |

>At least one parameter out of `logset_name` and `period` must be provided.

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Length: 0
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

If the update is successful, there will be no response parameters.

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
