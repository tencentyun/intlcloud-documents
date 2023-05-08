## API Calling Description
**Request method**: POST.
```plaintext
Service URL/v3/device/tag
```
The API service address corresponds to the service access point one by one; therefore, please select the service address corresponding to your application [service access point](https://www.tencentcloud.com/document/product/1024/38517).

**API features**:
Tag API is the general term for all tag APIs. Tag API includes various APIs for setting, updating, and deleting which are described as below:
For use cases of tags, see [Tag Feature](https://www.tencentcloud.com/document/product/1024/35392).



## Parameter description
#### Request parameters

| Parameter | Type | Required | Description |
| -------------- | ------- | ---- | ---------------------------------------- |
| operator_type | Integer | Yes | Operation type:<br>`1`: add a tag to a token.<br>`2`: delete a tag from a token.<br>`3`: add multiple tags to a token.<br>`4`: delete multiple tags from a token.<br>`5`: delete all tags from a token.<br>`6`: add one or more tags or custom tags to a token in an overwriting manner.<br>(This API starts to set new tags only after the tag history is cleared. Therefore, for the same token, it is recommended that the interval between API calls be over 1s; otherwise, the update may fail.)<br>`7`: add a tag to multiple tokens.<br>`8`: delete a tag from multiple tokens.<br>`9`: batch add tags (up to 20 pairs are allowed per call; in each tag-token pair, the tag is before the token).<br>`10`: batch delete tags (up to 20 pairs are allowed per call; in each tag-token pair, the tag is before the token). |
| token_list | Array  | No | Device list:<li>Required when `operator_type` is `1`, `2`, `3`, `4`, `5`, `6`, `7`, or `8`.<li>When `operator_type` is `1`, `2`, `3`, `4`, `5`, or `6` and this parameter contains multiple tokens, only the first token will be set.<li>Format example: ["token1","token2"]<li>The list can contain up to 500 values.<li>A token string cannot exceed 36 characters. |
| tag_list | Array  | No | Tag list:<li>Required when `operator_type` is `1`, `2`, `3`, `4`, `6`, `7`, or `8`; ignored when `operator_type` is `5`.<li>When `operator_type` is `1`, `2`, `7`, or `8` and this parameter contains multiple tags, only the first tag will be set.<li>Format example: ["tag1","tag2"]<li>The list can contain up to 500 values.<li>A tag string cannot exceed 50 characters. |
| tag_token_list | Array  | No | Tag-device pair list:<li>Required when `operator_type` is `9` or `10`.<li>Format example: [{"tag":"tag123", "token":"token123"}]<li>In each pair, the tag is before the token.<li>The list can contain up to 500 values.<li>A tag string cannot exceed 50 characters.<li>A token string cannot exceed 36 characters.</li> |

>!
- One application can have up to 10,000 custom tags. One device token can be bound to up to 100 custom tags. If you want to increase this limit, contact [our online customer service](https://cloud.tencent.com/online-service). One custom tag can be bound to an unlimited number of device tokens.
- If the API needs to be called only once, then there are no restrictions on the API call method.
- If the API needs to be called continuously, note the following:
 - If the API needs to be called continuously to set more than 10 tags or tokens, you are advised to use batch APIs. It is recommended that the interval between API calls be no less than 1s to guarantee correct tag operations.
 - When not using batch APIs, then the API for the next non-batched tag is called after the returned value of the Tencent Push Notification Service server is clearly obtained. It is not recommended that multi-thread async be used at the same time as performing tag API calling.
- Colon `:` is a keyword used by the Tencent Push Notification Service backend for tag categorization. If you include `:` in a tag when setting it, the string before the first `:` serves as the category name of the tag. This is only used when `operator_type` is `6`, which means overwriting tags by category. For example, if the existing tags of a device are `level:1`, `level:2`, and `male`, you can directly overwrite `level:1` and `level:2` with `level:3` without having to unbind `level:1` and `level:2` one by one, and then bind `level:3`. For more information, please see the following sample request where `operator_type` is `6`.


#### Response parameters

| Parameter | Type    | Required | Description |
| -------- | ------- | -------- | ------------------------------------------------------------ |
| ret_code    | Integer | Yes       | Error code. For more information, please see the error codes table.                                 |
| err_msg     | String  | No      | Error message when a request error occurs                                         |
| result      | String  | No | When the request is correct:<li>If there is extra data to return, the result will be encapsulated in this parameter in JSON format.<li>If there is no extra data, this parameter may not exist.</li> |



## Samples
#### Examples of Tag Binding and Unbinding Requests

- Add a tag (tag1) to a token (token1)
```json
{
    "operator_type": 1,
    "tag_list": [
        "tag1"
    ],
    "token_list": [
        "token1"
    ]
}
```
- Delete a tag (tag1) from a token (token1)
```json
{
    "operator_type": 2,
    "tag_list": [
        "tag1"
    ],
    "token_list": [
        "token1"
    ]
}
```
- Add multiple tags (tag1 and tag2) to a token (token1)
```json
{
    "operator_type": 3,
    "tag_list": [
        "tag1",
        "tag2"
    ],
    "token_list": [
        "token1"
    ]
}
```
- Delete multiple tags (tag1 and tag2) from a token (token1)
```json
{
    "operator_type": 4,
    "tag_list": [
        "tag1",
        "tag2"
    ],
    "token_list": [
        "token1"
    ]
}
```
- Delete all tags from a token (token1)
```json
{
    "operator_type": 5,
    "tag_list": [
        "tag1",
        "tag2"
    ],
    "token_list": [
        "token1"
    ]
}
```
- Overwrite custom tags of a token (token1)
```json
{
    "operator_type": 6,
    "tag_list": [
        "test:2",
        "level"
    ],
    "token_list": [
        "token1"
    ]
}
```
>? If one or more tags do not contain `:`, then the `test:2` and `level` tags overwrite all custom tags of `token1`.
>
- Batch overwrite custom tags of a token (this API overwrites custom tags only, not all tags)
```json
{
    "operator_type": 6,
    "tag_list": [
        "test:2",
        "level:2"
    ],
    "token_list": [
        "token1"
    ]
}
```
>? If all the tags contain `:`, since the string before the first `:` is the tag category, only tags in the same category bound to the device will be overwritten; for example, `test:2` overwrites `test:*`, and `level:2` overwrites `level:*`, without affecting other tags.
>
- Add a tag (tag1) to multiple tokens (token1 and token2)
```json
{
    "operator_type": 7,
    "tag_list": [
        "tag1"
    ],
    "token_list": [
        "token1",
        "token2"
    ]
}
```
- Delete a tag (tag1) from multiple tokens (token1 and token2)
```json
{
    "operator_type": 8,
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


#### Example of Tag Setting Request

```json
POST /v3/device/tag HTTP/1.1
Host: api.tpns.tencent.com
Content-Type: application/json
Authorization: Basic YTViNWYwNzFmZjc3YTplYTUxMmViNzcwNGQ1ZmI1YTZhOTM3Y2FmYTcwZTc3MQ==
Cache-Control: no-cache
Postman-Token: 4b82a159-afdd-4f5c-b459-de978d845d2f
{
    "operator_type": 1,
    "tag_list": [
        "tag1"
    ],
    "token_list": [
        "token1"
    ]
}
```

#### Example of Tag Setting Response

```json
{
    "seq": 0,
    "ret_code": 0
}
```






