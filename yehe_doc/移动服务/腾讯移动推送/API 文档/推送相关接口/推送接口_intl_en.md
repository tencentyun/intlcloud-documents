## API Description

**Request method**: POST.

The API request address corresponds to the service access point one by one; therefore, please select the request address corresponding to your application service access point.

Service access point in Guangzhou:

```plaintext
https://api.tpns.tencent.com/v3/push/app
```

Service access point in Hong Kong (China):

```plaintext
https://api.tpns.hk.tencent.com/v3/push/app
```

Service access point in Singapore:

```plaintext
https://api.tpns.sgp.tencent.com/v3/push/app
```

**Feature**: `Push` API is the general term for all push APIs. Push API has many types of push targets, which are described as follows.
All request parameters are uploaded via JSON encapsulation to the backend, which distinguishes among different push targets based on the request parameters. If you have any questions, please see [Server Error Codes](https://intl.cloud.tencent.com/document/product/1024/33763).

## Required Parameters

The required push parameters refer to the parameters that must be carried in a push message.

| Parameter Name | Type | Required | Description |
| ------------- | ------- | ---------------------- | ------------------------------------------------------------ |
| audience_type | String | Yes | Push target <li>all: full push </li><li>tag: tag push </li><li>token: single-device push </li><li>token_list: device list push </li><li>account: single-account push </li><li>account_list: account list push</li><li>package_account_push: number package push |
| message       | Object | Yes | This is the message body; for more information, please see [Message Body Types](#Message Body Types) |
| message_type | String | Yes | Message type <li>notify: notification </li><li>message: in-app/silent message</li> |
| environment | String | Yes (only for iOS) | This specifies the push environment (only available for pushes on iOS) <li>product: production push environment </li><li>dev: development push environment </li> |
| upload_id   | Integer  | Yes (only available for number package push)        | Number package upload ID  |

<span id="audience_type"></span>

### audience_type: push target

Push target indicates which devices a push can be delivered to.
Push API provides a variety of push targets, such as all, tag, single device, device list, single account, and account list.

| Push Target | Description | Required Parameters and Use Instructions |
| -------------------- | ------------ | ------------------------------------------------------------ |
| all | Full push | None |
| tag | Tag push | 1. `tag_list`: <li>Push to devices with tag1 and tag2 `{"tags":["tag1","tag2"],"op":"AND"}`</li><li> Push to devices with tag1 or tag2 `{"tags":["tag1","tag2"],"op":"OR"}`</li><li> Tag list cannot exceed 512 characters</li>2. `tag_rules`: <li>for tag combination push, you can set "AND", "OR", and "NOT" combining rules. </li><li>**Note:** if both this parameter and `tag_list` are present, `tag_list` will be automatically invalid. For parameter descriptions, please see [Tag combination rules](#biaoqianzh). |
| token | Single-device push | `token_list`<li>If the parameter contains multiple tokens, it will only push to the first token </li><li>Format example: ["token1"] </li><li>A token string cannot exceed 36 characters</li> |
| token_list   | Device list group push | `token_list`<li>Up to 1,000 tokens</li><li>Format example: ["token1","token2"]</li><li>A token string cannot exceed 36 characters</li> |
| account | Single-account push | `account_list` <li>If the parameter contains multiple account, it will only push to the first account</li><li>Format example: ["account1"] </li> |
| account_list | Account list group push | `account_list` <li>has a maximum of 1000 accounts<li> Format example: ["account1","account2"]</li> |
| package_account_push | Number package push | Required for number package push |

<span id="biaoqianzh"></span>

### Tag combination rules

| Field   |  Type  | Required | Description |
| --------- | ----- | ---- | ---------------------------------------------- |
| tag_rules | Array | Yes | Tag rule set. For more information, please see [tag_rules description](#tag_rules). |

<span id="tag_rules"></span>

#### tag_rules description

| Field | Type | Parent Item | Required | Description |
| --------- | ------- | --------- | ---- | ------------------------------------------------------------ |
| tag_items | Array   | tag_rules | Yes| Tag rule. For more information, please see [tag_items description](#tag_items2). |
| operator  | String  | tag_rules | Yes | Operator between elements in the `tag_rules` array. The operator of the first `tag_rules` element is invalid data, the operator of the second `tag_rules` element is the operator between the first and second `tag_rules` elements, and so on. <li>OR: OR operation <li>AND: AND operation |
| is_not    | Boolean | tag_rules | Yes | Whether to perform "NOT" operation on the calculation result of the `tag_items` array. <li>true: yes <li>false: no </li>|



<span id="tag_items2"></span>

#### tag_items description

| Field | Type | Parent Item | Required | Description |
| -------------- | ------- | --------- | ---- | ------------------------------------------------------------ |
| tags           | Array   | tag_items | Yes | Specific tag value in string type, such as tag1 and guangdong. |
| is_not         | Boolean | tag_items | Yes| Whether to perform "NOT" operation on the calculation result of the tag array. <li>true: yes <li>false: no |
| tags_operator  | String  | tag_items | Yes| Operator for tags in `tags`. <li>OR: OR operation <li>AND: AND operation |
| items_operator | String  | tag_items | Yes| Operator between elements in `tag_items` array. The `items_operator` of the first element is invalid data, the `items_operator` of the second element is the operator between the first and second elements, and so on. <li>OR: OR operator<li>AND: AND operation</li>|
| tag_type       | String  | tag_items | Yes   | Please see [tag_type value table](#tag123)                              |

<span id="tag123"></span>

#### tag_type value table

| **Tag Name**          | **tag_type Value**   | **Tag Name Example** |
| ------------ | ---------------------- | ----------------------- |
| Custom tag | xg_user_define | tag1, tag2, etc.   |
| Application version       | xg_auto_version | 1.1.0, 1.2.0.1, etc.  |
| Device district information  | xg_auto_province | guangdong, shanghai, etc.  |
| Active information | xg_auto_active  | 20200131, 20200201, etc.                |
| XG SDK version   | xg_auto_sdkversion  | 1.1.5.2, 1.1.5.3, etc.              |
| System language   | xg_auto_systemlanguage  | zh, en, etc.            |
| Phone brand   | xg_auto_devicebrand  | Mi, Vivo, etc.             |
| Phone model   | xg_auto_deviceversion | Mi 9 SE, Vivo X9 Plus, etc.             |

> ?For detailed usage, please see [Tag push samples](#biaoqianshili).

- Full push: push to all devices

```json
  {
    "audience_type": "all"
  }
```

- Tag push (in `tag_rules` method): male users who were active on April 8, 2020 in Guangdong or Hunan

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

- Single-device push: push to devices with token1 as the token

```json
  {
    "audience_type": "token",
    "token_list": [
        "token1"
    ]
  }
```

- Device list push: push to devices with token1 and token2 as their tokens

```json
  {
    "audience_type": "token_list",
    "token_list": [
        "token1",
        "token2"
    ]
  }
```

- Single-account push: push to device(s) bound to account1

```json
  {
    "audience_type": "account",
    "account_list": [
        "account1"
    ]
  }
```

- Account list push: push to device(s) bound to account1 and account2

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

### message_type: message body type

For different platforms, the message types are slightly different. For more information, please see the table below:

| Message Type | Description | Supported Platform | Feature Description |
| -------- | ----------------- | -------------------------------------- | ------------------------------------------------------------ |
| notify | Notification bar message | Android and iOS | Message is displayed in the notification bar |
| message | In-app or silent message | Android (in-app message) <br>iOS (silent message) | Notifications are not displayed in the notification bar. Due to vendor restrictions, Android in-app messages are only delivered through the TPNS channel and cannot be delivered through the vendor channel |

### message: message body

The message body is the message delivered to the client.
The Push API handles messages on iOS and Android differently, so you need to implement message pushes for the two platforms separately. The push message body is in JSON format.

### General message on Android

The specific fields for the Android platform are as follows:

| Field Name | Type | Parent Item | Default Value | Required | Parameter Description |
| ------------------------ | ------ | ------- | ------ | ---- | ------------------------------------------------------------ |
| title                | String  |       message       | None          | Yes        | Message title.  |
| content | String | message | None | Yes | Message content. |
| accept_time    | Array  | message       | None    | No    | The time period at which the message is allowed to be pushed to users. <li>A single element is formed by a "start" time and an "end" time. <li>"start" and "end" are indicated by hour and minute. For more information, please see the samples. <li>**Note:** this is only valid for the TPNS channel due to vendor restrictions. |
| thread_id       | String  | message       |None    | No    | Thread name for collapsed notification in threaded display |
| thread_sumtext      | String  | message       |None    | No    | Summary displayed after the notification is collapsed in a thread, which is valid if `thread_id` is not empty |
| xg_media_resources       | String | message | None     | No   | URL address of big image in notification bar, which takes effect only for the TPNS and Mi channels; <li>**Note:** if you want to use the big image notification feature of the Mi channel, you need to call the Mi image uploading API to upload an image file, get the `pic_url` image address specified by Mi, and enter it in the corresponding parameter `xg_media_resources` of TPNS. For more information, please see the image uploading API section in [Rich Text Message in Mi Push](https://dev.mi.com/console/doc/detail?pId=1163#_10_0). |
| xg_media_audio_resources    | String  | message       | None    | No    | Element address for audio rich media, <li>which can be audio in .mp3 format and is recommended to be of no more than 5 MB in size. <li>**Note:** only the TPNS channel supports delivering this parameter, while other channels do not deliver it. |
| android              | Object | message      | None    | No    | Structure of advanced settings for Android notification. For more information, please see the [Android structure description](#intent1) |

<span id="intent1"></span>

#### Android structure description

| Field Name | Type | Parent Item | Default Value | Required | Parameter Description |
| -------------- | ------- | ------- | ------ | ---- | ------------------------------------------------------------ |
| n_ch_id     | String    | Android      | None    | No    | Notification channel ID (only valid for the TPNS channel). For more information, please see [Creating Notification Channels](https://intl.cloud.tencent.com/document/product/1024/30715)                                 |
| n_ch_name     | String    | Android      | None    | No    | Notification channel name (only valid for the TPNS channel). For more information, please see [Creating Notification Channels](https://intl.cloud.tencent.com/document/product/1024/30715) |
| xm_ch_id    | String    |   Android      | None    | No    | Mi channel ID (only valid for the Mi channel)                            |
| hw_ch_id   | String    |   Android      | None    | No    | Huawei channel ID (only valid for the Huawei channel)                            |
| oppo_ch_id    | String    |   Android      | None    | No    | OPPO channel ID (only valid for the OPPO push channel)                           |
| vivo_ch_id     | String  | Android | 0      | No    | Vivo channel ID. "0" indicates operation message, and "1" indicates system message (this parameter takes effect only for the Vivo push channel) |
| builder_id     | Integer    | Android      | 0    | No | Local notification style ID |
| badge_type     | Integer | android | -1     | No|Notification badge, which takes effect only for Huawei devices. Valid values: <li>-2: auto increased by 1; </li><li>-1: unchanged</li> |
| ring           | Integer | Android | 1      | No    | Whether there is a ringtone<li>0: no</li><li>1: yes  </li>           |
| ring_raw       | String  | Android | None | No | This specifies the name of the ringtone file in the raw directory of the Android project; no extension is needed |
| vibrate        | Integer    | Android       | 1    | No    | Whether the device vibrates</li><li>0: no<li>1: yes</li>            |
| lights         | Integer | Android | 1      | No    | Whether the breathing light is used</li><li>0: no <li>1: yes</li>       |
| clearable      | Integer    | Android      | 1    | No | Whether the notification bar can be dismissed. |
| icon_type      | Integer    | Android      | 0    | No    | Whether the notification bar icon is an in-app icon or an uploaded icon<li>0: in-app icon</li><li>1: uploaded icon</li> |
| icon_res       | String | Android       | None    | No    | URL address of thumbnail on notification bar, which is supported only for the TPNS and Huawei channels                     |
| style_id       | Integer    | Android | 1 | No | This specifies whether to override the notification style with the specified number |
| small_icon | String | Android | None | No | The icon that the message displays in the status bar. If not set, the application icon will be displayed |
| action | Object   | Android | Yes | No | This sets the action after the notification bar is clicked; the default action is to open the application. |
| action_type    | Integer | Action  | Yes   | No     | Click action type. <li>1: opens activity or the application itself </li><li>2: opens browser</li><li>3: opens Intent (recommended; for more information, please see [Configuration Guide](https://intl.cloud.tencent.com/document/product/1024/32624))  </li> |
| custom_content | String  | Android | None     | No   | User-defined parameter (required to be serialized into a JSON string) <br> **Note:** <li>To adapt to advanced vendor features, TPNS upgraded the Huawei push protocol to v4 on July 15, 2020, which does not support carrying custom parameters through the `custom_content` field. <li>If you have integrated the Huawei vendor channel, we recommend you use  [intent](https://intl.cloud.tencent.com/document/product/1024/32624) to carry custom parameters; otherwise, custom parameters cannot be delivered through the Huawei channel. <li>If you need to continue using the original v2 protocol, please click **Submit a ticket** in the top-right corner in the console, and you will be added to the allowlist. |
| show_type      | Integer | Android | 2      | No | Whether to display notification when the application is in the foreground, which is displayed by default. This takes effect only for TPNS and FCM channels. <li>1: no<li>2: yes. <br>Note: if the value is 1 and the application is in the foreground, the end user will not be aware of the push, but arrival data will be reported.</br> |



Below is an example of a complete message:

```json
{
    "title": "xxx",
    "content": "xxxxxxxxx",
    "xg_media_resources": "xxx1" , // Enter the rich media element address, such as https://www.xx.com/img/bd_logo1.png?qua=high
    "xg_media_audio_resources":"xxx", // Enter the audio rich media element address, such as http://sc1.111ttt.cn/2018/1/03/13/396131227447.mp3 
    "thread_id":"Event_id",
    "thread_sumtext":"Marketing event",
    "accept_time": [
        {
            "start": {// Period start time,
                "hour": "13",// Start time in hour. Value range: [0:24)
                "min": "00"// Start time in minute. Value range: [0:60)
            },
            "end": {// Period end time
                "hour": "14",// End time in hour. Value range: [0:24)
                "min": "00" // End time in minute. Value range: [0:60)

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
                "if": 0, // Intent's `Flag` attribute
                "pf": 0  // PendingIntent's `Flag` attribute
            },
            "browser": {
                "url": "xxxx ", // Only `http` and `https` are supported
                "confirm": 1 // Whether user's confirmation is needed
            },
            "intent": "xxx" // The SDK version must be 1.0.9 or higher. Configure the data tag in the client's intent and set the scheme attribute
        },
      "custom_content":"{\"key\":\"value\"}"
    }
}

```

### General message on iOS

The specific fields for the iOS platform are as follows:

| Field Name | Type | Parent Item | Default Value | Required | Parameter Description |
| ------ | ------ | ------- | ------ | ---- | -------- |
| title                | String  |       message       | None          | Yes        | Message title.  |
| content | String | message | None | Yes | Message content. | 
| thread_id       | String  | message       |None    | No    | Thread name for collapsed notification in threaded display |
| ios    | Object       |message  | None    | Yes    | iOS message structure. For more information, please see the [iOS field description](#iOS)  |
| xg_media_resources    | String     | message | None    | No    | URL address of rich media element such as image, audio, and video                          |


<span id="iOS"></span>

#### iOS field description

| Field Name | Type | Parent Item | Default Value | Required | Parameter Description |
| --------------- | ------- | ------ | ------ | ---- | ------------------------------------------------------------ |
| aps    | Object   | ios  | None    | Yes    | APNs-specific field. For more information, please see [Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1) |
| alert           | Object  | aps    | None    | Yes    | It contains the title and message content |
| badge_type | Integer | aps | None | No | The user-configured badge number: <li> -1: badge number does not change <li> -2: badge number automatically increases by 1 <li> >=0: a custom badge number is configured |
| category        | String  | aps    | None    | No    | The action ID displayed when the message is pulled down |
| mutable-content | Integer |     aps | None    | No    | This is a notification expansion parameter that carries "mutable-content" during push: <li>1 means that the Service Extension supports iOS 10. <li>Once enabled, the push details will include the arrival data report. Before using this feature, please implement the Service Extension API as instructed in [Notification Service Extension Use Instructions](https://intl.cloud.tencent.com/document/product/1024/30730). If this field is not carried, arrival data will not be reported. |
| sound           | String  | aps    | None    | No    | The `sound` field is used as follows: <br>1. To play back the system default ringtone, use `"sound":"default"`<br>2. To play back local custom ringtone, use `"sound":"chime.aiff"` <br>3. To mute, use `"sound":""` or remove the custom ringtone description in the `sound` field. Note: the ringtone must be in Linear PCM, MA4 (IMA/ADPCM), alaw, or μLaw format, put in the `bundle` directory of the project, and of no more than 30s in length; otherwise, the system default ringtone will be used. |
| custom_content  | String  | ios    | None    | No    | Parameters for custom delivery, which must be serialized to JSON string                                |
| xg | String | ios | None | No | key reserved by the system, which should not be used |

Below is an example of a complete message:

```json
{
    "title": "xxx",
    "content": "xxxxxxxxx",
    "thread_id":"Event_id",
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

In-app message is unique to the Android platform and not displayed in the notification bar of the mobile phone. It can be used to deliver messages with control information to users in an imperceptible manner.

> !Due to vendor restrictions, Android in-app messages can only be delivered through the TPNS channels and cannot be delivered through the vendor channels.

The specific fields for the Android platform are as follows:

| Field Name | Type | Parent Item | Default Value | Required | Parameter Description |
| -------------- | ------ | ------- | ------ | -------- | ------------------------------------------------------------ |
| title          | String | message | None    | Yes    | Command description                     |
| content | String | message | None | Yes | Command content |
| android              | Object  | message      | None     | No    | Android message structure |
| custom_content | String | android | None    | No    | This must be serialized to JSON string                                |
| accept_time    | Array  | message       | None    | No    | The time period at which the message is allowed to be pushed to users. <li>A single element is formed by a "start" time and an "end" time. </li><li>"start" and "end" are indicated by hour and minute. For more information, please see the samples. </li><li>**Note:** this is only valid for the TPNS channel due to vendor restrictions. </li> |

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

### Silent message on iOS

Similar to in-app message on Android, silent message is unique to the iOS platform and not displayed. When the message arrives at the device, iOS will wake up the application for a period of time (less than 30 seconds) in the background to let the application handle the message logic.

The specific fields are as follows:

| Field Name | Type | Parent Item | Default Value | Required | Parameter Description |
| -------------- | ------ | ------- | ------ | -------- | ------------------------------------------------------------ |
| aps    | Object | ios  | None    | Yes    | APNs-specific field, where the most important `key-value` pair is as follows:<br>content-available: it identifies the message type (which must be 1) and cannot contain alert, sound, or badge_type fields<br>For more information, please see [Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1). |
| ios            | Object | message | None    | Yes    | iOS message structure  |
| custom_content | String | ios     |  None    | No    | This must be serialized to JSON string                                |
| xg | String | ios | None | No | key reserved by the system, which should not be used |



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

## Optional Parameters

Optional Push API parameters are the optional advanced parameters except `audience_type`, `message_type`, and `message`.



| Parameter Name | Type | Parent Item | Required | Default Value | Description |
| -------------------- | ------- | ------ | ------------------------------ | ------------------------------------ | ------------------------------------------------------------ |
| expire_time          | Integer | None | No | 259200 (72 hours) | Offline message retention duration (in seconds), up to 72 hours. <li>If `expire_time` = 0, it indicates real-time message </li><li>If `expire_time` is greater than 0 and less than 800 seconds, the system will reset it to 800 seconds </li><li>If `expire_time` >= 800 seconds, the message will be retained according to the actual set duration, up to 72 hours </li><li>The value set cannot exceed 2147483647; otherwise, the push will fail.</li> |
| send_time            | String  | None | No | Current system time | This specifies the push time: <li>The format is yyyy-MM-DD HH:MM:SS</li><li>If it is less than the current server time, the message will be pushed immediately </li><li>This field is supported only for full push and tag push.</li> |
| multi_pkg | Boolean | None | No| false | Multi-package name push: for an application that has multiple channel packages (such as for MyApp and Wandoujia), if you want the application in all channels to receive the push message, you can set this value to `true`. <br>**Note:** this parameter controls the multi-package name push of the TPNS channel by default. To implement multi-package name push for vendor channels, please see [Multi-Package Name Push for Vendor Channels](https://intl.cloud.tencent.com/document/product/1024/35393). |
| loop_param | Object | None | No                | 0       | For more information on loop push (full push and tag push), please see the [loop_param field description](#loop_param field description) below |
| group_id             | String  | None     | No                             | tpns_yyyymmdd, where `yyyymmdd` indicates the push date | This field has been disused and will be deactivated subsequently. If you need to use the aggregate statistics feature, please use the push plan field (plan_id). |
| plan_id              | String  | None     | No                             | None                                   | Push plan ID.  |
| tag_list      | Object | None | Only required for tag push          | None       | <li>Push to devices with tag1 and tag2: `{"tags":["tag1","tag2"],"op":"AND"}`</li><li>Push to devices with tag1 or tag2: `{"tags":["tag1","tag2"],"op":"OR"}` </li> |
| account_list  | Array  |None | Only required by single-account push and account list push | None       | For single-account push:<li>`audience_type` must be `account`</li><li>Parameter format: [ "account1" ]</li><br>For account list push: <li>Parameter format: `["account1","account2"]`</li><li>Up to 1,000 accounts </li> |
| account_push_type  | Integer  |  None | Optional for account push         | 0                                    | <li> 0: push message to the latest device of the account</li><li> 1: push message to all devices associated with the account</li> |
| token_list    | Array   |None | Required by single-device push and device list push | None       | For single-device push: <li>`audience_type` must be `token`<li>Parameter format: [ "token1" ]<br>For device list push: <li>Parameter format: [ "token1","token2" ]</li><li>Up to 1,000 tokens </li> |
| push_speed           | Integer | None | Only valid for full push and tag push | None | Sets push speed limit to X pushed per second. Value range of X: 1000–50000           |
| collapse_id          | Integer | None|No| The system assigns a `collapse_id` by default         | <li>Message overwriting parameter. After the first push task has been scheduled and delivered, if the second push task carries the same `collapse_id`, it will stop the TPNS channel data in the first push task that has not been delivered yet and will also overwrite the message in the first push task. <li>The `collapse_id` of a completed task can be obtained through the [single task push information querying API](https://intl.cloud.tencent.com/document/product/1024/33773). <li>Currently, this is supported only for full push, tag push, and number package push.  |
| channel_rules        | Array   | None|No|None| Push channel selection policy. <li>You can select the channels through which a push can be delivered. The push can be delivered through all channels by default. For detailed push policy, please see [Channel Policy](https://intl.cloud.tencent.com/document/product/1024/36151). <li>For the data structure of single elements in `channel_rules`, please see the [channel_rules parameter description](#channel_rules parameter description 1) below. |
force_collapse|Boolean|None|No|false| Whether to deliver messages to OPPO and Vivo devices that do not support message overwriting. <li>false: no <li>true: yes |

> ?For `collapse_id`, the following conditions of use apply:
>
> - This parameter currently is not customizable, and the `collapse_id` generated by TPNS is required. <li>This feature currently is supported only for the TPNS channel, APNs channel, Mi channel, Meizu channel, and Huawei devices on EMUI 10 and above. <li>For the Huawei channel, custom parameters can be carried in the [intent](#intent1) method during message overwriting. If you use `custom_content` to carry custom parameters, the API layer will block them. <li>Currently, the OPPO and Vivo channels do not support message overwriting. When an overwriting message is created, delivery to the OPPO and Vivo channels can be disabled by setting the `force_collapse` field to `false`.

<span id="channel_rules parameter description1"></span>

### channel_rules parameter description

| Field Name | Type | Required | Description |
| ------- | ------- | -------- | ------------------------------------------------------------ |
| channel | String | Yes       | Delivery push channel. <br> <li> hw: Huawei channel <li> xm: Mi channel <li> mz: Meizu channel <li> vivo: Vivo channel <li>oppo: OPPO channel |
| disable | Boolean   | No       | Whether to disable the corresponding channel in `channel`, which is enabled by default. <br><li>true: disable<li> false: enable |

<span id="loop_param parameter description"></span>

### loop_param parameter description

| Field Name | Type | Required | Description |
| ------------- | ------- | -------- | ------------------------------------------------------------ |
| startDate      | String | Yes    | Loop interval start date, with format of YYYY-MM-DD, such as 2019-07-01       |
| endDate | String   | Yes    | Loop interval start date, with format of YYYY-MM-DD, such as 2019-07-07               |
| loopType      | Integer | Yes | Loop type: <li>1: daily <li>2: weekly <li>3: monthly |
| loopDayIndexs | Array | Yes   | For weekly loop, enter number of weeks [0-6], and enter days as 0. If it is [0, 1, 2], it indicates that the push will be done on Monday, Tuesday, and Wednesday every week.                                |
| dayTimes   | Array  | Yes    | Specific push time, with the format as HH:MM:SS, such as ["19:00:00", "20:00:00"], indicates that the push will be done at 19:00 and 20:00 every day. |



## Response Parameters

| Field Name | Type | Required | Description |
| ----------- | ------- | -------- | ------------------------------------------------------------ |
| seq      | Integer | Yes | The same as the request packet (if the request packet is invalid JSON, this field is 0) |
| push_id | String | Yes | Push id |
| ret_code | Integer | Yes | Error code. For more information, please see the error codes table |
| environment | String | Yes | The push environment specified by the user (only for iOS). <li>product: production environment </li><li>dev: development environment </li> |
| err_msg | String | No | Error message when an error occurs in the request |
| result   | String  | No       | When the request is correct:<li>If there is extra data to be returned, the result will be encapsulated in the json of this field. If there is no extra data, <li>there may be no such field </li> |



## Samples

### Android tag push request message (tag_list)

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
    "xg_media_resources": "xxx1" , // Enter the rich media element address, such as https://www.xx.com/img/bd_logo1.png?qua=high
    "xg_media_audio_resources":"xxx", // Enter the audio rich media element address, such as http://sc1.111ttt.cn/2018/1/03/13/396131227447.mp3 
    "accept_time": [
        {
            "start": {// Period start time,
                "hour": "13",// Start time in hour. Value range: [0:24)
                "min": "00"// Start time in minute. Value range: [0:60)
            },
            "end": {// Period end time
                "hour": "14",// End time in hour. Value range: [0:24)
                "min": "00" // End time in minute. Value range: [0:60)

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
                "if": 0, // Intent's `Flag` attribute
                "pf": 0  // PendingIntent's `Flag` attribute
            },
            "browser": {
                "url": "xxxx ", // Only `http` and `https` are supported
                "confirm": 1 // Whether user's confirmation is needed
            },
            "intent": "xxx" // The SDK version must be 1.0.9 or higher. Configure the data tag in the client's intent and set the scheme attribute
        },
      "custom_content":"{\"key\":\"value\"}"
    }
}
}
```

### Tag push response message

```json
{
    "seq": 0,
    "environment": "product",
    "ret_code": 0,
    "push_id": "3895624686"
}

```

### iOS single-device push request message

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
       "custom_content":"{\"key\":\"value\"}",
        "xg": "oops"
    }
 }
}
```

### Single-Device push response message

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

### Tag push scenarios (tag_rules)

**Scenario 1: push a message to male users who were active on April 8, 2020 in Guangdong or Hunan**
Expression: (`xg_auto_province.guangdong` OR `xg_auto_province.hunan`) AND `xg_auto_active.20200408` AND `xg_user_define.male`

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
                    "is_not": false,   // Whether to perform "NOT" operation on the calculation result of the tags in `tags`. true: yes, false: no
                    "tags_operator": "OR",  // Operator for tags in `tags`
                    "items_operator": "OR", // Operator between elements in `tag_items`. The `items_operator` of the first element is invalid data, the `items_operator` of the second `TagItems` element is the operator between the first and second elements, and so on. |
                    "tag_type": "xg_auto_province" // Type of tags in `tags`
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

**Scenario 2: push a message to Huawei users on application version other than 1.0.2 who were active in the last three days**
Expression: (`xg_auto_active.20200406` OR `xg_auto_active.20200407` OR `xg_auto_active.20200408`) AND (NOT `xg_auto_version.1.0.2`) AND `xg_auto_devicebrand.huawei`

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
                    "is_not": false,   // Whether to perform "NOT" operation on the calculation result of the tags in `tags`. true: yes, false: no
                    "tags_operator": "OR",  // Operator for tags in `tags`
                    "items_operator": "OR", // Operator between elements in `tag_items`. The `items_operator` of the first element is invalid data, the `items_operator` of the second `TagItems` element is the operator between the first and second elements, and so on. |
                    "tag_type": "xg_auto_active" // Type of tags in `tags`
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

