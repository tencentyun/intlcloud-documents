## API Description
**Request method**: POST.

The API request address corresponds to the service access point one by one; therefore, please select the request address corresponding to your application service access point.

Service access point in Guangzhou:
```shell
https://api.tpns.tencent.com/v3/push/app
```
Service access point in Hong Kong (China):
```shell
https://api.tpns.hk.tencent.com/v3/push/app
```
Service access point in Singapore:
```shell
https://api.tpns.sgp.tencent.com/v3/push/app
```


**Feature**: `Push` API is the general term for all push APIs. Push API has many types of push targets, which are described as follows.
All request parameters are uploaded via JSON encapsulation to the backend, which distinguishes among different push targets based on the request parameters. If you have any questions, please see [Server Error Codes](https://intl.cloud.tencent.com/document/product/1024/33763).


## Required Parameters

The required push parameters refer to the parameters that must be carried in a push message.

| Parameter Name | Type | Required | Description |
| ------------- | ------ | ---- | ---------------------------------------- |
| audience_type | string | Yes | Push target <li>all: full push </li><li>tag: tag push </li><li>token: single-device push </li><li>token_list: device list push </li><li>account: single-account push </li><li>account_list: account list push</li><li>package_account_push: number package push |
| message       | object | Yes | This is the message body; for more information, please see [Message Body Types](#Message Body Types) |
| message_type | string | Yes | Message type <li>notify: notification </li><li>message: in-app/silent message</li> |
| environment | string | Yes (only for iOS) | This specifies the push environment (only available for pushes on iOS) <li>product: production push environment </li><li>dev: development push environment </li> |
| upload_id   | int32  | Yes (only available for number package push)        | Number package upload ID  |


### audience_type: push target

Push target indicates which devices a push can be delivered to.
Push API provides a variety of push targets, such as all, tag, single device, device list, single account, and account list.

| Push Target | Description | Usage |
| ------------ | ------------ | ------------------------------------------------------------ |
| all | Full push | None |
| tag | Tag push | 1. `tag_list`: <li>Push to devices with tag1 and tag2 `{"tags":["tag1","tag2"],"op":"AND"}`</li><li> Push to devices with tag1 or tag2 `{"tags":["tag1","tag2"],"op":"OR"}`</li><li> Tag list cannot exceed 512 characters</li>2. `tag_rules`: <li>for tag combination push, you can set "AND", "OR", and "NOT" combining rules. </li><li>⚠️ If both this parameter and `tag_list` are present, `tag_list` will be automatically invalid. For parameter descriptions, please see [Tag combination rules](#biaoqianzh). |
| token | Single-device push | `token_list`<li>If the parameter contains multiple tokens, it will only push to the first token </li><li>Format example: ["token1"] </li><li>A token string cannot exceed 36 characters</li> |
| token_list   | Device list group push | `token_list`<li>Up to 1,000 tokens</li><li>Format example: ["token1","token2"]</li><li>A token string cannot exceed 36 characters</li> |
| account | Single-account push | `account_list` <li>If the parameter contains multiple account, it will only push to the first account</li><li>Format example: ["account1"] </li>|
| account_list | Account list group push | `account_list` <li>can have a maximum of 1,000 accounts<li> Format example: ["account1","account2"]</li> |
|package_account_push | Number package push | Required for number package push |


<span id="biaoqianzh"></span>
### Tag combination rules

| Field   |  Type  | Required | Description |
| ------  | ----|----- -|--- |
|tag_rules| jsonArray|Yes | Tag rule set. For more information, please see [tag_rules description](#tag_rules). |


<span id="tag_rules"></span>
#### tag_rules description

| Field | Type | Parent Item | Required | Description |
| ------  | ----|-----|--- |--- |
|tag_items|jsonArray|tag_rules |Yes| Tag rule. For more information, please see [tag_items description](#tag_items2). |
|operator|string|tag_rules |Yes | Operator between elements in the `tag_rules` array. The operator of the first `tag_rules` element is invalid data, the operator of the second `tag_rules` element is the operator between the first and second `tag_rules` elements, and so on. <li>OR: OR operation <li>AND: AND operation |
|is_not |string|tag_rules | Yes | Whether to perform "NOT" operation on the calculation result of the `tag_items` array. <li>true: yes <li>false: no </li>|


<span id="tag_items2"></span>
#### tag_items description

| Field | Type | Parent Item | Required | Description |
| ------  | ----|-----|--- |--- |
|tags|array|tag_items | Yes | Specific tag value in string type, such as tag1 and guangdong. |
|is_not|string|tag_items |Yes| Whether to perform "NOT" operation on the calculation result of the tag array. <li>true: yes <li>false: no |
| tags_operator|string|tag_items |Yes| Operator for tags in `tags`. <li>OR: OR operation <li>AND: AND operation. |
| items_operator|string|tag_items |Yes| Operator between elements in `tag_items`. The `items_operator` of the first element is invalid data, the `items_operator` of the second element is the operator between the first and second elements, and so on. <li>OR: OR operator<li>AND: AND operation</li>|
| tag_type|string|tag_items |Yes| Please see [tag_type value table](#tag123). |

<span id="tag123"></span>
#### tag_type value table

| **Tag Name**          | **tag_type Value**   | **Tag Name Example** |
| ------------- | ------ | ---- |
| Custom tag | xg_user_define | tag1, tag2, etc.   |
| Application version       | xg_auto_version | 1.1.0, 1.2.0.1, etc.  |
| Device district information  | xg_auto_province | guangdong, shanghai, etc.  |
| Active status   | xg_auto_active  | 20200131, 20200201, etc.                |
| XG SDK version   | xg_auto_sdkversion  | 1.1.5.2, 1.1.5.3, etc.              |
| System language   | xg_auto_systemlanguage  | zh, en, etc.            |
| Phone brand   | xg_auto_devicebrand  | Mi, Vivo, etc.             |
| Phone model   | xg_auto_deviceversion | Mi 9 SE, Vivo X9 Plus, etc.             |

>For detailed usage, please see [Tag push samples](#biaoqianshili).

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
| -------- | ---------- | ------------- | -------------- |
| notify | Notification bar message | Android and iOS | Message is displayed in the notification bar |
| message | In-app or silent message | Android (in-app message) <br>iOS (silent message) | Notifications are not displayed in the notification bar. Due to vendor restrictions, Android in-app messages are only delivered through the TPNS channel and cannot be delivered through the vendor channel |

### message: message body

The message body is the message delivered to the client.
The Push API handles messages on iOS and Android differently, so you need to implement message pushes for the two platforms separately. The push message body is in JSON format.

### General message on Android

The specific fields for the Android platform are as follows:

| Field Name | Type | Parent Item | Default Value | Required | Parameter Description |
| -----               | ------   | ----       |-----      |    ---- | ----------- ------------------------ |
| title                | string  |       message       | None          | Yes        | Message title.  |                                   |
| content | string | message | None | Yes | Message content. |
| accept_time    | jsonArray  | message       |None    | No    | The time period at which the message is allowed to be pushed to users. <li>A single element is formed by a "start" time and an "end" time. <li>"start" and "end" are indicated by hour and minute. For more information, please see the samples. <li>⚠️This is only valid for the TPNS channel due to vendor restrictions. |
| xg_media_resources    | string  | message       |None  | No    | Element address for image rich media. ⚠️Due to vendor restrictions, pushes containing rich media cannot be delivered through the vendor channel. All must be delivered through the TPNS channel. |
| xg_media_audio_resources    | string  | message       |None  | No    | Element address for audio rich media. <li>MP3 format audio is supported. It is recommended that the content be smaller than 5 MB.<li>⚠️Due to vendor restrictions, pushes containing rich media cannot be delivered through the vendor channel. All must be delivered through the TPNS channel. |
| android              | JSON  | message      | None    | No    | Structure of advanced settings for Android notification. For more information, please see the [Android structure description](#intent1)|

<span id="intent1"></span>
#### Android structure description

| Field Name | Type | Parent Item | Default Value | Required | Parameter Description |
| -----           | ------   | ----       |-----      |    ---- | ----------- ------------------------    |
| n_ch_id     | string    | Android      | None    | No    | Notification channel ID (only valid for the TPNS channel). For more information, please see [Creating Notification Channels](https://intl.cloud.tencent.com/document/product/1024/30715)                                 |
| n_ch_name     | string    | Android      | None    | No    | Notification channel name (only valid for the TPNS channel). For more information, please see [Creating Notification Channels](https://intl.cloud.tencent.com/document/product/1024/30715)|
| xm_ch_id    | string    |   Android      | None    | No    | Mi channel ID (only valid for the Mi channel) |
| hw_ch_id   | string    |   Android      | None    | No    | Huawei channel ID (only valid for the Huawei channel) |
| oppo_ch_id    | string    |   Android      | None    | No    | OPPO channel ID (only valid for the OPPO push channel) |
| n_id           | int    | Android       |0    | No   | Unique ID of the notification message object (only valid for the TPNS channel).<li>Greater than 0: overwrites the previous message with the same ID.</li><li>Equal to 0: displays this notification and not affect other messages.</li><li>Equal to -1: all previous messages are cleared and only this message is shown </li> |
| builder_id     | int    | Android      |0    | No | Local notification style ID |
| badge_type	 |int	 |android	|-1	|No	|Notification badge, which takes effect only for Huawei devices. Valid values: <li>-2: automatically increase by one; </li><li>-1: unchanged</li>|
| ring           | int    |Android      |1    | No    | Whether there is a ringtone<li>0: no</li><li>1: yes  </li>           |
| ring_raw | string | Android | None | No | This specifies the name of the ringtone file in the raw directory of the Android project; no extension is needed |
| vibrate        | int    | Android       |1    | No    | Whether the device vibrates</li><li>0: no<li>1: yes</li>            |
| lights         | int    |Android       |1    | No    | Whether the LED indicator is used</li><li>0: no <li>1: yes</li>       |
| clearable | int | Android | 1 | No | Whether the notification bar can be dismissed. |
| icon_type      | int    | Android      |0    | No    | Whether the notification bar icon is an in-app icon or an uploaded icon<li>0: in-app icon</li><li>1: uploaded icon</li> |
| icon_res | string | Android | None | No | In-app icon file name or URL address of downloaded icon |
| style_id | int | Android | 1 | No | This specifies whether to overwrite the notification style with the specified number |
| small_icon | string | Android | None | No | The icon that the message displays in the status bar. If not set, the application icon will be displayed. |
| action | JSON | Android | Yes | No | This sets the action after the notification bar is clicked; the default action is to open the application. |
| action_type| int | Action      |Yes   | No     | Click action type. <li>1: opens activity or the application itself </li><li>2: opens browser</li><li>3: opens Intent (recommended ⚠️  [Configuration Guide](https://intl.cloud.tencent.com/document/product/1024/32624))          </li>  |
| custom_content | string | Android | None    | No    |  User-customized parameters. ⚠️ This must be serialized as a JSON string <li>If message overwriting is required, you cannot use `custom_content` to pass in custom parameters; instead, you need to change to use the intent method. |
| show_type | int | Android |2 | No | Whether to display notification when the application is in the foreground, which is displayed by default. This takes effect only for TPNS and FCM channels. <li>1: no<li>2: yes. <br>Note: if the value is 1 and the application is in the foreground, the end user will not be aware of the push, but arrival data will be reported.</br> |



Below is an example of a complete message:
```json
{
    "title": "xxx",
    "content": "xxxxxxxxx",
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
```

### General message on iOS

The specific fields for the iOS platform are as follows:


| Field Name | Type | Parent Item | Default Value | Required | Parameter Description |
| ------ | ----------- | ---- |--------------| ---- | ---------------------------------------- |
| ios    | JSON       |message  | None    | Yes    | iOS message structure. For more information, please see the [iOS field description](#iOS field description) |
| xg_media_resources    | string     | message | None    | No    | Rich media element address                          |
| xg | string | message| None | No | key reserved by the system, which should not be used |


<span id="iOS field description"></span>
#### iOS field description

| Field Name | Type | Parent Item | Default Value | Required | Parameter Description |
| ------ | ----------- | ---------------------------|---- | ---- | ---------------------------------------- |
| aps    | JSON       | ios  | None    | Yes    | APNs-specific field. For more information, please see [Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1)|
| alert   | JSON       |aps | None    | Yes    | It contains the title and message content |
| badge_type  | int   |   aps  | None    | No    | The badge number displayed by the application |
| category  | string    |    aps| None    | No    | The action ID displayed when the message is pulled down |
| mutable-content | int |     aps | None    | No    | This is a notification expansion parameter that carries "mutable-content" during push: <li>1 means that the Service Extension supports iOS 10. <li>After it is enabled, the push details will include the arrival data report. Before using this feature, implement the Service Extension API as instructed in [Notification Service Extension Use Instructions](https://intl.cloud.tencent.com/document/product/1024/30730). If this field is not carried, arrival data will not be reported. |
| sound  | string     | aps| None    | No    | The sound field is used as follows:<br>1: plays back system default prompt sound, "sound":"default"<br>2: plays back local custom ringtone ("sound":"chime.aiff")<br>3: mutes effect ("sound":"" or custom ringtone with the `sound` field removed). Note: the format must be Linear PCM, MA4 (IMA/ADPCM), alaw, or μLaw. Put the audio file in the project's `bundle` directory. The duration should be less than 30 seconds; otherwise, the system's default ringtone will be used.|
| custom_content | string |ios | None    | No    | Parameters for custom delivery, which must be serialized to JSON string                                |

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

### In-app message on Android
In-app message is unique to the Android platform and not displayed in the notification bar of the mobile phone. It can be used to deliver messages with control information to users in an imperceptible manner.

>Due to vendor restrictions, Android in-app messages can only be delivered through the TPNS channels and cannot be delivered through the vendor channels.

The specific fields for the Android platform are as follows:

| Field Name | Type | Parent Item | Default Value | Required | Parameter Description |
| -------------- | ------ |---------------| ---- | ---- | ------------------------ |
| title          | string |message| None    | Yes    | Command description                     |
| content        | string |message| None    | Yes    | Command content                    |
| android              | JSON  | message      | None     | No    | Android message structure |
| custom_content | string | android | None    | No    | This must be serialized to JSON string                                |
| accept_time    | array | message       |None    | No    | The time period at which the message is allowed to be pushed to users. <li>A single element is formed by a "start" time and an "end" time. <li>"start" and "end" are indicated by hour and minute. For more information, please see the samples. <li>⚠️This is only valid for the TPNS channel due to vendor restrictions. |

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
| ------ | -----------| --------| ---- | ---- | ---------------------------------------- |
| aps    | JSON       | ios  | None    | Yes    | APNs-specific field, where the most important `key-value` pair is as follows:<br>content-available: it identifies the message type (which must be 1) and cannot contain alert, sound, or badge_type fields<br>For more information, please see [Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1). |
| ios    | JSON       |message  | None    | Yes    | iOS message structure  |
| custom_content | String | ios | None | No    | This must be serialized to JSON string                                |
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

## Optional Parameters

Optional Push API parameters are the optional advanced parameters except `audience_type`, `message_type`, and `message`.



| Parameter Name | Type | Parent Item | Required | Default Value | Description |
| ------------- | ------- |---------------| ---------------- | ------- | ---------------------------------------- |
| expire_time | int | None | No | 259200 (72 hours) | Offline message retention duration (in seconds), up to 72 hours. <li>If `expire_time` = 0, it indicates real-time message </li><li>If `expire_time` is greater than 0 and less than 800 seconds, the system will reset it to 800 seconds </li><li>If `expire_time` >= 800 seconds, the message will be retained according to the actual set duration, up to 72 hours </li><li>The value set cannot exceed 2147483647; otherwise, the push will fail.</li>|
| send_time | string | None | No | Current system time | This specifies the push time: <li>The format is yyyy-MM-DD HH:MM:SS</li><li>If it is less than the current server time, the message will be pushed immediately </li><li>This field is supported only for full push and tag push.</li> |
| multi_pkg | bool | None | No| false | Multi-package name push: for an application that has multiple channel packages (such as for MyApp and Wandoujia), if you want the application in all channels to receive the push message, you can set this value to `true`. <br>⚠️This parameter controls the multi-package name push of the TPNS channel by default. To implement multi-package name push for vendor channels, please see [Multi-Package Name Push for Vendor Channels](https://intl.cloud.tencent.com/document/product/1024/35393). |
| loop_param | json | None | No                | 0       | For more information on loop push (full push and tag push), please see the [loop_param field description](#loop_param parameter description) below. |
|badge_type     |int  |  iOS  |No                 |-1        | The user-configured badge number. This is only used on the iOS platform, and is put in the aps field. <li> -1: badge number does not change. </li> <li> -2: badge number automatically increases by 1. </li><li> >=0: a custom badge number is configured.</li>|
|group_id     |string   | None  | No                 |tpns_yyyymmdd, with yyyymmdd represents the push date       | Statistics tag, used for aggregated statistic. Format requirement: it can contain up to 25 letters, digits, and symbols and cannot contain spaces. |
| tag_list      | object  | None | Only required for tag push          | None       | <li>Push to devices with tag1 and tag2: `{"tags":["tag1","tag2"],"op":"AND"}`</li><li>Push to devices with tag1 or tag2: `{"tags":["tag1","tag2"],"op":"OR"}` </li>|
| account_list  | array  |None | Only required by single-account push and account list push | None       | For single-account push:<li>Requires `audience_type=account`</li><li>Parameter format: ["account1"]</li><br>For account list push: <li>Parameter format: `["account1","account2"]`</li><li>Up to 1,000 accounts </li>|
| account_push_type  | int  |  None | Optional for account push         | 0       |<li> 0: push message to the latest device of the account</li><li> 1: push message to all devices associated with the account</li>|
| token_list    | array   |None | Required by single-device push and device list push | None       | For single-device push: <li>audience_type must be token<li>Parameter format: ["token1"]<br>For device list push: <li>Parameter format: ["token1","token2"]</li><li>Up to 1,000 tokens </li>|
| push_speed   |int | None | Only valid for full push and tag push | None | Sets push speed limit to X pushed per second. Value range of X: 1000–50000 |
| collapse_id  |uint32 |None|No| The system assigns a `collapse_id` by default | <li>Message overwriting parameter. After the first push task has been scheduled and delivered, if the second push task carries the same `collapse_id`, it will stop the TPNS channel data in the first push task that has not been delivered yet and will also overwrite the message in the first push task. <li>The `collapse_id` of a completed task can be obtained through the [single task push information querying API](https://intl.cloud.tencent.com/document/product/1024/33773).<li>Currently, this is supported only for full push, tag push, and number package push. |
| channel_rules |array |None|No|None| Push channel selection policy. <li>You can select the channels through which a push can be delivered. The push can be delivered through all channels by default. For detailed push policies, please see [Channel Policy](https://intl.cloud.tencent.com/document/product/1024/36151). <li>For the data structure of single elements in `channel_rules`, please see the [channel_rules parameter description](#channel_rules parameter description 1) below. |
force_collapse|bool|None|No|false| Whether to deliver messages to OPPO and Vivo devices that do not support message overwriting.<li>false: no <li>true: yes |


>For `collapse_id`, the following conditions of use apply:
- This parameter currently is not customizable, and the `collapse_id` generated by TPNS is required. <li>This feature currently is supported only for the TPNS channel, APNs channel, Mi channel, Meizu channel, and Huawei devices on EMUI 10 and above. <li>For the Huawei channel, custom parameters can be carried in the [intent](#intent1) method during message overwriting. If you use `custom_content` to carry custom parameters, the API layer will block them. <li>Currently, the OPPO and Vivo channels do not support message overwriting. When an overwriting message is created, delivery to the OPPO and Vivo channels can be disabled by setting the `force_collapse` field to `false`.
<span id="channel_rules parameter description 1"></span>
### channel_rules parameter description

| Field name | Type | Required | Comments |
| ------- | ------ | -------- | ------------------------------------------------------------ |
| channel | string | Yes       | Delivery push channel. <br> <li> hw: Huawei channel <li> xm: Mi channel <li> mz: Meizu channel <li> vivo: Vivo channel <li>oppo: OPPO channel |
| disable | bool   | No       | Whether to disable the corresponding channel in `channel`, which is enabled by default. <br><li>true: disable<li> false: enable |


<span id="loop_param parameter description"></span>
### loop_param parameter description

| Field name | Type | Required | Comments |
| -------- | ------- | ---- | ----------------------------------------          |
| startDate      | string | Yes    | Loop interval start date, with format of YYYY-MM-DD, such as 2019-07-01       |
| endDate | string   | Yes    | Loop interval start date, with format of YYYY-MM-DD, such as 2019-07-07|                 |
| loopType | int| Yes | Loop type: <li>1: daily <li>2: weekly <li>3: monthly |
| loopDayIndexs | array | Yes   | For weekly loop, enter number of weeks [0-6], and enter days as 0. If it is [0, 1, 2], it indicates that the push will be done on Monday, Tuesday, and Wednesday every week.                                |
| dayTimes   | array  | Yes    | Specific push time, with the format as HH:MM:SS, such as ["19:00:00", "20:00:00"], indicates that the push will be done at 19:00 and 20:00 every day. |



## Response Parameters

| Field name | Type | Required | Comments |
| -------- | ------- | ---- | ----------------------------------------          |
| seq | int64_t | Yes | The same as the request packet (if the request packet is invalid JSON, this field is 0) |
| push_id | string | Yes | Push id |
| ret_code | int32_t | Yes | Error code. For more information, please see the error codes table |
| environment | string | Yes | The push environment specified by the user (only for iOS). <li>product: production environment </li><li>dev: development environment </li>|
| err_msg | string | No | Error message when an error occurs in the request |
| result   | string  | No       | When the request is correct:<li>If there is extra data to be returned, the result will be encapsulated in the JSON of this field. If there is no extra data, <li>there may be no such field </li> |



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
    "title": "test title",
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
    "token_list": [ "05da87c0ae5973bd2dfa9e08d884aada5bb2"],
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



