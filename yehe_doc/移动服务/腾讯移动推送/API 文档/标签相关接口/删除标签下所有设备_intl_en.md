
## API Description

**Request method**: POST.
Each API request address corresponds to one service access point. Select the request address corresponding to service access point of your applications.

Service access point in Guangzhou:
```shell
https://api.tpns.tencent.com/v3/device/tag/delete_all_device
```
Service access point in Hong Kong (China):
```shell
https://api.tpns.hk.tencent.com/v3/device/tag/delete_all_device
```
Service access point in Singapore
```shell
https://api.tpns.sgp.tencent.com/v3/device/tag/delete_all_device
```
Service access point in Shanghai:

```shell
https://api.tpns.sh.tencent.com/v3/device/tag/delete_all_device
```
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


