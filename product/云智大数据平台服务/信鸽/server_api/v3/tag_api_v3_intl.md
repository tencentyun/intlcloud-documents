## Tag API v3

### Tag API Overview

- Tag API is a general term for all tag APIs
- Tag API includes various APIs used to set, update, and delete tags as follows:
  - Add a single tag
  - Delete a single tag
  - Add multiple tags
  - Delete multiple tags
  - Delete all tags
  - Update a tag
  - Set a tag for multiple tokens
  - Delete a tag from multiple tokens
  - Batch set tags
  - Batch delete tags
- All push targets use the same URL to initiate the request (URL: `https://openapi.xg.qq.com/v3/device/tag`).
- All request parameters are uploaded via JSON encapsulation to the backend, which distinguishes among different push targets based on the request parameters.
  

### Tag API Call Address

```text
https://openapi.xg.qq.com/v3/device/tag
```



### Tag API Request Parameters

| Parameter name | Type | Required | Description |
| -------------- | ------- | ---- | ---------------------------------------- |
| operator_type  | int     | Yes    | Operation type <br>1) 1: add a single tag to a single token <br>2) 2: delete a single tag from a single token <br>3) 3: add multiple tags to a single token <br>4) 4: delete multiple tags from a single token <br> 5) 5: delete all tags from a single token <br>6) 6: add one or more tags to a single token in an overriding manner <br>7) 7: add a single tag to multiple tokens <br>8) 8: delete a single tag from multiple tokens <br>9) 9: batch add tags (up to 20 pairs are allowed per call; in each tag-token pair, the tag is before the token) <br>10) 10: batch delete tags (up to 20 pairs are allowed per call; in each tag-token pair, the tag is before the token) |
| platform       | string  | Yes | Client platform type <br>1) android: Android <br>2) ios: Apple |
| token_list     | array   | No    | Device list <br>1) Required when operator_type =1,2,3,4,5,6,7,8 <br>2) When operator_type =1,2,3,4,5,6, if this parameter contains multiple tokens, only the first one will be set <br>3) Format example: ["token1","token2"]  <br>4) The list can contain up to 20 values  <br>5) A token string cannot exceed 64 characters |
| tag_list       | array   | No | Tag list <br>1) Required when operator_type =1,2,3,4,6,7,8; ignored when =5 <br>2) When operator_type =1,2,3,4,6,7,8, if this parameter contains multiple tags, only the first tag will be set if for a single tag <br>3) Format example: ["tag1","tag2"] <br>4) The list can contain up to 20 values <br>5) A tag string cannot exceed 50 characters |
| tag_token_list | array   | No    | Tag-device list <br>1) Required when operator_type =9,10 <br>2) Format example:  [["tag1","token1"],["tag2","token2"]] <br>3) In each pair, the tag must be before the token  <br>4) The list can contain up to 20 values <br>5) A tag string cannot exceed 50 characters <br>6) A token string cannot exceed 64 characters |
| seq | int64_t | No | When the API is called, TPNS will return this field in the response packet, which can be used for async request <br>Usage scenario: In async service, the corresponding response packet returned by the server can be found through this field |
| op_type        | string  | No    | API operator type: qq, rtx, email, other |
| op_id          | string  |  No | API operator type: API operator id (qq\rtx\email) |

Tag API Samples 

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

- Add multiple tags (tag1 and) tag2 to a single token (token1)

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

- Add multiple tags (tag1 and tag2) to a single token (token1) in an overriding manner

  ```json
  {   
    "operator_type": 6,
    "platform": "android",
    "tag_list": ["tag1","tag2"],
    "token_list": ["token1"]
   }
  ```


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

- Batch set tags for [tag1,token1],[tag2,token2]

  ```json
  {   
    "operator_type": 9,
    "platform": "android",
    "tag_token_list":  [["tag1","token1"],["tag2","token2"]]
 
  }
  ```

- Batch delete tags for [tag1,token1],[tag2,token2]

  ```json
  {   
    "operator_type": 10,
    "platform": "android",
    "tag_token_list":  [["tag1","token1"],["tag2","token2"]]
  }
  ```

### Tag API Response Parameters 

| Field name | Type | Required | Comments |
| -------- | ------- | ---- | ---------------------------------------- |
| seq | int64_t | Yes | The same as the request packet (if the request packet is invalid JSON, this field is 0) |
| ret_code | int32_t | Yes | Error code; for details, see the error codes table |
| err_msg | string | No | error message when an error occurs in the request |
| result | string | No | When the request is correct, if there is extra data to be returned, the result will be encapsulated in the json of this field. If there is no extra data, there may be no such field |



### Complete Example of Tag API Request

#### Tag Setting Request Message

```json
POST /v3/device/tag HTTP/1.1
Host: openapi.xg.qq.com
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

#### Tag Setting Response Message

```
{
    "seq": 0,
    "ret_code": 0,
}
```



## Error Codes

You may encounter various problems when using APIs. Below are the common error codes and their definitions:

| Error code | Meaning |
| ----- | -------------------- |
| 0 | Normal |
| 10000 | Unknown exception |
| 10001 | Failed due to timeout. Please retry            |
| 10102 | Parameter is missing. Please check and retry         |
| 10103 | Parameter value is invalid. Please check and retry        |
10104 | Authentication failed. Please check the secret key |
| 11001 | Internal error. Please retry later          |
| 11002 | Internal error. Please retry later          |
| 11003 | Internal error. Please retry later          |
| 11004 | Internal error. Please retry later          |
| 11005 | Internal error. Please retry later          |
| 11006 | Internal error. Please retry later          |
| 11007 | Internal error. Please retry later          |
| 10113 | Internal error. Please retry later          |
