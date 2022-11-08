## MsgBody
Message content is entered in the fields of MsgBody. Instant Messaging (IM) supports multiple message elements in one message, for example, a message can contain both text and emojis. Therefore, MsgBody is defined as an array that can include as many message elements as needed. The name for a message element is TIMMsgElement. For examples of the TIMMsgElements that constitute the MsgBody, see [MsgBody Message Content Examples](https://intl.cloud.tencent.com/document/product/1047/33527).

The format of TIMMsgElement is defined as follows:
```
{
    "MsgType": "",
    "MsgContent": {}
}
```

| Field | Type | Description |
|---------|---------|---------|
| MsgType | String | The type of the message element. Currently, these message objects are supported: TIMTextElem (text message), TIMLocationElem (location message), TIMFaceElem (emoji message), TIMCustomElem (custom message), TIMSoundElem (audio message), TIMImageElem (image message), TIMFileElem (file message), and TIMVideoFileElem (video message). |
| MsgContent | Object | The content of the message element. Each MsgType has its own MsgContent format. For more information, see below. |

The following table lists the supported message types (MsgType):

| Value of MsgType | Type |
|---------|---------|
| TIMTextElem | Text message |
| TIMLocationElem | Geographic location message|
| TIMFaceElem | Emoji |
| TIMCustomElem | Custom message. When the receiver is an iOS device and the app is working in the background, this type of message provides fields other than text to APNs. A combined message can contain only one TIMCustomElem custom message element. |
| TIMSoundElem | Audio message |
| TIMImageElem | Image |
| TIMFileElem | File |
| TIMVideoFileElem | Video message |

>!Messages of the above types can be sent by server-side integrated RESTful APIs.

## TIMMsgElement

### Text message element

```
{
    "MsgType": "TIMTextElem",
    "MsgContent": {
        "Text": "hello world"
    }
}
```

| Field | Type | Description |
|---------|---------|---------|
| Text | String | Content of the message. When the receiver is an iOS or Android device and the app is working in the background, messages of this type are displayed as offline push text. |

When the receiver is an iOS or Android device and the app is working in the background, the `Text` field in the JSON request packet is displayed as offline push text.

### Location message element

```
{
    "MsgType": "TIMLocationElem", 
    "MsgContent": {
        "Desc": "someinfo", 
        "Latitude": 29.340656774469956, 
        "Longitude": 116.77497920478824
    }
}
```

| Field | Type | Description |
|---------|---------|---------|
| Desc | String | Description of the location |
| Latitude | Number | Latitude |
| Longitude | Number | Longitude |

When the receiver is an iOS or Android device and the app is working in the background, the offline push text is **[Location]** for the English version.

### Emoji message element

```
{
    "MsgType": "TIMFaceElem", 
    "MsgContent": {
        "Index": 1, 
        "Data": "content"
    }
}
```

| Field | Type | Description |
|---------|---------|---------|
| Index | Number | Emoji index customized by users |
| Data | String | Additional data |

When the receiver is an iOS or Android device and the app is working in the background, the offline push text is **[Face]** for the English version.


<dx-alert infotype="explain" title="Description">
When a message contains only one `TIMCustomElem` custom message element, if both the `Desc` and `OfflinePushInfo.Desc` fields are not entered, the offline push of the message will not be received, unless the `OfflinePushInfo.Desc` field is entered.
</dx-alert>


### Custom message element

```
{
    "MsgType": "TIMCustomElem", 
    "MsgContent": {
        "Data": "message", 
        "Desc": "notification", 
        "Ext": "url", 
        "Sound": "dingdong.aiff"
    }
}
```

| Field | Type | Description |
|---------|---------|---------|
| Data | String | Custom message data. This field is not delivered as a payload field by APNs, and therefore the data field cannot be obtained in payload. |
| Desc | String | Custom message description. When the receiver is an iOS or Android device, and the app is working in the background, the offline push text is displayed.<br>If a custom message is sent with the [OfflinePushInfo.Desc](https://intl.cloud.tencent.com/document/product/1047/33527) field set, the field will be overwritten; therefore, please enter the OfflinePushInfo.Desc field first.<br><dx-alert infotype="explain" title="Note">
When a message contains only one `TIMCustomElem` custom message element, if both the `Desc` and `OfflinePushInfo.Desc` fields are not entered, the offline push of the message will not be received, unless the `OfflinePushInfo.Desc` field is entered.
</dx-alert>|
| Ext | String | Extended field. When the receiver is an iOS or Android device and the app is working in the background, this field is delivered as an Ext key value in APNs request packet payloads. The protocol format of Ext is defined by the business end, the APNs is only responsible for passthrough. |
| Sound | String | Custom APNs push ringtone |

When the receiver is an iOS or Android device and the app is working in the background, the `Desc` field is delivered as push text, the `Ext` field is delivered as an `Ext` key value in APNs request packet payloads, and the `Data` field is not delivered as a payload field by APNs. Note that a combined message can contain only one TIMCustomElem custom message element.

### Audio message element

>!To send an audio message through the server-side RESTful API, you need to enter the `Url`, `UUID`, and `Download_Flag` fields. Make sure that the audio can be downloaded via the `Url` and the `UUID` is a globally unique string value, usually the MD5 value of the audio file. The message recipient can obtain the specified `UUID` through `V2TIMSoundElem.getUUID()` and the app can use the `UUID` to identify the audio. `Download_Flag` must be set to `2`.

4.X versions of IM SDK (for Android, iOS, Mac, and Windows) send audio message elements in the following format:
```
{
    "MsgType": "TIMSoundElem",
    "MsgContent": {
        "Url": "https://1234-5678187359-1253735226.cos.ap-shanghai.myqcloud.com/abc123/c9be9d32c05bfb77b3edafa4312c6c7d",
        "UUID": "1053D4B3D61040894AC3DE44CDF28B3EC7EB7C0F",
        "Size": 62351,
        "Second": 1,
        "Download_Flag": 2
    }
}
```

| Field | Type | Description |
|---------|---------|---------|
| Url | String | Audio download URL, through which the audio content can be downloaded directly. |
| UUID | String | Unique identifier of the audio, key value used by the client to index the audio |
| Size | Number | Audio data size, in bytes. |
| Second | Number | Audio duration, in seconds. |
| Download_Flag | Number | Flag of the audio download method. Currently, the value of `Download_Flag` must be `2`, which means that the audio content can be downloaded from the URL specified by the `Url` field. |

>?2.X and 3.X versions of IM SDK (for Android, iOS, Mac, and Windows) send audio message elements in the following format:
```
{
    "MsgType": "TIMSoundElem",
    "MsgContent": {
        "UUID": "305c0201", //Unique identifier of the audio in String type. This is the key value the client uses to index the audio. The audio cannot be downloaded through this field. To obtain the audio, upgrade the IM SDK to version 4.X.
        "Size": 62351,      //Audio data size in bytes, in Number type.
        "Second": 1         //Audio duration in seconds, in Number type.
    }
}
```


### Image message element

>!To send an image message through the server-side RESTful API, you need to enter the `URL`, `UUID`, `Width`, and `Height` fields. Make sure that the image can be downloaded via the `URL`. `Width` and `Height` are the width and height (unit: pixels) of the image. `UUID` must be set to a globally unique string value, usually the MD5 value of the image. The message recipient can obtain the `V2TIMImage` object by calling `V2TIMImageElem.getImageList()` and then get the specified `UUID` by calling `V2TIMImage.getUUID()`. The app can use the `UUID` to identify the image.

```
{
    "MsgType": "TIMImageElem",
    "MsgContent": {
        "UUID": "1853095_D61040894AC3DE44CDFFFB3EC7EB720F",
        "ImageFormat": 1,
        "ImageInfoArray": [
            {
                "Type": 1,           //Original image
                "Size": 1853095,
                "Width": 2448,
                "Height": 3264,
                "URL": "http://xxx/3200490432214177468_144115198371610486_D61040894AC3DE44CDFFFB3EC7EB720F/0"
            },
            {
                "Type": 2,      //Large image
                "Size": 2565240,
                "Width": 0,
                "Height": 0,
                "URL": "http://xxx/3200490432214177468_144115198371610486_D61040894AC3DE44CDFFFB3EC7EB720F/720"
            },
            {
                "Type": 3,   //Thumbnail
                "Size": 12535,
                "Width": 0,
                "Height": 0,
                "URL": "http://xxx/3200490432214177468_144115198371610486_D61040894AC3DE44CDFFFB3EC7EB720F/198"
            }
        ]
    }
}
```

| Field | Type | Description |
|---------|---------|---------|
| UUID | String | Unique identifier of the image, key value used by the client to index the image |
| ImageFormat | Number | Image format. JPG = 1, GIF = 2, PNG = 3, BMP = 4, Others = 255. |
| ImageInfoArray | Array | Download information of the original image, thumbnail, or large image. |
| Type | Number | Image type. 1: Original image, 2: Large image, 3: Thumbnail. |
| Size | Number | Image size in bytes. |
| Width | Number | Image width in pixels |
| Height | Number | Image height in pixels |
| URL | String | Download URL of the image. |

### File message element

>!To send a file message through the server-side RESTful API, you need to enter the `Url`, `UUID`, and `Download_Flag` fields. Make sure that the file can be downloaded via the `Url` and the `UUID` is a globally unique string value, usually the MD5 value of the file. The message recipient can obtain the specified `UUID` by calling `V2TIMFileElem.getUUID()` and the app can use the `UUID` to identify the file. `Download_Flag` must be set to `2`.

4.X versions of IM SDK (for Android, iOS, Mac, and Windows) send file message elements in the following format:
```
{
    "MsgType": "TIMFileElem",
    "MsgContent": {
        "Url": "https://7492-5678539059-1253735326.cos.ap-shanghai.myqcloud.com/abc123/49be9d32c0fbfba7b31dafa4312c6c7d",
        "UUID": "1053D4B3D61040894AC3DE44CDF28B3EC7EB7C0F",
        "FileSize": 1773552,
        "FileName": "file:///private/var/Application/tmp/trim.B75D5F9B-1426-4913-8845-90DD46797FCD.MOV",
		"Download_Flag": 2
    }
}
```

| Field | Type | Description |
|---------|---------|---------|
| Url | String | Download URL of the file, through which the file can be downloaded directly. |
| UUID | String | Unique identifier of the file, key value used by the client to index the file |
| FileSize | Number | Size of file data in bytes. |
| fileName | String | File name. |
| Download_Flag | Number | Flag of the file download method. Currently, the value of `Download_Flag` must be 2, which means that the file can be downloaded from the URL specified by the `Url` field. |

>?2.X and 3.X versions of IM SDK (for Android, iOS, Mac, and Windows) send file message elements in the following format:
>```
>{
>"MsgType": "TIMFileElem",
>"MsgContent": {
>  "UUID": "305c02010", //Unique identifier of the file in String type. This is the key value the client uses to index the file. The file cannot be downloaded through this field. To obtain the file, upgrade the IM SDK to version 4.X.
>  "FileSize": 1773552, //Size of file data in bytes, in Number type.
>  "FileName": "file:///private/var/Application/tmp/trim.B75D5F9B-1426-4913-8845-90DD46797FCD.MOV" //File name in String type.
>}
>}
>```


### Video message element

>!To send a video message through the server-side RESTful API, you need to enter the `VideoUrl`, `VideoUUID`, `ThumbUrl`, `ThumbUUID`, `ThumbWidth`, `ThumbHeight`, `VideoDownloadFlag`, and `ThumbDownloadFlag` fields. Make sure that the video and video thumbnail can be downloaded via the `VideoUrl` and `ThumbUrl` respectively. `VideoUUID` and `ThumbUUID` must be globally unique string values, usually the MD5 values of the video and video thumbnail. The message recipient can obtain the specified `VideoUUID` and `ThumbUUID` by calling `V2TIMVideoElem.getVideoUUID()` and `V2TIMVideoElem.getSnapshotUUID()` respectively. The app can use the `VideoUUID` to identify the video. `VideoDownloadFlag` and `ThumbDownloadFlag` must be set to `2`.

4.X versions of IM SDK (for Android, iOS, Mac, and Windows) send video message elements in the following format:
```
{
    "MsgType": "TIMVideoFileElem",
    "MsgContent": {
        "VideoUrl": "https://0345-1400187352-1256635546.cos.ap-shanghai.myqcloud.com/abcd/f7c6ad3c50af7d83e23efe0a208b90c9",
        "VideoUUID": "5da38ba89d6521011e1f6f3fd6692e35",
        "VideoSize": 1194603,
        "VideoSecond": 5,
		"VideoFormat": "mp4",
		"VideoDownloadFlag":2,
		"ThumbUrl": "https://0345-1400187352-1256635546.cos.ap-shanghai.myqcloud.com/abcd/a6c170c9c599280cb06e0523d7a1f37b",
		"ThumbUUID": "6edaffedef5150684510cf97957b7bc8",
		"ThumbSize": 13907,
		"ThumbWidth": 720,
		"ThumbHeight": 1280,
		"ThumbFormat": "JPG",
		"ThumbDownloadFlag":2
    }
}
```

| Field | Type | Description |
|---------|---------|---------|
| VideoUrl | String | Download URL of the video, through which the video can be downloaded directly. |
| VideoUUID | String | Unique identifier of the video, key value used by the client to index the video |
| VideoSize | Number | Size of video data, in bytes. |
| VideoSecond | Number | Video duration, in seconds. |
| VideoFormat | String | Video format, for example, MP4. |
| VideoDownloadFlag | Number | Flag of the video download method. Currently, the value of `VideoDownloadFlag` must be 2, which means that the video can be downloaded from the URL specified by the `VideoUrl` field. |
| ThumbUrl | String | Download URL of the video thumbnail, through which the video thumbnail can be downloaded directly. |
| ThumbUUID | String | Unique identifier of the video thumbnail, key value used by the client to index the video thumbnail |
| ThumbSize | Number | Size of thumbnail data, in bytes. |
| ThumbWidth | Number | Thumbnail width in pixels |
| ThumbHeight | Number | Thumbnail height in pixels |
| ThumbFormat | String | Video thumbnail format, such as JPG or BMP. |
| ThumbDownloadFlag | Number | Flag of the video thumbnail download method. Currently, the value of `ThumbDownloadFlag` must be 2, which means that the video thumbnail can be downloaded from the URL specified by the `ThumbUrl` field. |


?2.X and 3.X versions of IM SDK (for Android, iOS, Mac, and Windows) send video message elements in the following format:
```
{
    "MsgType": "TIMVideoFileElem",
    "MsgContent": {
        "VideoUUID": "1400123456_dramon_34ca36be7dd214dc50a49238ef80a6b5",//Unique identifier of the video in String type. This is the key value the client uses to index the video. The video cannot be downloaded through this field. To obtain the video, upgrade the IM SDK to version 4.X.
        "VideoSize": 1194603, //Size of video data in bytes, in Number type.
        "VideoSecond": 5,     //Video duration in seconds, in Number type.
		"VideoFormat": "mp4", //Video format in String type, for example, MP4.
		"ThumbUUID": "1400123456_dramon_893f5a7a4872676ae142c08acd49c18a",//Unique identifier of the video thumbnail in String type. This is the key value the client uses to index the video thumbnail. The video thumbnail cannot be downloaded through this field. To obtain the video thumbnail, upgrade the IM SDK to version 4.X.
		"ThumbSize": 13907,   //Size of thumbnail data in bytes, in Number type.
		"ThumbWidth": 720,    //Thumbnail width in Number type.
		"ThumbHeight": 1280,  //Thumbnail height in Number type.
		"ThumbFormat": "JPG"  //Video thumbnail format in String type, such as JPG or BMP.
    }
}
```

## MsgBody Examples

### Single text element message

A single message contains only one text message element. The text content is **hello world**.

```
{
    "MsgBody": [
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "hello world"
            }
        }
    ]
}
```

### Combined messages

The following single message contains two text message elements and one emoji message element, in the sequence of text + emoji + text.
```
{
    "MsgBody": [
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "hello"
            }
        }, 
        {
            "MsgType": "TIMFaceElem", 
            "MsgContent": {
                "Index": 1, 
                "Data": "content"
            }
        }, 
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "world"
            }
        }
    ]
}
```

>!A combined message can contain only one `TIMCustomElem` custom message element, and an unlimited number of other message elements.

## Custom Message Data CloudCustomData
Each message can carry custom data `CloudCustomData`.

`CloudCustomData` is saved on the cloud together with the `MsgBody` of the message. It will be sent to the peer end and can still be pulled after the program is uninstalled and reinstalled.

The following example shows the formats of `CloudCustomData` and `MsgBody`:
```
{
    "MsgBody": [
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "hello"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```

## Message Formats for Apple Push Notification Service (APNs)
### Push notification display format on the client
- **Account without a nickname**
For an account without a nickname, APNs displays only text content: **push text** for one-to-one chat messages, and **(group name): push text** for group messages.

- **Account with a nickname**
For an account with a nickname, APNs displays **nickname: push text** for one-to-one chat messages, and **nickname (group name): push text** for group messages.
![](https://main.qcloudimg.com/raw/7bdb0f41aaa943190ce949fea8d20095.png)

- **Display format of combined messages**
For combined messages, the text displayed shows the push text of each message element in sequence. The following example shows a one-to-one chat message with an account nickname set, and the push text is **helloworld**. Note that the text contains no spaces. The backend connects message elements in sequence without adding any extra characters. If spaces or other characters need to be added between different message elements, the caller should take control.
```
{
    "MsgBody": [
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "hello"  
            }
        },
        {
            "MsgType": "TIMCustomElem",
            "MsgContent": {
                "Data": "message",
                "Desc": "world",
                "Ext": "https://www.example.com",               
                "Sound": "dingdong.aiff"
            }
        }
    ] 
}
```
![](https://main.qcloudimg.com/raw/8a9b70df695ecf77c10c5ffba03d9864.png)

The following table summarizes the push text of different message elements.

| Value of MsgType | Type | Push Text of the Message Element |
|---------|---------|---------|
| TIMTextElem | Text | `Text` field. |
| TIMLocationElem | Location | Offline push text is **[Location]** for the English version. |
| TIMFaceElem | Emoji | Offline push text is **[Face]** for the English version. |
| TIMCustomElem | Custom | `Desc` field. |

### RESTful APIs for nickname and group name settings
RESTful API for setting the account nickname: [Setting the Profile](https://intl.cloud.tencent.com/document/product/1047/34916).
RESTful API for setting the group name: [Modifying Basic Group Information](https://intl.cloud.tencent.com/document/product/1047/34962).

### Advanced usage
#### Customizing push sounds and extended fields delivered by APNs
Use TIMCustomElem to customize message elements. In the `Sound` field, enter the file name of the custom audio. In the `Ext` field, enter the delivered extended field, which can be obtained from the `Ext` field in the APNs payload.
```
{
    "To_Account": "lumotuwe5", 
    "MsgRandom": 121212, 
    "MsgBody": [
        {
            "MsgType": "TIMCustomElem", 
            "MsgContent": {
                "Data": "other information", 
                "Desc": "hello", 
                "Ext": "www.qq.com", 
                "Sound": "dingdong.aiff"
            }
        }, 
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "world"
            }
        }
    ]
}

```

The received APNs JSON payload is displayed as follows on the client:

```
{
    "aps": {
        "alert": "Nickname:helloworld",   //Push text of each message element is connected in sequence
        "badge": 5,                       
        "sound": "dingdong.aiff"         //Corresponds to the `Sound` field in `TIMCustomElem`
    }, 
    "ext": "www.qq.com"                //Corresponds to the `Ext` field in `TIMCustomElem`
}

```

## OfflinePushInfo

`OfflinePushInfo` is a JSON object dedicated for configuring offline push. It allows you to configure whether to disable push, push text description content, and push passthrough strings for a message. With `OfflinePushInfo`, you can easily set offline push information, eliminating the need to encapsulate through `TIMCustomElem`.

>!If `OfflinePushInfo` has been filled in, the offline push settings in `TIMCustomElem` are ignored. Currently, `OfflinePushInfo` can work with APNs and the push services of various Android device brands, including Mi, Huawei, Meizu, OPPO, and vivo.

The following example shows the format of `OfflinePushInfo`:

```
{
    // ...
    "MsgBody": [...] //Same with `MsgBody` in this case
    "OfflinePushInfo": {
        "PushFlag": 0,
        "Title":"This is the push title",
        "Desc": "This is the offline push content",
        "Ext": "Passthrough content",
        "AndroidInfo": { 
			"Sound": "android.mp3",
			"OPPOChannelID": "test_OPPO_channel_id",
			"VIVOClassification": 1
        },
        "ApnsInfo": {
            "Sound": "apns.mp3",
            "BadgeMode": 1,
            "Title":"apns title",
            "SubTitle":"apns subtitle",
            "Image":"www.image.com",
            "MutableContent": 1
        }
    }
}
```

The preceding fields are described as follows:

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| PushFlag | Integer | Optional | 0: Enable push, 1: Disable offline push. |
| Title | String | Optional | Offline push title. This field is applicable to both iOS and Android. |
| Desc | String | Optional | Offline push content. This field overwrites the offline push display text of the [TIMMsgElement](https://intl.cloud.tencent.com/document/product/1047/33527) elements mentioned above.<br>If the message sent has only one [TIMCustomElem](https://intl.cloud.tencent.com/document/product/1047/33527) element, this `Desc` field will overwrite the `Desc` field in the TIMCustomElem. If neither of the `Desc` fields is filled in, the offline push notification for the message will not be received. |
| Ext | String | Optional | Passthrough content of offline push. To make sure the offline push of all Android vendors are attainable, this field must be in JSON format. |
| AndroidInfo.Sound | String | Optional | Path to the offline push sound file in Android. |
| AndroidInfo.HuaWeiChannelID | String | Optional | Notification channel field for Huawei phones with EMUI 10.0 or later. When this field is not empty, it will overwrite the `ChannelID` value configured in the console; otherwise, it will not. |
| AndroidInfo.XiaoMiChannelID | String | Optional | Notification type (Channel) adaptation field for Mi phones with MIUI 10 or later. When this field is not empty, it will overwrite the `ChannelID` value configured in the console; otherwise, it will not. |
| AndroidInfo.OPPOChannelID | String | Optional | `NotificationChannel` notification adaptation field for OPPO phones with Android 8.0 or later. When this field is not empty, it will overwrite the `ChannelID` value configured in the console; otherwise, it will not. |
| AndroidInfo.GoogleChannelID | String | Optional | Notification channel field for Google mobile phones with Android 8.0 or later. This field is supported by the new Google push API (uploading the certificate file) but not the old API (entering the server key). |
| AndroidInfo.VIVOClassification | Integer | Optional | Push message classification for Vivo phones. Valid values: 0: Operation message; 1: System message (default value). |
| AndroidInfo.HuaWeiImportance | String | Optional | Push notification message classification for Huawei phones. Valid values: LOW, NORMAL (default value). |
| AndroidInfo.ExtAsHuaweiIntentParam | Integer | Optional | After Huawei Push is configured to **Open specified in-app page** in the console, "1" indicates to use the passthrough content `Ext` as the `Intent` parameter, while "0" (default value) indicates to use the passthrough content `Ext` as the `Action` parameter. For the differences between the two parameters, see [Guides](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/andorid-basic-clickaction-0000001087554076#section20203190121410). |
| ApnsInfo.BadgeMode | Integer | Optional | The default value or 0 indicates that counting is required. 1 indicates that counting is not required for this message, in which case the number in the upper-right icon does not increase. |
| ApnsInfo.Title | String | Optional | Title of an APNs push message. The top-level title is replaced when this field is filled in. |
| ApnsInfo.SubTitle | String | Optional | Subtitle of an APNs push message. |
| ApnsInfo.Image | String | Optional | Image URL carried by APNs. When the client obtains this field, it displays the image in a pop-up window by downloading the image through the URL. |
| ApnsInfo.MutableContent | Integer | Optional | Valid values: 1: enable the push extension of iOS 10; 0 (default value). |

>!The maximum data packet size supported by APNs is 4 KB. Therefore, we recommend that the total size of the `Desc` and `Ext` fields does not exceed 3 KB.

## References

APNs development: [Local and Remote Notifications Overview](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/Introduction.html#//apple_ref/doc/uid/TP40008194-CH1-SW1)
[Offline Push (iOS)](https://intl.cloud.tencent.com/zh/document/product/1047/34347)
