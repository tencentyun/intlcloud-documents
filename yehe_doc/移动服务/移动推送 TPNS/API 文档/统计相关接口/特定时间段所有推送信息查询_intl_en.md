## API Description

**Request method**: POST
**Calling frequency limit**: 200 times/hour.

```plaintext
request address/v3/statistics/get_push_record
```
The API request address is corresponding to the service access point. Select the [request address](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.

**Feature**: this API is used to query the basic information and settings of all tasks within a specified time range.



## Parameter Description
#### Request parameters

| Parameter Name  | Required | Type   | Description       |
| --------- | ---- | ------ | ---------- |
| startDate | Yes   | String | Query start date,<li>Format: YYYY-MM-DD<li>Query limit: within the last 1 months |
| endDate | Yes | String | Query end date. Format: YYYY-MM-DD |
| msgType | No | String | Message type:<li>notify: notification<li>message: silent message |
| pushType | No | String | Push type:<li>all: full push<li>tag: tag push<li>token: device list/device single push<li>account: account list/account single push |
| offset | No | Integer | Start offset for paginated query |
| limit | No | Integer | Number of messages per page for paginated query (maximum value: 200) |

#### Response parameters

| Parameter Name       | Type      | Description                                     |
| -------------- | --------- | ---------------------------------------- |
| retCode        | Integer       | Returned status code                              |
| errMsg | String | Error message |
| pushRecordData | Array | Returned result, with `pushRecordData` structure variables shown in following table |
|count  | Integer  |  Number of eligible records  |

#### pushRecordData

| Parameter Name         | Type               | Description                   | Value Description                                                     |
| ---------------- | ------------------ | ---------------------- | ------------------------------------------------------------ |
| date             | String             | Push time               | Format: YYYY-MM-DD hh:mm:ss                                    |
| pushId           | String                | Message ID                 | -                                                            |
| title            | String             | Push title              | -                                                            |
| content          | String             | Push content               | -                                                            |
| status           | String             | Push status               | <li>PUSH_INIT //Task created<li>PUSH_WAIT// Waiting for task to be scheduled<li>PUSH_STARTED// Push started<li>PUSH_FINISHED// Push finished<li>PUSH_FAILED// Push failed<li>PUSH_CANCELED// Push canceled by user<li>PUSH_DELETED// Push deleted<li>PUSH_REVOKED// Push revoked<li>PUSH_COLLAPSED// Push overwritten<li>PUSH_DELETED_PUSH_MSG// Push terminated |
| pushType         | String             | Push target               | <li>all //Full push<li>tag //Tag push<li>token_list //Device list<li>account_list //Account list<li>package_account_push //Number package push |
| messageType      | String             | Push type               | <li>notification //Notification<li>message //Message                              |
| environment      | String             | Push environment               | <li>product //Production environment<li>dev //Development environment                         |
| expireTime       | Integer             | Expiration time               | Unit: second                                                       |
| xgMediaResources | String             | Rich media information             | -                                                            |
| multiPkg         | Boolean               | Whether it is multi-package name push         |  <li>true // Enable multi-package name push <li>false // Disable multi-package name push                                                            |
| targetList       | Array(String) | Push account or push device list | Valid if `pushType` is `token_list` or `account_list`                   |
| collapseID       | Integer  | Message overwriting ID | Valid if `pushType` is `all`, `tag`, or `package_account_push`                    |
| tagSet           | Object         | Tag settings               | Valid if `pushType` is `tag`<br>Data structure:<code><br>{<br>"op":"OR", // Inter-tag logic operation<br>"tagWithType":[<br>{ "tagTypeName":"xg_user_define", // Tag type<br>"tagValue":"test68" // Tag value}<br>]<br>}</code> |
| uploadId         | Integer             | Number package ID               | Valid if `pushType` is `package_account_push`                         |
| pushConfig       | Object         | Push configuration information           | <br>"Android": for specific push configuration information related to Android, please see the following code<br>"iOS": for specific push configuration related to iOS, please see the following code<br> |


## Configuration Information
#### Android push configuration information

```json
"android": {
        "ring": 1, // Ring     
        "vibrate": 1,// Vibrate
        "lights": 1,// LED indicator
        "clearable": 1, // Whether dismissible or not     
        "action": {
            "action_type": 3,// Action type; 1. open activity or application; 2. open browser; 3. open Intent         
            "intent": "" // The SDK version must be 1.0.9 or higher. Configure the data tag in the client's intent and set the scheme attribute
        },
      "custom_content":"{}"
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
            "category": "INVITE_CATEGORY",
            "sound":"default", // If this parameter is left empty, the default sound effect will be used
            "mutable-content":1
        },
```
## Samples

#### Sample request
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
#### Sample response


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
