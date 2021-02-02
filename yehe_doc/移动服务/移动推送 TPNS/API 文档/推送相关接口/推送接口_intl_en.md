## API Description

**Request method**: POST

```plaintext
Service URL/v3/push/app
```

API service URLs correspond to service access points one by one. Please select the [service URL](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.

**Feature**: Push API is the general term for all push APIs. Push API supports different push targets, as described below.
All request parameters are JSON encapsulated and uploaded to the backend, which differentiates push targets based on the request parameters. If an error code is returned, see [Server Error Codes](https://intl.cloud.tencent.com/document/product/1024/33763).

## Required Parameters

The required push parameters refer to the parameters that must be carried in a push message.

| Parameter | Type | Required | Description |
| ------------- | ------- | ---------------------------------------- | ------------------------------------------------------------ |
| audience_type | String  | Yes                                       | Push target. Valid values:<li>all: push to all devices</li><li>tag: push to devices with specified tags</li><li>token: push to a single device</li><li>token_list: push to a list of devices</li><li>account: push to a single account</li><li>account_list: push to a list of accounts</li><li>package_account_push: push by account package<li>package_token_push: push by token package |
| message       | Object  | Yes                     | Message body. For more information, please see [message body type](#message_type)                     |
| message_type  | String  | Yes                                       | Message type. Valid values:<li>notify: notification</li><li>message: in-app message/silent message</li> |
| environment   | String  | Yes (only for iOS)                    | Push environment (only available for pushes on iOS). Valid values:<li>product: production environment</li><li>dev: development environment</li> |
| upload_id   | Integer  | Yes (only available for account package push/token package push)        | Account/token package upload ID  |

<span id="audience_type"></span>

### audience_type: push target

Push target indicates which devices a push can be delivered to.
Push API supports a variety of push targets. For example, you can push to all devices, devices with specified tags, a single device, a list of devices, a single account, or a list of accounts.

| Push Target     | Description         | Required Parameters and Instructions                                          |
| -------------------- | ---------------- | ------------------------------------------------------------ |
| all                  | Push to all devices     | None                                                           |
| tag                  | Push to devices with specified tags        | `tag_rules` (recommended):<li>Push by a combination of tags. You can set 'AND', 'OR' and 'NOT' rules.</li>**Note:** if both `tag_rules` and `tag_list` are specified, `tag_list` becomes invalid automatically. For parameter descriptions, see [Tag combination rules](#tag_rules).</li><br>`tag_list` (no further updates):<li>Push to devices with tag1 and tag2 `{"tags":["tag1","tag2"],"op":"AND"}`</li><li>Push to devices with tag1 or tag2 `{"tags":["tag1","tag2"],"op":"OR"}`</li> <li>A tag list cannot exceed 512 characters.</li> |
| token | Push to a single device | `token_list`<li>If the parameter contains multiple tokens, messages are pushed only to the first token.</li><li>Format example: ["token1"]</li><li>A token string cannot exceed 36 characters.</li> |
| token_list           | Push to a list of devices     | `token_list`<li>Up to 1,000 tokens</li><li>Format example: ["token1","token2"]</li><li>A token string cannot exceed 36 characters.</li>**Note:** if the token list contains more than 1,000 tokens, the push will fail. To push messages to more than 1,000 tokens, you are recommended to use the [Token Package Upload API](https://intl.cloud.tencent.com/document/product/1024/38862). |
| account | Push to a single account | `account_list`<li>If the parameter contains multiple accounts, messages are pushed only to the first account.</li><li>Format example: ["account1"] </li> |
| account_list         | Push to a list of accounts     | `account_list`<li>Up to 1,000 accounts<li>Format example: ["account1","account2"]</li>**Note:** if the account list contains more than 1,000 accounts, the push will fail. To push messages to more than 1,000 accounts, you are recommended to use the [Account Package Upload API](https://intl.cloud.tencent.com/document/product/1024/33765). |
| package_account_push | Push by account package | Required for uploading the account package to push                                           |
| package_token_push | Push by token package   | Required for uploading the token package to push |





- Push to all devices

```json
  {
    "audience_type": "all"
  }
```

- Push to devices with specified tags (using `tag_rules`): push to male users who were active on April 8, 2020 in Guangdong or Hunan province

```json
 {
  "audience_type": "tag",
  "tag_rules": [
        {
            "tag_items": [
                {
                    "tags": [
                        "guangdong",
                        "hunan"
                    ],
                    "is_not": false,   
                    "tags_operator": "OR",  
                    "items_operator": "OR", 
                    "tag_type": "xg_auto_province" 
                },
                {
                    "tags": [
                        "20200408"
                    ],
                    "is_not": false,
                    "tags_operator": "OR",
                    "items_operator": "AND",
                    "tag_type": "xg_auto_active"
                },
                {
                    "tags": [
                        "male"
                    ],
                    "is_not": false,
                    "tags_operator": "OR",
                    "items_operator": "AND",
                    "tag_type": "xg_user_define"
                }
            ],
            "operator": "OR", 
            "is_not": false  
        }
    ]
}
```

- Push to a single device: push to the device with `token1` as the token

```json
  {
    "audience_type": "token",
    "token_list": [
        "token1"
    ]
  }
```

- Push to a list of devices: push to devices with `token1` and `token2` as their tokens

```json
  {
    "audience_type": "token_list",
    "token_list": [
        "token1",
        "token2"
    ]
  }
```

- Push to a single account: push to the device bound to `account1`

```json
  {
    "audience_type": "account",
    "account_list": [
        "account1"
    ]
  }
```

- Push to a list of accounts: push to devices bound to `account1` and `account2`

```json
  {
    "audience_type": "account_list",
    "account_list": [
        "account1",
        "account2"
    ]
  }
```

<span id="message-body-type"></span>

### message_type: message type

The message types may vary slightly depending on the platform. For more information, see the table below:

| Message Type | Description              | Supported Platform                              | Feature Description                                                    |
| -------- | ----------------- | -------------------------------------- | ------------------------------------------------------------ |
| notify   | Notification bar message        | Android and iOS                          | Messages are displayed in the notification bar.      <br>**Note:** this field is mutually exclusive with [content-available: 1](#aps2). Do not use them at the same time.                                         |
| message | In-app message or silent message | Android (in-app message)<br>iOS (silent message) | Messages are not displayed in the notification bar.<br>**Note:** due to vendor restrictions, Android in-app messages can be delivered only through the TPNS channel, but not vendor channels. |

<span id= "message_type"></span>
### message: message body

The message body is the message delivered to the client.
Push API handles messages on iOS and Android differently, so you need to implement message pushes for the two platforms separately. The push message body is in JSON format.

### General message on Android

The table below specifies fields for the Android platform.

| Field Name | Type | Parent Item | Default Value | Required | Description |
| ------------------------ | ------ | ------- | ------ | ---- | ------------------------------------------------------------ |
| title                    | String | message | Empty     | Yes   | Message title.                                                     |
| content                  | String | message | Empty     | Yes   | Message content.                                                     |
| accept_time   | Array  | message      | Empty    | No    | The time period at which the message push is allowed to users.<li>A single element is formed by a "start" time and an "end" time.<li>"start" and "end" are indicated by hour and minute. For more information, please see the samples.<li>**Note:** this is valid only for the TPNS channel due to vendor restrictions.|
| thread_id                | String | message | Empty     | No   |Thread ID for collapsed notification in threaded display. <li>**Note:** this is valid only for the TPNS channel due to vendor restrictions. |
| thread_sumtext           | String | message | Empty     | No   | Summary displayed after the notification is collapsed in a thread, which is valid if `thread_id` is not empty. <li>**Note:** this is valid only for the TPNS channel due to vendor restrictions. |
| xg_media_resources       | String | message | Empty     | No   | URL of big image in the notification bar, which takes effect only for the TPNS and Mi channels.<li>**Note:** to use the big image notification feature of the Mi channel, you need to call the Mi image uploading API to upload an image file, get the `pic_url` image address specified by Mi, and enter it in the parameter `xg_media_resources` of TPNS. For more information, see the image uploading API section in [Rich Text Message in Mi Push](https://dev.mi.com/console/doc/detail?pId=1163#_10_0). |
| xg_media_audio_resources | String | message | Empty     | No   | URL of audio rich media elements.<li>It supports audio in MP3 format and the suggested size is within 5 MB.<li>**Note:** this parameter is valid only for the TPNS channel and is unsupported by other channels. |
| android                  | Object | message | Empty     | No   | Structure of advanced settings for Android notification. For more information, please see [Android structure description](#intent1) |


<span id="intent1"></span>
#### Android structure description

| Field Name | Type | Parent Item | Default Value | Required | Description |
| -------------- | ------- | ------- | ------ | ---- | ------------------------------------------------------------ |
| n_ch_id        | String  | android | Empty    | No    | Notification channel ID (valid only for the TPNS channel). For more information, see [Creating Notification Channel](https://intl.cloud.tencent.com/document/product/1024/30715).                                 |
| n_ch_name      | String  | android | Empty    | No    | Notification channel name (valid only for the TPNS channel). For more information, please see [Creating Notification Channel](https://intl.cloud.tencent.com/document/product/1024/30715).                                 |
| xm_ch_id       | String  | android | Empty     | No   | Mi channel ID (valid only for the Mi channel).                            |
| hw_ch_id       | String  | android | Empty     | No   | Huawei channel ID (valid only for the Huawei channel).                           |
| oppo_ch_id     | String  | android | Empty     | No   | OPPO channel ID (valid only for the OPPO channel).                          |
| vivo_ch_id     | String  | android | 0      | No   | Vivo channel ID (valid only for the Vivo channel). Valid values: `0`: operation message; `1`: system message |
| n_id           | Integer | android | 0      | No   | **(This field has been deprecated and will be deactivated in the future. If you need the override feature, please use the override parameter `collapse_id`.)**<br>Unique ID of the notification message object (valid only for the TPNS channel)<br>(1) Greater than 0: overrides the previous message with the same ID<br>(2) Equal to 0: displays this message without affecting other messages<br>(3) Equal to -1: clears all previous messages and displays this message only. |
| builder_id     | Integer | android | 0      | No   | Local notification style identifier.                                             |
| badge_type     | Integer | android | -1     | No  | Notification badge, which takes effect only for Huawei and Vivo devices. Valid values:<li>-2: automatically increased by 1;</li><li>-1: unchanged</li> |
| ring           | Integer | android | 1      | No   | Whether there is a ringtone. Valid values:<li>0: no</li><li>1: yes</li>           |
| ring_raw       | String  | android | Empty     | No   | This specifies the name of the ringtone file in the `raw` directory of the Android project; no extension is needed.     |
| vibrate        | Integer | android | 1      | No   | Whether the device vibrates. Valid values:<li>0: no</li><li>1: yes</li>           |
| lights         | Integer | android | 1      | No    | Whether the breathing light is used. Valid values:<li>0: no</li><li>1: yes</li>        |
| clearable      | Integer | android | 1      | No   | Whether the notification bar can be cleared. Valid values:<li>0: no</li><li>1: yes</li> |
| icon_type      | Integer | android | 0      | No   | Whether the notification bar thumbnail is an in-app icon or an uploaded icon. Valid values:<li>0: in-app icon</li><li>1: uploaded icon</li>This parameter is supported only for the TPNS and Huawei channels. |
| icon_res       | String  | android | Empty     | No   | URL of the uploaded notification thumbnail. This parameter is supported only for the TPNS and Huawei channels. For more information about the thumbnail formats, see [Rich Media Notification](https://intl.cloud.tencent.com/document/product/1024/37858). |
| style_id       | Integer | android | 1      | No   | Whether the notification style with the specified number will be overwritten. |
| small_icon     | String  | android | Empty | No | The icon that the message displays in the status bar. If not set, the application icon will be displayed. |
| icon_color      | Integer | android | 0      | No | Color of the icon in the notification bar. <li>This parameter takes effect only for the TPNS channel. <li>To use an RGB color such as #01e240, enter `123456`. |
| action         | Object  | android | Yes | No | The action after the notification bar is clicked; the default action is to open the app. For more information, see [action parameter description](#action). |
| custom_content | String  | android | Empty     | No   | User-defined parameter (which should be serialized into a JSON string)<br><b> Note:</b>Huawei officially announced that "the v2 protocol will be disused starting September 30, 2021". TPNS has upgraded the Huawei push protocol to v5, which does not support carrying custom parameters through the **extra parameter(s)** field. If you have integrated the Huawei vendor channel, we recommend you use <a href="https://intl.cloud.tencent.com/document/product/1024/32624">Intent</a> to carry custom parameters; otherwise, custom parameters cannot be delivered through the Huawei channel. |
| show_type      | Integer | android | 2      | No  | Whether to display notification when the application is running in the foreground, which is displayed by default. This takes effect only for TPNS and FCM channels. Valid values:<li>1: no<li>2: yes<br>Note: if the value is 1 and the application is running in the foreground, this push is imperceptible to end users, but arrival data will be reported.</br> |



<span id="action"></span>
**action parameter description**

| Field Name | Type | Parent Item | Default Value | Required | Description |
| ----------- | ------- | ------ | ------ | ------------------------------------------- | ------------------------------------------------------------ |
| action_type    | Integer | action  | 1     | No   | One-click actions. Valid values:<li>1: open activity or the app</li><li>2: open the browser</li><li>3: open the app custom page (recommended; for more information, see [Guide for redirection through Intent](https://intl.cloud.tencent.com/document/product/1024/32624)).</li> |
| activity    | String  | action | Empty     | Yes if `action_type` is `1` and an activity needs to be opened | Full name of activity, such as `com.x.y.PushActivity`.                   |
| aty_attr    | Object  | action | Empty     | No if `action_type` is `1` and an activity needs to be opened | Activity attribute<li>if: `Flag` attribute of `Intent` in `Integer` type<li>pf: `Flag` attribute of `PendingIntent` in `Integer` type |
| browser     | Object  | action | Empty     | Yes if `action_type` is `2`                       | Action to open a browser.<li>url: webpage URL in `String` type. Only HTTP and HTTPS URLs are supported</li><li>confirm: whether user's confirmation is required. The value is in `Integer` type</li>1: yes<br>0: no |
| intent      | String  | action | Empty     | Yes if `action_type` is `3`                       | Custom scheme, such as `xgscheme://com.tpns.push/notify_detail`.     |

Below is a sample of a complete message:

```json
{
    "title": "xxx",
    "content": "xxxxxxxxx",
    "xg_media_resources": "xxx" , // Enter the URL of rich media elements, such as `https://www.xx.com/img/bd_logo1.png?qua=high`
    "xg_media_audio_resources":"xxx", // Enter the URL of audio rich media elements, such as `http://sc1.111ttt.cn/2018/1/03/13/396131227447.mp3` 
    "thread_id":"Activity_id",
    "thread_sumtext":"Operational activity",
    "accept_time": [
        {
            "start": {// Period start time
                "hour": "13",// Start time in hour. Value range: [0,24)
                "min": "00"// Start time in minute. Value range: [0,60)
            },
            "end": {// Period end time
                "hour": "14",// End time in hour. Value range: [0,24)
                "min": "00" // End time in minute. Value range: [0,60)

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
		"n_ch_id": "default_message",
		"n_ch_name": "default notification",
        "n_id": 0,
        "builder_id": 0,
        "ring": 1,
        "ring_raw": "ring",
		"badge_type":-1, 
        "vibrate": 1,
        "lights": 1,
        "clearable": 1,
        "icon_type": 0,
        "icon_res": "xg",
        "style_id": 1,
        "small_icon": "xg",
        "action": {
            "action_type": 1,// Action type; 1. Open activity or application; 2. Open browser; 3. Open Intent
            "activity": "com.x.y.PushActivity",
            "aty_attr": {// activity attribute, only for action_type=1
                "if": 0, // Intent's Flag attribute
                "pf": 0  // PendingIntent's Flag attribute
            },
            "browser": {
                "url": "https://cloud.tencent.com ", // Only HTTP and HTTPS URLs are supported
                "confirm": 1 // Whether user’s confirmation is required
            },
            "intent": "xgscheme://com.tpns.push/notify_detail" //The SDK must be version 1.0.9 or later. Configure the data tag in the client's Intent and set the scheme attribute
        },
      "custom_content":"{\"key\":\"value\"}"
    }
}
```

### Notification message on iOS

The table below specifies fields for the iOS platform.

| Field Name | Type | Parent Item | Default Value | Required | Description |
| ------ | ------ | ------- | ------ | ---- | -------------------------------------------------- |
| title                    | String | message | Empty     | Yes   | Message title, which will override the content in `title` under `alert`.                                                   |
| content                  | String | message | Empty     | Yes   | Message content, which will override the content in `body` under `alert`.
| thread_id                | String | message | Empty     | No   |Thread ID for collapsed notification in threaded display.                                     |
| ios    | Object       | message  | Empty    | Yes    | iOS message structure. See [iOS field description](#iOS) for more information. |
| xg_media_resources    | String     | message | Empty    | No    | URL of rich media elements such as image, audio, and video                          |


<span id="iOS"></span>
#### iOS field description

| Field Name | Type | Parent Item | Default Value | Required | Description |
| -------------- | ------ | ------ | ------ | ---- | ------------------------------------------------------------ |
| aps             | Object  | ios    | Empty    | No    | APNs-specific field. For more information, see [aps parameter description](#aps). For further information, see [Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1). |
| custom_content  | String  | ios    | Empty    | No    | Custom parameters for delivery, which must be serialized to a JSON string.                                |
| xg             | String | ios     | Empty     | No       | Reserved key, which should not be used.                                     |

<span id="aps"></span>
**aps parameter description**

| Field Name | Type | Parent Item | Default Value | Required | Description |
| --------------- | ------- | ------ | ------ | ---- | ------------------------------------------------------------ |
| alert           | Object  | aps    | Empty     | Yes   | It contains the title and message content.                                           |
| badge_type      | Integer | aps    | Empty                 | No        | The user-configured badge number. Valid values:<li>-1: badge number does not change.<li> -2: badge number automatically increases by 1.<li> >=0: a custom badge number is configured.|
| category        | String  | aps    | Empty     | No   | The action identifier displayed when the message is pulled down.                                     |
| mutable-content | Integer | aps    | Empty     | No   |This is an additional notification parameter that carries "mutable-content" during push.<li>1 means that the Service Extension supports iOS 10. <li>Once enabled, the push details will include the arrival data report. Before using this feature, see [Notification Service Extension Usage Instructions](https://intl.cloud.tencent.com/document/product/1024/30730) to implement the Service Extension API. If `mutable-content` is not carried, arrival data will not be reported. |
| sound           | String  | aps    |  Empty    | No    | The sound field is used as follows.<br>1. To play the system default ringtone, use "sound":"default"<br>2. To play local custom ringtone, use "sound":"chime.aiff"<br>3. To mute, use "sound":"" or remove the `sound` field. Note: if you want to use a custom ringtone, the ringtone must be in Linear PCM, MA4 (IMA/ADPCM), alaw, or μLaw format, saved in the `bundle` directory of the project, and of no more than 30 sec in length; otherwise, the system default ringtone will be used.|

Below is a sample of a complete message:

```json
{
    "title": "xxx",
    "content": "xxxxxxxxx",
    "thread_id":"Activity_id",
    "xg_media_resources":"https://www.xx.com/img/bd_logo1.png",
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

### In-app message on Android

In-app message is unique to the Android platform and not displayed in the notification bar of the mobile phone. It can be used to deliver controlled messages to users imperceptibly.

>!Due to vendor restrictions, Android in-app messages can be delivered only through the TPNS channel, but not vendor channels.

The table below specifies fields for the Android platform.

| Field Name | Type | Parent Item | Default Value | Required | Description |
| -------------- | ------ | ------- | ------ | -------- | ------------------------------------------------------------ |
| title          | String | message | Empty     | Yes       | Command description.                                                    |
| content                  | String | message | Empty     | Yes   | Command content.                                                     |
| android        | Object | message | Empty     | No       | Android message structure.                                               |
| accept_time    | Array  | message |  Empty    | No    | The time period at which the message push is allowed to users.<li>A single element is formed by a "start" time and an "end" time.</li><li>"start" and "end" are indicated by hour and minute. For more information, please see the samples.</li><li>**Note:** this is valid only for the TPNS channel due to vendor restrictions.</li> |
| custom_content | String | android | Empty     | No       | This must be serialized to a JSON string.                                    |

Complete sample:

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

<span id="aps2"></span>
### Silent message on iOS

Similar to in-app message on Android, silent message is unique to the iOS platform and not displayed. When the message arrives at the device, iOS will wake up the application for a period of time (less than 30 seconds) in the background to let the application handle the message logic.

The specific fields are as follows:

| Field Name | Type | Parent Item | Default Value | Required | Description |
| -------------- | ------ | ------- | ------ | -------- | ------------------------------------------------------------ |
| ios            | Object | message | Empty     | Yes       | iOS message structure.                                               |
| aps    | JSON       | ios  | Empty    | Yes    | APNs-specific field, where the most important key-value pair is as follows:<li>content-available: identifies the message type (which must be 1), in integer format.<li>The value cannot contain the `alert`, `sound`, or `badge_type` fields. For more information, see [Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1). <br>**Note:** `content-available: 1` is mutually exclusive with [message_type:"notify"](#message-body-type). Do not use them at the same time. |
| custom_content | String | ios     | Empty    | No    | This must be serialized to a JSON string.                                |
| xg             | String | ios     | Empty     | No       | Reserved key, which should not be used.                                     |



Complete sample:

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

## Optional Parameters

Optional Push API parameters refer to advanced parameters that can be carried in a push message, except `audience_type`, `message_type`, and `message`.



| Parameter  Name            | Type    | Parent Item | Required                          | Default Value                   | Description                                                         |
| --------------------- | ------- | ------ | ------------------------------ | ------------------------------------ | ------------------------------------------------------------ |
| expire_time          | Integer | None     | No                            | 259200 (72 hours)                     | Offline message retention duration (in seconds), up to 72 hours.<li>If `expire_time` is equal to `0`, it indicates a real-time message.</li><li>If `expire_time` is greater than 0 and less than 800 seconds, the system will reset it to 800 seconds.</li><li>If `expire_time` is greater than or equal to 800 seconds, the message will be retained according to the set value, up to 72 hours.</li><li>The value set cannot exceed `2147483647`; otherwise, the push will fail.</li> |
| send_time            | String  | None     | No                             | Current system time                         | Push time. You can specify a push time in the next 90 days.<li>The format is yyyy-MM-DD HH:MM:SS.</li><li>If the push time specified is earlier than the current server time, the push starts immediately.</li><li>This field is supported only for push to all devices or devices with specified tags.</li> |
| multi_pkg            | Boolean | None     | No                             | false                                | Multi-package name push: for an application that has multiple packages (such as for MyApp and Wandoujia), if you want the application in all channels to receive the push message, you can set this value to `true`.<br>**Note**: this parameter controls the multi-package name push of the TPNS channel by default. To implement multi-package name push on vendor channels, see [Configuring vendor channel for multi-package name](https://intl.cloud.tencent.com/document/product/1024/35393). |
| loop_param           | Object  | None     | No                             | 0                                    | Loop push parameters (related to push to all devices or devices with specified tags). For more information about loop push parameters, see the [loop_param field description](#loop_param) below. |
| group_id             | String  | None    | No                             | tpns_yyyymmdd, where `yyyymmdd` indicates the push date | **This field has been deprecated and will be deactivated subsequently. If you need to use the aggregate statistics feature, please use the push plan field (plan_id).** |
| plan_id              | String  | None    | No                             | Empty                                   | Push plan ID. For more information about how to create and use the push plan, click [here](https://intl.cloud.tencent.com/document/product/1024/37452). |
| tag_rules             | Array  | None     | Yes for tag push only                 | Empty                                   |  <li>For push based on a combination of tags, you can set 'AND', 'OR', and 'NOT' rules</li><li>**Note:** if both `tag_rules` and `tag_list` are specified, `tag_list` becomes invalid automatically. For parameter descriptions, please see [tag_rules parameter description](#tag_rules).</li> |
| account_list         | Array   | None | Required for push to a single account or a list of accounts | Empty       | For push to a single account:<li>`audience_type` must be `account`</li><li>Parameter format: ["account1"]</li><br>For push to a list of accounts: <li>Parameter format: `["account1","account2"]`</li><li>Up to 1,000 accounts</li> |
| account_push_type    | Integer | None     | Optional for push by account                 | 0                                    | Push type. Valid values: <li>0: push messages to the latest device of the account</li><li>1: push messages to all devices associated with the account</li> |
| token_list    | array   | None | Required for push to a single device or a list of devices | Empty       | For push to a single device: <li>`audience_type` must be `token`<li>Parameter format: ["token1"]<br>For push to a list of devices: <li>Parameter format: ["token1","token2"]</li><li>Up to 1,000 tokens</li> |
| push_speed           | Integer | None    | Valid only for push to all devices or devices with specified tags  | Empty                                  | Push speed limit to X pushes per second. Value range of X: 1000-50000           |
| collapse_id          | Integer | None    | No                             | System-assigned `collapse_id`       | <li>Message overwriting parameter. After the first push task has been scheduled and delivered, if the second push task carries the same `collapse_id`, it will stop the TPNS channel data in the first push task that has not been delivered yet and will also overwrite the message in the first push task.<li>The `collapse_id` of a completed task can be obtained via the [Querying Push Information for One Task](https://intl.cloud.tencent.com/document/product/1024/33773) API.<li>Currently, this is supported only for push to all devices, push to devices with specified tags, and push by account package. |
| channel_rules        | Array   | None    | No                             | Empty                                   | Push channel selection policy.<li>You can select the channels through which a push can be delivered. Messages are pushed through all channels by default. For more information about the push policy, see [Channel Policy](https://intl.cloud.tencent.com/document/product/1024/36151).<li>For the data structure of single elements in the `channel_rules` array, see [channel_rules parameter description](#channel_rules1) below. |
| tpns_online_push_type | Integer | None | No | 0 | Whether to push the message to online devices through the TPNS channel. Valid values: <li>0: the message will be pushed to online devices through the TPNS channel by default<li> 1: the message will not be pushed to online devices preferably through the TPNS channel. |
| force_collapse | Boolean | None | No | false | Whether to deliver messages to OPPO or Vivo devices that do not support message overwriting. Valid values:<li>false: no<li>true: yes |



> ? The `collapse_id` parameter is subject to the following restrictions:
> - This parameter currently cannot be customized. Only `collapse_id` values generated by TPNS can be used.
> - This parameter is supported only for the TPNS channel, APNs channel, Mi channel, Meizu channel, and Huawei devices on EMUI 10 and above.
> - For the Huawei channel, you must use [intent](#intent1) to carry custom parameters to implement message override. If you use `custom_content`, the API layer will block custom parameters.
> - Currently, the OPPO and Vivo channels do not support message override. When an override message is created, delivery to the OPPO and Vivo channels can be disabled by setting the `force_collapse` field to `false`.


<span id="tag_rules"></span>
### tag_rules parameter description

| Field Name     | Type    | Parent Item    | Required | Description                                                         |
| --------- | ------- | --------- | ---- | ------------------------------------------------------------ |
| tag_items | Array   | tag_rules | Yes   | Tag rule. See [tag_items description](#tag_items2)                 |
| operator  | String  | tag_rules | Yes   | Operator between elements in the `tag_rules` array. The operator of the first `tag_rules` element is invalid data. The operator of the second `tag_rules` element is the operator between the first and second `tag_rules` elements, and so on. Valid values:<li>OR: OR operation<li>AND: AND operation |
| is_not    | Boolean | tag_rules | Yes   | Whether to perform "NOT" operation on the calculation result of the `tag_items` array.<li>true: yes<li>false: no</li> |




<span id="tag_items2"></span>
#### tag_items description

| Field      | Type    | Parent Item    | Required | Description                                                         |
| -------------- | ------- | --------- | ---- | ------------------------------------------------------------ |
| tags           | Array   | tag_items | Yes   | Specific tag value in string type, such as `tag1` and `guangdong`.            |
| is_not         | Boolean | tag_items | Yes   | Whether to perform "NOT" operation on the calculation result of the tag array. Valid values:<li>true: yes<li>false: no |
| tags_operator  | String  | tag_items | Yes   | Operator for tag in `tags`. Valid values: <li>OR: OR operation<li>AND: AND operation    |
| items_operator | String  | tag_items | Yes   | Operator between elements in the `tag_items` array. The `items_operator` of the first `tag_items` element is invalid. The `items_operator` of the second `tag_items` element is the operator between the first and second `tag_items` elements, and so on. Valid values:<li>OR: OR operation<li>AND: AND operation</li> |
| tag_type       | String  | tag_items | Yes   | See [tag_type value table](#tag123)                              |


<span id="tag123"></span>
#### tag_type value table

| **Tag Name** | **tag_type Value**      | **Sample Tag**          |
| ------------ | ---------------------- | ----------------------- |
| Custom tag   | xg_user_define         | tag1, tag2           |
| Application version      | xg_auto_version        | 1.1.0, 1.2.0.1        |
| Device district information | xg_auto_province       | guangdong, shanghai  |
| Active information     | xg_auto_active         | 20200131, 20200201    |
| XG SDK version   | xg_auto_sdkversion     | 1.1.5.2, 1.1.5.3      |
| System language     | xg_auto_systemlanguage | zh, en                |
| Mobile phone brand     | xg_auto_devicebrand    | Xiaomi, Vivo         |
| Mobile phone model     | xg_auto_deviceversion  | MI 9 SE, Vivo X9Plus |
| Country/Region | xg_auto_country | CN, SG |

> ? For more information about the usage, see [Sample tag push](#biaoqianshili).


<span id="channel_rules parameter description 1"></span>

### channel_rules parameter description

| Field  Name | Type    | Parent Item | Required | Description                                                        |
| ------- | ------- | ------------- | -------- | ------------------------------------------------------------ |
| channel | String  | channel_rules | Yes       | Delivery push channel. Valid values:<br> <li> hw: Huawei channel <li> xm: Mi channel<li> mz: Meizu channel<li> vivo: Vivo channel<li>oppo: OPPO channel<li>apns: APNs channel |
| disable | Boolean | channel_rules | Yes       | Whether to disable the channel specified in `channel`, which is enabled by default. Valid values:<br><li>true: disable<li>false: enable |

<span id="loop_param parameter description"></span>

### loop_param parameter description

| Field Name | Type    |  Parent Item | Required | Description                                                        |
| ------------- | ------- | ---------- | -------- | ------------------------------------------------------------ |
| startDate     | String  | loop_param | Yes       | Loop interval start date in YYYY-MM-DD format, such as 2019-07-01. You can choose a date in the next 90 days. |
| endDate       | String  | loop_param | Yes       | Loop interval end date in YYYY-MM-DD format, such as 2019-07-07. You can choose a date in the next 90 days. |
| loopType      | Integer | loop_param | Yes       | Loop type. Valid values:<li>1: daily<li>2: weekly<li>3: monthly                  |
| loopDayIndexs | Array   | loop_param | Yes       | For weekly loop, enter days [0-6] in a week. If the value is [0, 1, 2], it indicates that the push will be done on Monday, Tuesday, and Wednesday every week. |
| dayTimes      | Array   | loop_param | Yes       | Specific push time in HH:MM:SS format. If the value is ["19:00:00", "20:00:00"], it indicates that the push will be done at 19:00 and 20:00 every day. |



## Response Parameters

| Field Name   | Type    | Required | Description                                                        |
| ----------- | ------- | -------- | ------------------------------------------------------------ |
| seq         | Integer | Yes | The same as the request packet (if the request packet is invalid JSON, this field is 0). |
| push_id     | String  | Yes       | Push ID.                                                      |
| ret_code    | Integer | Yes       | Error code. For more information, please see the error codes table.                                 |
| environment | String  | Yes | The push environment specified by the user (only for iOS). Valid values: <li>product: production environment</li><li>dev: development environment</li> |
| err_msg     | String  | No       | Error message when an error occurs in the request                                         |
| result      | String  | No | When the request is correct:<li>If there is extra data to be returned, the result will be encapsulated in the field in JSON format.<li>If there is no extra data, this field may not exist.</li> |



## Samples

#### Android request message for push by account

```json
{
    "audience_type": "account",
    "account_list": [
      "account1"
  ],
	"multi_pkg":true,
	"push_speed":50000,
    "channel_rules": [
        {
            "channel": "mz",
            "disable": true
        },
        {
            "channel": "xm",
            "disable": false
        }
    ],
    "message_type": "notify",
    "message": {
    "title": "Test title",
    "content": "Test content",
    "xg_media_resources": "xxx1" , // Enter the URL of rich media elements, such as `https://www.xx.com/img/bd_logo1.png?qua=high`
    "xg_media_audio_resources":"xxx", // Enter the URL of audio rich media elements, such as `http://sc1.111ttt.cn/2018/1/03/13/396131227447.mp3` 
    "accept_time": [
        {
            "start": {// Period start time
                "hour": "13",// Start time in hour. Value range: [0,24)
                "min": "00"// Start time in minute. Value range: [0,60)
            },
            "end": {// Period end time
                "hour": "14",// End time in hour. Value range: [0,24)
                "min": "00" // End time in minute. Value range: [0,60)

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
		"n_ch_id": "default_message",
		"n_ch_name": "default notification",
        "n_id": 0,
        "builder_id": 0,
        "ring": 1,
        "ring_raw": "ring",
		"badge_type":-1,
        "vibrate": 1,
        "lights": 1,
		"clearable": 1,
        "icon_type": 0,
        "icon_res": "xg",
        "style_id": 1,
        "small_icon": "xg",
        "action": {
            "action_type": 1,// Action type; 1. Open activity or application; 2. Open browser; 3. Open Intent
            "activity": "xxx",
            "aty_attr": {// activity attribute, only for action_type=1
                "if": 0, // Intent's Flag attribute
                "pf": 0  // PendingIntent's Flag attribute
            },
            "browser": {
                "url": "xxxx ", // Only HTTP and HTTPS URLs are supported
                "confirm": 1 // Whether user’s confirmation is required
            },
            "intent": "xxx" // The SDK must be version 1.0.9 or later. Configure the data tag in the client's intent and set the scheme attribute
        },
      "custom_content":"{\"key\":\"value\"}"
    }
}
}
```

### Response message for push by account

```json
{
    "seq": 0,
    "environment": "product",
    "ret_code": 0,
    "push_id": "3895624686"
}
```

### iOS request message for push to a single device

```json
{
    "audience_type": "token",
    "environment":"dev",
    "token_list": [ "05da87c0ae********fa9e08d884aada5bb2"],
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

### Response message for push to a single device

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


<span id="biaoqianshili"></span>
### Sample push to devices with specified tags (using tag_rules)

**Sample 1: push messages to male users who were active on April 8, 2020 in Guangdong or Hunan province**
Expression: (xg_auto_province.guangdong OR xg_auto_province.hunan) AND xg_auto_active.20200408 AND xg_user_define.male

```
{
  "audience_type": "tag",
  "tag_rules": [
        {
            "tag_items": [
                {
                    "tags": [
                        "guangdong",
                        "hunan"
                    ],
                    "is_not": false,   //Whether to perform the "NOT" operation on the calculation result of the tags in `tags`. Valid values: true: yes; false: no
                    "tags_operator": "OR",  //Operator for tags in `tags`
                    "items_operator": "OR", //Operator between elements in `tag_items`. The `items_operator` of the first element is invalid data. The `items_operator` of the second element is the operator between the first and second elements, and so on.
                    "tag_type": "xg_auto_province" //Type of tags in `tags`
                },
                {
                    "tags": [
                        "20200408"
                    ],
                    "is_not": false,
                    "tags_operator": "OR",
                    "items_operator": "AND",
                    "tag_type": "xg_auto_active"
                },
                {
                    "tags": [
                        "male"
                    ],
                    "is_not": false,
                    "tags_operator": "OR",
                    "items_operator": "AND",
                    "tag_type": "xg_user_define"
                }
            ],
            "operator": "OR", 
            "is_not": false  
        }
    ]
}
```

**Sample 2: push messages to Huawei users who were active in the last 3 days on an app version other than 1.0.2**
Expression: (xg_auto_active.20200406 OR xg_auto_active.20200407 OR xg_auto_active.20200408) AND (NOT xg_auto_version.1.0.2) AND xg_auto_devicebrand.huawei

```
{
  "audience_type": "tag",
  "tag_rules": [
        {
            "tag_items": [
                {
                    "tags": [
                        "20200406",
                        "20200407",
                        "20200408"
                    ],
                    "is_not": false,   //Whether to perform the "NOT" operation on the calculation result of the tags in `tags`. Valid values: true: yes; false: no
                    "tags_operator": "OR",  //Operator for tags in `tags`
                    "items_operator": "OR", //Operator between elements in `tag_items`. The `items_operator` of the first element is invalid data. The `items_operator` of the second element is the operator between the first and second elements, and so on.
                    "tag_type": "xg_auto_active" //Type of tags in `tags`
                },
                {
                    "tags": [
                        "1.0.2"
                    ],
                    "is_not": true,
                    "tags_operator": "OR",
                    "items_operator": "AND",
                    "tag_type": "xg_auto_verison"
                },
                {
                    "tags": [
                        "huawei"
                    ],
                    "is_not": false,
                    "tags_operator": "OR",
                    "items_operator": "AND",
                    "tag_type": "xg_auto_devicebrand"
                }
            ],
            "operator": "OR", 
            "is_not": false  
        }
    ]
}
```

