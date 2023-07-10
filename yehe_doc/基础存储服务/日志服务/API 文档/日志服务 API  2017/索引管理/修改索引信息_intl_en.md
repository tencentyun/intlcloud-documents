## API Description

This API is used to modify the existing index information.

## Request

#### Sample request 

```
PUT /index HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json
{
			"topic_id": "xxxx-xx-xx-xx-xxxxxxxx",
			"effective": true,
			"rule": {
				"full_text": {
					"case_sensitive": false,
					"tokenizer": "*{^&%"
				},
			    "key_value": {
					"case_sensitive": false,
					"keys": ["age","name"],
					"types": ["long","text"],
					"tokenizers": ["", "-"],
					"sql_flags":[true,false]
				},
				"tag": {
					"case_sensitive": false,
					"keys": ["age","name"],
					"types": ["long","text"],
					"tokenizers": ["", "-"],
					"sql_flags":[true,false]
				 }
			}
}
```

#### Request line

```
PUT /index
```

#### Request headers

No special request headers. Only common headers are used.

#### Request parameters

| Parameter | Type | Location | Required | Description |
|--------------|--------|------|--------|-----------------------------------------------|
| topic_id | string | body | Yes | ID of the topic to which the index to be modified belongs |
| effective | bool | body | Yes | Whether to enable the index |
| rule | object | body | No | Index rule, which is required when `effective` is set to `true`. |


**Parameter for CLS users**


| Parameter | Type | Location | Required | Description |
|---------|---------|---------|---------|---------|
| custom_uin | long | body |  No |  Customer UIN to which the index belongs |


Parameters in `rule`:

| Parameter  | Type    | Required | Description                                                        |
|------------|--------|---------|-------------------------------|
| full_text | object | No | Configuration for full-text index |
| key_value | object | No | Configuration for key-value index |

> You need specify at least one of `full_text` and `key_value` when setting `rule`.

Parameters in `full_text`:

| Parameter  | Type    | Required | Description                                                        |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | Yes | Whether this parameter is case-sensitive |
| tokenizer | string | No      | Separator for full-text index, which cannot be empty. You’re recommended to set it to <code>!@#%^&*()-_="', &lt;>/?\|\\;:\n\t\r[]{}</code>. |

Parameters in `key_value`:

| Parameter  | Type    | Required | Description                                                        |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | Yes | Whether this parameter is case-sensitive |
| keys | array (string) | Yes | Key names for which indexes need to be created |
| types | array (string) | Yes | Types of keys for which indexes need to be created. One type corresponds to one key. This is only applicable to parameters of `long`, `double`, or `text` type. |
| tokenizers | array (string) | No | Separators for the above keys. One separator corresponds to one key. This parameter is only applicable to parameters of `text` type, and is empty for other types of parameters. |
| sql_flags| array (bool) | No      | An array of values indicating whether to enable SQL statistics for corresponding keys. Valid values: `false` (default): disable; `true`: enable |

Parameters in `tag`:

| Parameter  | Type    | Required | Description                                                        |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | Yes | Whether this parameter is case-sensitive |
| keys | array (string) | Yes | Keys for which indexes need to be created |
| types | array (string) | Yes | Types of the above keys. One type corresponds to one key. This is only applicable to parameters of `long`, `double`, or `text` type. |
| tokenizers | array (string) | No | Separators for the above keys. One separator corresponds to one key. This parameter is only applicable to parameters of `text` type, and is empty for other types of parameters. |
| sql_flags| array (bool) | No      | An array of values indicating whether to enable SQL statistics for corresponding keys. Valid values: `false` (default): disable; `true`: enable  |


## Response

#### Sample response

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
```

#### Response headers

No special response headers. Only common headers are used.

#### Response parameters

None.

## Error Codes

For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).

