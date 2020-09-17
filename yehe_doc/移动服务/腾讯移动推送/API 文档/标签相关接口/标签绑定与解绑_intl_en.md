## API Description
**Request method**: POST.
The API request address corresponds to the service access point one by one; therefore, please select the request address corresponding to your application service access point.

Service access point in Guangzhou:
```shell
https://api.tpns.tencent.com/v3/device/tag
```
Service access point in Hong Kong (China):
```shell
https://api.tpns.hk.tencent.com/v3/device/tag
```
Service access point in Singapore:
```shell
https://api.tpns.sgp.tencent.com/v3/device/tag
```
Service access point in Shanghai:
```shell
https://api.tpns.sh.tencent.com/v3/device/tag
```

**API feature**
`Tag` API is the general term for all tag APIs. It includes various APIs for setting, updating, and deleting which are described as below:
For use cases of the tag feature, please see [Tag Feature Use Instructions](https://intl.cloud.tencent.com/document/product/1024/35392).



## Parameter Description
#### Request parameters

| Parameter Name | Type | Required | Description |
| -------------- | ------- | ---- | ---------------------------------------- |
| operator_type | Integer | Yes | Operation type: <br>1: add a single tag to a single token.<br>2: delete a single tag from a single token.<br>3: add multiple tags to a single token.<br>4: delete multiple tags from a single token.<br>5: delete all tags from a single token.<br>6: add one or more tags or custom tags to a single token in an overwriting manner.<br>(This API only starts to set up new tags after the tag history is cleared, so calling it for the same token should be made at a certain interval (more than 1s recommended); otherwise, it may cause updating failure.)<br>7: add a single tag to multiple tokens.<br>8: delete a single tag from multiple tokens.<br>9: batch add tags (up to 20 pairs are allowed per call; in each tag-token pair, the tag is before the token).<br>10: batch delete tags (up to 20 pairs are allowed per call; in each tag-token pair, the tag is before the token). |
| platform | String | Yes | Client platform type: <li>Android: Android <li>iOS: iOS |
| token_list | Array | No | Device list:<li>Required if `operator_type` is 1, 2, 3, 4, 5, 6, 7, or 8.<li>If `operator_type` is 1, 2, 3, 4, 5, or 6, if this parameter contains multiple tokens, only the first one will be set.<li>Format example:["token1","token2"] <li>The list can contain up to 20 values.<li>A token string cannot exceed 36 characters. |
| tag_list | Array | No | Tag list:<li>Required if `operator_type` is 1, 2, 3, 4, 6, 7, or 8; ignored if `operator_type` is 5.<li>If `operator_type` is 1, 2, 7, or 8, if this parameter contains multiple tags, only the first tag will be set if for a single tag.<li>Format example: ["tag1","tag2"]<li>The list can contain up to 20 values.<li>A tag string cannot exceed 50 characters. |
| tag_token_list | Array | No | Tag-device list:<li>Required if `operator_type` is 9 or 10.<li>Format example: [{"tag":"tag123", "token":"token123"}]<li>In each pair, the tag must be before the token.<li>The list can contain up to 20 values.<li>A tag string cannot exceed 50 characters.<li>A token string cannot exceed 64 characters. |

>
- One application can have up to 10,000 custom `tags`, one device `token` can be bound to up to 100 customized `tags` (if you want to increase this limit, please submit a ticket), and one custom `tag` can be bound to an unlimited number of device tokens.
- If the API is being called just one time without setting up continuous tags, then there are no restrictions on the API call method.
- If the API is called by setting up continuous tags, then the following must be noted:
 - If there is a need to set up API calling by using continuous tags with more than 10 tags or more than 10 tokens, it is recommended that batch APIs be used. However, it is recommended that the interval between API calls be no less than 1s to guarantee correct tag operations.
 - If you are not using batch APIs, then the API for the next non-batched tag should be called after the returned value of the TPNS server is clearly obtained. It is not recommended that multi-thread async be used at the same time as performing tag API calling.
- Colon ":" is a keyword used by the TPNS backend for tag categorization. If ":" is included when a tag is set, then the string before the first ":" will be used as the category name of the tag. This is only used when `operator_type` is 6 (overwriting tags by category). For example, if the existing tags of a device are `level:1`, `level:2`, and `male`, you can directly use tag `level:3` to overwrite tags `level:1` and `level:2` without having to unbind `level:1` and `level:2` one by one, and then bind tag `level:4`. For more information, please see the following sample request where `operator_type` is 6.




#### Response parameters

| Field name   | Type    | Required | Comments                                                         |
| -------- | ------- | -------- | ------------------------------------------------------------ |
| ret_code | Integer | Yes       | Error code. For more information, please see the error codes table                                 |
| err_msg  | String  | No       | Error message when an error occurs in the request                                         |
| result   | String  | No       | When the request is correct:<li>If there is extra data to be returned, the result will be encapsulated in the JSON of this field. If there is no extra data, <li>there may be no such field |



## Samples
#### Sample tag binding and unbinding requests

- Add a single tag (tag1) to a single token (token1)

```json
{
    "operator_type": 1,
    "platform": "android",
    "tag_list": [
        "tag1"
    ],
    "token_list": [
        "token1"
    ]
}
```

- Delete a single tag (tag1) from a single token (token1)

```json
{
    "operator_type": 2,
    "platform": "android",
    "tag_list": [
        "tag1"
    ],
    "token_list": [
        "token1"
    ]
}
```

- Add multiple tags (tag1 and tag2) to a single token (token1)

```json
{
    "operator_type": 3,
    "platform": "android",
    "tag_list": [
        "tag1",
        "tag2"
    ],
    "token_list": [
        "token1"
    ]
}
```

- Delete multiple tags (tag1 and tag2) from a single token (token1)

```json
{
    "operator_type": 4,
    "platform": "android",
    "tag_list": [
        "tag1",
        "tag2"
    ],
    "token_list": [
        "token1"
    ]
}
```

- Delete all tags from a single token (token1)

```json
{
    "operator_type": 5,
    "platform": "android",
    "tag_list": [
        "tag1",
        "tag2"
    ],
    "token_list": [
        "token1"
    ]
}
```

- Tag overwrites custom tags of token1.

```json
{
    "operator_type": 6,
    "platform": "android",
    "tag_list": [
        "test:2",
        "level"
    ],
    "token_list": [
        "token1"
    ]
}
```
>If one or more of the tags do not contain ":", then the `test:2` and `level` tags overwrite all custom tags of token1.

- Batch overwrite custom tags of a single token (this API only overwrites custom but not all tags)

```json
{
    "operator_type": 6,
    "platform": "android",
    "tag_list": [
        "test:2",
        "level:2"
    ],
    "token_list": [
        "token1"
    ]
}
```
>If all the tags have ":", as the string before the first ":" is the tag category, only tags in the same category corresponding to the device will be overwritten; for example, `test:2` will overwrite `test:*`, and `level:2` will overwrite `level:*`, without affecting other tags.

- Add a single tag (tag1) to multiple tokens (token1 and token2)

```json
{
    "operator_type": 7,
    "platform": "android",
    "tag_list": [
        "tag1"
    ],
    "token_list": [
        "token1",
        "token2"
    ]
}
```

- Delete a single tag (tag1) from multiple tokens (token1 and token2)

```json
{
    "operator_type": 8,
    "platform": "android",
    "tag_list": [
        "tag1"
    ],
    "token_list": [
        "token1",
        "token2"
    ]
}
```

- Batch set tags

```json
{
    "operator_type": 9,
    "platform": "android",
    "tag_token_list": [
        {
            "tag": "tag1",
            "token": "token1"
        }
    ]
}
```

- Batch delete tags (tag1, tag2, and tag3)

```json
{
    "operator_type": 10,
    "platform": "android",
    "tag_token_list": [
        {
            "tag": "tag1",
            "token": "token1"
        },
        {
            "tag": "tag2",
            "token": "token2"
        },
        {
            "tag": "tag3",
            "token": "token3"
        }
    ]
}
```


#### Sample tag setting request

```json
POST /v3/device/tag HTTP/1.1
Host: api.tpns.tencent.com
Content-Type: application/json
Authorization: Basic YTViNWYwNzFmZjc3YTplYTUxMmViNzcwNGQ1ZmI1YTZhOTM3Y2FmYTcwZTc3MQ==
Cache-Control: no-cache
Postman-Token: 4b82a159-afdd-4f5c-b459-de978d845d2f
{
    "operator_type": 1,
    "platform": "android",
    "tag_list": [
        "tag1"
    ],
    "token_list": [
        "token1"
    ]
}
```

#### Sample tag setting response

```json
{
    "seq": 0,
    "ret_code": 0
}
```






