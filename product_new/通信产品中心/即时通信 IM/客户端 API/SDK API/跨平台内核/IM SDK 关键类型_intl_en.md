## Common Macros and Basic Configuration Options


### TIMResult

Value returned after an API is called.

| Parameter | Value | Description |
|-----|-----|-----|
| TIM_SUCC | 0 | The API was called successfully. |
| TIM_ERR_SDKUNINIT | –1 | The API failed to be called because the IM SDK was not initialized yet. |
| TIM_ERR_NOTLOGIN | –2 | The API failed to be called because the user has not logged in yet. |
| TIM_ERR_JSON | –3 | The API failed to be called because the JSON format or JSON key is incorrect. |
| TIM_ERR_PARAM | –4 | The API failed to be called because parameters are incorrect. |
| TIM_ERR_CONV | –5 | The API failed to be called because the conversation is invalid. |
| TIM_ERR_GROUP | –6 | The API failed to be called because the group is invalid. |

> If the API parameters contain a callback function, the callback function is called only when the API returns TIM_SUCC.


### TIMLogLevel

Log level.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMLog_Off | 0 | Log output is disabled. |
| kTIMLog_Verbose | 1 | Detailed logs during development and commissioning |
| kTIMLog_Debug | 2 | Debugging logs |
| kTIMLog_Info | 3 | Information logs |
| kTIMLog_Warn | 4 | Warning logs |
| kTIMLog_Error | 5 | Error logs |
| kTIMLog_Assert | 6 | Assertion logs |

### TIMNetworkStatus

Connection event type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMConnected | 0 | Connected |
| kTIMDisconnected | 1 | Disconnected |
| kTIMConnecting | 2 | Connecting |
| kTIMConnectFailed | 3 | Failed to connect |

### TIMConvEvent

Conversation event type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMConvEvent_Add | 0 | Conversation addition. For example, this event is triggered when a new message is received and a new conversation is generated. |
| kTIMConvEvent_Del | 1 | Conversation deletion. For example, this event is triggered when you delete a conversation. |
| kTIMConvEvent_Update | 2 | Conversation update. This event is triggered when the unread message count changes in a conversation and a new message is received. |

### TIMConvType

Conversation type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMConv_Invalid | 0 | Invalid conversation |
| kTIMConv_C2C | 1 | Customer-to-customer (C2C) conversation |
| kTIMConv_Group | 2 | Group conversation |
| kTIMConv_System | 3 | System conversation |

### SdKConfig

Configuration used for initialization of the IM SDK.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMSdkConfigConfigFilePath | String | Write-only (optional) | The configuration file path. The default path is "/". |
| kTIMSdkConfigLogFilePath | String | Write-only (optional) | The log file path. The default path is "/". |
| kTIMSdkConfigJavaVM | UInt64 | Write-only (optional) | The Java VM pointer for Android configuration. |

### TIMGroupMemberInfoFlag

Group member information flag.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupMemberInfoFlag_None | 0x00 | None |
| kTIMGroupMemberInfoFlag_JoinTime | 0x01 | Join time |
| kTIMGroupMemberInfoFlag_MsgFlag | 0x01 << 1 | Group message receiving option |
| kTIMGroupMemberInfoFlag_MsgSeq | 0x01 << 2 | Seq of the message that has been read by the member |
| kTIMGroupMemberInfoFlag_MemberRole | 0x01 << 3 | Member role |
| kTIMGroupMemberInfoFlag_ShutupUntill | 0x01 << 4 | Mute time. 0: mute is disabled. |
| kTIMGroupMemberInfoFlag_NameCard | 0x01 << 5 | Group name card |

### TIMGroupMemberRoleFlag

Group member role flag.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupMemberRoleFlag_All | 0x00 | Obtains all role types. |
| kTIMGroupMemberRoleFlag_Owner | 0x01 | Obtains the owners (group owners). |
| kTIMGroupMemberRoleFlag_Admin | 0x01 << 1 | Obtains the admins, excluding group owners. |
| kTIMGroupMemberRoleFlag_Member | 0x01 << 2 | Obtains common group members, excluding group owners and admins. |

### GroupMemberGetInfoOption

Options for obtaining the group member information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupMemberGetInfoOptionInfoFlag | UInt64 [TIMGroupMemberInfoFlag](#timgroupmemberinfoflag) | Read-write (optional) | Filters by desired information. The default value is 0xffffffff, indicating that all information is obtained. |
| kTIMGroupMemberGetInfoOptionRoleFlag | UInt64 [TIMGroupMemberRoleFlag](#timgroupmemberroleflag) | Read-write (optional) | Filters by member role. The default value is kTIMGroupMemberRoleFlag_All, indicating that all roles are obtained. |
| kTIMGroupMemberGetInfoOptionCustomArray | Array string | Write-only (optional) | For more information, see [Custom fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### TIMGroupGetInfoFlag

Group member information flag.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupInfoFlag_None | 0x00 | - |
| kTIMGroupInfoFlag_Name | 0x01 | Group name |
| kTIMGroupInfoFlag_CreateTime | 0x01 << 1 | Group creation time |
| kTIMGroupInfoFlag_OwnerUin | 0x01 << 2 | Group creator account |
| kTIMGroupInfoFlag_Seq | 0x01 << 3 | - |
| kTIMGroupInfoFlag_LastTime | 0x01 << 4 | Last modification time of group information |
| kTIMGroupInfoFlag_NextMsgSeq | 0x01 << 5 | - |
| kTIMGroupInfoFlag_LastMsgTime | 0X01 << 6 | Last group message time |
| kTIMGroupInfoFlag_AppId | 0x01 << 7 | - |
| kTIMGroupInfoFlag_MemberNum | 0x01 << 8 | Number of group members |
| kTIMGroupInfoFlag_MaxMemberNum | 0x01 << 9 | Maximum number of group members |
| kTIMGroupInfoFlag_Notification | 0x01 << 10 | Group notification content |
| kTIMGroupInfoFlag_Introduction | 0x01 << 11 | Group introduction content |
| kTIMGroupInfoFlag_FaceUrl | 0x01 << 12 | Group profile photo URL |
| kTIMGroupInfoFlag_AddOpton | 0x01 << 13 | Group adding option |
| kTIMGroupInfoFlag_GroupType | 0x01 << 14 | Group type |
| kTIMGroupInfoFlag_LastMsg | 0x01 << 15 | Latest message in the group |
| kTIMGroupInfoFlag_OnlineNum | 0x01 << 16 | Number of online group members |
| kTIMGroupInfoFlag_Visible | 0x01 << 17 | Indicates whether the group is visible. |
| kTIMGroupInfoFlag_Searchable | 0x01 << 18 | Indicates whether the group is searchable. |
| kTIMGroupInfoFlag_ShutupAll | 0x01 << 19 | Indicates whether all members of the group are muted. |

### GroupGetInfoOption

Options for obtaining the group information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupGetInfoOptionInfoFlag | UInt64 [TIMGroupGetInfoFlag](#timgroupgetinfoflag) | Read-write (optional) | Filters by desired information. The default value is 0xffffffff, indicating that all information is obtained. |
| kTIMGroupGetInfoOptionCustomArray | Array string | Write-only (optional) | For more information, see [Custom fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### UserConfig

User configuration.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMUserConfigIsReadReceipt | Bool | Write-only (optional) | true: the read receipt event is received. |
| kTIMUserConfigIsSyncReport | Bool | Write-only (optional) | true: the server deletes messages in read state. |
| kTIMUserConfigIsIngoreGroupTipsUnRead | Bool | Write-only (optional) | true: the group tips are excluded from the read group message count. |
| kTIMUserConfigIsDisableStorage | Bool | Write-only (optional) | Indicates whether to disable the local database. true: yes. false: no. The default value is false. |
| kTIMUserConfigGroupGetInfoOption | Object [GroupGetInfoOption](#groupgetinfooption) | Write-only (optional) | Obtains the default option for the group information. |
| kTIMUserConfigGroupMemberGetInfoOption | Object [GroupMemberGetInfoOption](#groupmembergetinfooption) | Write-only (optional) | Obtains the default option for the group member information. |

### HttpProxyInfo

HTTP proxy information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMHttpProxyInfoIp | String | Write-only (required) | IP address of the proxy |
| kTIMHttpProxyInfoPort | Int | Write-only (required) | Port of the proxy |

### Socks5ProxyInfo

SOCKS5 proxy information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMSocks5ProxyInfoIp | String | Write-only (required) | IP address of the SOCKS5 proxy |
| kTIMSocks5ProxyInfoPort | Int | Write-only (required) | Port of the SOCKS5 proxy |
| kTIMSocks5ProxyInfoUserName | String | Write-only (optional) | Authenticated username |
| kTIMSocks5ProxyInfoPassword | String | Write-only (optional) | Authenticated password |

### SetConfig

**Update the configuration**

- Custom data
The IM SDK only transparently transfers the data customized by developers to the IM backend. The maximum length of custom data is 64 bytes. The IM backend notifies the developer business backend of the custom data through the third-party callback [State Change Callback](https://intl.cloud.tencent.com/document/product/1047/34357).
- HTTP proxy
The HTTP proxy uploads related files to the COS when image, voice, file, and micro video messages are sent and downloads related files to the local server when image, voice, file, and micro video messages are received. To enable the HTTP proxy, you must specify the IP address of the proxy and cannot set the port to 0 (port 0 cannot be used). To disable the HTTP proxy, you only need to set the IP address of the proxy to a null string and the port to 0.
- SOCKS5 proxy
The SOCKS5 proxy must be enabled before initialization. After the SOCKS5 proxy is enabled, all protocols sent by the IM SDK are sent to the IM backend through the SOCKS5 proxy server.


| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMSetConfigLogLevel | UInt [TIMLogLevel](#timloglevel) | Write-only (optional) | Level of logs output to the log file |
| kTIMSetConfigCackBackLogLevel | UInt [TIMLogLevel](#timloglevel) | Write-only (optional) | Log level for the log callback |
| kTIMSetConfigIsLogOutputConsole | Bool | Write-only (optional) | Indicates whether to output logs to the console. |
| kTIMSetConfigUserConfig | Object [UserConfig](#userconfig) | Write-only (optional) | User configuration |
| kTIMSetConfigUserDefineData | String | Write-only (optional) | User-defined data, which must be set before initialization if needed |
| kTIMSetConfigHttpProxyInfo | Object [HttpProxyInfo](#httpproxyinfo) | Write-only (optional) | Sets the HTTP proxy. The HTTP proxy (if needed) must be enabled before image, file, voice, and video messages are sent. |
| kTIMSetConfigSocks5ProxyInfo | Object [Socks5ProxyInfo](#socks5proxyinfo) | Write-only (optional) | Sets the SOCKS5 proxy. The SOCKS5 proxy (if needed) must be enabled before initialization. |

## Message Key Types

Definitions of message-related macros and JSON keys for related struct member retrieval.

### IOSOfflinePushConfig

Offline message push configuration on iOS.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMIOSOfflinePushConfigTitle | string | Read-write | Notification title |
| kTIMIOSOfflinePushConfigSound | String | Read-write | URL of the offline push prompt tone of the current message on iOS devices. push.no_sound means no prompt tone or vibration. |
| kTIMIOSOfflinePushConfigIgnoreBadge | Bool | Read-write | Indicates whether to ignore the badge count. If this field is set to true, this message will not increase the unread message count on the app icon on the iOS receiving end. |

### TIMAndroidOfflinePushNotifyMode

Android offline push mode.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMAndroidOfflinePushNotifyMode_Normal | 0 | Common notification bar message mode. After an offline message is sent, users can click notification bar messages to directly launch the app, without triggering a callback for the app. |
| kTIMAndroidOfflinePushNotifyMode_Custom | 1 | Custom message mode. After an offline message is sent, a click of notification bar messages will trigger a callback for the app. |

### AndroidOfflinePushConfig

Offline message push configuration on Android.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMAndroidOfflinePushConfigTitle | String | Read-write | Notification title |
| kTIMAndroidOfflinePushConfigSound | string | Read-write | URL of the offline push prompt tone of the current message on Android devices |
| kTIMAndroidOfflinePushConfigNotifyMode | UInt [TIMAndroidOfflinePushNotifyMode](#timandroidofflinepushnotifymode) | Read-write | Notification mode of the current message |
| kTIMAndroidOfflinePushConfigOPPOChannelID | String | Read-write | OPPO ChannelID |

> ChannelID description
For Android 8.0 and later versions, channelid configuration is added to notification bar messages. This field is required for OPPO mobile phones. If it is not specified, OPPO mobile phones of Android 8.0 and later versions will not receive offline push messages. In the future, xiaomi_channel_id_, huawei_channel_id, etc. may also be added.


### TIMOfflinePushFlag

Push rules.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMOfflinePushFlag_Default | 0 | Push according to default rules |
| kTIMOfflinePushFlag_NoPush | 1 | No push |

### OfflinePushConfig

Offline message push configuration.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMOfflinePushConfigDesc | String | Read-write | Displayed content of the current message when the recipient receives the offline push. |
| kTIMOfflinePushConfigExt | String | Read-write | Extension field of the current message pushed offline |
| kTIMOfflinePushConfigFlag | UInt [TIMOfflinePushFlag](#timofflinepushflag) | Read-write | Indicates whether the current message can be pushed. The default value kTIMOfflinePushFlag_Default indicates that the current message can be pushed. |
| kTIMOfflinePushConfigIOSConfig | Object [IOSOfflinePushConfig](#iosofflinepushconfig) | Read-write | iOS offline push configuration |
| kTIMOfflinePushConfigAndroidConfig | Object [AndroidOfflinePushConfig](#androidofflinepushconfig) | Read-write | Android offline push configuration |

### TIMMsgStatus

Definition of the current message status.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMMsg_Sending | 1 | The message is being sent. |
| kTIMMsg_SendSucc | 2 | The message was successfully sent. |
| kTIMMsg_SendFail | 3 | The message failed to be sent. |
| kTIMMsg_Deleted | 4 | The message was deleted. |
| kTIMMsg_LocalImported | 5 | The message was imported to the local server. |
| kTIMMsg_Revoked | 6 | The message was recalled. |

### TIMMsgPriority

Message priority. A larger number indicates a lower priority.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMMsgPriority_High | 0 | Highest priority. Generally, the priority of a red packet or gift message is the highest. |
| kTIMMsgPriority_Normal | 1 | Second priority. It is recommended that the priority of common messages be set to Normal. |
| kTIMMsgPriority_Low | 2 | It is recommended that the priority of like messages be set to Low. |
| kTIMMsgPriority_Lowest | 3 | Lowest priority. Generally, this is the priority for notifications of joining or quitting a group (sent by the backend). |

### Message

Message JSON keys.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgElemArray | Array [Elem](#elem) | Read-write (required) | Message element list |
| kTIMMsgConvId | String | Read-write (optional) | Conversation ID of the message |
| kTIMMsgConvType | UInt [TIMConvType](#timconvtype) | Read-write (optional) | Conversation type of the message |
| kTIMMsgSender | String | Read-write (optional) | Message sender |
| kTIMMsgPriority | UInt [TIMMsgPriority](#timmsgpriority) | Read-write (optional) | Message priority |
| kTIMMsgClientTime | UInt64 | Read-write (optional) | Client time |
| kTIMMsgServerTime | UInt64 | Read-write (optional) | Server time |
| kTIMMsgIsFormSelf | Bool | Read-write (optional) | Indicates whether the message comes from yourself. |
| kTIMMsgIsRead | Bool | Read-write (optional) | Indicates whether the message has been read. |
| kTIMMsgIsOnlineMsg | Bool | Read-write (optional) | Indicates whether the message is an online message. The default value is false. false: a common message. true: a message that will be deleted immediately after being read. |
| kTIMMsgIsPeerRead | Bool | Read-only | Indicates whether the message has been read by the peer party of the conversation. |
| kTIMMsgStatus | UInt [TIMMsgStatus](#timmsgstatus) | Read-write (optional) | Current message status |
| kTIMMsgUniqueId | UInt64 | Read-only | Unique ID of the message |
| kTIMMsgRand | UInt64 | Read-only | Random code of the message |
| kTIMMsgSeq | UInt64 | Read-only | Message sequence number |
| kTIMMsgCustomInt | UInt32_t | Read-write (optional) | Custom integer value field |
| kTIMMsgCustomStr | String | Read-write (optional) | Custom data field |
| kTIMMsgSenderProfile | Object [UserProfile](#userprofile) | Read-write (optional) | User profile of the message sender |
| kTIMMsgSenderGroupMemberInfo | Object [GroupMemberInfo](#groupmemberinfo) | Read-write (optional) | The message sender’s group member information, which is valid only in group conversations. Currently, only the kTIMGroupMemberInfoIdentifier and kTIMGroupMemberInfoNameCard fields can be obtained. For other fields, it is recommended that they be obtained through the `TIMGroupGetMemberInfoList` API. |
| kTIMMsgOfflinePushConfig | Object [OfflinePushConfig](#offlinepushconfig) | Read-write (optional) | Offline push configuration of the message |

>
- Corresponding elem sequence.
Currently, the file and voice elem are not necessarily transmitted in the sequence in which they are added. Other elem are transmitted in the sequence that they are added. However, it is recommended that you do not heavily rely on the elem sequence to process elements. Instead, you should process elem by type to prevent process crashes when exceptions occur.
- Red packet and like messages in the group.
The like and red packet features are supported in the live-broadcast scenario. The priority of a like message is lower than that of a red packet message. You can define the specific message content by using the custom message [CustomElem](#customelem). When sending a message, you can use `kTIMMsgPriority` to define the message priority.
- Messages that will be deleted immediately after being read.
When `kTIMMsgIsOnlineMsg` is set to true, a message that will be deleted immediately after being read is sent. This message has the following features:
 - C2C conversation: when this message is sent, the peer party can receive the message only when they are online. If the peer party is offline when the message is sent, they can no longer receive this message even if they log in to IM later.
 - Group conversation: when this message is sent, only online members in the group can receive the message. If a member is offline when the message is sent, they can no longer receive this message even if they log in to IM later.
 - The server does not store this message.
 - This message is excluded from the unread message count.
 - This message is not stored locally.
- Message custom fields.
Developers can add the following custom fields to messages: custom integer fields (specified by `kTIMMsgCustomInt`) and custom binary data fields (specified by `kTIMMsgCustomStr` and must be converted to a string. JSON does not support binary transfer). These two fields can be used to achieve different effects, for example, indicating whether a voice message has been played. Note that the custom fields are only stored locally and are not synchronized to the server. Therefore, these custom fields cannot be obtained on a different terminal.


### MessageReceipt

Message read receipt.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgReceiptConvId | String | Read-only | Conversation ID |
| kTIMMsgReceiptConvType | UInt [TIMConvType](#timconvtype) | Read-only | Conversation type |
| kTIMMsgReceiptTimeStamp | UInt64 | Read-only | Timestamp |

### TIMElemType

Element type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMElem_Text | 0 | Text element |
| kTIMElem_Image | 1 | Image element |
| kTIMElem_Sound | 2 | Voice element |
| kTIMElem_Custom | 3 | Custom element |
| kTIMElem_File | 4 | File element |
| kTIMElem_GroupTips | 5 | Group system message element |
| kTIMElem_Face | 6 | Emoji element |
| kTIMElem_Location | 7 | Location element |
| kTIMElem_GroupReport | 8 | Group system notification element |
| kTIMElem_Video | 9 | Video element |
| kTIMElem_FriendChange | 10 | Relationship chain change message element |
| kTIMElem_ProfileChange | 11 | Profile change message element |

### Elem

Element type.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMElemType | UInt [TIMElemType](#timelemtype) | Read-write (required) | Element type |

### TextElem

Text element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMTextElemContent | String | Read-write (required) | Text content |

### FaceElem

Emoji element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFaceElemIndex | Int | Read-write (required) | Emoji index |
| kTIMFaceElemBuf | String | Read-write (optional) | Other extra data, which can be customized by the user. To transmit binary data, convert it to strings because JSON only supports strings. |

> The IM SDK does not provide any emoji packages. If developers have an emoji package, they can use `kTIMFaceElemIndex` to store the index of an emoji in the emoji package. Developers can customize the emoji indexes. Alternatively, they can directly use `kTIMFaceElemBuf` to store the binary data of the emoji, which must be converted into strings because JSON does not support transmission of binary data. Developers can customize the binary data of emojis, and the IM SDK only transparently transmits the binary data.


### LocationElem

Location element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMLocationElemDesc | String | Read-write (optional) | Location description |
| kTIMLocationElemLongitude | double | Read-write (required) | Longitude |
| kTIMLocationElemlatitude | double | Read-write (required) | Latitude |

### TIMImageLevel

Image quality level.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMImageLevel_Orig | 0 | Send the original image. |
| kTIMImageLevel_Compression | 1 | Send the compressed image, which has a smaller size. This is the default value. |
| kTIMImageLevel_HD | 2 | Send the high definition (HD) image, which has a larger size. |

### ImageElem

Image element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMImageElemOrigPath | String | Read-write (required) | Path of the image to be sent |
| kTIMImageElemLevel | UInt [TIMImageLevel](#timimagelevel) | Read-write (required) | Quality level of the image to be sent |
| kTIMImageElemFormat | Int | Read-write (required) | Format of the image to be sent |
| kTIMImageElemOrigId | String | Read-only | UUID of the original image |
| kTIMImageElemOrigPicHeight | Int | Read-only | Height of the original image |
| kTIMImageElemOrigPicWidth | Int | Read-only | Width of the original image |
| kTIMImageElemOrigPicSize | Int | Read-only | Size of the original image |
| kTIMImageElemThumbId | String | Read-only | UUID of the thumbnail |
| kTIMImageElemThumbPicHeight | Int | Read-only | Height of the thumbnail |
| kTIMImageElemThumbPicWidth | Int | Read-only | Width of the thumbnail |
| kTIMImageElemThumbPicSize | Int | Read-only | Size of the thumbnail |
| kTIMImageElemLargeId | String | Read-only | UUID of the large image |
| kTIMImageElemLargePicHeight | Int | Read-only | Height of the large image |
| kTIMImageElemLargePicWidth | Int | Read-only | Width of the large image |
| kTIMImageElemLargePicSize | Int | Read-only | Size of the large image |
| kTIMImageElemOrigUrl | String | Read-only | URL of the original image |
| kTIMImageElemThumbUrl | String | Read-only | URL of the thumbnail |
| kTIMImageElemLargeUrl | String | Read-only | URL of the large image |
| kTIMImageElemTaskId | Int | Read-only | Task ID |

>
- Each image has three specifications, including Original (original image), Large (large image), and Thumb (thumbnail).
 - Original: users send the original image without changing its size.
 - Large: the original image is proportionally compressed. After compression, the height or width (whichever is smaller) is set to 720 pixels.
 - Thumb: the original image is proportionally compressed. After compression, the height or width (whichever is smaller) is set to 198 pixels.
- If the size of the original image is smaller than 198 pixels, the original size is retained for the three specifications, and no compression is needed.
- If the size of the original image falls between 198 and 720 pixels, the large image is the same as the original image, and no compression is needed.
- When an image is displayed on a mobile phone, it is recommended that the thumbnail be displayed first. When the user taps the thumbnail, the large image is downloaded. When the user taps the large image, the original image is downloaded. Alternatively, developers can choose to skip the large image so that the original image is directly downloaded when the user taps the thumbnail.
- When an image is displayed on a tablet or PC, it is recommended that the large image be displayed directly and the original image be downloaded when the user taps or clicks the large image, because the resolution is high resolution and a Wi-Fi or wired network is used.


### SoundElem

Sound element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMSoundElemFilePath | String | Read-write (required) | Path of the voice file. The developer must first store the voice file and then specify the path. |
| kTIMSoundElemFileSize | Int | Read-write (required) | Size (in seconds) of the sound element voice file |
| kTIMSoundElemFileTime | Int | Read-write (required) | Duration of the voice file |
| kTIMSoundElemFileId | String | Read-only | ID of the voice file when the file is downloaded |
| kTIMSoundElemBusinessId | Int | Read-only | BusinessID used upon download |
| kTIMSoundElemDownloadFlag | Int | Read-only | Indicates whether a download address needs to be applied for. 0: yes. 1: apply from the COS. 2: directly use the URL for download. |
| kTIMSoundElemUrl | String | Read-only | Download URL |
| kTIMSoundElemTaskId | Int | Read-only | Task ID |

>
- A message custom field can be used to indicate whether a voice message file has been played. For example, the value 0 can be defined to indicate that the voice message file has not been played yet, and the value 1 can be defined to indicate that the voice message file has been played. When the user taps Play, the value of the field can change to 1.
- Only one sound element can be added to one message. If multiple sound elements are added to a message, the message may fail to be sent.


### CustomElem

Custom element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMCustomElemData | String | Read-write | Data of the custom element, which can be the binary data |
| kTIMCustomElemDesc | String | Read-write | Description of the custom element |
| kTIMCustomElemExt | String | Read-write | Ext field pushed by the backend |
| kTIMCustomElemSound | String | Read-write | Custom sound |

> When the built-in message types cannot meet special requirements, developers can customize message formats. The content of each custom message is completely defined by developers, and the IM SDK only transparently transmits the content.


### FileElem

File element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFileElemFilePath | String | Read-write (required) | File path (including the file name) |
| kTIMFileElemFileName | String | Read-write (required) | Displayed file name. If this parameter is not specified, kTIMFileElemFileName is the file name in the file path specified by kTIMFileElemFilePath by default. |
| kTIMFileElemFileSize | Int | Read-write (required) | File size |
| kTIMFileElemFileId | String | Read-only | UUID when the file is downloaded |
| kTIMFileElemBusinessId | Int | Read-only | BusinessID used upon download |
| kTIMFileElemDownloadFlag | Int | Read-only | File download flag |
| kTIMFileElemUrl | String | Read-only | File download URL |
| kTIMFileElemTaskId | Int | Read-only | Task ID |

> Only one file element can be added to one message. If multiple file elements are added to a message, the message may fail to be sent.


### VideoElem

Video element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMVideoElemVideoType | String | Read-write (required) | Type of the video file, which is set when a message is sent |
| kTIMVideoElemVideoSize | UInt | Read-write (required) | Size of the video file |
| kTIMVideoElemVideoDuration | UInt | Read-write (required) | Duration of the video file, which is set when a message is sent |
| kTIMVideoElemVideoPath | String | Read-write (required) | Path of the video file |
| kTIMVideoElemVideoId | String | Read-only | UUID when the video file is downloaded |
| kTIMVideoElemBusinessId | Int | Read-only | BusinessID used upon download |
| kTIMVideoElemVideoDownloadFlag | Int | Read-only | Video file download flag |
| kTIMVideoElemVideoUrl | String | Read-only | URL used to download the video file |
| kTIMVideoElemImageType | String | Read-write (required) | Type of the screenshot file, which is set when a message is sent |
| kTIMVideoElemImageSize | UInt | Read-write (required) | Size of the screenshot file |
| kTIMVideoElemImageWidth | UInt | Read-write (required) | Width of the screenshot, which is set when a message is sent |
| kTIMVideoElemImageHeight | UInt | Read-write (required) | Height of the screenshot, which is set when a message is sent |
| kTIMVideoElemImagePath | String | Read-write (required) | Path for saving the screenshot |
| kTIMVideoElemImageId | String | Read-only | ID used when the video screenshot is downloaded |
| kTIMVideoElemImageDownloadFlag | Int | Read-only | Screenshot file download flag |
| kTIMVideoElemImageUrl | String | Read-only | URL used to download the screenshot file |
| kTIMVideoElemTaskId | UInt | Read-only | Task ID |

### TIMGroupTipGroupChangeFlag

Group information change type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupTipChangeFlag_Name | 0xa | The group name is modified |
| kTIMGroupTipChangeFlag_Introduction | 11 | Group introduction is modified. |
| kTIMGroupTipChangeFlag_Notification | 12 | Group notification is modified. |
| kTIMGroupTipChangeFlag_FaceUrl | 13 | The group profile photo URL is modified. |
| kTIMGroupTipChangeFlag_Owner | 14 | The group owner is modified. |

### GroupTipGroupChangeInfo

Group system message - modifying group information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupTipGroupChangeInfoFlag | UInt [TIMGroupTipGroupChangeFlag](#timgrouptipgroupchangeflag) | Read-only | Group information change flag for the group message |
| kTIMGroupTipGroupChangeInfoValue | String | Read-only | Value after the change. Different `info_flag` fields have different meanings. |

### GroupTipMemberChangeInfo

Group system message - muting group members.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupTipMemberChangeInfoIdentifier | String | Read-only | Group member ID |
| kTIMGroupTipMemberChangeInfoShutupTime | UInt | Read-only | Mute time |

### TIMGroupTipType

Group system message type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupTip_None | 0 | Invalid group tip |
| kTIMGroupTip_Invite | 1 | Tip for inviting a user to join the group |
| kTIMGroupTip_Quit | 2 | Tip for quitting a group |
| kTIMGroupTip_Kick | 3 | Tip for removing a member from a group |
| kTIMGroupTip_SetAdmin | 4 | Tip for setting an admin |
| kTIMGroupTip_CancelAdmin | 5 | Tip for canceling an admin |
| kTIMGroupTip_GroupInfoChange | 6 | Tip for changing the group information |
| kTIMGroupTip_MemberInfoChange | 7 | Tip for changing the group member information |

### GroupTipsElem

Group system message element (applicable to all group members).

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupTipsElemTipType | UInt [TIMGroupTipType](#timgrouptiptype) | Read-only | Group message type |
| kTIMGroupTipsElemOpUser | String | Read-only | Operator ID |
| kTIMGroupTipsElemGroupName | String | Read-only | Group name |
| kTIMGroupTipsElemGroupId | String | Read-only | Group ID |
| kTIMGroupTipsElemTime | UInt | Read-only | Group message time |
| kTIMGroupTipsElemUserArray | Array string | Read-only | List of operated accounts |
| kTIMGroupTipsElemGroupChangeInfoArray | Array [GroupTipGroupChangeInfo](#grouptipgroupchangeinfo) | Read-only | Group profile change information list, which is valid only when `tips_type` is set to `kTIMGroupTip_GroupInfoChange` |
| kTIMGroupTipsElemMemberChangeInfoArray | Array [GroupTipMemberChangeInfo](#grouptipmemberchangeinfo) | Read-only | Group member change information list, which is valid only when `tips_type` is set to `kTIMGroupTip_MemberInfoChange` |
| kTIMGroupTipsElemOpUserInfo | Object [UserProfile](#userprofile) | Read-only | Personal profile of the operator |
| kTIMGroupTipsElemOpGroupMemberInfo | Object [GroupMemberInfo](#groupmemberinfo) | Read-only | Group member information |
| kTIMGroupTipsElemChangedUserInfoArray | Array [UserProfile](#userprofile) | Read-only | Changed user information list |
| kTIMGroupTipsElemChangedGroupMemberInfoArray | Array [GroupMemberInfo](#groupmemberinfo) | Read-only | Group member information list |
| kTIMGroupTipsElemMemberNum | UInt | Read-only | Current number of group members, which is valid only when `tips_type` is set to `kTIMGroupTip_Invite`, `kTIMGroupTip_Quit`, or `kTIMGroupTip_Kick` |
| kTIMGroupTipsElemPlatform | String | Read-only | Operator platform information |

### TIMGroupReportType

Group system notification type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupReport_None | 0 | Unknown type |
| kTIMGroupReport_AddRequest | 1 | Application to join a group. This notification can only be received by the admin. |
| kTIMGroupReport_AddAccept | 2 | Application to join a group accepted. This notification can only be received by the applicant. |
| kTIMGroupReport_AddRefuse | 3 | Application to join a group rejected. This notification can only be received by the applicant. |
| kTIMGroupReport_BeKicked | 4 | Kicked out of the group by the admin. This notification can only be received by the member who is kicked out of the group. |
| kTIMGroupReport_Delete | 5 | Group disbanded. This notification can be received by all members of the group. |
| kTIMGroupReport_Create | 6 | Group created. This notification can only be received by the creator and is not displayed. |
| kTIMGroupReport_Invite | 7 | User invited to join a group. This notification can only be received by the invited user. |
| kTIMGroupReport_Quit | 8 | Quit a group. This notification can only be received by the member who quits the group and is not displayed. |
| kTIMGroupReport_GrantAdmin | 9 | Admin set. This notification can only be received by the user who is set as an admin. |
| kTIMGroupReport_CancelAdmin | 10 | Admin canceled. This notification can only be received by the user whose admin role is canceled. |
| kTIMGroupReport_RevokeAdmin | 11 | Group revoked. This notification can be received by all members of the group and is not displayed. |
| kTIMGroupReport_InviteReq | 12 | User invited to join a group. This notification can only be received by the invited user. |
| kTIMGroupReport_InviteAccept | 13 | Invitation to join a group accepted. This notification can only be received by the inviting user. |
| kTIMGroupReport_InviteRefuse | 14 | Invitation to join a group rejected. This notification can only be received by the inviting user. |
| kTIMGroupReport_ReadReport | 15 | Read report synchronized across multiple terminals. This notification can only be received by the reporter. |
| kTIMGroupReport_UserDefine | 16 | User-defined notification. This notification can be received by all group members by default. |

### GroupReportElem

Group system notification elements (for individuals).

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupReportElemReportType | UInt [TIMGroupReportType](#timgroupreporttype) | Read-only | Type |
| kTIMGroupReportElemGroupId | String | Read-only | Group ID |
| kTIMGroupReportElemGroupName | String | Read-only | Group name |
| kTIMGroupReportElemOpUser | String | Read-only | Operator ID |
| kTIMGroupReportElemMsg | String | Read-only | Reason of the operation |
| kTIMGroupReportElemUserData | String | Read-only | Custom data entered by the operator |
| kTIMGroupReportElemOpUserInfo | Object [UserProfile](#userprofile) | Read-only | Personal profile of the operator |
| kTIMGroupReportElemOpGroupMemberInfo | Object [GroupMemberInfo](#groupmemberinfo) | Read-only | Group information of the operator |
| kTIMGroupReportElemPlatform | String | Read-only | Operator platform information |

### TIMProfileChangeType

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMProfileChange_None | 0 | Unknown type |
| kTIMProfileChange_Profile | 1 | Profile change |

### ProfileChangeElem

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMProfileChangeElemChangeType | UInt [TIMProfileChangeType](#timprofilechangetype) | Read-only | Profile change type |
| kTIMProfileChangeElemFromIndentifier | String | Read-only | UserID of the user whose profile is changed |
| kTIMProfileChangeElemUserProfileItem | Object [UserProfileItem](#userprofileitem) | Read-only | Specific change information, which is valid only when `change_type` is set to `kTIMProfileChange_Profile` |

### TIMFriendChangeType

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMFriendChange_None | 0 | Unknown type |
| kTIMFriendChange_FriendAdd | 1 | Added a friend list |
| kTIMFriendChange_FriendDel | 2 | Deleted a friend list |
| kTIMFriendChange_PendencyAdd | 3 | Added a pending request |
| kTIMFriendChange_PendencyDel | 4 | Deleted a pending request |
| kTIMFriendChange_BlackListAdd | 5 | Added users to the blacklist |
| kTIMFriendChange_BlackListDel | 6 | Deleted users from the blacklist |
| kTIMFriendChange_PendencyReadedReport | 7 | Reported read pending requests |
| kTIMFriendChange_FriendProfileUpdate | 8 | Updated friend profiles |
| kTIMFriendChange_FriendGroupAdd | 9 | Added a group |
| kTIMFriendChange_FriendGroupDel | 10 | Deleted a group |
| kTIMFriendChange_FriendGroupModify | 11 | Group modification |

### FriendProfileUpdate

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendProfileUpdateIdentifier | String | Write-only | UserID of a friend whose profile is updated |
| kTIMFriendProfileUpdateItem | Object [FriendProfileItem](#friendprofileitem) | Write-only | Profile update item |

### FriendChangeElem

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendChangeElemChangeType | UInt [TIMFriendChangeType](#timfriendchangetype) | Read-only | Profile change type |
| kTIMFriendChangeElemFriendAddIdentifierArray | Array string | Read-only | List of added friend UserIDs, which is valid only when `change_type` is set to `kTIMFriendChange_FriendAdd` |
| kTIMFriendChangeElemFriendDelIdentifierArray | Array string | Read-only | List of deleted friend UserIDs, which is valid only when `change_type` is set to `kTIMFriendChange_FriendDel` |
| kTIMFriendChangeElemFriendAddPendencyItemArray | Array [FriendAddPendency](#friendaddpendency) | Read-only | List of pending friend requests, which is valid only when `change_type` is set to `kTIMFriendChange_PendencyAdd` |
| kTIMFriendChangeElemPendencyDelIdentifierArray | Array string | Read-only | List of deleted pending friend requests, which is valid only when `change_type` is set to `kTIMFriendChange_PendencyDel` |
| kTIMFriendChangeElemPendencyReadedReportTimestamp | UInt64 | Read-only | Timestamp for reporting the pending requests, which is valid only when `change_type` is set to `kTIMFriendChange_PendencyReadedReport` |
| kTIMFriendChangeElemBlackListAddIdentifierArray | Array string | Read-only | List of UserIDs added to the blacklist, which is valid only when `change_type` is set to `kTIMFriendChange_BlackListAdd` |
| kTIMFriendChangeElemBlackListDelIdentifierArray | Array string | Read-only | List of UserIDs deleted from the blacklist, which is valid only when `change_type` is set to `kTIMFriendChange_BlackListDel` |
| kTIMFriendChangeElemFreindProfileUpdateItemArray | Array [FriendProfileUpdate](#friendprofileupdate) | Read-only | Friend profile update list, which is valid only when `change_type` is set to `kTIMFriendChange_FriendProfileUpdate` |
| kTIMFriendChangeElemFriendGroupAddIdentifierArray | Array string | Read-only | List of added friend groups, which is valid only when `change_type` is set to `kTIMFriendChange_FriendGroupAdd` |
| kTIMFriendChangeElemFriendGroupDelIdentifierArray | Array string | Read-only | List of deleted friend groups, which is valid only when `change_type` is set to `kTIMFriendChange_FriendGroupDel` |
| kTIMFriendChangeElemFriendGroupModifyIdentifierArray | Array string | Read-only | List of modified friend groups, which is valid only when `change_type` is set to `kTIMFriendChange_FriendGroupModify` |

### MsgBatchSendParam

Parameters of the API for sending messages in batches.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgBatchSendParamIdentifierArray | Array string | Write-only (required) | List of IDs for batch sending |
| kTIMMsgBatchSendParamMsg | Object [Message](#message) | Write-only (required) | Messages that are sent in batches |

### MsgBatchSendResult

Result returned by the API for sending messages in batches.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgBatchSendResultIdentifier | String | Read-only | Single ID for batch sending |
| kTIMMsgBatchSendResultCode | Int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Result of batch message sending |
| kTIMMsgBatchSendResultDesc | String | Read-only | Description of message sending |
| kTIMMsgBatchSendResultMsg | Object [Message](#message) | Read-only | Sent messages |

### MsgLocator

Message locator.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgLocatorConvId | Bool | Read-write | ID of the conversation to which the message to be searched for belongs |
| kTIMMsgLocatorConvType | Bool | Read-write | Type of the conversation to which the message to be searched for belongs |
| kTIMMsgLocatorIsRevoked | Bool | Read-write (required) | Indicates whether the message to be searched for has been recalled. true: recalled. false: not recalled. The default value is false. |
| kTIMMsgLocatorTime | UInt64 | Read-write (required) | Timestamp of the message to be searched for |
| kTIMMsgLocatorSeq | UInt64 | Read-write (required) | Sequence number of the message to be searched for |
| kTIMMsgLocatorIsSelf | Bool | Read-write (required) | Indicates whether the sender of the message to be searched for is yourself. true: yes. false: no. The default value is false. |
| kTIMMsgLocatorRand | UInt64 | Read-write (required) | Random code of the message to be searched for |
| kTIMMsgLocatorUniqueId | UInt64 | Read-write (required) | Unique ID of the message to be searched for |

### MsgGetMsgListParam

Parameters of the API for obtaining messages.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgGetMsgListParamLastMsg | Object [Message](#message) | Write-only (optional) | Specified message, which cannot be null |
| kTIMMsgGetMsgListParamCount | UInt | Write-only (optional) | Number of messages counted starting from the specified message |
| kTIMMsgGetMsgListParamIsRamble | Bool | Write-only (optional) | Indicates whether the messages are roaming messages |
| kTIMMsgGetMsgListParamIsForward | Bool | Write-only (optional) | Indicates whether the messages are forward sequenced |

### MsgDeleteParam

Parameters of the API for deleting a message.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgDeleteParamMsg | Object [Message](#message) | Write-only (optional) | Specified message to be deleted from the conversation |
| kTIMMsgDeleteParamIsRamble | Bool | Write-only (optional) | Indicates whether to delete all the local/roaming messages. true: delete roaming messages. false: delete local messages. The default value is false. |

### TIMDownloadType

UUID type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMDownload_VideoThumb | 0 | Video thumbnail |
| kTIMDownload_File | 1 | File |
| kTIMDownload_Video | 2 | Video |
| kTIMDownload_Sound | 3 | Sound |

### DownloadElemParam

Parameters of the API for downloading elements.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgDownloadElemParamFlag | UInt | Write-only | Element download type, which is extracted from the message element |
| kTIMMsgDownloadElemParamType | UInt [TIMDownloadType](#timdownloadtype) | Write-only | Element type, which is extracted from the message element |
| kTIMMsgDownloadElemParamId | String | Write-only | Element ID, which is extracted from the message element |
| kTIMMsgDownloadElemParamBusinessId | UInt | Write-only | Element BusinessID, which is extracted from the message element |
| kTIMMsgDownloadElemParamUrl | String | Write-only | Element URL, which is extracted from the message element |

### MsgDownloadElemResult

Result returned by the API for downloading elements.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgDownloadElemResultCurrentSize | UInt | Read-only | Size of currently downloaded data |
| kTIMMsgDownloadElemResultTotalSize | UInt | Read-only | Total size of the file to be downloaded |

## Conversation Key Types

Definitions of conversation-related macros and JSON keys for related struct member retrieval.

### Draft

Draft information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMDraftMsg | Object [Message](#message) | Read-only | Message in drafts |
| kTIMDraftUserDefine | String | Read-only | User-defined data |
| kTIMDraftEditTime | UInt | Read-only | Last editing time of the draft |

### ConvInfo

Conversation information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMConvId | String | Read-only | Conversation ID |
| kTIMConvType | UInt [TIMConvType](#timconvtype) | Read-only | Conversation type |
| kTIMConvOwner | String | Read-only | Conversation owner |
| kTIMConvUnReadNum | UInt64 | Read-only | Unread conversation count |
| kTIMConvActiveTime | UInt64 | Read-only | Conversation activation time |
| kTIMConvIsHasLastMsg | Bool | Read-only | Indicates whether the conversation has the last message. |
| kTIMConvLastMsg | Object [Message](#message) | Read-only | Last message of the conversation |
| kTIMConvIsHasDraft | Bool | Read-only | Indicates whether the conversation has a draft. |
| kTIMConvDraft | Object [Draft](#draft) | Read-only (optional) | Conversation draft |

## Group Key Types

Definitions of group-related macros and JSON keys for related struct member retrieval.

### TIMGroupAddOption

Group adding option.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupAddOpt_Forbid | 0 | Adding to groups is prohibited. |
| kTIMGroupAddOpt_Auth | 1 | Approval from the admin is required. |
| kTIMGroupAddOpt_Any | 2 | Anyone can add to the group. |

### TIMGroupType

Group Type

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroup_Public | 0 | Public group |
| kTIMGroup_Private | 1 | Private group |
| kTIMGroup_ChatRoom | 2 | Chat room |
| kTIMGroup_BChatRoom | 3 | Broadcasting chat room |
| kTIMGroup_AVChatRoom | 4 | Audio-video chat room |

### TIMGroupMemberRole

Group member role.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMMemberRole_None | 0 | Undefined |
| kTIMMemberRole_Normal | 1 | Common group member |
| kTIMMemberRole_Admin | 2 | Admin |
| kTIMMemberRole_Owner | 3 | Super admin (group owner) |

### GroupMemberInfoCustemString

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupMemberInfoCustemStringInfoKey | string | Write-only | Key of the custom field |
| kTIMGroupMemberInfoCustemStringInfoValue | string | Write-only | Value of the custom field |

## GroupMemberInfo

Group member information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupMemberInfoIdentifier | String | Read-write (required) | ID of the group member |
| kTIMGroupMemberInfoJoinTime | UInt | Read-only | Time when the group member joined the group |
| kTIMGroupMemberInfoMemberRole | UInt [TIMGroupMemberRole](#timgroupmemberrole) | Read-write (optional) | Role of the group member |
| kTIMGroupMemberInfoMsgFlag | UInt | Read-only | Message receiving option of the group member |
| kTIMGroupMemberInfoMsgSeq | UInt | Read-only | - |
| kTIMGroupMemberInfoShutupTime | UInt | Read-only | Mute time of the group member |
| kTIMGroupMemberInfoNameCard | String | Read-only | Group namecard of the group member |
| kTIMGroupMemberInfoCustomInfo | Array [GroupMemberInfoCustemString](#groupmemberinfocustemstring) | Read-only | For more information, see [Custom fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### GroupInfoCustemString

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupInfoCustemStringInfoKey | String | Write-only | Key of the custom field |
| kTIMGroupInfoCustemStringInfoValue | String | Write-only | Value of the custom field |

### CreateGroupParam

Parameters of the API for creating a group.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMCreateGroupParamGroupName | String | Write-only (required) | Group name |
| kTIMCreateGroupParamGroupId | String | Write-only (optional) | Group ID. If this field is not specified, the callback triggered when the group is successfully created will return a group ID assigned by the backend. |
| kTIMCreateGroupParamGroupType | UInt [TIMGroupType](#timgrouptype) | Write-only (optional) | Group type. The default value is Public. |
| kTIMCreateGroupParamGroupMemberArray | Array [GroupMemberInfo](#groupmemberinfo) | Write-only (optional) | Array of initial members of the group |
| kTIMCreateGroupParamNotification | String | Write-only (optional) | Group notification |
| kTIMCreateGroupParamIntroduction | String | Write-only (optional) | Group introduction |
| kTIMCreateGroupParamFaceUrl | String | Write-only (optional) | Group profile photo URL |
| kTIMCreateGroupParamAddOption | UInt [TIMGroupAddOption](#timgroupaddoption) | Write-only (optional) | Group adding option. The default value is Any. |
| kTIMCreateGroupParamMaxMemberCount | UInt | Write-only (optional) | Maximum number of members in the group |
| kTIMCreateGroupParamCustomInfo | Array [GroupInfoCustemString](#groupinfocustemstring) | Read-only (optional) | For more information, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### CreateGroupResult

Result returned by the API for creating a group.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMCreateGroupResultGroupId | String | Read-only | ID of the created group |

### GroupInviteMemberParam

Parameters of the API for inviting members.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupInviteMemberParamGroupId | String | Write-only (required) | Group ID |
| kTIMGroupInviteMemberParamIdentifierArray | Array string | Write-only (required) | ID array of users who are invited to join the group |
| kTIMGroupInviteMemberParamUserData | String | Write-only (optional) | User-defined data |

### HandleGroupMemberResult

Basic group information.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupMember_HandledErr | 0 | Failed |
| kTIMGroupMember_HandledSuc | 1 | Succeeded |
| kTIMGroupMember_Included | 2 | Already a group member |
| kTIMGroupMember_Invited | 3 | Already invited |

### GroupInviteMemberResult

Result returned by the API for inviting members.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupInviteMemberResultIdentifier | String | Read-only | ID of the user who was invited to join the group |
| kTIMGroupInviteMemberResultResult | UInt [HandleGroupMemberResult](#handlegroupmemberresult) | Read-only | Invitation result |

### GroupDeleteMemberParam

Parameters of the API for deleting members.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupDeleteMemberParamGroupId | String | Write-only (required) | Group ID |
| kTIMGroupDeleteMemberParamIdentifierArray | Array string | Write-only (required) | ID array of users who are deleted from the group |
| kTIMGroupDeleteMemberParamUserData | String | Write-only (optional) | User-defined data |

### GroupDeleteMemberResult

Result returned by the API for deleting members.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupDeleteMemberResultIdentifier | String | Read-only | ID of the deleted member |
| kTIMGroupDeleteMemberResultResult | UInt [HandleGroupMemberResult](#handlegroupmemberresult) | Read-only | Deletion result |

### TIMGroupReceiveMessageOpt

Group message receiving option.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMRecvGroupMsgOpt_ReceiveAndNotify | 0 | Receive group messages and notify. |
| kTIMRecvGroupMsgOpt_NotReceive | 1 | Do not receive group messages. The server will not forward group messages. |
| kTIMRecvGroupMsgOpt_ReceiveNotNotify | 2 | Receive group message but do not notify. |

### GroupSelfInfo

Self information in the group.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupSelfInfoJoinTime | UInt | Read-only | Time when the user joins the group |
| kTIMGroupSelfInfoRole | UInt | Read-only | Role of the user in the group |
| kTIMGroupSelfInfoUnReadNum | UInt | Read-only | Unread message count |
| kTIMGroupSelfInfoMsgFlag | UInt [TIMGroupReceiveMessageOpt](#timgroupreceivemessageopt) | Read-only | Group message receiving option |

### GroupBaseInfo

Result (basic group information) returned by the API for obtaining the list of groups that a user has joined.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupBaseInfoGroupId | String | Read-only | Group ID |
| kTIMGroupBaseInfoGroupName | String | Read-only | Group name |
| kTIMGroupBaseInfoGroupType | UInt [TIMGroupType](#timgrouptype) | Read-only | Group type |
| kTIMGroupBaseInfoFaceUrl | String | Read-only | Group profile photo URL |
| kTIMGroupBaseInfoInfoSeq | UInt | Read-only | Seq of the group profile. The value of this field increases by one each time the group profile is changed. |
| kTIMGroupBaseInfoLastestSeq | UInt | Read-only | Seq of the latest message in the group. Each message in the group has a unique seq, which is consecutive based on the message sending sequence. The value of LastestSeq starts from 1 and increases by 1 each time a message is added to the group. |
| kTIMGroupBaseInfoReadedSeq | UInt | Read-only | Seq of the read message in the group |
| kTIMGroupBaseInfoMsgFlag | UInt | Read-only | Message receiving option |
| kTIMGroupBaseInfoIsShutupAll | Bool | Read-only | Indicates whether the mute all feature is enabled for the group. |
| kTIMGroupBaseInfoSelfInfo | Object [GroupSelfInfo](#groupselfinfo) | Read-only | Self information of the user in the group |

### GroupDetailInfo

Group detail information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupDetialInfoGroupId | String | Read-only | Group ID |
| kTIMGroupDetialInfoGroupType | UInt [TIMGroupType](#timgrouptype) | Read-only | Group type |
| kTIMGroupDetialInfoGroupName | String | Read-only | Group name |
| kTIMGroupDetialInfoNotification | String | Read-only | Group announcement |
| kTIMGroupDetialInfoIntroduction | String | Read-only | Group introduction |
| kTIMGroupDetialInfoFaceUrl | String | Read-only | Group profile photo URL |
| kTIMGroupDetialInfoCreateTime | UInt | Read-only | Group creation time |
| kTIMGroupDetialInfoInfoSeq | UInt | Read-only | Seq of the group profile. The value of this field increases by one each time the group profile is changed. |
| kTIMGroupDetialInfoLastInfoTime | UInt | Read-only | Last modification time of the group information |
| kTIMGroupDetialInfoNextMsgSeq | UInt | Read-only | Seq of the latest message in the group |
| kTIMGroupDetialInfoLastMsgTime | UInt | Read-only | Time of the latest message in the group |
| kTIMGroupDetialInfoMemberNum | UInt | Read-only | Current number of members in the group |
| kTIMGroupDetialInfoMaxMemberNum | UInt | Read-only | Maximum number of members in the group |
| kTIMGroupDetialInfoAddOption | UInt [TIMGroupAddOption](#timgroupaddoption) | Read-only | Group adding option |
| kTIMGroupDetialInfoOnlineMemberNum | UInt | Read-only | Number of online group members |
| kTIMGroupDetialInfoVisible | UInt | Read-only | Indicates whether group members are visible to users outside the group. |
| kTIMGroupDetialInfoSearchable | UInt | Read-only | Indicates whether the group can be searched for. |
| kTIMGroupDetialInfoIsShutupAll | Bool | Read-only | Indicates whether the mute all feature is enabled for the group. |
| kTIMGroupDetialInfoOwnerIdentifier | String | Read-only | ID of the group owner |
| kTIMGroupDetialInfoCustomInfo | Array [GroupInfoCustemString](#groupinfocustemstring) | Read-only | For more information, see [Custom fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### GetGroupInfoResult

Result returned by the API for obtaining the group information list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGetGroupInfoResultCode | Int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Result for obtaining the detailed group information |
| kTIMGetGroupInfoResultDesc | String | Read-only | Description of the failure to obtain the detailed group information |
| kTIMGetGroupInfoResultInfo | Object [GroupDetailInfo](#groupdetailinfo) | Read-only | Detailed group information |

### TIMGroupModifyInfoFlag

Group information setting (modification) type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupModifyInfoFlag_None | 0x00 | - |
| kTIMGroupModifyInfoFlag_Name | 0x01 | Modify the group name. |
| kTIMGroupModifyInfoFlag_Notification | 0x01 << 1 | Modify the group announcement. |
| kTIMGroupModifyInfoFlag_Introduction | 0x01 << 2 | Modify the group introduction. |
| kTIMGroupModifyInfoFlag_FaceUrl | 0x01 << 3 | Modify the group profile photo URL. |
| kTIMGroupModifyInfoFlag_AddOption | 0x01 << 4 | Modify the group addition option. |
| kTIMGroupModifyInfoFlag_MaxMmeberNum | 0x01 << 5 | Modify the maximum number of members in the group. |
| kTIMGroupModifyInfoFlag_Visible | 0x01 << 6 | Modify whether the group is visible. |
| kTIMGroupModifyInfoFlag_Searchable | 0x01 << 7 | Modify whether the group can be searched for. |
| kTIMGroupModifyInfoFlag_ShutupAll | 0x01 << 8 | Modify whether the mute all feature is enabled for the group. |
| kTIMGroupModifyInfoFlag_Custom | 0x01 << 9 | Modify group custom information. |
| kTIMGroupModifyInfoFlag_Owner | 0x01 << 31 | Modify the group owner. |

### GroupModifyInfoParam

Parameters of the API for changing group information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupModifyInfoParamGroupId | String | Write-only (required) | Group ID |
| kTIMGroupModifyInfoParamModifyFlag | UInt [TIMGroupModifyInfoFlag](#timgroupmodifyinfoflag) | Write-only (required) | Modification flag. You can set multiple values, and the bitwise OR result of these values will be used. |
| kTIMGroupModifyInfoParamGroupName | String | Write-only (optional) | Modify the group name. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Name`. |
| kTIMGroupModifyInfoParamNotification | String | Write-only (optional) | Modify the group announcement. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Notification`. |
| kTIMGroupModifyInfoParamIntroduction | String | Write-only (optional) | Modify the group introduction. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Introduction`. |
| kTIMGroupModifyInfoParamFaceUrl | String | Write-only (optional) | Modify the group profile photo URL. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_FaceUrl`. |
| kTIMGroupModifyInfoParamAddOption | UInt | Write-only (optional) | Modify the group adding option. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_AddOption`. |
| kTIMGroupModifyInfoParamMaxMemberNum | UInt | Write-only (optional) | Modify the maximum number of members in the group. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_MaxMmeberNum`. |
| kTIMGroupModifyInfoParamVisible | UInt | Write-only (optional) | Modify whether the group is visible. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Visible`. |
| kTIMGroupModifyInfoParamSearchAble | UInt | Write-only (optional) | Modify whether the group can be searched. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Searchable`. |
| kTIMGroupModifyInfoParamIsShutupAll | Bool | Write-only (optional) | Modify whether the mute all feature is enabled for the group. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_ShutupAll`. |
| kTIMGroupModifyInfoParamOwner | String | Write-only (optional) | Modify the group owner. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Owner`. At this time, `modify_flag` cannot contain other values because changing other information is meaningless when the group owner is changed. |
| kTIMGroupModifyInfoParamCustomInfo | Array [GroupInfoCustemString](#groupinfocustemstring) | Write-only (optional) | For more information, see [Custom fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### GroupGetMemberInfoListParam

Parameters of the API for obtaining the group member list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupGetMemberInfoListParamGroupId | String | Write-only (required) | Group ID |
| kTIMGroupGetMemberInfoListParamIdentifierArray | Array string | Write-only (optional) | List of group member IDs |
| kTIMGroupGetMemberInfoListParamOption | Object [GroupMemberGetInfoOption](#groupmembergetinfooption) | Write-only (optional) | Option for obtaining the group member information |
| kTIMGroupGetMemberInfoListParamNextSeq | UInt64 | Write-only (optional) | Pulling-by-page flag. It is set to 0 when the information is pulled for the first time. If the callback succeeds and the result is not 0, paging is needed. The value of this field is passed in via API calling for the next pulling until the value is 0. |

### GroupGetMemberInfoListResult

Result returned by the API for obtaining the group member list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupGetMemberInfoListResultNexSeq | UInt64 | Read-only | Next pulling flag. If the server returns 0, no more data can be pulled. Otherwise, this flag must be included next time the API is called to obtain the data. |
| kTIMGroupGetMemberInfoListResultInfoArray | Array [GroupMemberInfo](#groupmemberinfo) | Read-only | Member information list |

### TIMGroupMemberModifyInfoFlag

Group member information setting (modification) type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupMemberModifyFlag_None | 0x00 | - |
| kTIMGroupMemberModifyFlag_MsgFlag | 0x01 | Modification of the message receiving option |
| kTIMGroupMemberModifyFlag_MemberRole | 0x01 << 1 | Modification of the member role |
| kTIMGroupMemberModifyFlag_ShutupTime | 0x01 << 2 | Modification of the mute time |
| kTIMGroupMemberModifyFlag_NameCard | 0x01 << 3 | Modification of the group name card |
| kTIMGroupMemberModifyFlag_Custom | 0x01 << 4 | Modification of the group member custom information |

### GroupModifyMemberInfoParam

Parameters of the API for setting the group member information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupModifyMemberInfoParamGroupId | String | Write-only (required) | Group ID |
| kTIMGroupModifyMemberInfoParamIdentifier | String | Write-only (required) | ID of the member whose information is set |
| kTIMGroupModifyMemberInfoParamModifyFlag | UInt [TIMGroupMemberModifyInfoFlag](#timgroupmembermodifyinfoflag) | Write-only (required) | Modification type. You can set multiple values, and the bitwise OR result of these values will be used. |
| kTIMGroupModifyMemberInfoParamMsgFlag | UInt | Write-only (optional) | Modify the message receiving option. This field is required only when `modify_flag` contains `kTIMGroupMemberModifyFlag_MsgFlag`. |
| kTIMGroupModifyMemberInfoParamMemberRole | UInt [TIMGroupMemberRole](#timgroupmemberrole) | Write-only (optional) | Modify the member role. This field is required only when `modify_flag` contains `kTIMGroupMemberModifyFlag_MemberRole`. |
| kTIMGroupModifyMemberInfoParamShutupTime | UInt | Write-only (optional) | Modify the mute time. This field is required only when `modify_flag` contains `kTIMGroupMemberModifyFlag_ShutupTime`. |
| kTIMGroupModifyMemberInfoParamNameCard | UInt | Write-only (optional) | Modify the group name card. This field is required only when `modify_flag` contains `kTIMGroupMemberModifyFlag_NameCard`. |
| kTIMGroupModifyMemberInfoParamCustomInfo | Array [GroupMemberInfoCustemString](#groupmemberinfocustemstring) | Write-only (optional) | For more information, see [Custom fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### GroupPendencyOption

Parameters of the API for obtaining the group pending request list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupPendencyOptionStartTime | UInt64 | Write-only (required) | Pulling timestamp. It is set to 0 for the first request, and later is set based on the timestamp specified by the kTIMGroupPendencyResultNextStartTime key of [GroupPendencyResult](#grouppendencyresult) returned by the server. |
| kTIMGroupPendencyOptionMaxLimited | UInt | Write-only (optional) | Recommended number of pending requests to be pulled. The server can return pending requests as required, but this key cannot be used as a flag that indicates whether pulling of all pending requests was completed. |

### TIMGroupPendencyType

Pending request type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupPendency_RequestJoin | 0 | Request to join the group |
| kTIMGroupPendency_InviteJoin | 1 | Invitation to a user to join the group |
| kTIMGroupPendency_ReqAndInvite | 2 | Invitation and request to join the group |

### TIMGroupPendencyHandle

Group pending request status.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupPendency_NotHandle | 0 | Not handled |
| kTIMGroupPendency_OtherHandle | 1 | Handled by others |
| kTIMGroupPendency_OperatorHandle | 2 | Handled by the operator |

### TIMGroupPendencyHandleResult

Handling operation type of group pending requests.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupPendency_Refuse | 0 | Reject |
| kTIMGroupPendency_Accept | 1 | Accept |

### GroupPendency

Definition of the group pending request.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupPendencyGroupId | String | Read-write | Group ID |
| kTIMGroupPendencyFromIdentifier | String | Read-write | Requester ID, for example, ID of the requester who requests to join the group or ID of the inviter who invites a user to join the group |
| kTIMGroupPendencyToIdentifier | String | Read-write | Decider ID, for example, "" for a request to join the group or ID of the user who is invited to join the group |
| kTIMGroupPendencyAddTime | UInt64 | Read-only | Time that the pending request is added |
| kTIMGroupPendencyPendencyType | UInt [TIMGroupPendencyType](#timgrouppendencytype) | Read-only | Type of the pending request |
| kTIMGroupPendencyHandled | UInt [TIMGroupPendencyHandle](#timgrouppendencyhandle) | Read-only | Group pending request status |
| kTIMGroupPendencyHandleResult | UInt [TIMGroupPendencyHandleResult](#timgrouppendencyhandleresult) | Read-only | Handling operation type of the group pending request |
| kTIMGroupPendencyApplyInviteMsg | String | Read-only | Additional information of the application or invitation |
| kTIMGroupPendencyFromUserDefinedData | String | Read-only | Custom field of the applicant or inviter |
| kTIMGroupPendencyApprovalMsg | String | Read-only | Approval information, which is the acceptance or rejection information |
| kTIMGroupPendencyToUserDefinedData | String | Read-only | Custom field of the approver |
| kTIMGroupPendencyKey | string | Read-only | Signing information, which customers can ignore |
| kTIMGroupPendencyAuthentication | string | Read-only | Signing information, which customers can ignore |
| kTIMGroupPendencySelfIdentifier | string | Read-only | Your own ID |

### GroupPendencyResult

Result returned by the API for obtaining the group pending request list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupPendencyResultNextStartTime | UInt64 | Read-only | Start timestamp for the next pull. If the server returns 0, no more data can be pulled. Otherwise, this timestamp is used as the start timestamp for the next pull. |
| kTIMGroupPendencyResultReadTimeSeq | UInt64 | Read-only | Timestamp of the read pending request |
| kTIMGroupPendencyResultUnReadNum | UInt | Read-only | Number of unread pending requests |
| kTIMGroupPendencyResultPendencyArray | Array [GroupPendency](#grouppendency) | Read-only | List of group pending requests |

### GroupHandlePendencyParam

Parameters of the API for handling group pending requests.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupHandlePendencyParamIsAccept | Bool | Write-only (optional) | true: accept. false: reject. The default value is false. |
| kTIMGroupHandlePendencyParamHandleMsg | String | Write-only (optional) | Acceptance or rejection information, which is a null string by default |
| kTIMGroupHandlePendencyParamPendency | Object [GroupPendency](#grouppendency) | Write-only (required) | Details of the pending request |

## Key Types of Relationship Chains and Profiles

Definitions of macros related to the relationship chains and profiles and JSON keys for related struct member retrieval.

### FriendShipGetProfileListParam

Parameters of the API for handling group pending requests.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendShipGetProfileListParamIdentifierArray | Array string | Write-only | List of UserIDs of target users whose profiles are desired |
| kTIMFriendShipGetProfileListParamForceUpdate | Bool | Write-only | Indicates whether to update the profiles forcibly. false: profiles are preferentially obtained from the local cache, and if such an attempt fails, profiles are pulled from the network. true: profiles are directly pulled from the network. The default value is false. |

### TIMGenderType

User gender.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGenderType_Unkown | 0 | Unknown gender |
| kTIMGenderType_Male | 1 | Male |
| kTIMGenderType_Female | 2 | Female |

### TIMProfileAddPermission

Friend adding option.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMProfileAddPermission_Unknown | 0 | Unknown |
| kTIMProfileAddPermission_AllowAny | 1 | Allows anyone to add friends. |
| kTIMProfileAddPermission_NeedConfirm | 2 | Requires confirmation when friends are added. |
| kTIMProfileAddPermission_DenyAny | 3 | Prohibits anyone from adding friends. |

### UserProfileCustemStringInfo

Custom profile field (string).

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMUserProfileCustemStringInfoKey | String | Write-only | Key value (containing the prefix Tag_Profile_Custom_) of the custom profile field |
| kTIMUserProfileCustemStringInfoValue | String | Write-only | String corresponding to the field |

> The string length cannot exceed 500 bytes.


### UserProfile

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMUserProfileIdentifier | String | Read-only | User ID |
| kTIMUserProfileNickName | String | Read-only | User’s nickname |
| kTIMUserProfileGender | UInt [TIMGenderType](#timgendertype) | Read-only | Gender |
| kTIMUserProfileFaceUrl | String | Read-only | User profile photo URL |
| kTIMUserProfileSelfSignature | String | Read-only | User’s personal signature |
| kTIMUserProfileAddPermission | UInt [TIMProfileAddPermission](#timprofileaddpermission) | Read-only | Friend adding option of the user |
| kTIMUserProfileLocation | String | Read-only | Location information of the user |
| kTIMUserProfileLanguage | UInt | Read-only | Language |
| kTIMUserProfileBirthDay | UInt | Read-only | Birthday |
| kTIMUserProfileLevel | UInt | Read-only | Level |
| kTIMUserProfileRole | UInt | Read-only | Role |
| kTIMUserProfileCustomStringArray | Array [UserProfileCustemStringInfo](#userprofilecustemstringinfo) | Read-only | For more information, see [Custom Profile Fields](https://intl.cloud.tencent.com/document/product/1047/33520#.E8.87.AA.E5.AE.9A.E4.B9.89.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5). |

### UserProfileItem

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMUserProfileItemNickName | String | Write-only | Modify the user’s nickname. |
| kTIMUserProfileGender | UInt [TIMGenderType](#timgendertype) | Write-only | Change the user’s gender. |
| kTIMUserProfileItemFaceUrl | String | Write-only | Modify the user’s profile photo URL. |
| kTIMUserProfileItemSelfSignature | String | Write-only | Change the user’s signature. |
| kTIMUserProfileItemAddPermission | UInt [TIMProfileAddPermission](#timprofileaddpermission) | Write-only | Modify the user’s friend adding option. |
| kTIMUserProfileItemLoaction | UInt | Write-only | Modify the user’s location. |
| kTIMUserProfileItemLanguage | UInt | Write-only | Modify the language. |
| kTIMUserProfileItemBirthDay | UInt | Write-only | Modify the birthday. |
| kTIMUserProfileItemLevel | UInt | Write-only | Modify the level. |
| kTIMUserProfileItemRole | UInt | Write-only | Modify the role. |
| kTIMUserProfileItemCustomStringArray | Array [UserProfileCustemStringInfo](#userprofilecustemstringinfo) | Write-only | Modify [custom profile fields](https://intl.cloud.tencent.com/document/product/1047/33520#.E8.87.AA.E5.AE.9A.E4.B9.89.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5). |

### FriendProfileCustemStringInfo

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendProfileCustemStringInfoKey | String | Write-only | Key of the friend custom profile field |
| kTIMFriendProfileCustemStringInfoValue | String | Write-only | Value of the friend custom profile field |

### FriendProfile

Friend profiles.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendProfileIdentifier | String | Read-only | UserID of the friend |
| kTIMFriendProfileGroupNameArray | Array string | Read-only | List of friend group names |
| kTIMFriendProfileRemark | String | Read-only | Friend remarks, which is 96 bytes at most. This field is null if the API is called to obtain your own profile. |
| kTIMFriendProfileAddWording | String | Read-only | Reason for adding a friend |
| kTIMFriendProfileAddSource | String | Read-only | Source for adding a friend |
| kTIMFriendProfileAddTime | UInt64 | Read-only | Friend adding time |
| kTIMFriendProfileUserProfile | object [UserProfile](#userprofile) | Read-only | Friend’s profile |
| kTIMFriendProfileCustomStringArray | Array [FriendProfileCustemStringInfo](#friendprofilecustemstringinfo) | Read-only | [Custom friend fields](https://intl.cloud.tencent.com/document/product/1047/33521#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.A5.BD.E5.8F.8B.E5.AD.97.E6.AE.B5) |

### FriendProfileItem

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendProfileItemRemark | String | Write-only | Modify the friend remarks. |
| kTIMFriendProfileItemGroupNameArray | Array string | Write-only | Modify the friend group name list. |
| kTIMFriendProfileItemCustomStringArray | Array [FriendProfileCustemStringInfo](#friendprofilecustemstringinfo) | Write-only | Modify [custom friend fields](https://intl.cloud.tencent.com/document/product/1047/33521#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.A5.BD.E5.8F.8B.E5.AD.97.E6.AE.B5). |

### TIMFriendType

| Parameter | Value | Description |
|-----|-----|-----|
| FriendTypeSignle | 0 | One-way friend. User B is in the friend list of user A, but user A is not in the friend list of user B. |
| FriendTypeBoth | 1 | Two-way friend. User B is in the friend list of user A, and user A is also in the friend list of user B. |

### FriendshipAddFriendParam

Parameters of the API for adding friends.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipAddFriendParamIdentifier | String | Write-only | UserID of the friend to be added |
| kTIMFriendshipAddFriendParamFriendType | UInt [TIMFriendType](#timfriendtype) | Write-only | Type of the friend to be added |
| kTIMFriendshipAddFriendParamRemark | String | Write-only | Remarks for the friend to be added |
| kTIMFriendshipAddFriendParamGroupName | String | Write-only | Group name |
| kTIMFriendshipAddFriendParamAddSource | String | Write-only | Description of the source from which the friend is added |
| kTIMFriendshipAddFriendParamAddWording | String | Write-only | Postscript for adding a friend |

### FriendResult

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendResultIdentifier | String | Read-only | ID of the user who performs the relationship chain operation |
| kTIMFriendResultCode | Int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Result of the relationship chain operation |
| kTIMFriendResultDesc | String | Read-only | Detailed description about the relationship chain operation failure |

### FriendshipModifyFriendProfileParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipModifyFriendProfileParamIdentifier | String | Write-only | UserID of the friend whose profile is modified |
| kTIMFriendshipModifyFriendProfileParamItem | Object [FriendProfileItem](#friendprofileitem) | Write-only | Each item of the modified friend profile |

### FriendAddPendency

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendAddPendencyIdentifier | String | Read-only | UserID of the requester who requests to add a friend |
| kTIMFriendAddPendencyNickName | String | Read-only | Nickname of the requester who requests to add a friend |
| kTIMFriendAddPendencyAddSource | String | Read-only | Source of the requester who requests to add a friend |
| kTIMFriendAddPendencyAddWording | String | Read-only | Postscript of the requester who requests to add a friend |

### TIMFriendPendencyType

| Parameter | Value | Description |
|-----|-----|-----|
| FriendPendencyTypeComeIn | 0 | Incoming |
| FriendPendencyTypeSendOut | 1 | Outgoing |
| FriendPendencyTypeBoth | 2 | Two-way |

### FriendshipGetPendencyListParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipGetPendencyListParamType | UInt [TIMFriendPendencyType](#timfriendpendencytype) | Write-only | Type of the pending friend request |
| kTIMFriendshipGetPendencyListParamStartSeq | UInt64 | Write-only | Seq of the pending request, starting from which the pending request list is obtained. It is recommended that the client save `seq` and the pending request list. When the pending request list needs to be obtained, this field is set to the seq returned by `server`. If `seq` is the latest one on the `server`, no data is returned. |
| kTIMFriendshipGetPendencyListParamStartTime | UInt64 | Write-only | Timestamp, starting from which the pending request information is obtained |
| kTIMFriendshipGetPendencyListParamLimitedSize | Int | Write-only | Size of each page of the obtained pending request list |

### PendencyPage

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMPendencyPageStartTime | UInt64 | Read-only | Start time of the pending request information page |
| kTIMPendencyPageUnReadNum | UInt64 | Read-only | Unread count on the pending request information page |
| kTIMPendencyPageCurrentSeq | UInt64 | Read-only | Current Seq of the pending request information page |
| kTIMPendencyPagePendencyInfoArray | Array [FriendAddPendencyInfo](#friendaddpendencyinfo) | Read-only | Pending request list on the pending request information page |

### FriendAddPendencyInfo

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendAddPendencyInfoType | UInt [TIMFriendPendencyType](#timfriendpendencytype) | Read-only | Type of the pending friend adding request |
| kTIMFriendAddPendencyInfoIdentifier | String | Read-only | UserID in the pending friend adding request |
| kTIMFriendAddPendencyInfoNickName | String | Read-only | Nickname in the pending friend adding request |
| kTIMFriendAddPendencyInfoAddTime | UInt64 | Read-only | Adding time in the pending add friend request |
| kTIMFriendAddPendencyInfoAddSource | String | Read-only | Source in the pending friend adding request |
| kTIMFriendAddPendencyInfoAddWording | String | Read-only | Postscript in the pending friend adding request |

### FriendshipDeletePendencyParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipDeletePendencyParamType | UInt [TIMFriendPendencyType](#timfriendpendencytype) | Read-only | Type of the pending friend deletion request |
| kTIMFriendshipDeletePendencyParamIdentifierArray | Array string | Read-only | UserID list in the pending friend deletion request |

### TIMFriendResponseAction

| Parameter | Value | Description |
|-----|-----|-----|
| ResponseActionAgree | 0 | Agree |
| ResponseActionAgreeAndAdd | 1 | Agree and add |
| ResponseActionReject | 2 | Reject |

### FriendRespone

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendResponeIdentifier | String | Write-only (required) | UserID in the friend adding response |
| kTIMFriendResponeAction | UInt [TIMFriendResponseAction](#timfriendresponseaction) | Write-only (required) | Action in the friend adding response |
| kTIMFriendResponeRemark | String | Write-only (optional) | Friend remark |
| kTIMFriendResponeGroupName | String | Write-only (optional) | Friend group list |

### FriendshipDeleteFriendParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipDeleteFriendParamFriendType | UInt [TIMFriendType](#timfriendtype) | Write-only | Type of the friend to be deleted |
| kTIMFriendshipDeleteFriendParamIdentifierArray | Array string | Write-only (optional) | List of UserIDs of friends to be deleted |

### FriendGroupInfo

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipCreateFriendGroupParamNameArray | Array string | Write-only | Name list of the created friend list |
| kTIMFriendshipCreateFriendGroupParamIdentifierArray | Array string | Write-only | List of UserIDs of friends to be put into the created friend list |

### FriendGroupInfo

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendGroupInfoName | String | Read-only | Group name |
| kTIMFriendGroupInfoCount | UInt64 | Read-only | Number of friends in the current group |
| kTIMFriendGroupInfoIdentifierArray | Array string | Read-only | List of UserIDs of friends in the current group |

### FriendshipModifyFriendGroupParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipModifyFriendGroupParamName | String | Write-only | Group name to be modified |
| kTIMFriendshipModifyFriendGroupParamNewName | String | Write-only (optional) | New group name |
| kTIMFriendshipModifyFriendGroupParamDeleteIdentifierArray | Array string | Write-only (optional) | List of UserIDs of friends to be deleted from the current group |
| kTIMFriendshipModifyFriendGroupParamAddIdentifierArray | Array string | Write-only (optional) | List of UserIDs of friends to be added to the current friend list |

### FriendshipCheckFriendTypeParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipCheckFriendTypeParamCheckType | UInt [TIMFriendType](#timfriendtype) | Write-only | Friend type to be checked |
| kTIMFriendshipCheckFriendTypeParamIdentifierArray | Array string | Write-only | List of UserIDs of friends to be checked |

### TIMFriendCheckRelation

| Parameter | Value | Description |
|-----|-----|-----|
| FriendCheckNoRelation | 0 | There is no relationship between two users. |
| FriendCheckAWithB | 1 | User B is in the friend list of user A, but user A is not in the friend list of user B. |
| FriendCheckBWithA | 2 | User A is in the friend list of user B, but user B is not in the friend list of user A. |
| FriendCheckBothWay | 3 | Two-way friendship |

### FriendshipCheckFriendTypeResult

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipCheckFriendTypeResultIdentifier | String | Read-only | UserID of the friend to be checked |
| kTIMFriendshipCheckFriendTypeResultRelation | UInt [TIMFriendCheckRelation](#timfriendcheckrelation) | Read-only | If the check succeeds, the relationship between two users is returned. |
| kTIMFriendshipCheckFriendTypeResultCode | Int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Check result |
| kTIMFriendshipCheckFriendTypeResultDesc | String | Read-only | Description about the friendship check failure |

