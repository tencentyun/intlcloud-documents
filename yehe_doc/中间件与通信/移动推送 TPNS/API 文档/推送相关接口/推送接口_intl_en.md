## API Calling Description

**Request method**: POST.

```plaintext
Service URL/v3/push/app
```

API service URLs correspond to service access points one to one. Please select the [service URL](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.

**Feature**: Push API is the general term for all push APIs. Push API supports different push targets, as described below.
All request parameters are JSON encapsulated and uploaded to the backend, which differentiates push targets based on the request parameters. If an error code is returned, see [Server-Side Error Codes](https://intl.cloud.tencent.com/document/product/1024/33763).

## Required Parameters

The required push parameters refer to the parameters that must be carried in a push message.

| Parameter | Type | Required | Description |
| ------------- | ------- | ---------------------------------------- | ------------------------------------------------------------ |
| audience_type | String  | Yes                                       | Push target. Valid values:<li>`all`: push to all devices</li><li>`tag`: push to devices with specified tags</li><li>`token`: push to a single device</li><li>`token_list`: push to a list of devices</li><li>`account`: push to a single account</li><li>`account_list`: push to a list of accounts</li><li>`package_account_push`: push by account package<li>`package_token_push`: push by token package |
| message       | Object  | Yes                     | Message body. For more information, please see [message body type](#message body type).                     |
| message_type  | String  | Yes                                       | Message type. Valid values:<li>`notify`: notification</li><li>`message`: in-app message/silent message</li> |
| environment   | String  | Yes (only for iOS)                    | Push environment (only available for pushes on iOS). Valid values:<li>`product`: production environment</li><li>`dev`: development environment</li> |
| upload_id   | Integer  | Yes (only available for push by account/token package)        | Account/Token package upload ID  |

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

<span id="message body type"></span>

### message_type: message type

The message types may vary slightly depending on the platform. For more information, see the table below:

| Message Type | Description              | Supported Platform                              | Feature Description                                                    |
| -------- | ----------------- | -------------------------------------- | ------------------------------------------------------------ |
| notify   | Notification bar message        | Android and iOS                          | Messages are displayed in the notification bar.      <br>**Note:** this parameter is mutually exclusive with [content-available: 1](#aps2). Do not use them at the same time.                                         |
| message | In-app message or silent message | Android (in-app message)<br>iOS (silent message) | Messages are not displayed in the notification bar.<br>**Note:** due to vendor restrictions, Android in-app messages can be delivered only through the TPNS channel, but not vendor channels. |

### message: message body

The message body is the message delivered to the client.
Push API handles messages on iOS and Android differently, so you need to implement message pushes for the two platforms separately. The push message body is in JSON format.

### General message on Android

The table below specifies parameters for the Android platform:

| Parameter | Type | Parent Project | Default Value | Required | Description |
| ------------------------ | ------ | ------- | ------ | ---- | ------------------------------------------------------------ |
| title                    | String | message | Empty     | Yes   | Message title                                                     |
| content                  | String | message | Empty     | Yes   | Message content                                                     |
| accept_time    | Array  | message |  Empty    | No    | The time period that allows pushes.<li>A single element is formed by a "start" time and an "end" time.</li><li>"start" and "end" are indicated by hour and minute. For more information, please see the samples.</br>**Note:** this is valid only for the TPNS channel due to vendor restrictions.</li> |
| thread_id                | String | message | Empty     | No   |Thread ID for collapsed notification in threaded display. </br>**Note:** this is valid only for the TPNS channel due to vendor restrictions. |
| thread_sumtext           | String | message | Empty     | No   | Summary displayed after the notification is collapsed in a thread, which is valid if `thread_id` is not empty. </br>**Note:** this is valid only for the TPNS channel due to vendor restrictions. |
| xg_media_resources       | String | message | Empty     | No   | URL of big image in the notification bar, which takes effect only for the TPNS and Mi channels.</br>**Note:** to use the big image notification feature of the Mi channel, you need to call the Mi image uploading API to upload an image file, get the `pic_url` image address specified by Mi, and enter it in the `xg_media_resources` parameter of TPNS. For more information, see the image uploading API section in [Rich Text Message in Mi Push](https://dev.mi.com/console/doc/detail?pId=1163#_10_0). |
| xg_media_audio_resources | String | message | Empty     | No   | URL of audio rich media elements.</br>It supports audio in MP3 format and the suggested size is within 5 MB.</br>**Note:** this parameter is valid only for the TPNS channel and is unsupported by other channels. |
| android                  | Object | message | Empty     | No   | Structure of advanced settings for Android notification. For more information, please see [Android structure description](#intent1). |



#### Android structure description [](id:intent1)

| Parameter | Type | Parent Project | Default Value | Required | Description |
| -------------- | ------- | ------- | ------ | ---- | ------------------------------------------------------------ |
| n_ch_id        | String  | android | Empty    | No    | Notification channel ID (valid only for the TPNS channel). For more information, see [Creating a notification channel](https://intl.cloud.tencent.com/document/product/1024/30715).                                 |
| n_ch_name      | String  | android | Empty    | No    | Notification channel name (valid only for the TPNS channel). For more information, please see [Creating a notification channel](https://intl.cloud.tencent.com/document/product/1024/30715).                                 |
| xm_ch_id       | String  | android | Empty     | No   | Mi channel ID (valid only for the Mi channel)                            |
| fcm_ch_id | String  | android | Empty     | No   | FCM channel ID (valid only for the FCM channel)                           |
| hw_biz_type            | Integer | android     | 0       | No                                  |Whether to enable notifications for Huawei quick apps. Valid values:<li>`1`: enable<li>`0`: disable</li>**Note**: this parameter takes effect only for the Huawei channel and you need to [contact Huawei business team](https://developer.huawei.com/consumer/cn/support/business) for activation.          |
| hw_ch_id       | String  | android | Empty     | No   | Huawei channel ID (valid only for the Huawei channel)                           |
| hw_importance       | Integer  | android | 0     | No   | Notification message type defined by Huawei, which determines the notification behavior of the user’s device. Valid values:<li>`1`: information and marketing messages</li><li>`2`: service and communication messages</li> |
| oppo_ch_id     | String  | android | Empty     | No   | OPPO channel ID (valid only for the OPPO channel)                          |
| vivo_ch_id     | String  | android | 0      | No   | vivo channel ID (valid only for the vivo channel). Valid values: `0`: operation message; `1`: system message |
| n_id           | Integer | android | 0      | No   | **(This parameter has been disused and will be unavailable in the future. If you need the override feature, please use the overriding parameter `collapse_id`.)**<br>Unique ID of the notification message object (valid only for the TPNS channel)<br>(1) Greater than 0: overrides the previous message with the same ID<br>(2) Equal to 0: displays this message without affecting other messages<br>(3) Equal to -1: clears all previous messages and displays this message only. |
| builder_id     | Integer | android | 0      | No   | Local notification style identifier                                             |
| badge_type     | Integer | android | -1     | No   | Notification badge: <li>-2: automatically increased by 1, valid only for Huawei devices</li><li>-1: unchanged, valid only for Huawei and vivo devices</li><li>[0, 100): direct configuration, valid only for Huawei and vivo devices</li>**Note**: the badge adaptation capabilities vary depending on the vendor device. For details about the implementation effect of each parameter value, see <a href="https://intl.cloud.tencent.com/document/product/1024/35828">Badge Adaptation Guide<a>. |
| ring           | Integer | android | 1      | No   | Whether there is a ringtone. Valid values:<li>`0`: no</li><li>`1`: yes</li>           |
| ring_raw       | String  | android | Empty     | No   | Name of the ringtone file in the `raw` directory of the Android project; no extension is needed. <br>**Note**: custom ringtones are supported only for the Huawei, Mi, FCM, and TPNS channels and must be used with the field `n_ch_id`. For the configuration process, see [How do I set a custom ringtone?](https://intl.cloud.tencent.com/document/product/1024/32624).    |
| vibrate        | Integer | android | 1      | No   | Whether to enable vibration. Valid values:<li>`0`: no</li><li>`1`: yes</li>           |
| lights         | Integer | android | 1      | No    | Whether to use the breathing light. Valid values:<li>`0`: no</li><li>`1`: yes</li> |
| clearable      | Integer | android | 1      | No   | Whether messages can be cleared from the notification bar. Valid values:<li>`0`: no</li><li>`1`: yes</li> |
| icon_type      | Integer | android | 0      | No   | Whether the notification bar thumbnail is an in-app icon or an uploaded icon. Valid values:<li>`0`: in-app icon</li><li>`1`: uploaded icon</li>This parameter is supported only for the TPNS, FCM, and Huawei channels. |
| icon_res       | String  | android | Empty     | No   | URL of the uploaded notification thumbnail. This parameter is supported only for the TPNS, FCM, and Huawei channels. For more information about the thumbnail formats, see [Rich Media Notification](https://intl.cloud.tencent.com/document/product/1024/37858). |
| style_id       | Integer | android | 1      | No   | Whether the notification style with the specified number will be overwritten |
| small_icon     | String  | android | Empty | No | The icon that the message displays in the status bar. If this parameter is not set, the application icon will be displayed. |
| icon_color      | Integer | android | 0      | No | Color of the icon in the notification bar <li>This parameter takes effect only for the TPNS channel.</li> <li>To use an RGB color such as #01e240, enter `123456`. </li> |
| action         | Object  | android | Yes | No | The action after the notification bar is clicked; the default action is to open the app. For more information, see [action parameter description](#action). |
| custom_content | String  | android | Empty     | No   | User-defined parameter (which should be serialized into a JSON string)<br><b> Note:</b>Huawei officially announced that "the v2 protocol will be disused starting September 30, 2021". TPNS has upgraded the Huawei push protocol to v5, which does not support carrying custom parameters through the **extra parameter(s)** field. If you have integrated the Huawei vendor channel, we recommend you use <a href="https://intl.cloud.tencent.com/document/product/1024/38354">Intent</a> to carry custom parameters; otherwise, custom parameters cannot be delivered through the Huawei channel. |
| show_type      | Integer | android | 2      | No  | Whether to display the notification when the application is running in the foreground, which is displayed by default. This parameter takes effect only for the TPNS and FCM channels. Valid values:<li>`1`: no</li><li>`2`: yes</br>Note: if the value is `1` and the application is running in the foreground, this push is imperceptible to end users, but arrival data will be reported.</li> |




**action parameter description**[](id:action)

| Parameter | Type | Parent Project | Default Value | Required | Description |
| ----------- | ------- | ------ | ------ | ------------------------------------------- | ------------------------------------------------------------ |
| action_type    | Integer | action  | 1     | No   | One-click actions. Valid values:<li>1: open activity or the application</li><li>2: open the browser</li><li>3: open the application’s custom page (recommended; for more information, see [here](https://intl.cloud.tencent.com/document/product/1024/32624)).</li> |
| activity    | String  | action | Empty     | Yes if `action_type` is `1` and an activity needs to be opened | Full name of activity, such as `com.x.y.PushActivity`                   |
| aty_attr    | Object  | action | Empty     | No if `action_type` is `1` and an activity needs to be opened | Activity attribute<li>if: `Flag` attribute of `Intent` in `Integer` type<li>pf: `Flag` attribute of `PendingIntent` in `Integer` type |
| browser     | Object  | action | Empty     | Yes if `action_type` is `2`                       | Action to open a browser<li>url: webpage URL in `String` type. Only HTTP and HTTPS URLs are supported</li><li>confirm: whether user's confirmation is required. The value is in `Integer` type.</li>1: yes<br>0: no |
| intent      | String  | action | Empty     | Yes if `action_type` is `3`                       | Custom scheme, such as `xgscheme://com.tpns.push/notify_detail`     |

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
						"aty_attr": {// Activity attribute, only for action_type=1
								"if": 0, // Intent's Flag attribute
								"pf": 0  // PendingIntent's Flag attribute
						},
						"browser": {
								"url": "https://cloud.tencent.com ", // Only HTTP and HTTPS URLs are supported
								"confirm": 1 // Whether user's confirmation is required
						},
						"intent": "xgscheme://com.tpns.push/notify_detail" //The SDK must be version 1.0.9 or later. Configure the data tag in the client's Intent and set the scheme attribute
				},
				"custom_content":"{\"key\":\"value\"}"
			}
}
```

### Notification message on iOS

The table below specifies parameters for the iOS platform.

| Parameter | Type | Parent Project | Default Value | Required | Description |
| ------ | ------ | ------- | ------ | ---- | -------------------------------------------------- |
| title                    | String | message | Empty     | Yes   | Message title, which will override the content in `title` under `alert`.                                                   |
| content                  | String | message | Empty     | Yes   | Message content, which will override the content in `body` under `alert`.
| thread_id                | String | message | Empty     | No   | Thread ID for collapsed notification in threaded display                                     |
| ios    | Object       | message  | Empty    | Yes    | iOS message structure. See [iOS parameter description](#iOS) for more information. |
| show_type      | Integer | message | 2      | No  | Whether to display the notification when the application is running in the foreground. Valid values:<li>`1`: no</li><li>`2`: yes</br>Note: if the value is `1` and the application is running in the foreground, this push is imperceptible to end users, but arrival data will be reported.</li> |
| xg_media_resources    | String     | message | Empty    | No    | URL of rich media elements such as image, audio, and video                          |



#### iOS parameter description[](id:iOS)

| Parameter | Type | Parent Project | Default Value | Required | Description |
| -------------- | ------ | ------ | ------ | ---- | ------------------------------------------------------------ |
| aps             | Object  | ios    | Empty    | Yes    | APNs-specific parameter. For more information, see [aps parameter description](#aps). For further information, see [Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1). |
| custom_content  | String  | ios    | Empty    | No    | Custom parameter for delivery, which must be serialized to a JSON string.                                |


**aps parameter description**[](id:aps)

| Parameter | Type | Parent Project | Default Value | Required | Description |
| --------------- | ------- | ------ | ------ | ---- | ------------------------------------------------------------ |
| alert           | Object  | aps    | Empty     | Yes   | Contains the title and message content.                                           |
| badge_type      | Integer | aps    | Empty                 | No        | User-configured badge number. Valid values:<li>-1: the badge number does not change.</li> <li> -2: the badge number automatically increases by 1.</li><li> >=0: a custom badge number is configured.</li> |
| category        | String  | aps    | Empty     | No   | Action identifier displayed when the message is pulled down.                                     |
| mutable-content | Integer | aps    | 1     | No   | This is an additional notification parameter that carries "mutable-content" during push.<li>1 means that the Service Extension supports iOS 10.</li><li>Once enabled, the push details will include the arrival data report. Before using this feature, see [Notification Service Extension](https://intl.cloud.tencent.com/document/product/1024/30730) to implement the Service Extension API. If `mutable-content` is not carried, arrival data will not be reported.</li> |
| sound           | String  | aps    |  Empty    | No    | Use instructions:<li>To play the system default ringtone, use "sound":"default"</li><li>To play local custom ringtone, use "sound":"chime.aiff"</li><li>To mute, use "sound":"" or remove the `sound` parameter. Note: if you want to use a custom ringtone, the ringtone must be in Linear PCM, MA4 (IMA/ADPCM), alaw, or μLaw format, saved in the `bundle` directory of the project, and last for 30 seconds at most; otherwise, the system default ringtone will be used.</li> |

Below is a sample of a complete message:

```json
{
    "title": "xxx",
    "content": "xxxxxxxxx",
    "thread_id":"Activity_id",
    "xg_media_resources":"https://www.xx.com/img/bd_logo1.png",
    "show_type":1,
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
       "custom_content":"{\"key\":\"value\"}"
    }
}
```

### In-app message on Android

In-app message is unique to the Android platform and not displayed in the notification bar of the mobile phone. It can be used to deliver controlled messages to users imperceptibly.

>!Due to vendor restrictions, Android in-app messages can be delivered only through the TPNS channel, but not vendor channels.

The table below specifies parameters for the Android platform:

| Parameter | Type | Parent Project | Default Value | Required | Description |
| -------------- | ------ | ------- | ------ | -------- | ------------------------------------------------------------ |
| title          | String | message | Empty     | Yes       | Command description                                                    |
| content                  | String | message | Empty     | Yes   | Command content                                                     |
| android        | Object | message | Empty     | No       | Android message structure                                               |
| accept_time    | Array  | message |  Empty    | No    | The time period that allows pushes.<li>A single element is formed by a "start" time and an "end" time.</li><li>"start" and "end" are indicated by hour and minute. For more information, please see the samples.</li><li>**Note:** this is valid only for the TPNS channel due to vendor restrictions.</li> |
| custom_content | String | android | Empty     | No       | Custom content, which must be serialized to a JSON string                                    |

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


### iOS silent messages[](id:aps2)

Similar to in-app messages on Android, silent messages are unique to the iOS platform and are not displayed. When a silent message arrives at the device, iOS wakes up the application for a period of time (less than 30 seconds) in the background to let the application handle the message logic.

The specific parameters are as follows:

| Parameter | Type | Parent Project | Default Value | Required | Description |
| -------------- | ------ | ------- | ------ | -------- | ------------------------------------------------------------ |
| ios            | Object | message | Empty     | Yes       | iOS message structure                                               |
| aps    | Object       | ios  | Empty    | Yes    | APNs-specific parameter, where the most important key-value pair is as follows:<li>content-available: identifies the message type (which must be 1), in integer format.</li><li>The value cannot contain the `alert`, `sound`, or `badge_type` parameters. For more information, see [Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1). </li>**Note:** `content-available: 1` is mutually exclusive with [message_type:"notify"](#message body type). Do not use them at the same time. |
| custom_content | String | ios     | Empty    | No    | Custom content, which must be serialized to a JSON string.                                |



Complete sample:

```json
{
    "ios":{
        "aps": {
            "content-available": 1
        },
      "custom_content":"{\"key\":\"value\"}"
    }
}
```

## Optional Parameters

Optional push API parameters refer to advanced parameters that can be carried in a push message, except `audience_type`, `message_type`, and `message`.


| Parameter            | Type    | Parent Project | Required                          | Default Value                   | Description                                                         |
| --------------------- | ------- | ------ | ------------------------------ | ------------------------------------ | ------------------------------------------------------------ |
| expire_time          | Integer | None     | No                            | 259200 (72 hours)                     | Offline message retention duration (in seconds), up to 72 hours.<li>If `expire_time` is `0`, it indicates a real-time message.</li><li>If `expire_time` is greater than 0 and less than 800 seconds, the system will reset it to 800 seconds.</li><li>If `expire_time` is greater than or equal to 800 seconds, the message will be retained according to the set value, up to 72 hours.</li><li>The value set cannot exceed `2147483647`; otherwise, the push will fail.</li> |
| send_time            | String  | None     | No                             | Current system time                         | Push time. You can specify a push time in the next 90 days.<li>The format is yyyy-MM-DD HH:MM:SS.</li><li>If the push time specified is earlier than the current server time, the push starts immediately.</li><li>This parameter is supported only for push to all devices, push by account package, or push to devices with specified tags.</li> |
| multi_pkg            | Boolean | None     | No                             | false                                | Multi-package name push: for an application that has multiple packages (such as for MyApp and Wandoujia), if you want the application in all channels to receive the push message, you can set this value to `true`.<br>**Note**: this parameter controls the multi-package name push of the TPNS channel by default. To implement multi-package name push on vendor channels, see [Configuring vendor channel for multi-package name](https://intl.cloud.tencent.com/document/product/1024/35393). |
| loop_param           | Object  | None     | No                             | 0                                    | Loop push parameters. This parameter is supported only for push to all devices, push by account package, or push to devices with specified tags. For more information about loop push parameters, see the [loop_param parameter description](#loop_param) below. |
| group_id             | String  | None    | No                             | tpns_yyyymmdd, where `yyyymmdd` indicates the push date | **This parameter has been disused and will be unavailable in the future. If you need to use the aggregate statistics feature, please use the push plan parameter (plan_id).** |
| plan_id              | String  | None    | No                             | Empty                                   | Push plan ID. For more information about how to create and use the push plan, see [Push Plan](https://intl.cloud.tencent.com/document/product/1024/37452). |
| tag_rules             | Array  | None     | Yes for tag push only                 | Empty                                   |  <li>For push based on a combination of tags, you can set 'AND', 'OR', and 'NOT' rules</li><li>**Note:** if both `tag_rules` and `tag_list` are specified, `tag_list` becomes invalid automatically. For parameter descriptions, please see [tag_rules parameter description](#tag_rules).</li> |
| account_list         | Array   | None | Yes for push to a single account or a list of accounts | Empty       | For push to a single account:<li>`audience_type` must be `account`</li><li>Format: ["account1"]</li><br>For push to a list of accounts: <li>Format: `["account1","account2"]`</li><li>Up to 1,000 accounts</li> |
| account_push_type    | Integer | None     | No for push by account                 | 0                                    | Push type. Valid values: <li>0: push messages to the latest device of the account</li><li>1: push messages to all devices associated with the account</li> |
| account_type     | Integer | None     | No                 | 0                                    | Account type, which must be consistent with that of the accounts to push to. For valid values, see [Account Type Value Table](https://intl.cloud.tencent.com/document/product/1024/40598). |
| token_list    | Array   | None | Yes for push to a single device or a list of devices | Empty       | For push to a single device: <li>`audience_type` must be `token`<li>Format: ["token1"]<br>For push to a list of devices:<li>Format: ["token1","token2"]</li><li>Up to 1,000 tokens</li> |
| ignore_invalid_token   |  int  | None  | No    | 0   |<li> `0`: the API call will fail if there is an invalid token.<li> `1`: ignore the invalid token and continue to deliver.</li>**Note**: this parameter takes effect only for push by a token or token list.
| push_speed           | Integer | None    | No  | Empty                                  |<li>Push speed limit to X pushes per second. Value range of X: 1000-50000</li><li>This parameter is valid only for push to all devices, push by account package, and push to devices with specified tags.</li> |
| collapse_id          | Integer | None    | No                             | System-assigned `collapse_id`       | <li>Message overriding parameter. After the first push task has been scheduled and delivered, if the second push task carries the same `collapse_id`, it will stop the TPNS channel data in the first push task that has not been delivered yet and will also overwrite the message in the first push task.<li>The `collapse_id` of a completed task can be obtained via the [Querying Push Information for One Task](https://intl.cloud.tencent.com/document/product/1024/33773) API.<li>Currently, this is supported only for push to all devices, push to devices with specified tags, and push by account package. |
| channel_rules        | Array   | None    | No                             | Empty                                   | Push channel selection policy.<li>You can select the channels through which a push can be delivered. Messages are pushed through all channels by default. For more information about the push policy, see [Channel Policies](https://intl.cloud.tencent.com/document/product/1024/36151).<li>For the data structure of single elements in the `channel_rules` array, see [channel_rules parameter description](#channel_rules parameter description 1) below. |
| tpns_online_push_type | Integer | None | No | 0 | Whether to push the message to online devices through the TPNS channel. Valid values: <li>`0`: yes<li> `1`: no |
| force_collapse | Boolean | None | No | false | Whether to deliver messages to OPPO or Vivo devices that do not support message overriding. Valid values:<li>`false`: no</li><li>`true`: yes</li> |



>? The `collapse_id` parameter is subject to the following restrictions:
> - This parameter currently cannot be customized. Only `collapse_id` values generated by TPNS can be used.
> - This parameter is supported only for the TPNS channel, APNs channel, Mi channel, Meizu channel, and Huawei devices on EMUI 10 and above.
> - For the Huawei channel, you must use [intent](#intent1) to carry custom parameters to implement message overriding. If you use `custom_content`, the API layer will block custom parameters.
> - Currently, the OPPO and vivo channels do not support message overriding. When an overriding message is created, delivery to the OPPO and vivo channels can be disabled by setting the `force_collapse` parameter to `false`.
> 



### tag_rules parameter description[](id:tag_rules)

| Parameter     | Type    | Parent Project    | Required | Description                                                         |
| --------- | ------- | --------- | ---- | ------------------------------------------------------------ |
| tag_items | Array   | tag_rules | Yes   | Tag rule. See [tag_items description](#tag_items2).                 |
| operator  | String  | tag_rules | Yes   | Operator between elements in the `tag_rules` array. The operator of the first `tag_rules` element is invalid data. The operator of the second `tag_rules` element is the operator between the first and second `tag_rules` elements, and so on. Valid values:<li>`OR`: OR operation<li>`AND`: AND operation |
| is_not    | Boolean | tag_rules | Yes   | Whether to perform "NOT" operation on the calculation result of the `tag_items` array.<li>`true`: yes<li>`false`: no</li> |


#### tag_items description[](id:tag_items2)

| Parameter      | Type    | Parent Project    | Required | Description                                                         |
| -------------- | ------- | --------- | ---- | ------------------------------------------------------------ |
| tags           | Array   | tag_items | Yes   | Specific tag value in string type, such as `tag1` and `guangdong`           |
| is_not         | Boolean | tag_items | Yes   | Whether to perform "NOT" operation on the calculation result of the `tags` array. Valid values:<li>`true`: yes<li>`false`: no |
| tags_operator  | String  | tag_items | Yes   | Operator for tag in `tags`. Valid values: <li>`OR`: OR operation<li>`AND`: AND operation    |
| items_operator | String  | tag_items | Yes   | Operator between elements in the `tag_items` array. The `items_operator` of the first `tag_items` element is invalid. The `items_operator` of the second `tag_items` element is the operator between the first and second `tag_items` elements, and so on. Valid values:<li>`OR`: OR operation<li>`AND`: AND operation</li>**Note:** between different rules, AND takes precedence over OR. |
| tag_type       | String  | tag_items | Yes   | See [tag_type value table](#tag123).                              |



#### tag_type value table[](id:tag123)

| **Tag Name** | **tag_type Value**      | **Sample Tag**          |
| ------------ | ---------------------- | ----------------------- |
| Custom tag   | xg_user_define         | tag1, tag2           |
| Application version      | xg_auto_version        | 1.1.0, 1.2.0.1        |
| Device district information | xg_auto_province       | guangdong, shanghai  |
| Active information     | xg_auto_active         | 20200131, 20200201    |
| XG SDK version   | xg_auto_sdkversion     | 1.1.5.2, 1.1.5.3      |
| System language     | xg_auto_systemlanguage | zh, en                |
| Mobile phone brand     | xg_auto_devicebrand    | Mi, vivo         |
| Mobile phone model     | xg_auto_deviceversion  | MI 9 SE, vivo X9Plus |
| Country/Region | xg_auto_country | CN, SG |

>? For more information about the usage, see [Sample tag push](#biaoqianshili).
>


<span id="channel_rules parameter description 1"></span>

### channel_rules parameter description

| Parameter | Type    | Parent Project | Required | Description                                                        |
| ------- | ------- | ------------- | -------- | ------------------------------------------------------------ |
| channel | String  | channel_rules | Yes       | Delivery push channel. Valid values:<li> `hw`: Huawei channel</li><li> `xm`: Mi channel</li><li> `mz`: Meizu channel</li><li> `vivo`: vivo channel</li><li>`oppo`: OPPO channel</li><li>`apns`: APNs channel</li> |
| disable | Boolean | channel_rules | Yes       | Whether to disable the channel specified in `channel`, which is enabled by default. Valid values:<li>`true`: disable</li><li>`false`: enable</li> |

<span id="loop_param parameter description"></span>

### loop_param parameter description

| Parameter | Type    |  Parent Project | Required | Description                                                        |
| ------------- | ------- | ---------- | -------- | ------------------------------------------------------------ |
| startDate     | String  | loop_param | Yes       | Loop interval start date in YYYY-MM-DD format, such as 2019-07-01. You can choose a date in the next 90 days. |
| endDate       | String  | loop_param | Yes       | Loop interval end date in YYYY-MM-DD format, such as 2019-07-07. You can choose a date in the next 90 days. |
| loopType      | Integer | loop_param | Yes       | Loop type. Valid values:<li>`1`: daily</li><li>`2`: weekly</li><li>`3`: monthly</li>                  |
| loopDayIndexs | Array   | loop_param | Yes       | For weekly loop, enter days [0-6] in a week. If the value is [0, 1, 2], it indicates that the push will be done on Monday, Tuesday, and Wednesday every week. |
| dayTimes      | Array   | loop_param | Yes       | Specific push time in HH:MM:SS format. If the value is ["19:00:00", "20:00:00"], it indicates that the push will be done at 19:00 and 20:00 every day. |



## Response Parameters

| Parameter      | Type    | Description                                                         |
| ----------- | -------| ------------------------------------------------------------ |
| seq         | Integer | Same as the request (if the request does not contain this parameter, this parameter returns `0`).              |
| push_id     | String | Push ID                                                      |
| invalid_targe_list | Array      |  This parameter is returned only when the push target is `token_list` and the value of `ignore_invalid_token` is `1`. This parameter stores filtered invalid tokens, and delivers to devices with valid tokens properly. |
| ret_code    | Integer | Error code. For more information, please see the error codes table.                                 |
| environment | String  | Push environment specified by the user (only for iOS). Valid values: <li>`product`: production environment</li><li>`dev`: development environment</li> |
| err_msg     | String  | Error message when a request error occurs                                         |
| result      | String   | When the request is correct:<li>If there is extra data to be returned, the result will be encapsulated in this parameter in JSON format.<li>If there is no extra data, this parameter may not exist.</li> |



## Examples
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
    "message":{
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
						"aty_attr": {// Activity attribute, only for action_type=1
								"if": 0, // Intent's Flag attribute
							    "pf": 0  // PendingIntent's Flag attribute
						},
						"browser": {
								"url": "xxxx ", // Only HTTP and HTTPS URLs are supported
								"confirm": 1 // Whether user's confirmation is required
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
     "title": "Push title",
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
       "custom_content":"{\"key\":\"value\"}"
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


### Push by tag (using tag_rules)[](id:biaoqianshili)

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
                    "is_not": false,   //Whether to perform the "NOT" operation on the calculation result of the tags in `tags`. Valid values: `true`: yes; `false`: no
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

**Sample 2: push messages to Huawei users who were active in the last 3 days on an application version other than 1.0.2**
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
                    "is_not": false,   //Whether to perform the "NOT" operation on the calculation result of the tags in `tags`. Valid values: `true`: yes; `false`: no
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

