

## API Description
**Request method**: POST.
```shell
https://api.tpns.tencent.com/v3/device/tag
```
**API description**: Tag API is the general term for all tag APIs. Tag API includes various APIs used to set, update, and delete tags as follows:



## Parameter Descriptions
#### Request Parameters

| Parameter name | Type | Required | Description |
| -------------- | ------- | ---- | ---------------------------------------- |
| operator_type | int | Yes | Operation type:<li>Add a single tag to a single token.<li>Delete a single tag from a single token.<li>Add multiple tags to a single token.<li>Delete multiple tags from a single token.<li>Delete all tags from a single token.<li>Add one or more tags or custom class tags to a single token in an overriding manner.<br>This API only starts to set up new tags after the tag history is cleared, so calling it up takes some time (more than 5s recommended). Otherwise it may cause updating failure.<li>Add a single tag to multiple tokens.<li>Delete a single tag from multiple tokens.<li>Batch add tags (up to 20 pairs are allowed per call; in each tag-token pair, the tag is before the token).<br><li>Batch delete tags (up to 20 pairs are allowed per call; in each tag-token pair, the tag is before the token). |
| platform | string | Yes | Client platform type: <li>Android: Android <li>iOS: Apple |
| token_list | array | No | Device list:<li>Required when operator_type = 1,2,3,4,5,6,7,8.<li>When operator_type = 1,2,3,4,5,6, if this parameter contains multiple tokens, only the first one will be set.<li>Format example:["token1","token2"] <li>The list can contain up to 20 values.<li>A token string cannot exceed 64 characters. |
| tag_list | array | No | Tag list:<li>Required when operator_type = 1,2,3,4,6,7,8; ignored when operator_type = 5.<li>When operator_type = 1,2,3,4,6,7,8, if this parameter contains multiple tags, only the first tag will be set if for a single tag.<li>Format example: ["tag1","tag2"]<li>The list can contain up to 20 values.<li>A tag string cannot exceed 50 characters. |
| tag_token_list | array | No | Tag-device list:<li>Required when operator_type =9,10.<li>Format example: [{"tag":"tag123", "token":"token123"}]<li>In each pair, the tag must be before the token.<li>The list can contain up to 20 values.<li>A tag string cannot exceed 50 characters.<li>A token string cannot exceed 64 characters. |

>
- If the API is being called just one time without setting up continuous tags, then there are no restrictions on the API call method.
- If the API is called by setting up continuous tags, then the following must be noted:
 - If there is a need to set up API calling by using continuous tags with more than 10 tags or more than 10 tokens, it is recommended that batch APIs be used. However, it is recommended that the interval between API calls be no less than 5s to guarantee correct tag operations.
 - When not using batch APIs, then the API for the next non-batched tag is called after the returned value of the TPNS server is clearly obtained. It is not recommended that multi-thread async be used at the same time as performing tag API calling.
- “:” is a keyword used by the TPNS backend for customizing tag categories. If the “:” field is included when setting up tags, then the tag in front of the first “:” is the category of this custom tag. The batch setting of tag categories is supported when the operator_type is 6. When performing batch tag deletion, the tag deletion can be performed by category. For details, see the example of when the operator_type is 6 in the following request example. 




#### Response Parameters

| Field name   | Type    | Required | Comments                                                         |
| -------- | ------- | -------- | ------------------------------------------------------------ |
| seq      | int64_t | Yes       | The same as the request packet (if the request packet is invalid JSON, this field is 0)              |
| ret_code | int32_t | Yes       | Error code; for details, see the error codes table                                 |
| err_msg  | string  | No       | Error message when an error occurs in the request                                         |
| result   | string  | No       | When the request is correct:<li>If there is extra data to be returned, the result will be encapsulated in the json of this field. If there is no extra data, there may be no such field |



## Example(s)
#### Examples of Tag Binding and Unbinding Requests

- Add a single tag (tag1) to a single token (token1)

```json
{
"operator_type": 1,
"platform": "android",
"tag_list": ["tag1"],
"token_list": ["token1"]
}
```

- Delete a single tag (tag1) from a single token (token1)

```json
{
"operator_type": 2,
"platform": "android",
"tag_list": ["tag1"],
"token_list": ["token1"]
}
```

- Add multiple tags (tag1 and tag2) to a single token (token1)

```json
{
"operator_type": 3,
"platform": "android",
"tag_list": ["tag1","tag2"],
"token_list": ["token1"]
}
```

- Delete multiple tags (tag1 and tag2) from a single token (token1)

```json
{
"operator_type": 4,
"platform": "android",
"tag_list": ["tag1","tag2"],
"token_list": ["token1"]
}
```

- Delete all tags from a single token (token1)

```json
{
"operator_type": 5,
"platform": "android",
"tag_list": ["tag1","tag2"],
"token_list": ["token1"]
}
```

- Tag overrides custom tags for token1.

```json
{
"operator_type": 6,
"platform": "android",
"tag_list": ["test:2", "level"], 
"token_list": ["token1"]
}
```
> If one or more tags does not contain the “:” symbol, then the test:2 and level tags override all custom tags for token1.

- Batch override custom tags for a single token (this API only overrides custom tags and does not override all tags)

```json
{
"operator_type": 6,
"platform": "android",
"tag_list": ["test:2", "level:2"],
"token_list": ["token1"]
}
```
> If all tags contain the “:” symbol, then only the custom tags of the tag type corresponding to token1 before the “:” symbol are overridden.

- Add a single tag (tag1) to multiple tokens (token1 and token2)

```json
{
"operator_type": 7,
"platform": "android",
"tag_list": ["tag1"],
"token_list": ["token1","token2"]
}
```

- Delete a single tag (tag1) from multiple tokens (token1 and token2)

```json
{
"operator_type": 8,
"platform": "android",
"tag_list": ["tag1"],
"token_list": ["token1","token2"]
}
```

- Batch set tags

```json
{
"operator_type": 9,
"platform": "android",
"tag_token_list":  [["tag1","token1"],["tag2","token2"]]

}
```

- Batch delete tags (tag1, tag2, and tag3)

```json
{
"operator_type": 10,
"platform": "android",
"tag_token_list": [
{
"tag":"tag1",
"token":"token1"
},
{
"tag":"tag2",
"token":"token2"
},
{
"tag":"tag3",
"token":"token3"
}]
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
"platform": "android",
"tag_list": ["tag1"],
"token_list": ["token1"]
}
```

#### Example of Tag Setting Response

```json
{
"seq": 0,
"ret_code": 0,
}
```






