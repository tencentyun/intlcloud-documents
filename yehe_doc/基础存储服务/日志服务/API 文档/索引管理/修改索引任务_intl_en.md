## Feature Description

This API is used to modify an existing index task.

## Request

#### Sample request

```
PUT /index HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
  "topic_id": "xxxx-xx-xx-xx-xxxxxxxx",
  "effective": true,
  "rule": {
    "full_text": {
      "case_sensitive": false,
      "tokenizer": "{^&%"
    },
    "key_value": {
      "case_sensitive": false,
      "keys": ["age","name"],
      "types": ["long","text"],
      "tokenizers": ["","-"]
    }
  }
}

```

#### Request line

```
PUT /index
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
|--------------|--------|------|--------|-----------------------------------------------|
| topic_id     | string | body | Yes      | Topic ID of the index to be modified                      |
| effective    | bool   | body | Yes      | Index status switch                                |
| rule         | object | body | No      | Index rule, which is required if `effective` is `true`               |


`rule` content description:

| Field Name | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| full_text  | object | No      | Full-text index configuration              |
| key_value  | object | No      | KV index configuration               |

>When setting `rule`, you must set at least one parameter out of `full_text` and `key_value`.

`full_text` content description:

| Field Name | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | Yes      | Case sensitivity              |
| tokenizer | string | No      | Tokenizer for full-text index, which cannot be empty. You are recommended to select one out of <code>@#%^&*()-_="', &lt;>/?\|\\;:\n\t\r[]{}</code> |

`key_value` content description:

| Field Name | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | Yes      | Case sensitivity              |
| keys | array(string) | Yes      | Names of the keys to be indexed            |
| types| array(string) | Yes      | Types of the keys to be indexed (in one-to-one correspondence). Currently, `long double text` is supported |
| tokenizers| array(string) | No      | Tokenizers corresponding to the above keys (in one-to-one correspondence). This parameter is only required for the `text` type and is an empty string for other types  |

## Response

#### Sample response

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

None.

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
