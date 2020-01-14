## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.
```shell
https://api.tpns.tencent.com/v3/statistics/get_push_record
```
**Feature**: This API queries the basic information and settings of a task according to its pushid.

## Parameter Descriptions
#### Request Parameters

| Parameter Name | Required | Type | Description |
| -------- | ---- | ------ | ---------- |
| pushId   | Yes   | string | Push task ID |

#### Response Parameters

| Parameter name | Type | Description |
| -------------- | --------- | ---------------------------------------- |
| retCode        | int       | Returned status code                              |
| errMsg | string | Error message |
| pushRecordData | JsonArray | Returned results, with pushRecordData structure variables shown in following table |

#### pushRecordData

| Parameter name         | Type               | Description                   | Value description                                                     |
| ---------------- | ------------------ | ---------------------- | ------------------------------------------------------------ |
| date             | string             | Push time               | Format: YYYY-MM-DD hh:mm:ss                                    |
| pushId           | int                | Message ID                 | -                                                            |
| title            | string             | Push title              | -                                                            |
| content          | string             | Push content               | -                                                            |
| status           | string             | Push status               | <li>PUSH_INIT //Task created<li>PUSH_WAIT; // Waiting for task to be scheduled<li>PUSH_STARTED; // Push started<li>PUSH_FINISHED; // Push finished<li>PUSH_FAILED; //Push failed<li>PUSH_CANCELED; // Push canceled by user<li>PUSH_DELETED; // Push deleted |
| pushType         | string             | Push target               | <li>all //Full push<li>tag //Tag push<li>token_list //Device list<li>account_list //Account list<li>package_account_push //Number package push |
| messageType      | string             | Push type               | <li>notify //Notification<li>message //Message                              |
| environment      | string             | Push environment               | <li>product //Production environment<li>dev //Development environment                         |
| expireTime       | uint32             | Expiration time               | Unit: second                                                       |
| xgMediaResources | string             | Rich media information             | -                                                            |
| multiPkg         | bool               | Multi-package-name push?         | -                                                            |
| targetList       | jsonArrary(string) | Push account or push device list | Valid when pushType is token_list or account_list                   |
| tagSet           | JsonObject         | Tag settings               | Valid when pushType is tag<br>Data structure:<br><code>{<br>"op":"OR", //Inter–tag logic operation<br>"tagWithType":[<br>{ "tagTypeName":"xg_user_define", //Tag type<br>"tagValue":"test68" //Tag value}<br>]<br>} </code>|
| uploadId         | uint32             | Number package ID               | Valid when pushType is package_account_push                         |
| pushConfig       | JsonObject         | Push configuration information           | <br>"Android": for specific push configuration information related to Android, refer to the following code<br>"iOS": for specific push configuration related to iOS, refer to the following code<br>|


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
 "pushId": "133703"
}
```

#### Response Example
```json
{
 "retCode": 0,
 "errMsg": "NO_ERROR",
 "pushRecordData": [
 {
 "date": "2019-07-25 20:06:28",
 "pushId": 133703,
 "title": "1",
 "content": "2",
 "status": "PUSH_FINISHED"
 "pushType":"tag",
 "targetList":null,
 "tagSet":{
 "op":"OR",
 "tagWithType":[
 {
 "tagTypeName":"xg_user_define",
 "tagValue":"test68"
 }
 ]
 },
 "uploadId":0,
 "expireTime":86400,
 "messageType":"notify",
 "xgMediaResources":"",
 "environment":"product",
 "pushConfig":{
 "android":{
 "ring":1,
 "vibrate":0,
 "lights":1,
 "clearable":1,
 "action":{
 "action_type":1
 },
 "custom_content":"{}"
 },
 "ios":null,
 },
 "multiPkg":false
 }
 ]
}
```

