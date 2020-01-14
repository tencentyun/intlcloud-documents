## API Description

**Request method**: POST
**Calling frequency limit**: 200 times/hour.
```shell
https://api.tpns.tencent.com/v3/statistics/get_push_record
```
**Feature**: This API queries the basic information and settings of all tasks within a specified time range.



## Parameter Descriptions
#### Request Parameters

| Parameter name  | Required | Type   | Description       |
| --------- | ---- | ------ | ---------- |
| startDate | Yes   | string | Start date of the query,<li>Format: YYYY-MM-DD<li>Query limit: within the last 3 months |
| endDate | Yes | string | End date of the query, format: YYYY-MM-DD |
| msgType | No | string | Message type:<li>notify: notification<li>message: silent message |
| pushType | No | string | Push type:<li>all: full push<li>tag: tag push<li>token: device list/device single push<li>account: account list/account single push |
| offset | No | int | Paged query starting offset |
| limit | No | int | Paged query number of messages by page (maximum 200) |

#### Response Parameters

| Parameter name       | Type      | Description                                     |
| -------------- | --------- | ---------------------------------------- |
| retCode        | int       | Returned status code                              |
| errMsg | string | Error message |
| pushRecordData | JsonArray | Returned results, with pushRecordData structure variables shown in following table |
|count  | int  |  Number of eligible records  |

#### pushRecordData

| Parameter name         | Type               | Description                   | Value description                                                     |
| ---------------- | ------------------ | ---------------------- | ------------------------------------------------------------ |
| date             | string             | Push time               | Format: YYYY-MM-DD hh:mm:ss                                    |
| pushId           | int                | Message ID                 | -                                                            |
| title            | string             | Push title              | -                                                            |
| content          | int                | Push content               | -                                                            |
| status           | string             | Push status               | <li>PUSH_INIT //Task created<li>PUSH_WAIT; // Waiting for task to be scheduled<li>PUSH_STARTED; // Push started<li>PUSH_FINISHED; // Push finished<li>PUSH_FAILED; //Push failed<li>PUSH_CANCELED; // Push canceled by user<li>PUSH_DELETED; // Push deleted |
| pushType         | string             | Push target               | <li>all //Full push<li>tag //Tag push<li>token_list //Device list<li>account_list //Account list<li>package_account_push //Number package push |
| messageType      | string             | Push type               | <li>notify //Notification<li>message //Message                              |
| environment      | string             | Push environment               | <li>product //Production environment<li>dev //Development environment                         |
| expireTime       | uint32             | Expiration time               | Unit: second                                                       |
| xgMediaResources | string             | Rich media information             | -                                                            |
| multiPkg         | bool               | Multi-package-name push?         | -                                                            |
| targetList       | jsonArrary(string) | Push account or push device list | Valid when pushType is token_list or account_list                   |
| tagSet           | JsonObject         | Tag settings               | Valid when pushType is tag<br>Data structure:<code><br>{<br>"op":"OR", //Inter–tag logic operation<br>"tagWithType":[<br>{ "tagTypeName":"xg_user_define", //Tag type<br>"tagValue":"test68" //Tag value}<br>]<br>}</code> |
| uploadId         | uint32             | Number package ID               | Valid when pushType is package_account_push                         |
| pushConfig       | JsonObject         | Push configuration information           | <br>"Android": for specific push configuration information related to Android, refer to the following code<br>"iOS": for specific push configuration related to iOS, refer to the following code<br> |


## Configuration Information
#### Android Push Configuration Information

```json
"android":{
 "ring":1, //ring
 "vibrate":0, //vibrate
 "lights":1, //breathing light
 "clearable":1, //whether clearable or not
 "action":{
 // Action type; 1. Open activity or app; 2. Open browser; 3. Open Intent
 "action_type":1
 },
 "custom_content":"{}" //custom parameter
}
```

#### iOS Push Configuration Information

```json
"ios":{
 "aps": {
 "alert": {
 "subtitle": "my subtitle"
 },
 "badge_type": 5, //badge number displayed by app (optional) -2 auto-increment，-1 unchanged,
 "sound":"notification sound effect", //default means the default sound effect
 "category": "INVITE_CATEGORY",
 "mutable-content" : 1
 }
}
```

## Example

#### Request Example
```json
{
 "limit": 50,
 "startDate": "2019-07-01",
 "endDate": "2019-08-01",
 "msgType": "notify",
 "pushType": "all",
 "offset": 0
}
```
#### Response Example
>Blind watermarking can protect against different kinds of image theft attacks such as clipping, smudging, and color change. The anti-theft effect is related to the original image size and the attack intensity. For more details, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

```json
{
    "retCode": 0,
    "errMsg": "NO_ERROR",
    "count": 126,
    "pushRecordData": [
        {
            "date": "2019-11-18 11:26:54",
            "pushId": "12",
            "title": "test title",
            "content": "test log",
            "status": "PUSH_FINISHED",
            "pushType": "all",
            "targetList": null,
            "tagSet": null,
            "uploadId": 0,
            "groupId": "",
            "expireTime": 43200,
            "messageType": "notify",
            "xgMediaResources": "",
            "environment": "product",
            "pushConfig": {
                "android": {
                    "n_id": 0,
                    "builder_id": 0,
                    "ring": 1,
                    "ring_raw": "",
                    "vibrate": 1,
                    "lights": 1,
                    "clearable": 1,
                    "icon_type": 0,
                    "icon_res": "",
                    "style_id": 0,
                    "small_icon": "",
                    "action": {
                        "action_type": 3,
                        "activity": "",
                        "aty_attr": null,
                        "browser": null,
                        "intent": ""
                    },
                    "custom_content": ""
                },
                "ios": null,
                "iot": null
            },
            "multiPkg": true,
            "source": "api"
        }
    ]
}
```
