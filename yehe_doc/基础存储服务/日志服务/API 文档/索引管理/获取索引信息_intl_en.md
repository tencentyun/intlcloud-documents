## Feature Description

This API is used to get the detailed information of a specified index policy.

## Request

#### Sample request

```shell
GET /index?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request line

```shell
GET /index
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
|---------------|--------|-------|---------|---------------------------|
| topic_id      | string | query | Yes      | Topic ID of the index to be queried    |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 153

{
  "topic_id": "yyyy-yy-yy-yy-yyyyyyyy",
  "effective": true,
  "rule": {
    "full_text": {
      "case_sensitive": false
    },
    "key_value": {
      "case_sensitive": false,
      "keys": ["age","name"],
      "types": ["long","text"]
    }
  }
}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| topic_id   | string | Yes      | Topic ID of index rule          |
| effective  | bool   | Yes      | Whether it is effective                       |
| rule       | object | No      | Index rule, which will be returned if `effective` is `true` |

`rule` content description:

| Field Name | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| full_text  | object | No      | Full-text index configuration              |
| key_value  | object | No      | KV index configuration               |

`full_text` content description:

| Field Name | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | Yes      | Case sensitivity              |

`key_value` content description:

| Field Name | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | Yes      | Case sensitivity              |
| keys | array(string) | Yes      | Names of the keys to be indexed            |
| types| array(string) | Yes      | Types of above keys (in one-to-one correspondence). Currently, `long double text` is supported |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
