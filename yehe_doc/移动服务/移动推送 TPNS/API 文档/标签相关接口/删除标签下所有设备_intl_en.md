
## API Description

```plaintext
request address/v3/device/tag/delete_all_device
```
The API request address is corresponding to the service access point. Select the [request address](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.


**Feature**: this API is used to delete all device APIs under a certain tag.


## Parameter Description

#### Request parameters


| Parameter Name | Type | Required | Description |
| -------- | ----- | -------- | ------------------------------------------------------------ |
| tag_list | Array | Yes       | List of tags to be deleted: `"tag_list": ["test_tag_3_Ik0N0", "test_tag_2_Ik0N0"]` |


#### Response parameters

| Field name   | Type    | Required | Comments                                                         |
| -------- | ------- | -------- | ------------------------------------------------------------ |
| seq | Integer | Yes | The same as the request packet (if the request packet is invalid JSON, this field is 0) |
| ret_code | Integer | Yes       | Error code. For more information, please see the error codes table                                 |
| err_msg  | String  | No       | Error message when an error occurs in the request                                         |
| result   | String  | No       | When the request is correct:<li>If there is extra data to be returned, the result will be encapsulated in the json of this field. If there is no extra data, <li>there may be no such field |


## Samples

#### Sample request
```json
{
    "tag_list": ["test_tag_3_Ik0N0", "test_tag_2_Ik0N0"]
}
```

#### Sample response
```json
{
    "ret_code": 0,
    "err_msg": "",
    "seq": 0,
    "result":{"":""}
}
```


