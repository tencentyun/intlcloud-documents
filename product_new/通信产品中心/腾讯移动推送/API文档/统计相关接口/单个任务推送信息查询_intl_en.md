## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.
```shell
https://api.tpns.tencent.com/v3/statistics/get_push_record
```
**Feature**: this API is used to query the basic information and settings of a task by using its pushid.

## Parameter Description
#### Request parameters

| Parameter Name | Required | Type | Description |
| -------- | ---- | ------ | ---------- |
| pushId   | Yes   | string | Push task ID |

#### Response parameters

| Parameter Name       | Type      | Description                                     |
| -------------- | --------- | ---------------------------------------- |
| retCode        | int       | Returned status code                              |
| errMsg | string | Error message |
| pushRecordData | JsonArray | Returned results, with pushRecordData structure variables shown in following table |

#### pushRecordData

| Parameter Name         | Type               | Description                   | Value Description                                                     |
| ---------------- | ------------------ | ---------------------- | ------------------------------------------------------------ |
| date             | string             | Push time               | Format: YYYY-MM-DD hh:mm:ss                                    |
| pushId           | int                | Message ID                 | -                                                            |
| title            | string             | Push title              | -                                                            |
| content          | string             | Push content               | -                                                            |
| status           | string             | Push status               | <li>PUSH_INIT //Task created<li>PUSH_WAIT; // Waiting for task to be scheduled<li>PUSH_STARTED; // Push started<li>PUSH_FINISHED; // Push finished<li>PUSH_FAILED; //Push failed<li>PUSH_CANCELED; // Push canceled by user<li>PUSH_DELETED; // Push deleted |
| pushType         | string             | Push target               | <li>all //Full push<li>tag //Tag push<li>token_list //Device list<li>account_list //Account list<li>package_account_push //Number package push |
| messageType      | string             | Push type               | <li>notification //Notification<li>message //Message                              |
| environment      | string             | Push environment               | <li>product //Production environment<li>dev //Development environment                         |
| expireTime       | uint32             | Expiry time               | Unit: second                                                       |
| xgMediaResources | string             | Rich media information             | -                                                            |
| multiPkg         | bool               | Whether a push to multiple packages         | -                                                            |
| targetList       | jsonArrary(string) | Push account or push device list | Valid if `pushType` is `token_list` or `account_list`                   |
| tagSet           | JsonObject         | Tag settings | Valid if `pushType` is `tag`<br>Data structure:<br><code>{<br>"op":"OR", // Inter-tag logic operation<br>"tagWithType":[<br>{ "tagTypeName":"xg_user_define", // Tag type<br>"tagValue":"test68" // Tag value}<br>]<br>} </code>|
| uploadId         | uint32             | Number package ID               | Valid if `pushType` is `package_account_push`                         |
| pushConfig       | JsonObject         | Push configuration information           | <br>"Android": specific push configuration information related to Android. For details, please see the following code<br>"iOS": specific push configuration related to iOS. For details, please see the following code<br>|


## Configuration Information
#### Android push configuration information

```json
"android":{
 "ring":1, // Ring
 "vibrate":0, // Vibrate
 "lights":1, // LED indicator
 "clearable":1, // Whether clearable or not
 "action":{
 // Action type; 1. Open activity or application; 2. Open browser; 3. Open Intent
 "action_type":1
 },
 "custom_content":"{}" // Custom parameter
}
```

#### iOS push configuration information

```json
"ios":{
 "aps": {
 "alert": {
 "subtitle": "my subtitle"
 },
 "badge_type": 5, // Badge number displayed by application (optional). -2: auto-increment, -1: unchanged,
 "sound":"notification sound effect", // If this parameter is left empty, the default sound effect will be used
 "category": "INVITE_CATEGORY",
 "mutable-content" : 1
 }
}
```


## Samples
#### Sample request
```json
{
 "pushId": "133703"
}
```

#### Sample response
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

