## Common Macros and Basic Configuration Options


### TIMResult

Value returned after an API is called.

| Parameter | Value | Description |
|-----|-----|-----|
| TIM_SUCC | 0 | Indicates that the API was called successfully. |
| TIM_ERR_SDKUNINIT | -1 | Indicates that the API failed to be called because the IM SDK was not initialized yet. |
| TIM_ERR_NOTLOGIN | -2 | Indicates that the API failed to be called because the user has not logged in yet. |
| TIM_ERR_JSON | -3 | Indicates that the API failed to be called because the JSON format or JSON key is incorrect. |
| TIM_ERR_PARAM | -4 | Indicates that the API failed to be called because parameters are incorrect. |
| TIM_ERR_CONV | -5 | Indicates that the API failed to be called because the conversation is invalid. |
| TIM_ERR_GROUP | -6 | Indicates that the API failed to be called because the group is invalid. |

> If the API parameters contain the callback, the callback is called only when the API returns TIM_SUCC.


### TIMLogLevel

Log level

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMLog_Off | 0 | Log output is disabled. |
| kTIMLog_Verbose | 1 | Detailed logs during development and commissioning |
| kTIMLog_Debug | 2 | Debugging log |
| kTIMLog_Info | 3 | Information log |
| kTIMLog_Warn | 4 | Warning log |
| kTIMLog_Error | 5 | Error log |
| kTIMLog_Assert | 6 | Assertion log |

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

Conversation type

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
| kTIMSdkConfigJavaVM | uint64 | Write-only (optional) | Configures the Android platform Java VM pointer. |

### TIMGroupMemberInfoFlag

Group member information flag.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupMemberInfoFlag_None | 0x00 | None |
| kTIMGroupMemberInfoFlag_JoinTime | 0x01 | Join time |
| kTIMGroupMemberInfoFlag_MsgFlag | 0x01 << 1 | Group message receiving option |
| kTIMGroupMemberInfoFlag_MsgSeq | 0x01 << 2 | Sequence number of the message that has been read by the member |
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
| kTIMGroupMemberGetInfoOptionInfoFlag | Uint64 [TIMGroupMemberInfoFlag](#timgroupmemberinfoflag) | Read/Write (optional) | Filters by desired information. The default value is 0xffffffff, indicating that all information is obtained. |
| kTIMGroupMemberGetInfoOptionRoleFlag | Uint64 [TIMGroupMemberRoleFlag](#timgroupmemberroleflag) | Read/Write (optional) | Filters by member role. The default value is kTIMGroupMemberRoleFlag_All, indicating that all roles are obtained. |
| kTIMGroupMemberGetInfoOptionCustomArray | Array string | Write-only (optional) | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5) |

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
| kTIMGroupGetInfoOptionInfoFlag | Uint64 [TIMGroupGetInfoFlag](#timgroupgetinfoflag) | Read/Write (optional) | Filters by desired information. The default value is 0xffffffff, indicating that all information is obtained. |
| kTIMGroupGetInfoOptionCustomArray | Array string | Write-only (optional) | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5) |

### UserConfig

User configuration.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMUserConfigIsReadReceipt | Bool | Write-only (optional) | true: the read receipt event is received. |
| kTIMUserConfigIsSyncReport | Bool | Write-only (optional) | true: the server deletes messages in the read state. |
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

- Custom data.
The IM SDK only transparently transfers the data customized by developers to the IM backend. The maximum length is 64 bytes. The developer business backend can be notified of the custom data through the third-party callback [status change callback](https://intl.cloud.tencent.com/zh/document/product/1047/34357).
- HTTP proxy.
The HTTP proxy uploads the related files to the COS when sending image, voice, file, and micro video messages, and downloads the related files to the local server when receiving image, voice, file, and micro video messages. To enable the HTTP proxy, you cannot set the IP address of the proxy to null or the port to 0 (port 0 cannot be used). To disable the HTTP proxy, you only need to set the IP address of the proxy to a null string and the port to 0.
- SOCKS5 proxy.
The SOCKS5 proxy must be enabled before initialization. After the SOCKS5 proxy is enabled, all protocols sent by the IM SDK are sent to the IM backend through the SOCKS5 proxy server.


| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMSetConfigLogLevel | Uint [TIMLogLevel](#timloglevel) | Write-only (optional) | Level of logs output to the log file |
| kTIMSetConfigCackBackLogLevel | Uint [TIMLogLevel](#timloglevel) | Write-only (optional) | Log level for the log callback |
| kTIMSetConfigIsLogOutputConsole | Bool | Write-only (optional) | Indicates whether to output logs to the console. |
| kTIMSetConfigUserConfig | Object [UserConfig](#userconfig) | Write-only (optional) | User configuration |
| kTIMSetConfigUserDefineData | String | Write-only (optional) | User-defined data, which must be set before initialization if such data is needed. |
| kTIMSetConfigHttpProxyInfo | Object [HttpProxyInfo](#httpproxyinfo) | Write-only (optional) | Sets the HTTP proxy. The HTTP proxy (if needed) must be enabled before image, file, voice, and video messages are sent. |
| kTIMSetConfigSocks5ProxyInfo | Object [Socks5ProxyInfo](#socks5proxyinfo) | Write-only (optional) | Sets the SOCKS5 proxy. The SOCKS5 proxy (if needed) must be enabled before initialization. |

## Message Key Types

Definitions of message-related macros and JSON keys for related struct member retrieval.

### IOSOfflinePushConfig

Offline push configuration for messages on iOS.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMIOSOfflinePushConfigTitle | string | Read/Write | Notification title |
| kTIMIOSOfflinePushConfigSound | string | Read/Write | Offline push alert sound URL of the current message on iOS devices. push.no_sound: no alert sound and no vibration. |
| kTIMIOSOfflinePushConfigIgnoreBadge | bool | Read/Write | Indicates whether to ignore badge count. true: on the iOS receiver, the message will not increase the unread message count on the app icon. |

### TIMAndroidOfflinePushNotifyMode

Android offline push mode.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMAndroidOfflinePushNotifyMode_Normal | 0 | Normal notification bar message mode. After an offline message is delivered, clicking the notification bar message will directly launch the app, without triggering callback for the app. |
| kTIMAndroidOfflinePushNotifyMode_Custom | 1 | Custom message mode. After an offline message is delivered, clicking the notification bar message will trigger callback for the app. |

### AndroidOfflinePushConfig

Offline push configuration for messages on Android.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMAndroidOfflinePushConfigTitle | string | Read/Write | Notification title |
| kTIMAndroidOfflinePushConfigSound | string | Read/Write | Offline push alert sound URL of the current message on Android devices |
| kTIMAndroidOfflinePushConfigNotifyMode | uint [TIMAndroidOfflinePushNotifyMode](#timandroidofflinepushnotifymode) | Read/Write | Notification mode of the current message |
| kTIMAndroidOfflinePushConfigOPPOChannelID | string | Read/Write | OPPO ChannelID |

>ChannelID notes
In Android 8.0 and later versions, channelid is added to notification bar messages. OPPO requires that it should be specified. If it is not specified, OPPO mobile phones with Android 8.0 or later will fail to receive offline push messages. In the future, xiaomi_channel_id_, huawei_channel_id, and other such parameters may also be added.


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
| kTIMOfflinePushConfigDesc | string | Read/Write | Content displayed by the current message when the recipient receives offline push |
| kTIMOfflinePushConfigExt | string | Read/Write | Extension fields for offline push of the current message |
| kTIMOfflinePushConfigFlag | uint [TIMOfflinePushFlag](#timofflinepushflag) | Read/Write | Indicates whether the current message allows push. By default, push is allowed: kTIMOfflinePushFlag_Default. |
| kTIMOfflinePushConfigIOSConfig | object [IOSOfflinePushConfig](#iosofflinepushconfig) | Read/Write | iOS offline push configuration |
| kTIMOfflinePushConfigAndroidConfig | object [AndroidOfflinePushConfig](#androidofflinepushconfig) | Read/Write | Android offline push configuration |

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

Message priority. A larger number indicates a higher priority.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMMsgPriority_High | 0 | The priority is the highest. Generally, the priority of a red packet or gift message is the highest. |
| kTIMMsgPriority_Normal | 1 | This is the normal priority and the second highest. We recommend that the priority of common messages be set to Normal. |
| kTIMMsgPriority_Low | 2 | We recommend that the priority of like messages be set to Low. |
| kTIMMsgPriority_Lowest | 3 | The lowest priority. Generally, this is the priority for notifications of joining or quitting a group (sent by the backend). |

### Message

Message JSON keys.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgElemArray | Array [Elem](#elem) | Read/Write (required) | Message element list |
| kTIMMsgConvId | String | Read/Write (optional) | Conversation ID of the message |
| kTIMMsgConvType | Uint [TIMConvType](#timconvtype) | Read/Write (optional) | Conversation type of the message |
| kTIMMsgSender | String | Read/Write (optional) | Message sender |
| kTIMMsgPriority | Uint [TIMMsgPriority](#timmsgpriority) | Read/Write (optional) | Message priority |
| kTIMMsgClientTime | Uint64 | Read/Write (optional) | Client time |
| kTIMMsgServerTime | Uint64 | Read/Write (optional) | Server time |
| kTIMMsgIsFormSelf | Bool | Read/Write (optional) | Indicates whether the message comes from yourself. |
| kTIMMsgIsRead | Bool | Read/Write (optional) | Indicates whether the message has been read. |
| kTIMMsgIsOnlineMsg | Bool | Read/Write (optional) | Indicates whether the message is an online message. false: a common message. true: a message that will be deleted immediately after being read. The default value is false. |
| kTIMMsgIsPeerRead | Bool | Read-only | Indicates whether the message has been read by the peer party of the conversation. |
| kTIMMsgStatus | Uint [TIMMsgStatus](#timmsgstatus) | Read/Write (optional) | Current message status |
| kTIMMsgUniqueId | Uint64 | Read-only | Unique ID of the message |
| kTIMMsgRand | Uint64 | Read-only | Random code of the message |
| kTIMMsgSeq | Uint64 | Read-only | Message sequence number |
| kTIMMsgCustomInt | Uint32_t | Read/Write (optional) | Custom integer value field |
| kTIMMsgCustomStr | String | Read/Write (optional) | Custom data field |
| kTIMMsgSenderProfile | object [UserProfile](#userprofile) | Read/Write (optional) | User profile of the message sender |
| kTIMMsgSenderGroupMemberInfo | object [GroupMemberInfo](#groupmemberinfo) | Read/Write (optional) | Group member information of the message sender, which is valid only in group conversations. Currently, only kTIMGroupMemberInfoIdentifier and kTIMGroupMemberInfoNameCard can be obtained. To obtain other fields, we recommend using the API `TIMGroupGetMemberInfoList`. |
| kTIMMsgOfflinePushConfig | object [OfflinePushConfig](#offlinepushconfig) | Read/Write (optional) | Offline push settings of the message |

>
- Corresponding element sequence.
Currently, the file and sound elements are not necessarily transferred in the sequence that they are added. Other elements are transferred in the sequence that they are added. However, we recommend that you should not rely heavily on the element sequence when processing elements. Instead, you should process elements by type to prevent process crashes when exceptions occur.
- Red packet and like messages in the group.
The like and red packet features are supported in the live broadcast scenario. The priority of a like message is lower than that of a red packet message. You can define the specific message content by using the custom message [CustomElem](#customelem). When sending a message, you can use `kTIMMsgPriority` to define the message priority.
- Messages that will be deleted immediately after being read.
When `kTIMMsgIsOnlineMsg` is set to true, a message that will be deleted immediately after being read is sent. This message has the following features:
 - C2C conversation: when this message is sent, the peer party can receive the message only when he/she is online. If the peer party is offline when the message is sent, he/she can no longer receive this message even if he/she logs on to IM later.
 - Group conversation: when this message is sent, only online members in the group can receive the message. If a member is offline when the message is sent, he/she can no longer receive this message even if he/she logs on to IM later.
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
| kTIMMsgReceiptConvType | Uint [TIMConvType](#timconvtype) | Read-only | Conversation type |
| kTIMMsgReceiptTimeStamp | Uint64 | Read-only | Timestamp |

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
| kTIMElem_Invalid       | -1    | Unknown element          |

### Elem

Element type.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMElemType | Uint [TIMElemType](#timelemtype) | Read/Write (required) | Element type |

### TextElem

Text element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMTextElemContent | String | Read/Write (required) | Text content |

### FaceElem

Emoji element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFaceElemIndex | Int | Read/Write (required) | Emoji index |
| kTIMFaceElemBuf | String | Read/Write (optional) | Other extra data, which can be customized by the user. If the binary data needs to be transferred, convert it to strings because JSON only supports the transfer of strings. |

> The IM SDK does not provide any emoji packages. If developers have an emoji package, they can use `kTIMFaceElemIndex` to store the index of an emoji in the emoji package. The emoji index is customized by the user. Alternatively, you can directly use `kTIMFaceElemBuf` to store the binary data of the emoji, which must be converted into a string because JSON does not support the transfer of binary data. The binary data of the emoji is customized by the user, and the IM SDK only passes through the binary data.


### LocationElem

Location element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMLocationElemDesc | String | Read/Write (optional) | Location description |
| kTIMLocationElemLongitude | double | Read/Write (required) | Longitude |
| kTIMLocationElemlatitude | double | Read/Write (required) | Latitude |

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
| kTIMImageElemOrigPath | String | Read/Write (required) | Path of the image to be sent |
| kTIMImageElemLevel | Uint [TIMImageLevel](#timimagelevel) | Read/Write (required) | Quality level of the image to be sent |
| kTIMImageElemFormat | Int | Read/Write (required) | Format of the image to be sent |
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
 - Original refers to the original image sent by the user, and its size remains unchanged.
 - Large refers to the image obtained after the original image is proportionally compressed. After compression, the height or width (whichever is smaller) is set to 720 pixels.
 - Thumb refers to the image obtained after the original image is proportionally compressed. After compression, the height or width (whichever is smaller) is set to 198 pixels.
- If the size of the original image is smaller than 198 pixels, the original size is retained for the three specifications, and no compression is needed.
- If the size of the original image falls between 198 and 720 pixels, the large image is the same as the original image, and no compression is needed.
- When an image is displayed on a mobile phone, we recommend that the thumbnail be displayed first. When the user taps the thumbnail, the large image is downloaded. When the user taps the large image, the original image is downloaded. Alternatively, developers can choose to skip the large image so that the original image is directly downloaded when the user taps the thumbnail.
- When an image is displayed on a tablet or PC, due to the high resolution and availability of a Wi-Fi or wired network, we recommend that the large image be displayed directly, and the original image be downloaded when the user taps or clicks the large image.


### SoundElem

Sound element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMSoundElemFilePath | String | Read/Write (required) | Path of the voice file. The developer must first store the voice file and then specify the path. |
| kTIMSoundElemFileSize | Int | Read/Write (required) | Size (in seconds) of the sound element voice file |
| kTIMSoundElemFileTime | Int | Read/Write (required) | Duration of the voice file |
| kTIMSoundElemFileId | String | Read-only | ID of the voice file when the file is downloaded |
| kTIMSoundElemBusinessId | Int | Read-only | BusinessID used upon download |
| kTIMSoundElemDownloadFlag | Int | Read-only | Indicates whether it is necessary to apply for a download address. 0: yes. 1: apply from the COS. 2: directly use the URL for download. |
| kTIMSoundElemUrl | String | Read-only | Download URL |
| kTIMSoundElemTaskId | Int | Read-only | Task ID |

>
- A message custom field can be used to indicate whether a voice message file has been played. For example, the value 0 can be defined to indicate that the voice message file has not been played yet, and the value 1 can be defined to indicate that the voice message file has been played. When the user taps Play, the value of the field can change to 1.
- Only one sound element can be added to one message. If multiple sound elements are added to a message, the message may fail to be sent.


### CustomElem

Custom element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMCustomElemData | String | Read/Write | Data of the custom element, which can be the binary data |
| kTIMCustomElemDesc | String | Read/Write | Description of the custom element |
| kTIMCustomElemExt | String | Read/Write | Ext field pushed by the backend |
| kTIMCustomElemSound | String | Read/Write | Custom element sound |

> When the built-in message types cannot meet special requirements, developers can customize message formats. The content of each custom message is completely defined by developers, and the IM SDK only passes through the content.


### FileElem

File element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFileElemFilePath | String | Read/Write (required) | File path (including the file name) |
| kTIMFileElemFileName | String | Read/Write (required) | Displayed file name. If this parameter is not specified, kTIMFileElemFileName takes the file name in the file path specified by kTIMFileElemFilePath by default. |
| kTIMFileElemFileSize | Int | Read/Write (required) | File size |
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
| kTIMVideoElemVideoType | String | Read/Write (required) | Type of the video file, which is set when a message is sent |
| kTIMVideoElemVideoSize | Uint | Read/Write (required) | Size of the video file |
| kTIMVideoElemVideoDuration | Uint | Read/Write (required) | Duration of the video file, which is set when a message is sent |
| kTIMVideoElemVideoPath | String | Read/Write (required) | Path of the video file |
| kTIMVideoElemVideoId | String | Read-only | UUID when the video file is downloaded |
| kTIMVideoElemBusinessId | Int | Read-only | BusinessID used upon download |
| kTIMVideoElemVideoDownloadFlag | Int | Read-only | Video file download flag |
| kTIMVideoElemVideoUrl | String | Read-only | URL used to download the video file |
| kTIMVideoElemImageType | String | Read/Write (required) | Type of the screenshot file, which is set when a message is sent |
| kTIMVideoElemImageSize | Uint | Read/Write (required) | Size of the screenshot file |
| kTIMVideoElemImageWidth | Uint | Read/Write (required) | Width of the screenshot, which is set when a message is sent |
| kTIMVideoElemImageHeight | Uint | Read/Write (required) | Height of the screenshot, which is set when a message is sent |
| kTIMVideoElemImagePath | String | Read/Write (required) | Path for saving the screenshot |
| kTIMVideoElemImageId | String | Read-only | ID used when the video screenshot is downloaded |
| kTIMVideoElemImageDownloadFlag | Int | Read-only | Screenshot file download flag |
| kTIMVideoElemImageUrl | String | Read-only | URL used to download the screenshot file |
| kTIMVideoElemTaskId | Uint | Read-only | Task ID |

### TIMGroupTipGroupChangeFlag

Group information change type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupTipChangeFlag_Name | 0xa | Change to the group name |
| kTIMGroupTipChangeFlag_Introduction | 11 | Change to the group introduction |
| kTIMGroupTipChangeFlag_Notification | 12 | Change to the group notification |
| kTIMGroupTipChangeFlag_FaceUrl | 13 | Change to the group profile photo URL |
| kTIMGroupTipChangeFlag_Owner | 14 | Change to the group owner |

### GroupTipGroupChangeInfo

Group system message - change to the group information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupTipGroupChangeInfoFlag | Uint [TIMGroupTipGroupChangeFlag](#timgrouptipgroupchangeflag) | Read-only | Group information change flag for the group message |
| kTIMGroupTipGroupChangeInfoValue | String | Read-only | Value after the change. Different `info_flag` fields have different meanings. |

### GroupTipMemberChangeInfo

Group system message - muting group members.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupTipMemberChangeInfoIdentifier | String | Read-only | Group member ID |
| kTIMGroupTipMemberChangeInfoShutupTime | Uint | Read-only | Mute time |

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
| kTIMGroupTipsElemTipType | Uint [TIMGroupTipType](#timgrouptiptype) | Read-only | Group message type |
| kTIMGroupTipsElemOpUser | String | Read-only | Operator ID |
| kTIMGroupTipsElemGroupName | String | Read-only | Group name |
| kTIMGroupTipsElemGroupId | String | Read-only | Group ID |
| kTIMGroupTipsElemTime | Uint | Read-only | Group message time |
| kTIMGroupTipsElemUserArray | Array string | Read-only | List of operated on accounts |
| kTIMGroupTipsElemGroupChangeInfoArray | Array [GroupTipGroupChangeInfo](#grouptipgroupchangeinfo) | Read-only | Group profile change information list, which is valid only when `tips_type` is set to `kTIMGroupTip_GroupInfoChange` |
| kTIMGroupTipsElemMemberChangeInfoArray | Array [GroupTipMemberChangeInfo](#grouptipmemberchangeinfo) | Read-only | Group member change information list, which is valid only when `tips_type` is set to `kTIMGroupTip_MemberInfoChange` |
| kTIMGroupTipsElemOpUserInfo | Object [UserProfile](#userprofile) | Read-only | Personal profile of the operator |
| kTIMGroupTipsElemOpGroupMemberInfo | Object [GroupMemberInfo](#groupmemberinfo) | Read-only | Group member information |
| kTIMGroupTipsElemChangedUserInfoArray | Array [UserProfile](#userprofile) | Read-only | Changed user information list |
| kTIMGroupTipsElemChangedGroupMemberInfoArray | Array [GroupMemberInfo](#groupmemberinfo) | Read-only | Group member information list |
| kTIMGroupTipsElemMemberNum | Uint | Read-only | Current number of group members, which is valid only when `tips_type` is set to `kTIMGroupTip_Invite`, `kTIMGroupTip_Quit`, or `kTIMGroupTip_Kick` |
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
| kTIMGroupReport_UserDefine | 16 | User-defined notification. This notification can only be received by all members of the group by default. |

### GroupReportElem

Group system notification element (applicable to individuals).

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupReportElemReportType | Uint [TIMGroupReportType](#timgroupreporttype) | Read-only | Type |
| kTIMGroupReportElemGroupId | String | Read-only | Group ID |
| kTIMGroupReportElemGroupName | String | Read-only | Group name |
| kTIMGroupReportElemOpUser | String | Read-only | Operator ID |
| kTIMGroupReportElemMsg | String | Read-only | Cause of the operation |
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
| kTIMProfileChangeElemChangeType | Uint [TIMProfileChangeType](#timprofilechangetype) | Read-only | Profile change type |
| kTIMProfileChangeElemFromIndentifier | String | Read-only | UserID of the user whose profile is changed |
| kTIMProfileChangeElemUserProfileItem | Object [UserProfileItem](#userprofileitem) | Read-only | Specific change information, which is valid only when `change_type` is `kTIMProfileChange_Profile` |

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
| kTIMFriendChange_FriendGroupModify | 11 | Modified a group |

### FriendProfileUpdate

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendProfileUpdateIdentifier | String | Write-only | UserID of a friend whose profile is updated |
| kTIMFriendProfileUpdateItem | Object [FriendProfileItem](#friendprofileitem) | Write-only | Profile update item |

### FriendChangeElem

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendChangeElemChangeType | Uint [TIMFriendChangeType](#timfriendchangetype) | Read-only | Profile change type |
| kTIMFriendChangeElemFriendAddIdentifierArray | Array string | Read-only | List of added friend UserIDs, which is valid only when `change_type` is `kTIMFriendChange_FriendAdd` |
| kTIMFriendChangeElemFriendDelIdentifierArray | Array string | Read-only | List of deleted friend UserIDs, which is valid only when `change_type` is `kTIMFriendChange_FriendDel` |
| kTIMFriendChangeElemFriendAddPendencyItemArray | Array [FriendAddPendency](#friendaddpendency) | Read-only | List of pending friend requests, which is valid only when `change_type` is `kTIMFriendChange_PendencyAdd` |
| kTIMFriendChangeElemPendencyDelIdentifierArray | Array string | Read-only | List of deleted pending friend requests, which is valid only when `change_type` is `kTIMFriendChange_PendencyDel` |
| kTIMFriendChangeElemPendencyReadedReportTimestamp | Uint64 | Read-only | Timestamp for reporting the pending requests, which is valid only when `change_type` is `kTIMFriendChange_PendencyReadedReport` |
| kTIMFriendChangeElemBlackListAddIdentifierArray | Array string | Read-only | List of UserIDs added to the blacklist, which is valid only when `change_type` is `kTIMFriendChange_BlackListAdd` |
| kTIMFriendChangeElemBlackListDelIdentifierArray | Array string | Read-only | List of UserIDs deleted from the blacklist, which is valid only when `change_type` is `kTIMFriendChange_BlackListDel` |
| kTIMFriendChangeElemFreindProfileUpdateItemArray | Array [FriendProfileUpdate](#friendprofileupdate) | Read-only | Friend profile update list, which is valid only when `change_type` is `kTIMFriendChange_FriendProfileUpdate` |
| kTIMFriendChangeElemFriendGroupAddIdentifierArray | Array string | Read-only | List of added friend groups, which is valid only when `change_type` is `kTIMFriendChange_FriendGroupAdd` |
| kTIMFriendChangeElemFriendGroupDelIdentifierArray | Array string | Read-only | List of deleted friend groups, which is valid only when `change_type` is `kTIMFriendChange_FriendGroupDel` |
| kTIMFriendChangeElemFriendGroupModifyIdentifierArray | Array string | Read-only | List of modified friend groups, which is valid only when `change_type` is `kTIMFriendChange_FriendGroupModify` |

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
| kTIMMsgBatchSendResultCode | int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Result of batch message sending |
| kTIMMsgBatchSendResultDesc | String | Read-only | Description of message sending |
| kTIMMsgBatchSendResultMsg | Object [Message](#message) | Read-only | Sent messages |

### MsgLocator

Message locator.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgLocatorConvId | bool | Read/write | Conversation ID of the message to be searched for |
| kTIMMsgLocatorConvType | bool | Read/write | Conversation type of the message to be searched for |
| kTIMMsgLocatorIsRevoked | bool | Read/write (required) | Indicates whether the message to be searched for has been recalled. true: recalled. false: not recalled. The default value is false. |
| kTIMMsgLocatorTime | Uint64 | Read/Write (required) | Timestamp of the message to be searched for |
| kTIMMsgLocatorSeq | Uint64 | Read/Write (required) | Sequence number of the message to be searched for |
| kTIMMsgLocatorIsSelf | Bool | Read/Write (required) | Indicates whether the sender of the message to be searched for is yourself. true: yes. false: no. The default value is false. |
| kTIMMsgLocatorRand | Uint64 | Read/Write (required) | Random code of the message to be searched for |
| kTIMMsgLocatorUniqueId | Uint64 | Read/Write (required) | Unique ID of the message to be searched for |

### MsgGetMsgListParam

Parameters of the API for obtaining messages.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgGetMsgListParamLastMsg | Object [Message](#message) | Write-only (optional) | Specified message, which cannot be null |
| kTIMMsgGetMsgListParamCount | Uint | Write-only (optional) | Number of messages counted starting from the specified message |
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
| kTIMMsgDownloadElemParamFlag | Uint | Write-only | Element download type, which is extracted from the message element |
| kTIMMsgDownloadElemParamType | Uint [TIMDownloadType](#timdownloadtype) | Write-only | Element type, which is extracted from the message element |
| kTIMMsgDownloadElemParamId | String | Write-only | Element ID, which is extracted from the message element |
| kTIMMsgDownloadElemParamBusinessId | Uint | Write-only | Element BusinessID, which is extracted from the message element |
| kTIMMsgDownloadElemParamUrl | String | Write-only | Element URL, which is extracted from the message element |

### MsgDownloadElemResult

Result returned by the API for downloading elements.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgDownloadElemResultCurrentSize | Uint | Read-only | Size of currently downloaded data |
| kTIMMsgDownloadElemResultTotalSize | Uint | Read-only | Total size of the file to be downloaded |

## Conversation Key Types

Definitions of conversation-related macros and JSON keys for related struct member retrieval.

### Draft

Draft information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMDraftMsg | Object [Message](#message) | Read-only | Message in drafts |
| kTIMDraftUserDefine | String | Read-only | User-defined data |
| kTIMDraftEditTime | Uint | Read-only | Last edit time of the draft |

### ConvInfo

Conversation information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMConvId | String | Read-only | Conversation ID |
| kTIMConvType | Uint [TIMConvType](#timconvtype) | Read-only | Conversation type |
| kTIMConvOwner | String | Read-only | Conversation owner |
| kTIMConvUnReadNum | Uint64 | Read-only | Unread conversation count |
| kTIMConvActiveTime | Uint64 | Read-only | Conversation activation time |
| kTIMConvIsHasLastMsg | Bool | Read-only | Indicates whether the conversation has the last message |
| kTIMConvLastMsg | Object [Message](#message) | Read-only | Last message of the conversation |
| kTIMConvIsHasDraft | Bool | Read-only | Indicates whether the conversation has a draft |
| kTIMConvDraft | Object [Draft](#draft) | Read-only (optional) | Conversation draft |

## Group Key Types

Definitions of group-related macros and JSON keys for related struct member retrieval.

### TIMGroupAddOption

Group adding option.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupAddOpt_Forbid | 0 | Prohibit adding to groups |
| kTIMGroupAddOpt_Auth | 1 | Require the approval of the admin |
| kTIMGroupAddOpt_Any | 2 | Anyone can add to the group |

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
| kTIMGroupMemberInfoIdentifier | string | Read/write (required) | ID of the group member |
| kTIMGroupMemberInfoJoinTime | uint | Read-only | Join time of the group member |
| kTIMGroupMemberInfoMemberRole | uint [TIMGroupMemberRole](#timgroupmemberrole) | Read/write (optional) | Role of the group member |
| kTIMGroupMemberInfoMsgFlag | uint | Read-only | Message receiving option of the group member |
| kTIMGroupMemberInfoMsgSeq | uint | Read-only | - |
| kTIMGroupMemberInfoShutupTime | uint | Read-only | Mute time of the group member |
| kTIMGroupMemberInfoNameCard | string | Read-only | Group namecard of the group member |
| kTIMGroupMemberInfoCustomInfo | array [GroupMemberInfoCustemString](#groupmemberinfocustemstring) | Read-only | For details, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

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
| kTIMCreateGroupParamGroupId | String | Write-only (optional) | Group ID. If this field is not specified, the callback triggered when the group is successfully created will return a group ID allocated by the backend. |
| kTIMCreateGroupParamGroupType | Uint [TIMGroupType](#timgrouptype) | Write-only (optional) | Group type. The default value is Public. |
| kTIMCreateGroupParamGroupMemberArray | Array [GroupMemberInfo](#groupmemberinfo) | Write-only (optional) | Array of initial members of the group |
| kTIMCreateGroupParamNotification | String | Write-only (optional) | Group notification |
| kTIMCreateGroupParamIntroduction | String | Write-only (optional) | Group introduction |
| kTIMCreateGroupParamFaceUrl | String | Write-only (optional) | Group profile photo URL |
| kTIMCreateGroupParamAddOption | Uint [TIMGroupAddOption](#timgroupaddoption) | Write-only (optional) | Group adding option. The default value is Any. |
| kTIMCreateGroupParamMaxMemberCount | Uint | Write-only (optional) | Maximum number of members in the group |
| kTIMCreateGroupParamCustomInfo | Array [GroupInfoCustemString](#groupinfocustemstring) | Read-only (optional) | For details, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

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
| kTIMGroupInviteMemberParamIdentifierArray | Array string | Write-only (required) | Array of IDs of the users who are invited to join the group |
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
| kTIMGroupInviteMemberResultResult | Uint [HandleGroupMemberResult](#handlegroupmemberresult) | Read-only | Invitation result |

### GroupDeleteMemberParam

Parameters of the API for deleting members.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupDeleteMemberParamGroupId | String | Write-only (required) | Group ID |
| kTIMGroupDeleteMemberParamIdentifierArray | Array string | Write-only (required) | Array of IDs of the users who are deleted from the group |
| kTIMGroupDeleteMemberParamUserData | String | Write-only (optional) | User-defined data |

### GroupDeleteMemberResult

Result returned by the API for deleting members.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupDeleteMemberResultIdentifier | String | Read-only | ID of the deleted member |
| kTIMGroupDeleteMemberResultResult | Uint [HandleGroupMemberResult](#handlegroupmemberresult) | Read-only | Deletion result |

### TIMGroupReceiveMessageOpt

Group message receiving option.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMRecvGroupMsgOpt_ReceiveAndNotify | 0 | Receive group messages and notify |
| kTIMRecvGroupMsgOpt_NotReceive | 1 | Do not receive group messages. The server will not forward group messages. |
| kTIMRecvGroupMsgOpt_ReceiveNotNotify | 2 | Receive group message but do not notify |

### GroupSelfInfo

Self information in the group.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupSelfInfoJoinTime | Uint | Read-only | Time that the user joins the group |
| kTIMGroupSelfInfoRole | Uint | Read-only | Role of the user in the group |
| kTIMGroupSelfInfoUnReadNum | Uint | Read-only | Unread message count |
| kTIMGroupSelfInfoMsgFlag | Uint [TIMGroupReceiveMessageOpt](#timgroupreceivemessageopt) | Read-only | Group message receiving option |

### GroupBaseInfo

Result (basic group information) returned by the API for obtaining the list of groups that a user has joined.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupBaseInfoGroupId | String | Read-only | Group ID |
| kTIMGroupBaseInfoGroupName | String | Read-only | Group name |
| kTIMGroupBaseInfoGroupType | String [TIMGroupType](#timgrouptype) | Read-only | Group type |
| kTIMGroupBaseInfoFaceUrl | String | Read-only | Group profile photo URL |
| kTIMGroupBaseInfoInfoSeq | Uint | Read-only | Sequence number of the group profile. The value of this field increases by one each time the group profile is changed. |
| kTIMGroupBaseInfoLastestSeq | Uint | Read-only | Sequence number of the latest message in the group. Each message in the group has a unique sequence number, which is consecutive based on the message sending sequence. The value of LastestSeq starts from 1 and increases by 1 each time a message is added to the group. |
| kTIMGroupBaseInfoReadedSeq | Uint | Read-only | Sequence number of the read message in the group |
| kTIMGroupBaseInfoMsgFlag | Uint | Read-only | Message receiving option |
| kTIMGroupBaseInfoIsShutupAll | Bool | Read-only | Indicates whether the mute all feature is enabled for the group. |
| kTIMGroupBaseInfoSelfInfo | Object [GroupSelfInfo](#groupselfinfo) | Read-only | Self information of the user in the group |

### GroupDetailInfo

Group detail information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupDetialInfoGroupId | String | Read-only | Group ID |
| kTIMGroupDetialInfoGroupType | Uint [TIMGroupType](#timgrouptype) | Read-only | Group type |
| kTIMGroupDetialInfoGroupName | String | Read-only | Group name |
| kTIMGroupDetialInfoNotification | String | Read-only | Group announcement |
| kTIMGroupDetialInfoIntroduction | String | Read-only | Group introduction |
| kTIMGroupDetialInfoFaceUrl | String | Read-only | Group profile photo URL |
| kTIMGroupDetialInfoCreateTime | Uint | Read-only | Group creation time |
| kTIMGroupDetialInfoInfoSeq | Uint | Read-only | Sequence number of the group profile. The value of this field increases by one each time the group profile is changed. |
| kTIMGroupDetialInfoLastInfoTime | Uint | Read-only | Last modification time of the group information |
| kTIMGroupDetialInfoNextMsgSeq | Uint | Read-only | Sequence number of the latest message in the group |
| kTIMGroupDetialInfoLastMsgTime | Uint | Read-only | Time of the latest message in the group |
| kTIMGroupDetialInfoMemberNum | Uint | Read-only | Current number of members in the group |
| kTIMGroupDetialInfoMaxMemberNum | Uint | Read-only | Maximum number of members in the group |
| kTIMGroupDetialInfoAddOption | Uint [TIMGroupAddOption](#timgroupaddoption) | Read-only | Group adding option |
| kTIMGroupDetialInfoOnlineMemberNum | Uint | Read-only | Number of online members in the group |
| kTIMGroupDetialInfoVisible | Uint | Read-only | Indicates whether group members are visible to users outside the group. |
| kTIMGroupDetialInfoSearchable | Uint | Read-only | Indicates whether the group can be searched for. |
| kTIMGroupDetialInfoIsShutupAll | Bool | Read-only | Indicates whether the mute all feature is enabled for the group. |
| kTIMGroupDetialInfoOwnerIdentifier | String | Read-only | ID of the group owner |
| kTIMGroupDetialInfoCustomInfo | Array [GroupInfoCustemString](#groupinfocustemstring) | Read-only | For details, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### GetGroupInfoResult

Result returned by the API for obtaining the group information list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGetGroupInfoResultCode | Int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Result for obtaining the group detail information |
| kTIMGetGroupInfoResultDesc | String | Read-only | Description of the failure to obtain the detailed group information |
| kTIMGetGroupInfoResultInfo | Object [GroupDetailInfo](#groupdetailinfo) | Read-only | Detailed group information |

### TIMGroupModifyInfoFlag

Group information setting (modification) type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupModifyInfoFlag_None | 0x00 | - |
| kTIMGroupModifyInfoFlag_Name | 0x01 | Modification of the group name |
| kTIMGroupModifyInfoFlag_Notification | 0x01 << 1 | Modification of the group notification |
| kTIMGroupModifyInfoFlag_Introduction | 0x01 << 2 | Modification of the group introduction |
| kTIMGroupModifyInfoFlag_FaceUrl | 0x01 << 3 | Modification of the group profile photo URL |
| kTIMGroupModifyInfoFlag_AddOption | 0x01 << 4 | Modification of the group addition option |
| kTIMGroupModifyInfoFlag_MaxMmeberNum | 0x01 << 5 | Modification of the maximum number of members in the group |
| kTIMGroupModifyInfoFlag_Visible | 0x01 << 6 | Modification of whether the group is visible |
| kTIMGroupModifyInfoFlag_Searchable | 0x01 << 7 | Modification of whether the group can be searched for |
| kTIMGroupModifyInfoFlag_ShutupAll | 0x01 << 8 | Modification of whether the mute all feature is enabled for the group |
| kTIMGroupModifyInfoFlag_Custom | 0x01 << 9 | Modification of group custom information |
| kTIMGroupModifyInfoFlag_Owner | 0x01 << 31 | Modification of the group owner |

### GroupModifyInfoParam

Parameters of the API for modifying the group information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupModifyInfoParamGroupId | String | Write-only (required) | Group ID |
| kTIMGroupModifyInfoParamModifyFlag | Uint [TIMGroupModifyInfoFlag](#timgroupmodifyinfoflag) | Write-only (required) | Modify the flag. You can set multiple values, and the bitwise OR result of these values will be used. |
| kTIMGroupModifyInfoParamGroupName | String | Write-only (optional) | Modify the group name. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Name`. |
| kTIMGroupModifyInfoParamNotification | String | Write-only (optional) | Modify the group notification. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Notification`. |
| kTIMGroupModifyInfoParamIntroduction | String | Write-only (optional) | Modify the group introduction. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Introduction`. |
| kTIMGroupModifyInfoParamFaceUrl | String | Write-only (optional) | Modify the group profile photo URL. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_FaceUrl`. |
| kTIMGroupModifyInfoParamAddOption | Uint | Write-only (optional) | Modify the group adding option. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_AddOption`. |
| kTIMGroupModifyInfoParamMaxMemberNum | Uint | Write-only (optional) | Modify the maximum number of members in the group. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_MaxMmeberNum`. |
| kTIMGroupModifyInfoParamVisible | Uint | Write-only (optional) | Modify whether the group is visible. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Visible`. |
| kTIMGroupModifyInfoParamSearchAble | Uint | Write-only (optional) | Modify whether the group can be searched. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Searchable`. |
| kTIMGroupModifyInfoParamIsShutupAll | Bool | Write-only (optional) | Modify whether the mute all feature is enabled for the group. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_ShutupAll`. |
| kTIMGroupModifyInfoParamOwner | String | Write-only (optional) | Modify the group owner. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Owner`. At this time, `modify_flag` cannot contain other values because modifying other information is meaningless when the group owner is modified. |
| kTIMGroupModifyInfoParamCustomInfo | Array [GroupInfoCustemString](#groupinfocustemstring) | Write-only (optional) | For details, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### GroupGetMemberInfoListParam

Parameters of the API for obtaining the group member list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupGetMemberInfoListParamGroupId | String | Write-only (required) | Group ID |
| kTIMGroupGetMemberInfoListParamIdentifierArray | Array string | Write-only (optional) | List of group member IDs |
| kTIMGroupGetMemberInfoListParamOption | Object [GroupMemberGetInfoOption](#groupmembergetinfooption) | Write-only (optional) | Option for obtaining the group member information |
| kTIMGroupGetMemberInfoListParamNextSeq | Uint64 | Write-only (optional) | Pulling-by-page flag. It is set to 0 when the information is pulled for the first time. If the callback succeeds and the result is not 0, paging is needed. The value of this field is passed in via API calling for the next pull until the value is equal to 0. |

### GroupGetMemberInfoListResult

Result returned by the API for obtaining the group member list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupGetMemberInfoListResultNexSeq | Uint64 | Read-only | Next pulling flag. If the server returns 0, no more data can be pulled. Otherwise, this flag must be included next time the API is called to obtain the data. |
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
| kTIMGroupMemberModifyFlag_Custom | 0x01 << 4 | Modification of group member custom information |

### GroupModifyMemberInfoParam

Parameters of the API for setting the group member information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupModifyMemberInfoParamGroupId | String | Write-only (required) | Group ID |
| kTIMGroupModifyMemberInfoParamIdentifier | String | Write-only (required) | ID of the member whose information is set |
| kTIMGroupModifyMemberInfoParamModifyFlag | Uint [TIMGroupMemberModifyInfoFlag](#timgroupmembermodifyinfoflag) | Write-only (required) | Modification type. You can set multiple values, and the bitwise OR result of these values will be used. |
| kTIMGroupModifyMemberInfoParamMsgFlag | Uint | Write-only (optional) | Modify the message receiving option. This field is required only when `modify_flag` contains `kTIMGroupMemberModifyFlag_MsgFlag`. |
| kTIMGroupModifyMemberInfoParamMemberRole | Uint [TIMGroupMemberRole](#timgroupmemberrole) | Write-only (optional) | Modify the member role. This field is required only when `modify_flag` contains `kTIMGroupMemberModifyFlag_MemberRole`. |
| kTIMGroupModifyMemberInfoParamShutupTime | Uint | Write-only (optional) | Modify the mute time. This field is required only when `modify_flag` contains `kTIMGroupMemberModifyFlag_ShutupTime`. |
| kTIMGroupModifyMemberInfoParamNameCard | Uint | Write-only (optional) | Modify the group name card. This field is required only when `modify_flag` contains `kTIMGroupMemberModifyFlag_NameCard`. |
| kTIMGroupModifyMemberInfoParamCustomInfo | Array [GroupMemberInfoCustemString](#groupmemberinfocustemstring) | Write-only (optional) | For details, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### GroupPendencyOption

Parameters of the API for obtaining the group pending request list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupPendencyOptionStartTime | Uint64 | Write-only (required) | Pulling timestamp. It is set to 0 for the first request, and later is set based on the timestamp specified by the kTIMGroupPendencyResultNextStartTime key of [GroupPendencyResult](#grouppendencyresult) returned by the server. |
| kTIMGroupPendencyOptionMaxLimited | Uint | Write-only (optional) | Recommended number of pending requests to be pulled. The server can return pending requests as required, but this key cannot be used as a flag that indicates whether pulling of all pending requests was completed or not. |

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
| kTIMGroupPendencyGroupId | String | Read/Write | Group ID |
| kTIMGroupPendencyFromIdentifier | String | Read/Write | Requester ID, for example, ID of the requester who requests to join the group or ID of the inviter who invites a user to join the group |
| kTIMGroupPendencyToIdentifier | String | Read/Write | Decider ID, for example, "" for a request to join the group or ID of the user who is invited to join the group |
| kTIMGroupPendencyAddTime | Uint64 | Read-only | Time that the pending request is added |
| kTIMGroupPendencyPendencyType | Uint [TIMGroupPendencyType](#timgrouppendencytype) | Read-only | Type of the pending request |
| kTIMGroupPendencyHandled | Uint [TIMGroupPendencyHandle](#timgrouppendencyhandle) | Read-only | Group pending request status |
| kTIMGroupPendencyHandleResult | Uint [TIMGroupPendencyHandleResult](#timgrouppendencyhandleresult) | Read-only | Handling operation type of the group pending request |
| kTIMGroupPendencyApplyInviteMsg | String | Read-only | Additional information of the application or invitation |
| kTIMGroupPendencyFromUserDefinedData | String | Read-only | Custom field of the applicant or inviter |
| kTIMGroupPendencyApprovalMsg | String | Read-only | Approval information, which is the acceptance or rejection information |
| kTIMGroupPendencyToUserDefinedData | String | Read-only | Custom field of the approver |
| kTIMGroupPendencyKey | string | Read-only | Signing information, which customers can ignore |
| kTIMGroupPendencyAuthentication | string | Read-only | Signing information, which customers can ignore |
| kTIMGroupPendencySelfIdentifier | string | Read-only | Self ID |

### GroupPendencyResult

Result returned by the API for obtaining the group pending request list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupPendencyResultNextStartTime | Uint64 | Read-only | Start timestamp for the next pull. If the server returns 0, no more data can be pulled. Otherwise, this timestamp is used as the start timestamp for the next pull. |
| kTIMGroupPendencyResultReadTimeSeq | Uint64 | Read-only | Timestamp of the read pending request |
| kTIMGroupPendencyResultUnReadNum | Uint | Read-only | Number of unread pending requests |
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
| kTIMFriendShipGetProfileListParamForceUpdate | Bool | Write-only | Indicates whether to update the profiles forcibly. false: profiles are preferentially obtained from the local cache, and if such an attempt fails, profiles are pulled from the network. true: profiles are directly pulled from the network. The default value is false |

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
| kTIMProfileAddPermission_AllowAny | 1 | Allows anyone to add the user as a friend |
| kTIMProfileAddPermission_NeedConfirm | 2 | Requires confirmation of friend requests |
| kTIMProfileAddPermission_DenyAny | 3 | Prohibits anyone from adding the user as a friend |

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
| kTIMUserProfileGender | Uint [TIMGenderType](#timgendertype) | Read-only | Gender |
| kTIMUserProfileFaceUrl | String | Read-only | User profile photo URL |
| kTIMUserProfileSelfSignature | String | Read-only | User’s personal signature |
| kTIMUserProfileAddPermission | Uint [TIMProfileAddPermission](#timprofileaddpermission) | Read-only | Friend adding option of the user |
| kTIMUserProfileLocation | String | Read-only | Location information of the user |
| kTIMUserProfileLanguage | Uint | Read-only | Language |
| kTIMUserProfileBirthDay | Uint | Read-only | Birthday |
| kTIMUserProfileLevel | Uint | Read-only | Level |
| kTIMUserProfileRole | Uint | Read-only | Role |
| kTIMUserProfileCustomStringArray | Array [UserProfileCustemStringInfo](#userprofilecustemstringinfo) | Read-only | For details, see [Custom Profile Fields](https://intl.cloud.tencent.com/document/product/1047/33520#.E8.87.AA.E5.AE.9A.E4.B9.89.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5). |

### UserProfileItem

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMUserProfileItemNickName | String | Write-only | Modify the user’s nickname |
| kTIMUserProfileGender | Uint [TIMGenderType](#timgendertype) | Write-only | Modify the user’s gender |
| kTIMUserProfileItemFaceUrl | String | Write-only | Modify the user’s profile photo URL |
| kTIMUserProfileItemSelfSignature | String | Write-only | Modify the user’s signature |
| kTIMUserProfileItemAddPermission | Uint [TIMProfileAddPermission](#timprofileaddpermission) | Write-only | Modify the user’s friend adding option |
| kTIMUserProfileItemLoaction | Uint | Write-only | Modify the user’s location |
| kTIMUserProfileItemLanguage | Uint | Write-only | Modify the language |
| kTIMUserProfileItemBirthDay | Uint | Write-only | Modify the birthday |
| kTIMUserProfileItemLevel | Uint | Write-only | Modify the level |
| kTIMUserProfileItemRole | Uint | Write-only | Modify the role |
| kTIMUserProfileItemCustomStringArray | Array [UserProfileCustemStringInfo](#userprofilecustemstringinfo) | Write-only | Modify [custom profile fields](https://intl.cloud.tencent.com/document/product/1047/33520#.E8.87.AA.E5.AE.9A.E4.B9.89.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5) |

### FriendProfileCustemStringInfo

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendProfileCustemStringInfoKey | String | Write-only | Key of the friend custom profile field |
| kTIMFriendProfileCustemStringInfoValue | String | Write-only | Value of the friend custom profile field |

### FriendProfile

Friend Profiles

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendProfileIdentifier | String | Read-only | UserID of the friend |
| kTIMFriendProfileGroupNameArray | Array string | Read-only | List of friend group names |
| kTIMFriendProfileRemark | String | Read-only | Friend remarks, which cannot exceed 96 bytes. This field is empty if the API is called to obtain your own profile. |
| kTIMFriendProfileAddWording | String | Read-only | Cause for adding a friend |
| kTIMFriendProfileAddSource | String | Read-only | Source for adding a friend |
| kTIMFriendProfileAddTime | Uint64 | Read-only | Friend adding time |
| kTIMFriendProfileUserProfile | object [UserProfile](#userprofile) | Read-only | Friend’s profile |
| kTIMFriendProfileCustomStringArray | Array [FriendProfileCustemStringInfo](#friendprofilecustemstringinfo) | Read-only | [Custom friend fields](https://intl.cloud.tencent.com/document/product/1047/33521#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.A5.BD.E5.8F.8B.E5.AD.97.E6.AE.B5) |

### FriendProfileItem

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendProfileItemRemark | String | Write-only | Modify the friend remarks |
| kTIMFriendProfileItemGroupNameArray | Array string | Write-only | Modify the friend group name list |
| kTIMFriendProfileItemCustomStringArray | Array [FriendProfileCustemStringInfo](#friendprofilecustemstringinfo) | Write-only | Modify the [custom friend fields](https://intl.cloud.tencent.com/document/product/1047/33521#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.A5.BD.E5.8F.8B.E5.AD.97.E6.AE.B5) |

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
| kTIMFriendshipAddFriendParamFriendType | Uint [TIMFriendType](#timfriendtype) | Write-only | Type of the friend to be added |
| kTIMFriendshipAddFriendParamRemark | String | Write-only | Remarks for the friend to be added |
| kTIMFriendshipAddFriendParamGroupName | String | Write-only | Group name |
| kTIMFriendshipAddFriendParamAddSource | String | Write-only | Description of the source from which the friend is added |
| kTIMFriendshipAddFriendParamAddWording | String | Write-only | Postscript for adding a friend |

### FriendResult

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendResultIdentifier | String | Read-only | ID of the user who performs the relationship chain operation |
| kTIMFriendResultCode | Int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Result of the relationship chain operation |
| kTIMFriendResultDesc | String | Read-only | Detailed description of the relationship chain operation failure |

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
| kTIMFriendshipGetPendencyListParamType | Uint [TIMFriendPendencyType](#timfriendpendencytype) | Write-only | Type of the pending friend request |
| kTIMFriendshipGetPendencyListParamStartSeq | Uint64 | Write-only | Sequence number of the pending request, starting from which the pending request list is obtained. We recommend that the client store `seq` and the pending request list. When the pending request list needs to be obtained, this field is set to the seq returned by `server`. If `seq` is the latest one on the `server`, no data is returned. |
| kTIMFriendshipGetPendencyListParamStartTime | Uint64 | Write-only | Timestamp, starting from which the pending request information is obtained |
| kTIMFriendshipGetPendencyListParamLimitedSize | Int | Write-only | Size of each page of the obtained pending request list |

### PendencyPage

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMPendencyPageStartTime | Uint64 | Read-only | Start time of the pending request information page |
| kTIMPendencyPageUnReadNum | Uint64 | Read-only | Unread count of the pending request information page |
| kTIMPendencyPageCurrentSeq | Uint64 | Read-only | Current sequence number of the pending request information page |
| kTIMPendencyPagePendencyInfoArray | Array [FriendAddPendencyInfo](#friendaddpendencyinfo) | Read-only | Pending request list on the pending request information page |

### FriendAddPendencyInfo

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendAddPendencyInfoType | Uint [TIMFriendPendencyType](#timfriendpendencytype) | Read-only | Type of the pending friend adding request |
| kTIMFriendAddPendencyInfoIdentifier | String | Read-only | UserID in the pending friend adding request |
| kTIMFriendAddPendencyInfoNickName | String | Read-only | Nickname in the pending friend adding request |
| kTIMFriendAddPendencyInfoAddTime | Uint64 | Read-only | Adding time in the pending friend adding request |
| kTIMFriendAddPendencyInfoAddSource | String | Read-only | Source in the pending friend adding request |
| kTIMFriendAddPendencyInfoAddWording | String | Read-only | Postscript in the pending friend adding request |

### FriendshipDeletePendencyParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipDeletePendencyParamType | Uint [TIMFriendPendencyType](#timfriendpendencytype) | Read-only | Type of the pending friend deletion request |
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
| kTIMFriendResponeAction | Uint [TIMFriendResponseAction](#timfriendresponseaction) | Write-only (required) | Action in the friend adding response |
| kTIMFriendResponeRemark | String | Write-only (optional) | Friend remark |
| kTIMFriendResponeGroupName | String | Write-only (optional) | Friend group list |

### FriendshipDeleteFriendParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipDeleteFriendParamFriendType | Uint [TIMFriendType](#timfriendtype) | Write-only | Type of the friend to be deleted |
| kTIMFriendshipDeleteFriendParamIdentifierArray | Array string | Write-only (optional) | List of UserIDs of friends to be deleted |

### FriendGroupInfo

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipCreateFriendGroupParamNameArray | Array string | Write-only | Name list of the created friend group |
| kTIMFriendshipCreateFriendGroupParamIdentifierArray | Array string | Write-only | List of UserIDs of friends to be put into the created friend group |

### FriendGroupInfo

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendGroupInfoName | String | Read-only | Group name |
| kTIMFriendGroupInfoCount | Uint64 | Read-only | Number of friends in the current group |
| kTIMFriendGroupInfoIdentifierArray | Array string | Read-only | List of UserIDs of friends in the current group |

### FriendshipModifyFriendGroupParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipModifyFriendGroupParamName | String | Write-only | Name of the group to be modified |
| kTIMFriendshipModifyFriendGroupParamNewName | String | Write-only (optional) | Name of the group after modification |
| kTIMFriendshipModifyFriendGroupParamDeleteIdentifierArray | Array string | Write-only (optional) | List of UserIDs of friends to be deleted from the current group |
| kTIMFriendshipModifyFriendGroupParamAddIdentifierArray | Array string | Write-only (optional) | List of UserIDs of friends to be added to the current group |

### FriendshipCheckFriendTypeParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipCheckFriendTypeParamCheckType | Uint [TIMFriendType](#timfriendtype) | Write-only | Friend type to be checked |
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
| kTIMFriendshipCheckFriendTypeResultRelation | Uint [TIMFriendCheckRelation](#timfriendcheckrelation) | Read-only | If the check succeeds, the relationship between two users is returned. |
| kTIMFriendshipCheckFriendTypeResultCode | Int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Check result |
| kTIMFriendshipCheckFriendTypeResultDesc | String | Read-only | Description of the friendship check failure |

