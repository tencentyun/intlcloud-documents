## Description of MsgBody Message Content
Message content is entered in the fields of MsgBody. Instant Messaging (IM) supports multiple message elements in one message, for example, a message can contain both text and emojis. Therefore, MsgBody is defined as an array that can include as many message elements as needed. The name for a message element is TIMMsgElement.  <!--For examples of TIMMsgElements constituting MsgBody, see [MsgBody Message Content Examples]().-->

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

The following table lists the message types (MsgType) that are currently supported:

| Value of MsgType | Type |
|---------|---------|
| TIMTextElem | Text |
| TIMLocationElem | Geographic location |
| TIMFaceElem | Emoji |
| TIMCustomElem | Custom. When the receiver is an iOS device and the app is working in the background, this type of messages provide fields other than text to APNs. A combined message can contain only one TIMCustomElem custom message element. |
| TIMSoundElem | Audio. Server-side integrated RESTful APIs cannot send this type of messages. |
| TIMImageElem | Image. Server-side integrated RESTful APIs cannot send this type of messages. |
| TIMFileElem | File. Server-side integrated RESTful APIs cannot send this type of messages. |
| TIMVideoFileElem | Video. Server-side integrated RESTful APIs cannot send this type of messages. |

>Only TIMTextElem, TIMLocationElem, TIMFaceElem, and TIMCustomElem messages can be sent through RESTful APIs integrated with the server. Other types of messages including TIMSoundElem, TIMImageElem, TIMFileElem, and TIMVideoFileElem messages cannot be sent through RESTful APIs.

## Message Element TIMMsgElement

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
| Text | String | The content of the message. When the receiver is an iOS or Android device and the app is working in the background, this type of messages are displayed as offline push text. |
    
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

When the receiver is an iOS or Android device and the app is working in the background, the offline push text is **[位置]** for the Chinese version and **[Location]** for the English version.

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

When the receiver is an iOS or Android device and the app is working in the background, the offline push text is **[表情]** for the Chinese version and **[Face]** for the English version.

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
| Desc | String | Custom message description. When the receiver is an iOS or Android device and the app is working in the background, it is displayed as offline push text. |
| Ext | String | The extended field. When the receiver is an iOS or Android device and the app is working in the background, this field is delivered as an Ext key value in APNs request packet payloads. The protocol format of Ext is defined by the business end, the APNs is only responsible for passthrough. |
| Sound | String | Custom APNs push ringtone |

When the receiver is an iOS or Android device and the app is working in the background, the `Desc` field is delivered as push text, the `Ext` field is delivered as an `Ext` key value in APNs request packet payloads, and the `Data` field is not delivered as a payload field by APNs. Note that a combined message can contain only one TIMCustomElem custom message element.

### Audio message element

>Audio messages cannot be sent through server-side integrated RESTful APIs. Instead, they can only be sent through client-side integrated APIs.

4.X versions of IM SDK (for Android, iOS, Mac, and Windows) send audio message elements in the following format:
```
{
    "MsgType": "TIMSoundElem",
    "MsgContent": {
        "Url": "https://1234-5678187359-1253735226.cos.ap-shanghai.myqcloud.com/abc123/c9be9d32c05bfb77b3edafa4312c6c7d",
        "Size": 62351,
        "Second": 1,
		"Download_Flag": 2
    }
}
```

| Field | Type | Description |
|---------|---------|---------|
| Url | String | The audio download URL, through which the audio content can be downloaded directly. |
| Size | Number | The audio data size in bytes. |
| Second | Number | The audio duration in seconds. |
| Download_Flag | Number | The flag of the audio download method. Currently, the value of Download_Flag must be 2, which means that the audio content can be downloaded from the URL that is the value of the `Url` field. |

>2.X and 3.X versions of IM SDK (for Android, iOS, Mac, and Windows) send audio message elements in the following format:
```
{
    "MsgType": "TIMSoundElem",
    "MsgContent": {
        "UUID": "305c0201", //The serial number of the audio in String type. This is the key value the backend uses to index the audio. Audio cannot be downloaded through this field. To obtain the audio, upgrade the IM SDK to 4.X version.
        "Size": 62351,//The audio data size in bytes, in Number type.
        "Second": 1         //The audio duration in seconds, in Number type.
    }
}
```
>

### Image message element

>Image messages cannot be sent through server-side integrated RESTful APIs. Instead, they can only be sent through client-side integrated APIs.

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
| UUID | String | The serial number of the image, which is the key value the backend uses to index image. |
| ImageFormat | Number | The image format. JPG = 1, GIF = 2, PNG = 3, BMP = 4, Others = 255. |
| ImageInfoArray | Array | The download information of the original image, thumbnail, or large image. |
| Type | Number | The image type. 1: original image, 2: large image, 3: thumbnail. |
| Size | Number | The size of image data in bytes. |
| Width | Number | The image width. |
| Height | Number | The image height. |
| URL | String | The download URL of the image. |

### File message element

>File messages cannot be sent through server-side integrated RESTful APIs. Instead, they can only be sent through client-side integrated APIs.

4.X versions of IM SDK (for Android, iOS, Mac, and Windows) send file message element in the following format:
```
{
    "MsgType": "TIMFileElem",
    "MsgContent": {
        "Url": "https://7492-5678539059-1253735326.cos.ap-shanghai.myqcloud.com/abc123/49be9d32c0fbfba7b31dafa4312c6c7d",
        "FileSize": 1773552,
        "FileName": "file:///private/var/Application/tmp/trim.B75D5F9B-1426-4913-8845-90DD46797FCD.MOV",
		"Download_Flag": 2
    }
}
```

| Field | Type | Description |
|---------|---------|---------|
| Url | String | The download URL of the file, through which the file can be downloaded directly. |
| FileSize | Number | The size of file data in bytes. |
| fileName | String | The file name. |
| Download_Flag | Number | The flag of the file download method. Currently, the value of `Download_Flag` must be 2, which means that the file can be downloaded from the URL that is the value of the `Url` field. |

>2.X and 3.X versions of IM SDK (for Android, iOS, Mac, and Windows) send file message elements in the following format:
>```
{
    "MsgType": "TIMFileElem",
    "MsgContent": {
        "UUID": "305c02010", //The serial number of the file in String type. This is the key value the backend uses to index the file. The file cannot be downloaded through this field. To obtain the file, upgrade the IM SDK to 4.X version.
        "FileSize": 1773552, //The size of file data in bytes, in Number type.
        "FileName": "file:///private/var/Application/tmp/trim.B75D5F9B-1426-4913-8845-90DD46797FCD.MOV" //The file name in String type.
    }
}
```

### Video message element

>Video messages cannot be sent through server-side integrated RESTful APIs. Instead, they can only be sent through client-side integrated APIs.

4.X versions of IM SDK (for Android, iOS, Mac, and Windows) send video message element in the following format:
```
{
    "MsgType": "TIMVideoFileElem",
    "MsgContent": {
        "VideoUrl": "https://0345-1400187352-1256635546.cos.ap-shanghai.myqcloud.com/abcd/f7c6ad3c50af7d83e23efe0a208b90c9",
        "VideoSize": 1194603,
        "VideoSecond": 5,
		"VideoFormat": "mp4",
		"VideoDownloadFlag":2,
		"ThumbUrl": "https://0345-1400187352-1256635546.cos.ap-shanghai.myqcloud.com/abcd/a6c170c9c599280cb06e0523d7a1f37b",
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
| VideoUrl | String | The download URL of the video, through which the video can be downloaded directly. |
| VideoSize | Number | The size of video data in bytes. |
| VideoSecond | Number | The video duration in seconds. |
| VideoFormat | String | The video format, such as mp4. |
| VideoDownloadFlag | Number | The flag of the video download method. Currently, the value of `VideoDownloadFlag` must be 2, which means that the video can be downloaded from the URL that is the value of the `VideoUrl` field. |
| ThumbUrl | String | The download URL of the video thumbnail, through which the video thumbnail can be downloaded directly. |
| ThumbSize | Number | The size of thumbnail data in bytes. |
| ThumbWidth | Number | The thumbnail width. |
| ThumbHeight | Number | The thumbnail height. |
| ThumbFormat | String | The video thumbnail format, such as JPG or BMP. |
| ThumbDownloadFlag | Number | The flag of the video thumbnail download method. Currently, the value of `ThumbDownloadFlag` must be 2, which means that the video thumbnail can be downloaded from the URL that is the value of the `ThumbUrl` field. |


>2.X and 3.X versions of IM SDK (for Android, iOS, Mac, and Windows) send video message elements in the following format:
>```
{
    "MsgType": "TIMVideoFileElem",
    "MsgContent": {
        "VideoUUID": "1400123456_dramon_34ca36be7dd214dc50a49238ef80a6b5",//The serial number of the video in String type. This is the key value the backend uses to index videos. The video cannot be downloaded through this field. To obtain the video, upgrade the IM SDK to 4.X version.
        "VideoSize": 1194603, //The size of video data in bytes, in Number type.
        "VideoSecond": 5,     //The video duration in seconds, in Number type.
		"VideoFormat": "mp4", //The video format in String type, such as mp4.
		"ThumbUUID": "1400123456_dramon_893f5a7a4872676ae142c08acd49c18a",//The serial number of the video thumbnail in String type. This is the key value the backend uses to index video thumbnails. The video thumbnail cannot be downloaded through this field. To obtain the video thumbnail, upgrade the IM SDK to 4.X version.
		"ThumbSize": 13907,   //The size of thumbnail data in bytes, in Number type.
		"ThumbWidth": 720,    //The thumbnail width in Number type.
		"ThumbHeight": 1280,  //The thumbnail height in Number type.
		"ThumbFormat": "JPG"  //The video thumbnail format in String type, such as JPG or BMP.
    }
}
```

## MsgBody Message Content Examples

### Single text message element

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

>A combined message can contain only one TIMCustomElem custom message element, and an unlimited number of other message elements.

## Description of Apple Push Notification Service (APNs)
### Push notification display format on the client
- **Account nickname is not set**
If an account has not set a nickname, APNs only displays text content. For one-to-one chat messages, **push text** is displayed. For group messages, **(group name): push text** is displayed.
![](https://main.qcloudimg.com/raw/7bdb0f41aaa943190ce949fea8d20095.png)

- **Account nickname is set**
If an account has set a nickname, for one-to-one chat messages, **nickname: push text** is displayed. For group messages, **nickname (group name): push text** is displayed.
![](https://main.qcloudimg.com/raw/04d71f109d6f56f9815a3c6d0fabf464.png)

- **Display format of combined messages**
For combined messages, the text displayed shows the push text of each message element in sequence. The following example shows a one-to-one chat message with an account nickname set, and the push text is **helloworld**. Note that the text contains no spaces. The backend connects message elements in sequence without adding any extra characters. If spaces or other characters need to be added between different message elements, the caller should take control.
<pre>
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
</pre>
![](https://main.qcloudimg.com/raw/8a9b70df695ecf77c10c5ffba03d9864.png)

The following table summarizes the push text of different message elements.

| Value of MsgType | Type | Push Text of the Message Element |
|---------|---------|---------|
| TIMTextElem | Text | The `Text` field. |
| TIMLocationElem | Location | The offline push text is **[Location]**. |
| TIMFaceElem | Emoji | The offline push text is **[Face]**. |
| TIMCustomElem | Custom | The `Desc` field. |

 <!--### RESTful APIs for the nickname and group name settings
RESTful API for setting the account nickname: [Setting the Profile]().
RESTful API for setting the group name: [Modifying Basic Group Information]().-->

### Advanced applications
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
        "alert": "Nickname:helloworld",   //The push text of each message element is connected in sequence.
        "badge": 5,                       
        "sound": "dingdong.aiff"         //Corresponds to the `Sound` field in `TIMCustomElem`.
    }, 
    "ext": "www.qq.com"                //Corresponds to the `Ext` field in `TIMCustomElem`.
}

```

## Description of Offline Push OfflinePushInfo

`OfflinePushInfo` is a JSON object dedicated for configuring offline push. `OfflinePushInfo` allows you to configure whether to disable push, push text description content, and push passthrough strings for a message. With `OfflinePushInfo`, you can easily set offline push information, removing the need to encapsulate through `TIMCustomElem`.

>If `OfflinePushInfo` has been filled in, the offline push settings in `TIMCustomElem` are ignored. Currently, `OfflinePushInfo` can work with APNs and the push services of various Android device brands, including Xiaomi, Huawei, MEIZU, OPPO, and Vivo.

The following example shows the format of `OfflinePushInfo`:

```
{
    // ...
    "MsgBody": [...] //Same with `MsgBody` in this case
    "OfflinePushInfo": {
        "PushFlag": 0,
        "Title":"This is the push title",
        "Desc": "This is the offline push content",
        "Ext": "This is the passthrough content",
        "AndroidInfo": { 
			"Sound": "android.mp3",
			"OPPOChannelID": "test_OPPO_channel_id"
        },
        "ApnsInfo": {
            "Sound": "apns.mp3",
            "BadgeMode": 1,
            "Title":"apns title",
            "SubTitle":"apns subtitle",
            "Image":"www.image.com"
        }
    }
}
```

The preceding fields are described as follows:

| Field | Type | Property | Description |
|---------|---------|---------|---------|
| PushFlag | Integer | Optional | 0: enable push, 1: disable offline push. |
| Title | String | Optional | The offline push title. This field is applicable to both iOS and Android. |
| Desc | String | Optional | Offline push content. |
| Ext | String | Optional | The passthrough content of offline push. |
| AndroidInfo.Sound | String | Optional | The file path for the offline push sound in Android. |
| AndroidInfo.OPPOChannelID | String | Optional | This field is used for NotificationChannel notifications in OPPO mobile phones with Android 8.0 or later. |
| ApnsInfo.BadgeMode | Integer | Optional | The default value or 0 indicates that counting is required. 1 indicates that counting is not required for this message, in which case the number in the upper-right icon does not increase. |
| ApnsInfo.Title | String | Optional | This field identifies the title of APNs push messages. The top-level title is replaced when this field is filled in. |
| ApnsInfo.SubTitle | String | Optional | This field identifies the subtitle of APNs push messages. |
| ApnsInfo.Image | String | Optional | This field identifies the image URL carried by APNs. When the client obtains this field, it displays the image in a pop-up window by downloading the image through the URL. |

>The maximum data packet size supported by APNs is 4 KB. Therefore, we recommend that the total size of the `Desc` and `Ext` fields does not exceed 3 KB.

## References

Apple Push Notification Service (APNs) [Apple Push Programming Documentation](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/Introduction.html#//apple_ref/doc/uid/TP40008194-CH1-SW1).
 <!--Configuration of iOS offline message push: [Offline Push (iOS)]().-->

