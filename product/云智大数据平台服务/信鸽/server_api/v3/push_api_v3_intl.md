# Push API v3

## Push API Overview

- Push API is a general term for all push APIs

- Push API has a variety of push targets as follows:
  - Full push
  - Tag push
  - Single-device push
  - Device list push
  - Single-account push
  - Account list push

- All push targets use the same URL to initiate the request (URL: `https://openapi.xg.qq.com/v3/push/app`).

- All request parameters are uploaded via JSON encapsulation to the backend, which distinguishes among different push targets based on the request parameters.

  

## Call Address

```text
https://openapi.xg.qq.com/v3/push/app
```



## Required Push API Parameters

The required push parameters refer to the parameters that must be carried in a push message.

| Parameter name | Type | Required | Description |
| ------------- | ------ | ---- | ---------------------------------------- |
| audience_type | string | Yes | Push target <br>1) all: full push <br>2) tag: tag push <br>3) token: single-device push <br>4) token_list: device list push <br> 5) account: single-account push <br> 6) account_list: account list push |
| platform | string | Yes | Client platform type <br>1) android: Android <br>2) ios: Apple iOS <br>3) all: Android and iOS, which is supported only for full push and tag push (reserved and not available yet) |
| message | object | Yes | Message body; for more information, see <a href="#message：消息体">Message Body</a> |
| message_type | string | Yes | Message type <br>1) notify: notification <br>2) message: passthrough/silent message |



### audience_type: Push Target

Push target indicates which devices a push can be delivered to.

Push API provides a variety of push targets, such as all, single device, device list, single account, and account list.

| Push target | Description | Usage |
| ------------ | ------ | ---------------------------------------- |
| all | Full push | None |
| tag | Tag push | `tag_list` <br>1) Push to devices with tag1 and tag2 <br>{“tags”:[“tag1”,”tag2”],”op”:”AND”} <br>2) Push to devices with tag1 or tag2 <br>{“tags”:[“tag1”,“tag2”],”op”:“OR”} <br>3) Tag list cannot exceed 512 characters |
| token | Single-device push | `token_list` <br>1) If the parameter contains multiple tokens, it will only push to the first token <br>2) Format example: [“token1”] <br>3) A token string cannot exceed 64 characters |
| token_list | Device list push | `token_list` <br>1) Up to 1,000 tokens <br>2) Format example: [“token1”,”token2”] <br>3) token string cannot exceed 64 characters <br>`push_id` <br>1) If 0 is entered for this parameter during the first push, the system will create the corresponding push task and return pushid: 123 <br>2) In subsequent pushes, if you enter 123 for push_id (with the same text copy), it indicates to use the text copy corresponding to 123 id for the push |
| account | Single-account push | `account_list` <br>1) If the parameter contains multiple account, it will only push to the first account <br>2) Format example: [“account1”] |
| account_list | Account list push | `account_list`<br>1) Up to 1,000 accounts 2) Format example: [“account1”,”account2”] <br>`push_id` <br>1) If 0 is entered for this parameter during the first push, the system will create the corresponding push task and return pushid: 123 <br>2) In subsequent pushes, if you enter 123 for push_id (with the same text copy), it indicates to use the text copy corresponding to 123 id for the push |

- Full push: Push to all devices

  ```json
  {
    "audience_type": "all"
  }
  ```

- Tag push: Push to devices with both "tag1" and "tag2"

  ```json
  {
    "audience_type": "tag",
    "tag_list": {
        "tags": [
            "tag1",
            "tag2"
        ],
        "op": "AND"
    }
  }
  ```

- Single-device push: Push to the device with token "token1"

  ```json
  {
    "audience_type": "token",
    "token_list": [
        "token1"
    ]
  }
  ```

- Device list push: Push to devices with token "token1" and "token2"

  ```json
  {
    "audience_type": "token_list",
    "token_list": [
        "token1",
        "token2"
    ],
    "push_id": "0"
  }
  ```

- Single-account push: Push to device with account "account1"

  ```json
  {
    "audience_type": "account",
    "account_list": [
        "account1"
    ]
  }
  ```

- Account list push: Push to devices with account "account1" and "account2"

  ```json
  {
    "audience_type": "account_list",
    "account_list": [
        "account1",
        "account2"
    ],
    "push_id": "0"
  }
  ```



### platform: Push Platform

Currently, TPNS supports push for Android and iOS platforms.

The keywords are "android", "ios". If you want to push for both platforms at the same time, the keyword is: "all".

- Push to both platforms:

  ```json
  {
    "platform": "all"
  }
  ```

- Push to the Android platform:

  ```json
  {
    "platform": "android"
  }
  ```

- Push to the iOS platform:

  ```json
  {
    "platform": "ios"
  }
  ```



### message_type: Message Body Type

For different platforms, the message types are slightly different; for details, see the table below:

| Message type | Description | Supported platform | Feature description |
| ------- | --------- | -------------------------- | -------- |
| notify | Notification bar message | Android, iOS | Message is displayed in the notification bar |
| message | Passthrough/silent message | Android (passthrough message) <br>iOS (silent message) | Message is not displayed in the notification bar |



### message: Message Body

The message body, i.e., the message delivered to the client.

The Push API handles messages on iOS and Android differently, so you need to implement message pushes for the two platforms separately. The push message body is in JSON format.

#### General Message on Android

The specific fields for the Android platform are as follows:

| Field name | Type | Default value | Required | Parameter description |
| -------------- | ------ | ---- | ---- | ---------------------------------------- |
| title | string | None | Yes | Message title |
| content | string | None | Yes | Message content |
| accept_time | array | None | No | This specifies during which time periods the message will be pushed to users; it is recommended to specify less than 10 ones; and this parameter cannot be null |
| xg_media_resources | string | None | No | Rich media element addresses; up to 5 ones recommended (only for SDK v4.2.0 and higher) |
| n_id           | int    | 0    | No | Unique identifier of the notification message object (only valid for the TPNS channel) <br>1) If greater than 0, it will override the previous message with the same id <br>2) If 0, it will display this notification and not affect other messages <br>3) If -1, it will clear all previous messages and only display this message |
| builder_id | int | 0 | No | Local notification style identifier |
| ring | int | 1 | No | Whether there a ringtone <br>1) 0: No <br>2) 1: Yes |
| ring_raw | string | None | No | This specifies the name of the ringtone file in the raw directory of the Android project; no extension is needed |
| vibrate | int | 1 | No | Whether to use vibration <br>1) 0: No <br>2) 1: Yes |
| lights | int | 1 | No | Whether to use breathing light <br>1) 0: No <br>2) 1: Yes |
| clearable | int | 1 | No | Whether the notification in the notification bar can be dismissed |
| icon_type | int | 0 | No| Whether the notification bar icon is an in-app icon or an uploaded icon <br>1) 0: In-app icon <br>2) 1: Uploaded icon |
| icon_res | string | None | No | In-app icon file name or URL address of the downloaded icon |
| style_id | int | 1 | No | This specifies whether to override the notification style with the specified number |
| small_icon | string | None | No | The icon that the message displays in the status bar. If not set, the app icon will be displayed |
| action | JSON | Yes | No | This sets the action after the notification bar is tapped; the default action is to open the app |
| custom_content | JSON | None | No | User-defined key-value pair |

Below is an example of a complete message:

```json
{
    "title": "xxx",
    "content": "xxxxxxxxx",
    "xg_media_resources": "xxx1" , // Enter the rich media element address, such as https://www.xx.com/img/bd_logo1.png?qua=high

    "accept_time": [
        {
            "start": {
                "hour": "13",
                "min": "00"
            },
            "end": {
                "hour": "14",
                "min": "00"
            }
        },
        {
            "start": {
                "hour": "00",
                "min": "00"
            },
            "end": {
                "hour": "09",
                "min": "00"
            }
        }
    ],
    "android": {
        "n_id": 0,
        "builder_id": 0,
        "ring": 1,
        "ring_raw": "ring",
        "vibrate": 1,
        "lights": 1,
        "clearable": 1,
        "icon_type": 0,
        "icon_res": "xg",
        "style_id": 1,
        "small_icon": "xg",
        "action": {
            "action_type": 1,// Action type; 1. Open activity or app; 2. Open browser; 3. Open Intent
            "activity": "xxx",
            "aty_attr": {// activity attribute, only for action_type=1
                "if": 0, // Intent's Flag attribute
                "pf": 0  // PendingIntent's Flag attribute
            },
            "browser": {
                "url": "xxxx ", // Only http and https are supported
                "confirm": 1 // Whether user confirmation is required
            },
            "intent": "xxx" // The SDK version must be 3.2.3 or higher. Configure the data tag in the client's intent and set the scheme attribute
        },
        "custom_content": {
            "key1": "value1",
            "key2": "value2"
        }
    }
}
```

#### General Message on iOS

The specific fields for the iOS platform are as follows:

| Field name | Type | Default value | Required | Parameter description |
| ------ | ----------- | ---- | ---- | ---------------------------------------- |
| aps | JSON | None | Yes | APNs-specific message body field, where important key-value pairs include: <br>alert: It contains the title and message content (required) <br>badge_type: The badge number displayed by the app (optional) <br>category: The action identifier displayed when the message is pulled down (optional) <br>For details, see [Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1) |
| custom | string/JSON | None | No | Custom delivery parameter |
| xg | string | None | No | key reserved by the system, which should not be used |


Below is an example of a complete message:

```json
{
    "title": "xxx",
    "content": "xxxxxxxxx",
    "ios":{
        "aps": {
            "alert": {
                "subtitle": "my subtitle"
            },
            "badge_type": 5,
            "category": "INVITE_CATEGORY"
        },
        "custom1": "bar",
        "custom2": [
            "bang",
            "whiz"
        ],
        "xg": "oops"
    }
}
```

#### Passthrough Message on Android

Passthrough message is unique to the Android platform and not displayed in the notification bar of the mobile phone. It can be used to deliver messages with control information to users in an imperceptible manner.

The specific fields for the Android platform are as follows:

| Field name | Type | Default value | Required | Parameter description |
| -------------- | ------ | ---- | ---- | ------------------------ |
| title | string | None | Yes | Message title |
| content | string | None | Yes | Message content |
| custom_content | JSON | None | No | Custom content |
| accept_time | array | None | No | This specifies during which time periods the message will be pushed to users; and it is recommended to specify less than 10 ones |

Complete example:

```json
{
    "title": "this is title",
    "content": "this is content",
    "android": {
       "custom_content": {
          "key1": "value1",
          "key2": "value2"
             }
    },
    "accept_time": [
        {
            "start": {
                "hour": "13",
                "min": "00"
            },
            "end": {
                "hour": "14",
                "min": "00"
            }
        },
        {
            "start": {
                "hour": "00",
                "min": "00"
            },
            "end": {
                "hour": "09",
                "min": "00"
            }
        }
    ]
}
```

#### Silent Message on iOS

Similar to passthrough message on Android, silent message is unique to the iOS platform and not displayed. When the message arrives at the device, iOS will wake up the app for a period of time (less than 30 seconds) in the background to let the app handle the message logic.

The specific fields are as follows:

| Field name | Type | Default value | Required | Parameter description |
| ------ | ----------- | ---- | ---- | ---------------------------------------- |
| aps | JSON | None | Yes | APNs-specific field, where the most important key-value pair is as follows <br>content-available: It identifies the message type (which must be 1) and cannot contain alert, sound, or badge_type fields <br>For details, see [Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1) |
| custom | string/JSON | None | No | Custom delivery parameter |
| xg | string | None | No | key reserved by the system, which should not be used |



Complete example:

```json
{
    "ios":{
        "aps": {
            "content-available": 1
        },
        "custom": {
            "key1": "value1",
            "key2": "value2"
        },
        "xg": "oops"
    }
}
```

### Optional Push API Parameters

Optional Push API parameters are the optional advanced parameters except `audience_type`, `platform`, `message_type`, and `message`.

| Parameter name | Type | Required | Default value | Description |
| ------------- | ------- | ---------------- | ------- | ---------------------------------------- |
| expire_time | int | No | 259200 (72 hours) | Offline message retention duration (in seconds), up to 72 hours <br>1) If expire_time=0, it indicates real-time message <br>2) If expire_time is greater than 0 and less than 800 seconds, the system will reset it to 800 seconds <br>3) If expire_time >= 800 seconds, the message will be retained according to the actual set duration, up to 72 hours <br>4) The value set cannot exceed 2147483647; otherwise, the push will fail |
| send_time | string | No | Current system time | This specifies the push time <br>1) The format is yyyy-MM-DD HH:MM:SS <br>2) If it is smaller than the current server time, the message will be pushed immediately <br>3) This field is supported only for full push and tag push |
| multi_pkg | bool | No| false | Multi-package name push <br>1) For an app that has multiple channel packages (such as for MyApp and Wandoujia), if you want the mobile phone to receive the push message no matter what channel is used for app installation, then you need to set this value to true |
| loop_times | int | No | 0 | Task repetitions <br>1) This is supported only for full push and tag push <br>2) Recommended value range: [1, 15] |
| loop_interval | int | No | 0 | Interval for looping message delivery <br>1) It must be used together with loop_times <br>2) In days, value range: [1, 14] <br>3) loop_times and loop_interval together indicate the loop rule for the message delivery task |
| environment | string | Yes (only for iOS) | product | This specifies the push environment (only available for pushes on iOS) <br>1) product: Production push environment <br>2) dev: Development push environment |
| badge_type | int | No | -1 | This specifies the badge number in the aps field (only for iOS) <br>1) -1: Badge number does not change <br>2) -2: Badge number is automatically increased by 1 <br>3) >=0: Set "custom" badge number |
| stat_tag | string | No | None | Statistics tag for aggregated statistics <br>Usage scenario (example): There is now one event id: active_picture_123, and you need to deliver a message via the single push API (or list push API) to 10,000 devices, and set this field to active_picture_123. After the push is completed, you can use the v3 statistics querying API to query the actual deliveries, arrivals, displays and taps for the 10,000 devices according to the active_picture_123 tag |
| seq | int64_t | No | 0 | When the API is called, TPNS will return this field in the response packet, which can be used for async request <br>Usage scenario: In async service, the corresponding response packet returned by the server can be found through this field |
| tag_list      | object  | Only required by tag push          | None       | 1) Push to devices with tag1 and tag2: {“tags”:[“tag1”,”tag2”],”op”:”AND”} <br>2) Push to devices with tag1 or tag2:  {“tags”:[“tag1”,“tag2”],”op”:“OR”} |
| account_list  | array   | Only required by single-account push and account list push  | None       | For single-account push <br>1)  audience_type must be account <br>2) Parameter format: [“account1”] <br>For account list push <br>1) Parameter format: [“account1”,”account2”] <br>2) Up to 1,000 accounts |
| account_push_type | int | Optional for single-account push | 0 |1) 0: Push message to the latest device of the single account <br>2) 1: Push message to all device associated with the single account |
| account_type | int | Optional for single-account push | 0 | 1) Account type (see the account description below) <br> 2) It must be the same as the account type set when the account is bound |
| token_list | array | Required by single-device push and device list push | None | For single-device push <br>1)  audience_type must be token <br>2) Parameter format: [“token1”] <br>For device list push <br>1) Parameter format: [“token1”,”token2”] <br>2) Up to 1,000 tokens |
| push_id       | string  | Required by account list push and device list push | None | For account list push and device list push, if 0 is entered for this parameter during the first push, the system will create the corresponding push task and return the corresponding pushid: 123. In subsequent pushes, if you enter 123 for push_id (with the same text copy), it indicates to use the text copy corresponding to 123 id for the push. (Note: The validity period of the text copy is determined by the expire_time field above) |



### Push API Response Parameters

| Field name | Type | Required | Comments |
| -------- | ------- | ---- | ----------------------------------------          |
| seq | int64_t | Yes | The same as the request packet (if the request packet is invalid JSON, this field is 0) |
| push_id | string | Yes | Push id |
| ret_code | int32_t | Yes | Error code; for details, see the error codes table |
| environment | string | Yes | This specifies the push environment (only for iOS) <br>product: Production environment <br>dev: Development environment |
| err_msg | string | No | error message when an error occurs in the request |
| result | string | No | When the request is correct, if there is extra data to be returned, the result will be encapsulated in the json of this field. If there is no extra data, there may be no such field |



### Complete Example of Push API Request

#### Android Tag Push Request Message

```json
POST /v3/push/app HTTP/1.1
Host: openapi.xg.qq.com
Content-Type: application/json
Authorization: Basic YTViNWYwNzFmZjc3YTplYTUxMmViNzcwNGQ1ZmI1YTZhOTM3Y2FmYTcwZTc3MQ==
Cache-Control: no-cache
Postman-Token: 4b82a159-afdd-4f5c-b459-de978d845d2f
{
    "platform": "android",
    "audience_type": "tag",
    "tag_list": {
        "tags": [
            "tag1",
            "tag2"
        ],
        "op": "AND"
    },
    "message_type": "notify",
    "message": {
        "title": "this is title",
        "content": "this is content",
        "custom_content": {
            "key1": "value1",
            "key2": "value2"
        },
        "accept_time": [
            {
                "start": {
                    "hour": "13",
                    "min": "00"
                },
                "end": {
                    "hour": "14",
                    "min": "00"
                }
            }
        ]
    }
}
```

#### Tag Push Response Message

```json
{
    "seq": 0,
    "environment": "product",
    "ret_code": 0,
    "push_id": "3895624686"
}
```
### iOS Single-device Push Request Message

```json

POST /v3/push/app HTTP/1.1
Host: openapi.xg.qq.com
Content-Type: application/json
Authorization: Basic ODhjNzE1Mzc1MDQ0ZDowNGM4NmNhZmI0ZTMxZDU4M2UzYjg0M2VhMDc4YTU5ZQ==
Cache-Control: no-cache
Postman-Token: 71670b5b-3149-4883-a427-d75cf9f42188

{
 
    "platform": "ios",
    "audience_type": "token",
    "environment":"dev",
    "token_list": [ "55c2ddba664e9abcacea7daab0887939893b18e1a2cf4475c5382f5bcb2ab25b"],
    "message_type":"notify",
    "message":{
     "title": "xxx",
    "content": "https://xg.qq.com/docs/ios_access/ios_faq.html",
    "ios":{
        "aps": {
            "alert": {
                "subtitle": "my subtitle"
            },
            "badge_type": -2,
            "sound":"Tassel.wav",
            "category": "INVITE_CATEGORY"
            
        },
        "custom1": "bar",
        "custom2": [
            "bang",
            "whiz"
        ],
        "xg": "oops"
    }
 }
}
```
#### Single-device Push Response Message

```json
{
    "seq": 0,
    "push_id": "427184209",
    "ret_code": 0,
    "environment": "dev",
    "err_msg": "",
    "result": "[0]"
}
```


## Account Type

The account type is bound by calling the SDK API by the client. The types are as shown in the table below:

| Account type | Meaning |
| ------ | --------- |
| 0 | Unknown |
| 1 | Mobile number |
| 2 | Email |
| 1000 | WeChat openid |
| 1001 | QQ openid |
| 1002 | Sina Weibo |
| 1003 | Alipay |
| 1004 | Taobao |
| 1005 | Douban |
| 1006 | Facebook |
| 1007 | Twitter |
| 1008 | Google |
| 1009 | Baidu |
| 1010 | JD |
| 1011 | LinkedIn |
| 1999 | Other |
| 2000 | Visitor login |
| 2001 or above | User-defined |



## Error Codes

There are many REST APIs in TPNS. You may encounter various problems when using them. Below are the common error codes and their definitions, which correspond to the ret_code field in the <a href="#通用基础返回值">General Basic Return Values</a>.

| Error code | Meaning |
| ----- | --------------------- |
| 10100 | System busy. Please retry later |
| 10101 | System busy. Please retry later |
| 10102 | Parameter is missing. Please check and retry |
| 10103 | Parameter value is invalid. Please check and retry |
10104 | Authentication failed. Please check the secret key |
| 10105 | Invalid certificate |
| 10106 | The current push type does not support multi-platform push |
| 10107 | Message body is in invalid JSON format |
| 10108 | Internal error. Please retry later |
| 10109 | Internal error. Please retry later |
| 10110 | Device not registered |
| 10111 | Internal error. Please retry later |
| 10112 | Internal error. Please retry later |
| 10113 | Internal error. Please retry later |
| 10114 | Internal error. Please retry later |
| 10115 | Account cannot be empty |
| 10116 | The account does not exist |
| 10117 | Push content too large |
| 10201 | Failed to create push task. Please retry |
| 10202 | Failed to convert the push message content to APNs |
| 10203 | Failed to create push task. Please retry |
| 10204 | Push failed. Please retry later |
| 10205 | Push task expired. Please check           |
| 10206 | Failed to get a copy of the message. Please retry later       |
| 10207 | Failed to get a copy of the message. Please retry later       |
| 10301 | Account list push failed. Please retry |
| 10302 | Account list push partially failed. Please check whether the failed accounts have been bound to devices           |
| 10303 | Account list push completely failed. Please check whether the accounts have been bound to devices
| 10304 | Token List push partially failed. Please check whether the failed devices have been normally registered       |
| 10305 | Token List push completely failed. Please check whether the devices have been normally registered
| 10401 | Internal error. Please retry later           |
| 10402 | Internal error. Please retry later           |
| 10403 | Internal error. Please retry later           |
| 10404 | Internal error. Please retry later           |
| 10405 | Internal error. Please retry later           |
| 10406 | Internal error. Please retry later           |
| 10407 | Internal error. Please retry later           |
| 10501 | Internal error. Please retry later           |
| 10502 | Internal error. Please retry later           |
| 10503 | Internal error. Please retry later           |
| 10504 | Internal error. Please retry later           |
| 10505 | Internal error. Please retry later           |
| 10506 | Internal error. Please retry later           |
| 10507 | Internal error. Please retry later           |
| 10601 | Internal error. Please retry later           |
| 10602 | Internal error. Please retry later           |
| 10603 | Internal error. Please retry later           |
| 10604 | Internal error. Please retry later           |
| 10605 | Internal error. Please retry later           |
| 10606 | App not registered. Please register and retry |
| 10701 | Internal error. Please retry later |
| 10702 | Internal error. Please retry later           |
| 10707 | Internal error. Please retry later           |
| 10708 | Internal error. Please retry later           |
| 10709 | Internal error. Please retry later           |
| 10710 | Internal error. Please retry later           |
| 10711 | Internal error. Please retry later           |
| 10712 | Internal error. Please retry later           |
| 10713 | Internal error. Please retry later           |
| Other | Unknown error. Please retry later |
