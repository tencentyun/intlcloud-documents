
## API Description

**Request method**: POST.
```shell
https://api.tpns.tencent.com/v3/device/tag/delete_all_device
```
**Description**: This API deletes all device APIs under a certain tag.


## Parameter Descriptions
#### Request Parameters


| Parameter name | Type | Required | Description |
| -------- | ----- | -------- | ------------------------------------------------------------ |
| tag_list | array | Yes       | List of tags to be deleted: `"tag_list": ["test_tag_3_Ik0N0", "test_tag_2_Ik0N0"]` |


#### Response Parameters

| Field name   | Type    | Required | Comments                                                         |
| -------- | ------- | -------- | ------------------------------------------------------------ |
| seq | int64_t | Yes | The same as the request packet (if the request packet is invalid JSON, this field is 0) |
| ret_code | int32_t | Yes | Error code; for details, see the error codes table |
| err_msg  | string  | No       | Error message when an error occurs in the request                                         |
| result   | string  | No       | When the request is correct:<li>If there is extra data to be returned, the result will be encapsulated in the JSON of this field. If there is no extra data, there may be no such field. |


## Example

#### Sample Request
```json
{
    "tag_list": ["test_tag_3_Ik0N0", "test_tag_2_Ik0N0"]
}
```

#### Response Example
```json
{
    "ret_code": 0,
    "err_msg": "",
    "seq": 0,
    "result":{"":""}
}
```


