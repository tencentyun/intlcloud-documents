

## API Description
**Request method**: POST.
```shell
https://api.tpns.tencent.com/v3/push/app
```
**API feature**: Push API is the general term for all push APIs. Push API has many types of push targets, which are described as follows.
All request parameters are uploaded via JSON encapsulation to the backend, which distinguishes among different push targets based on the request parameters. If there are any questions, see [Server Error Codes](https://cloud.tencent.com/document/product/548/39080).



## Parameter Descriptions
### Request parameters

#### Required parameters

The required push parameters refer to the parameters that must be carried in a push message.

| Parameter Name | Type | Required | Description |
| ------------- | ------ | ---- | ---------------------------------------- |
| audience_type | string | Yes | Push target: <li>all: full push <li>tag: tag push<li>token: single-device push <li>token_list: device list push <li>account: single-account push <li>account_list: account list push |
| message       | object | Yes | This is the message body; for more information, see [Message Body Types](#Message Body Types) |
| message_type | string | Yes | Message type: <li>notify: notification <li>message: pass-through or silent message |
| environment | string | Yes (only for iOS) | This specifies the push environment (only available for pushes on iOS): <li>product: production push environment <li>dev: development push environment |
| upload_id   | int32  | Yes (only available for number package push)        | Number package upload ID  |


#### audience_type: push target

Push target indicates which devices a push can be delivered to.

Push API provides a variety of push targets, such as all, tag, single device, device list, single account, and account list.

| Push Target     | Description         | Required Parameters and Use Description                                           |
| ------------ | ------------ | ------------------------------------------------------------ |
| all          | Full push    | None                                                           |
| tag         | Tag push    | `tag_list`<li>Push to devices with tag1 and tag2. `{"tags":["tag1","tag2"],"op":"AND"}`<li>Push to devices with tag1 or tag2. `{"tags":["tag1","tag2"],"op":"OR"}`<li>The tag list cannot contain more than 512 characters |
| token | Single-device push | `token_list` <li>If the parameter contains multiple tokens, it will only push to the first token <li>Format example: [“token1”] <li>The length of a token string cannot exceed 36 characters |
| token_list   | Device list group push | `token_list`<li>A maximum of 1000 tokens<li>Format example: ["token1","token2"]<li>The length of a token string cannot exceed 36 characters |
| account | Single-account push | `account_list` <li>If the parameter contains multiple accounts, it will only push to the first account <li>Format example: ["account1"] |
| account_list | Account list group push | `account_list` has a maximum of 1000 accounts. Format example: ["account1","account2"] |
|package_account_push | Number package push | Required for uploading number package pushes |

- Full push: Push to all devices
  ```json
  {
    "audience_type": "all"
  }
  ```
- Tag push: Push to devices with both tag1 and tag2 tags

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

- Single-device push: Push to devices with token1 as the token
  ```json
  {
    "audience_type": "token",
    "token_list": [
        "token1"
    ]
  }
  ```

- Device list push: Push to devices with token1 and token2 as their tokens
  ```json
  {
    "audience_type": "token_list",
    "token_list": [
        "token1",
        "token2"
    ]
  }
  ```
  
- Single-account push: Push to device(s) bound to account1
  ```json
  {
    "audience_type": "account",
    "account_list": [
        "account1"
    ]
  }
  ```

- Account list push: Push to device(s) bound to account1 and account2
  ```json
  {
    "audience_type": "account_list",
    "account_list": [
        "account1",
        "account2"
    ]
  }
  ```

<span id="消息体类型"></span>
#### message_type: message body type

For different platforms, the message types are slightly different; for details, see the table below:


| Message Type | Description | Supported Platform | Feature Description |
| -------- | ---------- | ------------- | -------------- |
| notify | Notification bar message | Android, iOS | The message is displayed in the notification bar |
| message | Pass-through or silent message | Android (pass-through message) <br>iOS (silent message) | Notifications are not displayed in the notification bar. Due to vendor restrictions, Android pass-through messages are only delivered through a self-built channel and cannot be delivered through the vendor channel |

#### message: message body

The message body is the message delivered to the client.

The Push API handles messages on iOS and Android differently, so you need to implement message pushes for the two platforms separately. The push message body is in JSON format.

#### General message on Android

The specific fields for the Android platform are as follows:

| Field Name | Type | Parent Project | Default Value | Required | Parameter Description |
| -----               | ------   | ----       |-----      |    ---- | ----------- ------------------------ |
| title                | string  |       message       | None          | Yes        | Message title|                                   |
| content        | string | message       |None    | Yes   | Message content                                     |
| accept_time    | jsonArray  | message       |None    | No    | The time period at which the message is allowed to be pushed to users. A single element consists of a start and end time with "start" and "end". "start" and "end" are indicated by hour and min. For details see the specific example. ⚠️Due to vendor restrictions, this is only effective on the self-built channel. |
| xg_media_resources    | string  | message       |None  | No    | Element address for image rich media. ⚠️Due to vendor restrictions, pushes containing rich media cannot be delivered through the vendor channel. All must be delivered through the self-built channel.|
| xg_media_audio_resources    | string  | message       |None  | No    | Element address for audio rich media. MP3 format audio supported. It is recommended that the content be smaller than 5M<br>⚠️Due to vendor restrictions, pushes containing rich media cannot be delivered through the vendor-specific channel. All must be delivered through the self-built channel. |
| xg_media_audio_resources    | string  | message       |None  | No    | Element address for audio rich media. MP3 format audio supported. It is recommended that the content be smaller than 5M<br>⚠️Due to vendor restrictions, pushes containing rich media cannot be delivered through the vendor-specific channel. All must be delivered through the self-built channel. |
| android              | JSON  | message      |None     |No    | Advanced setting structure for Android notifications. See the Android structure description for more information. |

#### Android structure description
| Field Name | Type | Parent Project | Default Value | Required | Parameter Description      |
| -----           | ------   | ----       |-----      |    ---- | ----------- ------------------------    |
| n_id           | int    | Android       |0    | No   | The unique identifier of the notification message object (only valid for the TPNS channel).<li>Greater than 0: Overrides the previous message with the same ID.<li>Equal to 0: Displays this notification and not affect other messages.<li>Equal to -1: All previous messages are cleared and only this message is shown. |
| builder_id | int | Android | 0 | No | Local notification style identifier |
| ring           | int    |Android      |1    | No    | Whether there’s a ringtone<li>0: no<li>1: yes             |
| ring_raw | string | Android | None | No | This specifies the name of the ringtone file in the raw directory of the Android project; no extension is needed |
| vibrate        | int    | 1    | No    | Whether the device vibrates<li>0: no<li>1: yes           |
| lights         | int    |Android       |1    | No    | Whether the breathing light is used <li>0: no <li>1: yes       |
| clearable | int | Android | 1 | No | Whether the notification bar can be dismissed. |
| icon_type | int | Android | 0 | No  | Whether the notification bar icon is an in-app icon or an uploaded icon <li>0: in-app icon <li>1: uploaded icon |
| icon_res | string | Android | None | No | In-app icon file name or URL address of the downloaded icon |
| style_id | int | Android | 1 | No | This specifies whether to override the notification style with the specified number |
| small_icon | string | Android | None | No | The icon that the message displays in the status bar. If not set, the app icon will be displayed. |
| action | JSON | Android | Yes | No | This sets the action after the notification bar is tapped; the default action is to open the app. |
| action_type| int | Action      |Yes   | No     | The tap action type. <li>1: opens activity or the app itself <li>2: opens browser<li>3: opens Intent             |
| custom_content | string | Android   |None    | No    | User-customized parameters. ⚠️Must be serialized as a string       |


Below is an example of a complete message:

```json
{
    "title": "xxx",
    "content": "xxxxxxxxx",
    "xg_media_resources": "xxx1" , // Enter the rich media element address, such as https://www.xx.com/img/bd_logo1.png?qua=high
    "xg_media_audio_resources":"xxx", //Enter the audio rich media element address, such as http://sc1.111ttt.cn/2018/1/03/13/396131227447.mp3 

    "accept_time": [
        {
            "start": {// Period start time,
                "hour": "13",// Start time, hours, value [0:24)
                "min": "00"// Start time, minutes, value [0:60)
            },
            "end": {// Period end time
                "hour": "14",// End time, hours, value [0:24)
                "min": "00" // End time, minutes, value [0:60)

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
            "intent": "xxx" // The SDK version must be 1.0.9 or higher. Configure the data tag in the client's intent and set the scheme attribute
        },
      "custom_content":"{\"key\":\"value\"}"
    }
}
```

#### Ordinary message on iOS

The specific fields for the iOS platform are as follows:


| Field Name | Type | Parent Project | Default Value | Required | Parameter Description  |
| ------ | ----------- | ---- || ---- | ---------------------------------------- |
| ios    | JSON       |message  | None    | Yes    | iOS message structure body. See iOS field descriptions for more information.  |
| xg_media_resources    | array     | message | None    | No    | Rich media element address                           |
| xg | string | message| None | No | key reserved by the system, which should not be used |



#### iOS field descriptions

| Field Name | Type | Parent Project | Default Value | Required | Parameter Description    |
| ------ | ----------- | |---- | ---- | ---------------------------------------- |
| aps   | JSON       |iOS | None    | No    | Message body field specific to Apple Push Notification service (APNs). For more information, see [Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1)|
| alert   | JSON       |aps | None    | Yes    | It contains the title and message content |
| badge_type  | int   |   aps  | None    | No    | The badge number displayed by the app |
| category  | string    |    aps| None    | No    | The action identifier displayed when the message is pulled down |
| mutable-content | int |     aps | None    | No    | This is a notification expansion parameter that carries "mutable-content" during push: 1 means that the Service Extension supports iOS10. After start-up, the push details will include the arrival data report. Before using this feature, develop the corresponding module according to the integration documentation. If this field is not carried, arrival data is not reported. |
| sound  | string      | None    | No    | The sound field is used as follows:<br>1: Playback system default prompt sound, "sound":"default"<br>2: Playback local custom ringtone, "sound":"chime.aiff"<br>3: Mute effect, "sound":"" or the instructions for removing custom ringtone from the sound field: the format must be Linear PCM, MA4 (IMA/ADPCM), alaw, or μLaw. Put the audio file in the project’s bundle directory. The duration should be less than 30 seconds, otherwise the system’s default ringtone will be used.|
| custom_content | string | None    | No    | Parameters for custom delivery. Must be serialized to string                                |


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
            "category": "INVITE_CATEGORY",
            "sound":"default",
            "mutable-content":1
        },
       "custom_content":"{\"key\":\"value\"}",
        "xg": "oops"
    }
}
```

#### Pass-through messages on Android

Pass-through message is unique to the Android platform and not displayed in the notification bar of the mobile phone. It can be used to deliver messages with control information to users in an imperceptible manner.

>Due to vendor restrictions, Android pass-through messages can only be delivered through the self-built channels and cannot be delivered through the vendor channels.

The specific fields for the Android platform are as follows:

| Field Name | Type | Parent Project | Default Value | Required | Parameter Description    |
| -------------- | ------ || ---- | ---- | ------------------------ |
| title                | string  |       message       | None          | Yes        | Command description |                                   |
| content        | string | message       |None    | Yes   | Command content |
| android              | JSON  | message      |None     |No    | Android message structure |
| custom_content | string | android  | None    | No    | Custom content                    |
| accept_time    | array | message       |None    | No    | The time period at which the message is allowed to be pushed to users. A single element is formed by a “start” time and an “end” time. "start" and "end" are indicated by hour and minute. For details, refer to the specific examples. ⚠️This is only valid for self-built channels due to vendor restrictions. |

Complete example:

```json
{
    "title": "this is title",
    "content": "this is content",
    "android": {
      "custom_content":"{\"key\":\"value\"}"
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

#### Silent messages on iOS

Similar to pass-through message on Android, silent message is unique to the iOS platform and not displayed. When the message arrives at the device, iOS will wake up the app for a period of time (less than 30 seconds) in the background to let the app handle the message logic.

The specific fields are as follows:

| Field Name | Type | Parent Project | Default Value | Required | Parameter Description |
| ------ | -----------| | ---- | ---- | ---------------------------------------- |
| aps    | JSON       | ios  | None    | Yes    | APNs-specific field, where the most important key-value pair is as follows:<br>content-available: it identifies the message type (which must be 1) and cannot contain alert, sound, or badge_type fields<br>For details, see [Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1) |
| ios    | JSON       |message  | None    | Yes    | iOS message structure  |
| custom_content | String | ios | None | No | Custom delivery parameter |
| xg | string | ios | None | No | key reserved by the system, which should not be used |



Complete example:
```json
{
    "ios":{
        "aps": {
            "content-available": 1
        },
      "custom_content":"{\"key\":\"value\"}",
        "xg": "oops"
    }
}
```

### Optional parameters

Optional Push API parameters are the optional advanced parameters except `audience_type`, `message_type`, and `message`.

| Parameter Name | Type | Parent Project | Required | Default Value | Description |
| ------------- | ------- || ---------------- | ------- | ---------------------------------------- |
| expire_time | int | None | No | 259200 (72 hours) | Offline message retention duration (in seconds), up to 72 hours. <li>If expire_time=0, it indicates real-time message <li>If expire_time is greater than 0 and less than 800 seconds, the system will reset it to 800 seconds <li>If expire_time >= 800 seconds, the message will be retained according to the actual set duration, up to 72 hours <li>The value set cannot exceed 2147483647; otherwise, the push will fail |
| send_time | string | None | No | Current system time | This specifies the push time: <li>The format is yyyy-MM-DD HH:MM:SS. <li>If it is less than the current server time, the message will be pushed immediately. <li>This field is supported only for full push and tag push. |
| multi_pkg | bool | None | No | false | Multi-package name push: for an app that has multiple channel packages (such as for MyApp and Wandoujia), if you want the mobile phone to receive the push message no matter what channel is used for app installation, then you need to set this value to true. |
| loop_param | json | None | No                | 0       | For details related to loop push (full push and tag push), see the loop_param field instructions in the following document. |
|badge_type     |int  |  iOS  |No                 |-1        | The user-configured badge number. This is only used on the iOS platform, and is put in the aps field. <li> -1: badge number does not change. <li> -2: badge number automatically increases by 1. <li> >=0: a custom badge number is configured.|
|group_id     |string   | None  | No                 |tpns_yyyymmdd, with yyyymmdd represents the push date       | Statistics tag, used for aggregated statistics|
| tag_list      | object | None | Only required for tag push           | None       | <li>Push to devices with tag1 and tag2: `{"tags":["tag1","tag2"],"op":"AND"}`<li>Push to devices with tag1 or tag2: `{"tags":["tag1","tag2"],"op":"OR"}` |
| account_list  | array  |None | Only required by single-account push and account list push | None       | For single-account push:<li>Requires `audience_type=account`<li>Parameter format: ["account1"]<br>For account list push: <li>Parameter format: `["account1","account2"]`<li>Up to 1,000 accounts |
| account_push_type  | int  |  None | Optional for single-account push         | 0       |<li> 0: push message to the latest device of the single account<li> 1: push message to all devices associated with the single account|
| token_list    | array   |None | Required by single-device push and device list push | None       | For single-device push: <li>audience_type must be token<li>Parameter format: ["token1"]<br>For device list push: <li>Parameter format: ["token1","token2"]<li>Up to 1,000 tokens |

#### loop_param parameter descriptions
| Field Name | Type | Required | Comments |
| -------- | ------- | ---- | ----------------------------------------          |
| startDate      | string | Yes    | Loop interval start date, with format of YYYY-MM-DD, such as 2019-07-01       |
| endDate      | string | Yes    | Loop interval end date, with format of YYYY-MM-DD, such as 2019-07-07       |
| loopType | int| Yes | Loop type: 1 = daily, 2 = weekly, 3 = monthly |
| loopDayIndexs | array | Yes   | For weekly loop, enter number of weeks [0-6], and enter days as 0. If it is [0, 1, 2], it indicates that the push will be done on Monday, Tuesday, and Wednesday every week.                                |
| dayTimes   | array  | Yes    | Specific push time, with the format as HH:MM:SS, such as ["19:00:00", "20:00:00"], indicates that the push will be done at 19:00 and 20:00 every day. |



### Response parameters

| Field Name | Type | Required | Comments |
| -------- | ------- | ---- | ----------------------------------------          |
| seq | int64_t | Yes | The same as the request packet (if the request packet is invalid JSON, this field is 0) |
| push_id | string | Yes | Push ID |
| ret_code | int32_t | Yes | Error code; for details, see the error codes table |
| environment | string | Yes | The push environment specified by the user (only for iOS). <li>product: production environment <li>dev: development environment |
| err_msg | string | No | Error message when an error occurs in the request |
| result | string | No | When the request is correct: <li>If there is extra data to be returned, the result will be encapsulated in the JSON of this field. <li>If there is no extra data, there may be no such field. |



## Example

#### Android tag push request message

```json
{
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
    "title": "Test title",
    "content": "Test content",
    "xg_media_resources": "xxx1" , // Enter the rich media element address, such as https://www.xx.com/img/bd_logo1.png?qua=high
    "xg_media_audio_resources":"xxx", //Enter the audio rich media element address, such as http://sc1.111ttt.cn/2018/1/03/13/396131227447.mp3 
    "accept_time": [
        {
            "start": {// Period start time,
                "hour": "13",// Start time, hours, value [0:24)
                "min": "00"// Start time, minutes, value [0:60)
            },
            "end": {// Period end time
                "hour": "14",// End time, hours, value [0:24)
                "min": "00" // End time, minutes, value [0:60)

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
            "intent": "xxx" // The SDK version must be 1.0.9 or higher. Configure the data tag in the client's intent and set the scheme attribute
        },
      "custom_content":"{\"key\":\"value\"}"
    }
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
#### iOS single-device push request message

```json
{
    "audience_type": "token",
    "environment":"dev",
    "token_list": [ "05da87c0ae5973bd2dfa9e08d884aada5bb2"],
    "message_type":"notify",
    "message":{
     "Title":"Push title",
    "content": "Push content",
    "ios":{
        "aps": {
            "alert": {
                "subtitle": "Push subtitle"
            },
            "badge_type": -2,
            "sound":"Tassel.wav",
            "category": "INVITE_CATEGORY"

        },
       "custom_content":"{\"key\":\"value\"}",
        "xg": "oops"
    }
 }
}
```
#### Single-device push response message

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


