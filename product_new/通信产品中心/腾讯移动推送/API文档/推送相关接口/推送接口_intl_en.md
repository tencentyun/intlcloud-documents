

### API Description
**Request method**: POST.

```shell
https://api.tpns.tencent.com/v3/push/app
```
**Description**: Push API is the general term for all push APIs. Push API has many types of push targets, which are described as follows.
All request parameters are uploaded via JSON encapsulation to the backend, which distinguishes among different push targets based on the request parameters. If there are any questions, see [Service Error Codes](https://intl.cloud.tencent.com/document/product/1024/33763).



## Parameter Descriptions
### Request Parameters

#### Required Parameters

The required push parameters refer to the parameters that must be carried in a push message.

| Parameter name | Type | Required | Description |
| ------------- | ------ | ---- | ---------------------------------------- |
| audience_type | string | Yes    | Push target:<li>all: full push<li>tag: tag push<li>token: single-device push<li>token_list: device list push<li>account: single-account push<li>account_list: account list push |
| message       | object | Yes    | This is the message body; see [Message Body Types](#Message Body Types) |
| message_type  | string | Yes    | Message type:<li>notify: notification<li>message: passthrough/silent message |
| environment   | string  | Yes (only for iOS)                |  This specifies the push environment (only available for pushes on iOS):<li>product: production push environment<li>dev: development push environment |
| upload_id   | int32  | Yes (only available for number package push)                | Number package upload ID  |


#### audience_type: Push Target

Push target indicates which devices a push can be delivered to.

Push API provides a variety of push targets, such as all, tag, single device, device list, single account, and account list.

| Push target     | Description         | Required parameters and instructions                                           |
| ------------ | ------------ | ------------------------------------------------------------ |
| all          | Full push     | None                                                           |
| tag          | Tag push     | `tag_list`<li>Push to devices with tag1 and tag2`{"tags":["tag1","tag2"],"op":"AND"}`<li>Push to devices with tag1 or tag2`{"tags":["tag1","tag2"],"op":"OR"}`<li> Tag list cannot exceed 512 characters |
| token        | Single-device push   | `token_list`<li>If the parameter contains multiple tokens, it will only push to the first token<li>Format example: [“token1”]<li>A token string cannot exceed 36 characters |
| token_list   | Device list group push | `token_list`<li>Up to 1,000 tokens<li>Format example:["token1","token2"]<li>A token string cannot exceed 36 characters |
| account      | Single-account push   | `account_list`<li>If the parameter contains multiple accounts, it will only push to the first account<li>Format example:["account1"] |
| account_list | Account list group push | `account_list`Up to 1,000 accounts. Format example:["account1","account2"] |
| package_account_push | Number package push | Upload number package push is required |

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

<span id="Message Body Type"></span>
#### message_type: Message Body Type

For different platforms, the message types are slightly different; for details, see the table below:


| Message type | Description | Supported platform | Feature description |
| -------- | ---------- | ------------- | -------------- |
| notify | Notification bar message | Android & iOS | Message is displayed in the notification bar |
| message | Passthrough/silent message | Android (passthrough message)<br>iOS (silent message) | Notification bar does not display message, and due to vendor limitations, Android passthrough messages are only delivered through a self-built channel and cannot be delivered through the vendor-specific channel|

#### message: Message Body

The message body is the message delivered to the client.

The Push API handles messages on iOS and Android differently, so you need to implement message pushes for the two platforms separately. The push message body is in JSON format.

#### General Message on Android

The specific fields for the Android platform are as follows:

| Field name | Type | Default value | Required | Parameter description |
| -------------- | ------ | ---- | ---- | ---------------------------------------- |
| title | string | None | Yes | Message title |
| content | string | None | Yes | Message content |
| accept_time    | jsonArray  | None    | No    | This is the time period when the message is allowed to be pushed to users. A single element is formed by a “start” time and an “end” time. The times of its “start” and “end” are defined using hours and minutes. For details, refer to the specific examples.⚠️This is only valid for self-built channels due to vendor limitations.                 |
| xg_media_resources    | string  | None    | No    | This is the image rich media element address. ⚠️Due to vendor limitations, pushes that included rich media cannot be delivered through the vendor-specific channel and must all be delivered through the self-built channel. |
| xg_media_audio_resources    | string  | None    | No    | This is the audio rich media element address, which supports audio in mp3 format. It is recommended that the size be kept smaller than 5M.<br>⚠️Due to vendor limitations, pushes that included rich media cannot be delivered through the vendor-specific channel and must all be delivered through the self-built channel. |
| n_id           | int    | 0    | No    | This is the unique identifier of the notification message object (only valid for the TPNS channel).<li>If greater than 0, it will override the previous message with the same ID.<li>If 0, it will display this notification and not affect other messages.<li>If -1, it will clear all previous messages and only display this message. |
| builder_id | int | 0 | No | Local notification style identifier |
| ring           | int    | 1    | No    | Whether there’s a ringtone<li>0: no<li>1: yes             |
| ring_raw | string | None | No | This specifies the name of the ringtone file in the raw directory of the Android project; no extension is needed |
| vibrate        | int    | 1    | No    | Whether to use vibrate<li>0: no<li>1: yes           |
| lights         | int    | 1    | No    | Whether to use breathing light<li>0: no<li>1: yes      |
| clearable | int | 1 | No | Whether the notification in the notification bar can be dismissed. |
| icon_type      | int    | 0    | No    | Whether the notification bar icon is an in-app icon or an uploaded icon<li>0: in-app icon<li>1: uploaded icon |
| icon_res       | string | None    | No    | In-app icon file name or URL address of the downloaded icon                     |
| style_id | int | 1 | No | This specifies whether to override the notification style with the specified number |
| small_icon | string | None | No | The icon that the message displays in the status bar. If not set, the app icon will be displayed. |
| action         | JSON   | Yes    | No    | This sets the action after the notification bar is tapped; the default action is to open the app.   |
| action_type| int | Yes    | No    | Click action type,<li>1: opens activity or App itself<li>2: opens browser<li>3: opens Intent             |
| custom_content | string | None    | No    | Parameters customized by user, ⚠️ requires to be serialized to string       |


Below is an example of a complete message:

```json
{
    "title": "xxx",
    "content": "xxxxxxxxx",
    "xg_media_resources": "xxx1" , // Enter the rich media element address, such as https://www.xx.com/img/bd_logo1.png?qua=high
    "xg_media_audio_resources":"xxx", //Enter the audio rich media element address, such as http://sc1.111ttt.cn/2018/1/03/13/396131227447.mp3 

    "accept_time": [
        {
            "start": {//Period start time,
                "hour": "13",//Start time, hours, value [0:24)
                "min": "00"// Start time, minutes, value [0:60)
            },
            "end": {//Period end time
                "hour": "14",//End time, hours, value [0:24)
                "min": "00" //End time, minutes, value [0:60)

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

#### General Message on iOS

The specific fields for the iOS platform are as follows:


| Field name | Type | Default value | Required | Parameter description |
| ------ | ----------- | ---- | ---- | ---------------------------------------- |
| aps    | JSON        | None    | Yes    | Refer to the  aps field instructions. For a detailed explanation, see [Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1) |
| custom_content | string | None    | No    | Parameters customized by user, requires to be serialized to string                                |
| xg_media_resources    | array      | None    | No    | Rich media element address                          |
| xg     | string      | None    | No    | Key reserved by the system, which should not be used            |



#### Aps Field Instructions

| Field name | Type | Default value | Required | Parameter description |
| ------ | ----------- | ---- | ---- | ---------------------------------------- |
| alert   | JSON        | None    | No    | It contains the title and message content |
| badge_type  | int        | None    | No    | The badge number displayed by the app |
| category  | string        | None    | No    | The action identifier displayed when the message is pulled down |
| mutable-content | int       | None    | No    | This is a notification expansion parameter that carries "mutable-content" during push: 1 means that the Service Extension of iOS10 is supported. After start-up, the push details will include the arrival and click data report. Before using this feature, develop the corresponding module according to the integration documentation. If it does not contain this field, then it means there is no arrival data report.|
| sound  | string      | None    | No    | The sound field is used as follows:<br>1: Playback system default prompt sound, "sound":"default"<br>2: Playback local custom ringtone, "sound":"chime.aiff"<br>3: Mute effect, "sound":"" or the instructions for removing the sound field<br>  Custom ringtone descriptions: the format must be Linear PCM, MA4 (IMA/ADPCM), alaw, or μLaw. The audio file is placed in the project bundle directory, and the length must be less than 30s, or else the system default ringtone will be used.|


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

#### Passthrough Message on Android

Passthrough message is unique to the Android platform and not displayed in the notification bar of the mobile phone. It can be used to deliver messages with control information to users in an imperceptible manner.

> Due to vendor limitations, Android passthrough messages can only be delivered through the self-built channels and cannot be delivered through the vendor-specific channels.

The specific fields for the Android platform are as follows:

| Field name | Type | Default value | Required | Parameter description |
| -------------- | ------ | ---- | ---- | ------------------------ |
| title | string | None | Yes | Message title |
| content | string | None | Yes | Message content |
| custom_content | string   | None    | No    | Custom content                    |
| accept_time    | array  | None    | No    | This is the time period when the message is allowed to be pushed to users. A single element is formed by a “start” time and an “end” time. The times of its “start” and “end” are defined using hours and minutes. For details, refer to the specific examples.⚠️This is only valid for self-built channels due to vendor limitations.  |

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

#### Silent Message on iOS

Similar to passthrough message on Android, silent message is unique to the iOS platform and not displayed. When the message arrives at the device, iOS will wake up the app for a period of time (less than 30 seconds) in the background to let the app handle the message logic.

The specific fields are as follows:

| Field name | Type | Default value | Required | Parameter description |
| ------ | ----------- | ---- | ---- | ---------------------------------------- |
| aps    | JSON        | None    | Yes    | APNs-specific field, where the most important key-value pair is as follows:<br>content-available: it identifies the message type (which must be 1) and cannot contain alert, sound, or badge_type fields<br>For details, see [Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1) |
| custom | string | None | No | Custom delivery parameter |
| xg | string | None | No | key reserved by the system, which should not be used |



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

### Optional Parameters

Optional Push API parameters are the optional advanced parameters except `audience_type`, `platform`, `message_type`, and `message`.

| Parameter name | Type | Required | Default value | Description |
| ------------- | ------- | ---------------- | ------- | ---------------------------------------- |
| expire_time| int     | No                | 259200 (72 hours) | Offline message retention duration (in seconds), up to 72 hours<li>If expire_time=0, it indicates real-time message<li>If expire_time is greater than 0 and less than 800 seconds, the system will reset it to 800 seconds<li>If expire_time >= 800 seconds, the message will be retained according to the actual set duration, up to 72 hours <li>The value set cannot exceed 2147483647; otherwise, the push will fail|
| send_time     | string  | No                | Current system time  | This specifies the push time:<li>The format is yyyy-MM-DD HH:MM:SS.<li>If it is smaller than the current server time, the message will be pushed immediately.<li>This field is supported only for full push and tag push. |
| multi_pkg     | bool    | No                | false   | Multi-package name push: for an app that has multiple channel packages (such as for MyApp and Wandoujia), if you want the mobile phone to receive the push message no matter what channel is used for app installation, then you need to set this value to true. |
| loop_param | json   | No                | 0       | For details related to loop push (full push and tag push), see the loop_param field instructions in the following document. |
|badge_type     |int      |No                 |-1        | This specifies the badge number in the aps field (only for iOS).<li>-1: badge number does not change. <li> -2: badge number is automatically increased by 1. <li> >=0: set "custom" badge number.|
|group_id     |string      |No                 |tpns_yyyymmdd, with yyyymmdd representing the push date        | Statistics tag, used for aggregated statistics|
| tag_list      | object  | Only required by tag push          | None       | <li>Push to devices with tag1 and tag2:`{"tags":["tag1","tag2"],"op":"AND"}`<li>Push to devices with tag1 or tag2: `{"tags":["tag1","tag2"],"op":"OR"}` |
| account_list  | array   | Only required by single-account push and account list push  | None       | For single-account push:<li>`audience_type must be account`<li>Parameter format:["account1"]<br>For account list push:<li>Parameter format:`["account1","account2"]`<li>Up to 1,000 accounts |
| account_push_type  | int     | Optional for single-account push         | 0       |<li>0: push message to the latest device of the single account<li> 1: push message to all device associated with the single account|
| account_type  | int     | Optional for single-account push         | 0       | <li>Account type: see the account description below.<li>It must be the same as the account type set when the account is bound.   |
| token_list    | array   | Required by single-device push and device list push  | None       | For single-device push:<li>audience_type must be token<li>Parameter format:["token1"]<br>For device list push:<li>Parameter format:["token1","token2"]<li>Up to 1,000 tokens |

#### loop_param Parameter Description
| Field name | Type | Required | Comments |
| -------- | ------- | ---- | ----------------------------------------          |
| startDate      | string | Yes    | Loop range start date, with format of YYYY-MM-DD, such as 2019-07-01       |
| endDate | string   | Yes    | Loop range end date, with format of YYYY-MM-DD, such as 2019-07-01|                 |
| loopType | int| Yes | Loop type: 1 = daily, 2 = weekly, 3 = monthly |
| loopDayIndexs | array | Yes   | For weekly loop, enter number of weeks [0-6], and enter days as 0. If it is [0, 1, 2], it indicates that the push will be done on Monday, Tuesday, and Wednesday every week.                               |
| dayTimes   | array  | Yes    | Specific push time, with the format as HH:MM:SS, such as ["19:00:00", "20:00:00"], indicating that the push will be done at 19:00 and 20:00 every day. |



### Response Parameters

| Field name | Type | Required | Comments |
| -------- | ------- | ---- | ----------------------------------------          |
| seq | int64_t | Yes | The same as the request packet (if the request packet is invalid JSON, this field is 0) |
| push_id | string | Yes | Push ID |
| ret_code | int32_t | Yes | Error code; for details, see the error codes table |
| environment | string | Yes | The push environment specified by the user (only for iOS).<li>product: production environment<li>dev: development environment |
| err_msg | string | No | error message when an error occurs in the request |
| result   | string  | No    | When the request is correct<li>if there is extra data to be returned, the result will be encapsulated in the JSON of this field. If there is no extra data, there may be no such field. |



## Example(s)

#### Android Tag Push Request Message

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
        "title": "this is title",
        "content": "this is content",
        "custom_content":"value",
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
#### iOS Single-device Push Request Message

```json
{
    "audience_type": "token",
    "environment":"dev",
    "token_list": [ "05da87c0ae5973bd2dfa9e08d884aada5bb2"],
    "message_type":"notify",
    "message":{
     "title": "push title",
    "content": "push content",
    "ios":{
        "aps": {
            "alert": {
                "subtitle": "push subtitle"
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


