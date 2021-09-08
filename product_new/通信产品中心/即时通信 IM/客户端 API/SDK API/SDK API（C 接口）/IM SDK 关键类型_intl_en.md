## Common Macro and Basic Configuration Options


### TIMResult

Values returned after an API is called.

| Name | Description |
|-----|-----|
| TIM_SUCC | API called successfully |
| TIM_ERR_SDKUNINIT | Failed to call the API because the IM SDK is not initialized. |
| TIM_ERR_NOTLOGIN | Failed to call the API because the user did not log in. |
| TIM_ERR_JSON | Failed to call the API because the JSON format or JSON Key is incorrect. |
| TIM_ERR_PARAM | Failed to call the API because parameters are incorrect. |
| TIM_ERR_CONV | Failed to call the API because the session is invalid. |
| TIM_ERR_GROUP | Failed to call the API because the group is invalid. |

>? If a callback exists in the API parameters, the callback is called only when the API returns a TIM_SUCC message.


### TIMLogLevel

Log level.

| Name | Description |
|-----|-----|
| kTIMLog_Off | Disables log output. |
| kTIMLog_Test | Full log |
| kTIMLog_Verbose | Log for detailed information during development and debugging |
| kTIMLog_Debug | Debugging log |
| kTIMLog_Info | Information log |
| kTIMLog_Warn | Alarm log |
| kTIMLog_Error | Error log |
| kTIMLog_Assert | Assertion log |

### TIMNetworkStatus

Connection event type.

| Name | Description |
|-----|-----|
| kTIMConnected | Connected |
| kTIMDisconnected | Disconnected |
| kTIMConnecting | Connecting |
| kTIMConnectFailed | Failed to connect |

### TIMConvEvent

Session event type.

| Name | Description |
|-----|-----|
| kTIMConvEvent_Add | Adds a session. For example, when a new message is received and a new session is generated, this operation is triggered. |
| kTIMConvEvent_Del | Deletes a session. For example, if you delete a session, this operation is triggered. |
| kTIMConvEvent_Update | Updates a session. When the number of unread messages in a session changes or a new message is received, this operation is triggered. |

### TIMConvType

Session type.

| Name | Description |
|-----|-----|
| kTIMConv_Invalid | Invalid session |
| kTIMConv_C2C | Personal session |
| kTIMConv_Group | Group session |
| kTIMConv_System | System session |

### TIMPlatform

Platform information.

| Name | Description |
|-----|-----|
| kTIMPlatform_Other | Unknown platform |
| kTIMPlatform_Windows | Windows platform |
| kTIMPlatform_Android | Android platform |
| kTIMPlatform_IOS | iOS platform |
| kTIMPlatform_Mac | MacOS platform |
| kTIMPlatform_Simulator | iOS simulator platform |

### SdKConfig

Configuration for initializing the IM SDK.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMSdkConfigConfigFilePath | string | Write-only (required) | Configures the file path. The default path is "/". |
| kTIMSdkConfigLogFilePath | string | Write-only (required) | Path of a log file. The default path is "/". |
| kTIMSdkConfigJavaVM | uint64 | Write-only (optional) | Configures the Java VM pointer of the Android platform. |

### TIMGroupMemberInfoFlag

Information IDs of group members.

| Name | Description |
|-----|-----|
| kTIMGroupMemberInfoFlag_None | None |
| kTIMGroupMemberInfoFlag_JoinTime | Join time |
| kTIMGroupMemberInfoFlag_MsgFlag | Option for receiving group messages |
| kTIMGroupMemberInfoFlag_MsgSeq | Member read message seq |
| kTIMGroupMemberInfoFlag_MemberRole | Member role |
| kTIMGroupMemberInfoFlag_ShutupUntill | Mute time. When the value is 0, mute is not enabled. |
| kTIMGroupMemberInfoFlag_NameCard | Group card |

### TIMGroupMemberRoleFlag

Role IDs of group members.

| Name | Description |
|-----|-----|
| kTIMGroupMemberRoleFlag_All | Obtains all role types. |
| kTIMGroupMemberRoleFlag_Owner | Obtains the owner (group owner). |
| kTIMGroupMemberRoleFlag_Admin | Obtains administrators, excluding group owners. |
| kTIMGroupMemberRoleFlag_Member | Obtains common group members, excluding group owners and administrators. |

### GroupMemberGetInfoOption

Option for obtaining group member information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupMemberGetInfoOptionInfoFlag | uint64 [TIMGroupMemberInfoFlag](#timgroupmemberinfoflag) | Read/Write (optional) | Group member information is filtered based on information you want to obtain. The default value is 0xffffffff (obtain all information). |
| kTIMGroupMemberGetInfoOptionRoleFlag | uint64 [TIMGroupMemberRoleFlag](#timgroupmemberroleflag) | Read/Write (optional) | Group member information is filtered based on member role. The default value is kTIMGroupMemberRoleFlag_All (obtain all roles). |
| kTIMGroupMemberGetInfoOptionCustomArray | array string | Write-only (optional) | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

### TIMGroupGetInfoFlag

Information IDs of group members.

| Name | Description |
|-----|-----|
| kTIMGroupInfoFlag_None | - |
| kTIMGroupInfoFlag_Name | Group name |
| kTIMGroupInfoFlag_CreateTime | Group creation time |
| kTIMGroupInfoFlag_OwnerUin | Group owner account |
| kTIMGroupInfoFlag_Seq | - |
| kTIMGroupInfoFlag_LastTime | Last group information modification time |
| kTIMGroupInfoFlag_NextMsgSeq | - |
| kTIMGroupInfoFlag_LastMsgTime | Time of the most recent group message |
| kTIMGroupInfoFlag_AppId | - |
| kTIMGroupInfoFlag_MemberNum | Number of group members |
| kTIMGroupInfoFlag_MaxMemberNum | Maximum number of group members |
| kTIMGroupInfoFlag_Notification | Group announcement content |
| kTIMGroupInfoFlag_Introduction | Group introduction |
| kTIMGroupInfoFlag_FaceUrl | URL of a group profile photo |
| kTIMGroupInfoFlag_AddOpton | Option for adding a group |
| kTIMGroupInfoFlag_GroupType | Group type |
| kTIMGroupInfoFlag_LastMsg | Latest message in a group |
| kTIMGroupInfoFlag_OnlineNum | Number of online group members |
| kTIMGroupInfoFlag_Visible | Whether a group is visible |
| kTIMGroupInfoFlag_Searchable | Whether a group can be searched |
| kTIMGroupInfoFlag_ShutupAll | Whether mute is enabled for all group members |

### GroupGetInfoOption

Option for obtaining group information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupGetInfoOptionInfoFlag | uint64 [TIMGroupGetInfoFlag](#timgroupgetinfoflag) | Read/Write (optional) | Group information is filtered based on information you want to obtain. The default value is 0xffffffff (obtain all information). |
| kTIMGroupGetInfoOptionCustomArray | array string | Write-only (optional) | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

### UserConfig

Used to configure information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMUserConfigIsReadReceipt | bool | Write-only (optional) | The value True indicates that a read receipt event will be received. |
| kTIMUserConfigIsSyncReport | bool | Write-only (optional) | The value true indicates that the server will delete the read status. |
| kTIMUserConfigIsIngoreGroupTipsUnRead | bool | Write-only (optional) | The value True indicates that group tips are not included in the read group message count. |
| kTIMUserConfigIsDisableStorage | bool | Write-only (optional) | Specifies whether to disable the local database. True: disabled. False: not disabled. The default value is False. |
| kTIMUserConfigGroupGetInfoOption | object [GroupGetInfoOption](#groupgetinfooption) | Write-only (optional) | Obtains the default option of group information. |
| kTIMUserConfigGroupMemberGetInfoOption | object [GroupMemberGetInfoOption](#groupmembergetinfooption) | Write-only (optional) | Obtains the default option of group member information. |

### HttpProxyInfo

HTTP proxy information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMHttpProxyInfoIp | string | Write-only (required) | IP address of the proxy |
| kTIMHttpProxyInfoPort | int | Write-only (required) | Port of the proxy |

### Socks5ProxyInfo

SOCKS5 proxy information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMSocks5ProxyInfoIp | string | Write-only (required) | IP address of the SOCKS5 proxy |
| kTIMSocks5ProxyInfoPort | int | Write-only (required) | Port of the SOCKS5 proxy |
| kTIMSocks5ProxyInfoUserName | string | Write-only (optional) | Authentication user name |
| kTIMSocks5ProxyInfoPassword | string | Write-only (optional) | Authentication password |

### SetConfig

**Update configuration**

- Custom data.
The IM SDK only passes through data customized by developers to the IM backend. The maximum length is 64 bytes. The developer service backend can be notified of the custom data through a third-party callback [status change callback](https://intl.cloud.tencent.com/zh/document/product/1047/34357).
- HTTP proxy.
The HTTP proxy uploads related files to the COS when it sends messages such as pictures, audios, files, and videos clips and downloads related files to the local server when it receives messages such as pictures, audio, files, and video clips. To enable the HTTP proxy, set the IP address of the proxy to a value other than null and the port to a value other than 0 (port 0 is unavailable). To disable the HTTP proxy, set the IP address of the proxy to a null string and the port to 0.
- SOCKS5 proxy.
The SOCKS5 proxy must be enabled before it is initialized. After the SOCKS5 proxy is enabled, all protocols sent by the IM SDK are sent to the IM backend through the SOCKS5 proxy server.


| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMSetConfigLogLevel | uint [TIMLogLevel](#timloglevel) | Write-only (optional) | Level of the log output to the log file |
| kTIMSetConfigCackBackLogLevel | uint [TIMLogLevel](#timloglevel) | Write-only (optional) | Log level for log callback |
| kTIMSetConfigIsLogOutputConsole | bool | Write-only (optional) | Whether to output to the console |
| kTIMSetConfigUserConfig | object [UserConfig](#userconfig) | Write-only (optional) | User configuration |
| kTIMSetConfigUserDefineData | string | Write-only (optional) | Custom data. If required, custom data is set before initialization. |
| kTIMSetConfigHttpProxyInfo | object [HttpProxyInfo](#httpproxyinfo) | Write-only (optional) | Sets the HTTP proxy. If required, the HTTP proxy must be enabled before it sends pictures, files, audio, and videos. |
| kTIMSetConfigSocks5ProxyInfo | object [Socks5ProxyInfo](#socks5proxyinfo) | Write-only (optional) | Sets the SOCKS5 proxy. If required, the SOCKS5 proxy must be enabled before it is initialized. |
| kTIMSetConfigIsOnlyLocalDNSSource | bool | Write-only (optional) | If the value is True, the SDK uses only LocalDNS when it selects the optimal IP address. |

## Key Message Types

Macro definitions related to messages and JSON Key definitions accessed by related structure members.

### IOSOfflinePushConfig

Offline push configuration for messages on iOS.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMIOSOfflinePushConfigTitle | string | Read/Write | Notification title |
| kTIMIOSOfflinePushConfigSound | string | Read/Write | Offline push alert tone URL of the current message for iOS devices. When the value is push.no_sound, no alert tone and no vibration are provided. |
| kTIMIOSOfflinePushConfigIgnoreBadge | bool | Read/Write | Whether to ignore the badge count. If the value is True, the message does not increase the value of the unread message count of the app icon on iOS devices. |

### TIMAndroidOfflinePushNotifyMode

Android offline push mode.

| Name | Description |
|-----|-----|
| kTIMAndroidOfflinePushNotifyMode_Normal | Common notification bar message mode. After an offline message is sent, if you click a message in the notification bar, the app is directly opened and no callback is triggered for the app. |
| kTIMAndroidOfflinePushNotifyMode_Custom | Custom message mode. After an offline message is sent, if you click a message in the notification bar, a callback is triggered for the app. |

### AndroidOfflinePushConfig

Offline push configuration for messages on Android devices.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMAndroidOfflinePushConfigTitle | string | Read/Write | Notification title |
| kTIMAndroidOfflinePushConfigSound | string | Read/Write | Offline push alert tone URL of the current message on Android devices |
| kTIMAndroidOfflinePushConfigNotifyMode | uint [TIMAndroidOfflinePushNotifyMode](#timandroidofflinepushnotifymode) | Read/Write | Notification mode of the current message |
| kTIMAndroidOfflinePushConfigOPPOChannelID | string | Read/Write | OPPO ChannelID |

>? Description of ChannelID
In Android 8.0 and later versions, the ChannelID setting is added to messages in the notification bar. At present, this parameter is required for OPPO phones. If this parameter is not specified, OPPO phones running Android 8.0 or later cannot receive offline push messages. In the future, parameters such as xiaomi_channel_id_ and huawei_channel_id may be added.


### TIMOfflinePushFlag

Push rules.

| Name | Description |
|-----|-----|
| kTIMOfflinePushFlag_Default | Messages are pushed based on default rules. |
| kTIMOfflinePushFlag_NoPush | Messages are not pushed. |

### OfflinePushConfig

Offline message push configuration.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMOfflinePushConfigDesc | string | Read/Write | Content displayed by the current message when the peer receives the message pushed offline |
| kTIMOfflinePushConfigExt | string | Read/Write | Extension field when the current message is pushed offline |
| kTIMOfflinePushConfigFlag | uint [TIMOfflinePushFlag](#timofflinepushflag) | Read/Write | Whether the current message allows push. By default, push is allowed (kTIMOfflinePushFlag_Default). |
| kTIMOfflinePushConfigIOSConfig | object [IOSOfflinePushConfig](#iosofflinepushconfig) | Read/Write | iOS offline push configuration |
| kTIMOfflinePushConfigAndroidConfig | object [AndroidOfflinePushConfig](#androidofflinepushconfig) | Read/Write | Android offline push configuration |

### TIMMsgStatus

Definition of the current status of a message.

| Name | Description |
|-----|-----|
| kTIMMsg_Sending | The message is being sent. |
| kTIMMsg_SendSucc | The message was sent successfully. |
| kTIMMsg_SendFail | Failed to send the message. |
| kTIMMsg_Deleted | The message was deleted. |
| kTIMMsg_LocalImported | The message was imported. |
| kTIMMsg_Revoked | The message was revoked. |

### TIMMsgPriority

Priority of a message. When the value is larger, the priority is lower.

| Name | Description |
|-----|-----|
| kTIMMsgPriority_High | Highest priority. This is generally used for red envelope and gift messages. |
| kTIMMsgPriority_Normal | Second highest priority. We recommend this priority for common messages. |
| kTIMMsgPriority_Low | Low priority. We recommend this priority for like notifications. |
| kTIMMsgPriority_Lowest | Lowest priority. This is generally used for group join and exit notifications (sent by the backend). |

### Message

Message JSON Keys.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgElemArray | array [Elem](#elem) | Read/Write (required) | List of elements in the message |
| kTIMMsgConvId | string | Read/Write (optional) | Session ID of the message |
| kTIMMsgConvType | uint [TIMConvType](#timconvtype) | Read/Write (optional) | Session type of the message |
| kTIMMsgSender | string | Read/Write (optional) | Sender of the message |
| kTIMMsgPriority | uint [TIMMsgPriority](#timmsgpriority) | Read/Write (optional) | Priority of the message |
| kTIMMsgClientTime | uint64 | Read/Write (optional) | Client time |
| kTIMMsgServerTime | uint64 | Read/Write (optional) | Server time |
| kTIMMsgIsFormSelf | bool | Read/Write (optional) | Whether the message is from the user himself or herself |
| kTIMMsgPlatform | bool | Read/Write (optional) | Platform that sends the message |
| kTIMMsgIsRead | bool | Read/Write (optional) | Whether the message is read |
| kTIMMsgIsOnlineMsg | bool | Read/Write (optional) | Whether the message is an online message. False: common message. True: message that is deleted immediately after it is read. The default value is False. |
| kTIMMsgIsPeerRead | bool | Read-only | Whether the message is read by the peer of the session |
| kTIMMsgStatus | uint [TIMMsgStatus](#timmsgstatus) | Read/Write (optional) | Current status of the message |
| kTIMMsgUniqueId | uint64 | Read-only | Unique ID of the message |
| kTIMMsgRand | uint64 | Read-only | Random code of the message |
| kTIMMsgSeq | uint64 | Read-only | Message sequence |
| kTIMMsgCustomInt | uint32_t | Read/Write (optional) | Custom integer field |
| kTIMMsgCustomStr | string | Read/Write (optional) | Custom data field |
| kTIMMsgSenderProfile | object [UserProfile](#userprofile) | Read/Write (optional) | User profile of the message sender |
| kTIMMsgSenderGroupMemberInfo | object [GroupMemberInfo](#groupmemberinfo) | Read/Write (optional) | Information of the message sender in a group. This parameter is only valid in a group session. Currently, only the kTIMGroupMemberInfoIdentifier and kTIMGroupMemberInfoNameCard fields can be obtained. Other fields are obtained through the API `TIMGroupGetMemberInfoList`. |
| kTIMMsgOfflinePushConfig | object [OfflinePushConfig](#offlinepushconfig) | Read/Write (optional) | Offline message push setting |

>?
- Corresponding element sequence:
Currently, files and voice elements may not be transmitted in the added sequence. Other elements are transmitted in sequence. However, we recommend that you do not overly depend on the element sequence for processing. Processing should be performed based on each element type to prevent process crashes when an exception occurs.
- For group red envelope and like notification messages:
In live-streaming scenarios, like and red envelope features are provided. The priority of like notifications is low and the priority of red envelope notifications is high. Message content can be customized using [CustomElem](#customelem). When a message is sent, `kTIMMsgPriority` can be used to define the message priority.
- Delete after read messages:
If the `kTIMMsgIsOnlineMsg` field is set to True, the message is a delete after read message. The message has the following characteristics.
 - C2C session: When the message is sent, the peer can receive the message only when the peer is online. If the peer is offline, the peer cannot receive the message even if the peer logs in later.
 - Group session: When the message is sent, only online members in the group can receive the message. If a member is offline at the time, the member cannot receive the message even if the member logs in later.
 - The message is not saved on the server.
 - The message is not included in the unread message count.
 - The message is not stored locally.
- Custom fields of the message:
Developers can add custom fields to the message. If integers (specified through `kTIMMsgCustomInt`) and binary data (specified through `kTIMMsgCustomStr`; data must be converted into a string and JSON data does not support binary transmission) are customized, different effects can be provided based on the two fields, such as whether voice messages are played. In addition, the values of the two fields are stored locally only and are not synchronized to the server. Therefore, users cannot retrieve these fields when they change devices.


### MessageReceipt

Message read receipt.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgReceiptConvId | string | Read-only | Session ID |
| kTIMMsgReceiptConvType | uint [TIMConvType](#timconvtype) | Read-only | Session type |
| kTIMMsgReceiptTimeStamp | uint64 | Read-only | Timestamp |

### TIMElemType

Element type.

| Name | Description |
|-----|-----|
| kTIMElem_Text | Text element |
| kTIMElem_Image | Image element |
| kTIMElem_Sound | Sound element |
| kTIMElem_Custom | Custom element |
| kTIMElem_File | File element |
| kTIMElem_GroupTips | Element of the group or system message |
| kTIMElem_Face | Emoji element |
| kTIMElem_Location | Location element |
| kTIMElem_GroupReport | Element of the group or system notification |
| kTIMElem_Video | Video element |
| kTIMElem_FriendChange | Relation chain change message element |
| kTIMElem_ProfileChange | Profile change message element |
| kTIMElem_Invalid | Unknown element type |

### Elem

Element type.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMElemType | uint [TIMElemType](#timelemtype) | Read/Write (required) | Element type |

### TextElem

Text element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMTextElemContent | string | Read/Write (required) | Text content |

### FaceElem

Emoji element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFaceElemIndex | int | Read/Write (required) | Emoji index |
| kTIMFaceElemBuf | string | Read/Write (optional) | Other additional data can be customized by the user. To transmit binary data, first convert the binary data into a string. JSON only supports strings. |

>? The IM SDK does not provide any emoji package. If a developer has emoji packages, the developer may use `kTIMFaceElemIndex` to store emoji indexes in emoji packages or directly use `kTIMFaceElemBuf` to store binary information of emojis (the information must be converted into a string. JSON does not support binary transmission). Emoji packages are customized by users, and the IM SDK only passes the data through.


### LocationElem

Location element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMLocationElemDesc | string | Read/Write (optional) | Location description |
| kTIMLocationElemLongitude | double | Read/Write (required) | Longitude |
| kTIMLocationElemlatitude | double | Read/Write (required) | Latitude |

### TIMImageLevel

Image quality level.

| Name | Description |
|-----|-----|
| kTIMImageLevel_Orig | The original image is sent. |
| kTIMImageLevel_Compression | A highly compressed image is sent (a small image by default). |
| kTIMImageLevel_HD | A high definition (HD) image is sent (a large image). |

### ImageElem

Image element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMImageElemOrigPath | string | Read/Write (required) | Path of the sent image |
| kTIMImageElemLevel | uint [TIMImageLevel](#timimagelevel) | Read/Write (required) | Quality level of the sent image |
| kTIMImageElemFormat | int | Read/Write | Format of the sent image |
| kTIMImageElemOrigId | string | Read-only | UUID of the original image |
| kTIMImageElemOrigPicHeight | int | Read-only | Height of the original image |
| kTIMImageElemOrigPicWidth | int | Read-only | Width of the original image |
| kTIMImageElemOrigPicSize | int | Read-only | Size of the original image |
| kTIMImageElemThumbId | string | Read-only | UUID of the thumbnail |
| kTIMImageElemThumbPicHeight | int | Read-only | Height of the thumbnail |
| kTIMImageElemThumbPicWidth | int | Read-only | Width of the thumbnail |
| kTIMImageElemThumbPicSize | int | Read-only | Size of the thumbnail |
| kTIMImageElemLargeId | string | Read-only | UUID of the large image |
| kTIMImageElemLargePicHeight | int | Read-only | Height of the large image |
| kTIMImageElemLargePicWidth | int | Read-only | Width of the large image |
| kTIMImageElemLargePicSize | int | Read-only | Size of the large image |
| kTIMImageElemOrigUrl | string | Read-only | URL of the original image |
| kTIMImageElemThumbUrl | string | Read-only | URL of the thumbnail |
| kTIMImageElemLargeUrl | string | Read-only | URL of the large image |
| kTIMImageElemTaskId | int | Read-only | Task ID |

>?
- Description of image specifications: each image has three specifications, Original (original image), Large (large image), and Thumb (thumbnail).
 - An original image refers to a sent original image. The size of the original image remains unchanged.
 - A large image is an image obtained after the original image is proportionally compressed. After the compression, the height or width (whichever is shorter) is equal to 720 pixels.
 - A thumbnail is an image obtained after the original image is proportionally compressed. After the compression, the height or width (whichever is shorter) is equal to 198 pixels.
- If the size of the original image is smaller than 198 pixels, the original size is retained for the three specifications and compression is not required.
- If the size of the original image is between 198 pixels and 720 pixels, no compression is required for the large image and original image.
- When an image is displayed on a phone, we recommend that you display the thumbnail first. Then, the user can tap the thumbnail to download the large image and tap the large image to download the original image. Developers may also choose to skip the large image, so the user directly downloads the original image by tapping the thumbnail.
- When images are displayed on a tablet or PC, because the resolution is high and the devices are usually connected to Wi-Fi or a wired network, we recommend that you directly display large images. Then, the user can tap the large image to download the original image.


### SoundElem

Sound element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMSoundElemFilePath | string | Read/Write (required) | Path of a voice message file. The developer must first save the language and then specify a path. |
| kTIMSoundElemFileSize | int | Read/Write (required) | Size of a voice message data file (in seconds) |
| kTIMSoundElemFileTime | int | Read/Write (required) | Voice message duration |
| kTIMSoundElemFileId | string | Read-only | ID of a downloaded voice message file |
| kTIMSoundElemBusinessId | int | Read-only | BusinessID used during download |
| kTIMSoundElemDownloadFlag | int | Read-only | Whether to apply for a download address. 0: yes; 1: apply for a download address from COS; 2: directly download from the URL. |
| kTIMSoundElemUrl | string | Read-only | Downloaded URL |
| kTIMSoundElemTaskId | int | Read-only | Task ID |

>?
- Whether the voice message has been played, which can be implemented using a message custom field. For example, the field can be set to 0 to indicate the message has not been played or 1 to indicate the message has been played. After the user clicks play, the field can be set to 1.
- Only one sound element can be added for a message. When multiple sound elements are added for one message, sending the message may fail.


### CustomElem

Custom element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMCustomElemData | string | Read/Write | Data. Binary data is supported. |
| kTIMCustomElemDesc | string | Read/Write | Custom description |
| kTIMCustomElemExt | string | Read/Write | The ext field pushed by the backend |
| kTIMCustomElemSound | string | Read/Write | Custom sound |

>? When the internal message types cannot meet special requirements, developers can use custom message types to customize a message format and message content. The IM SDK is only responsible for passing the messages through.


### FileElem

File element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFileElemFilePath | string | Read/Write (required) | File path (including file name) |
| kTIMFileElemFileName | string | Read/Write (required) | Displayed file name. If this parameter is not specified, by default, the value of kTIMFileElemFileName is the file name in the file path specified by kTIMFileElemFilePath. |
| kTIMFileElemFileSize | int | Read/Write (required) | File size |
| kTIMFileElemFileId | string | Read-only | UUID during video download |
| kTIMFileElemBusinessId | int | Read-only | BusinessID used during download |
| kTIMFileElemDownloadFlag | int | Read-only | File download flag |
| kTIMFileElemUrl | string | Read-only | URL for file download |
| kTIMFileElemTaskId | int | Read-only | Task ID |

>? Only one file element can be added for a message. When multiple file elements are added for one message, the message may fail to send.


### VideoElem

Video element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMVideoElemVideoType | string | Read/Write (required) | Video file type. This parameter is set when a message is sent. |
| kTIMVideoElemVideoSize | uint | Read/Write (required) | Video file size |
| kTIMVideoElemVideoDuration | uint | Read/Write (required) | Video duration. This parameter is set when a message is sent. |
| kTIMVideoElemVideoPath | string | Read/Write (required) | Corresponding file path |
| kTIMVideoElemVideoId | string | Read-only | UUID during video download |
| kTIMVideoElemBusinessId | int | Read-only | BusinessID used during download |
| kTIMVideoElemVideoDownloadFlag | int | Read-only | Flag for video file download |
| kTIMVideoElemVideoUrl | string | Read-only | URL for video file download |
| kTIMVideoElemImageType | string | Read/Write (required) | Screenshot file type. This parameter is set when a message is sent. |
| kTIMVideoElemImageSize | uint | Read/Write (required) | Screenshot file size |
| kTIMVideoElemImageWidth | uint | Read/Write (required) | Screenshot height. This parameter is set when a message is sent. |
| kTIMVideoElemImageHeight | uint | Read/Write (required) | Screenshot width. This parameter is set when a message is sent. |
| kTIMVideoElemImagePath | string | Read/Write (required) | Path for saving a screenshot |
| kTIMVideoElemImageId | string | Read-only | ID during download of a video screenshot |
| kTIMVideoElemImageDownloadFlag | int | Read-only | Flag for screenshot file download |
| kTIMVideoElemImageUrl | string | Read-only | URL for screenshot file download |
| kTIMVideoElemTaskId | uint | Read-only | Task ID |

### TIMGroupTipGroupChangeFlag

Group information modification type.

| Name | Description |
|-----|-----|
| kTIMGroupTipChangeFlag_Unknown | Unknown modification |
| kTIMGroupTipChangeFlag_Name | Modifies the group name. |
| kTIMGroupTipChangeFlag_Introduction | Modifies the group introduction. |
| kTIMGroupTipChangeFlag_Notification | Modifies the group announcement. |
| kTIMGroupTipChangeFlag_FaceUrl | Modifies the URL of a group profile photo. |
| kTIMGroupTipChangeFlag_Owner | Modifies the group owner. |
| kTIMGroupTipChangeFlag_Custom | Modifies group custom information. |

### GroupTipGroupChangeInfo

Group system message - group information modification.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupTipGroupChangeInfoFlag | uint [TIMGroupTipGroupChangeFlag](#timgrouptipgroupchangeflag) | Read-only | Group information flag for group message modification |
| kTIMGroupTipGroupChangeInfoValue | string | Read-only | Modified value. Different values of the `info_flag` field have different meanings. |
| kTIMGroupTipGroupChangeInfoKey | string | Read-only | The `key` value corresponding to custom information. The parameter is valid only when the value of `info_flag` is `kTIMGroupTipChangeFlag_Custom`. |

### GroupTipMemberChangeInfo

Group system message - mute for group members.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupTipMemberChangeInfoIdentifier | string | Read-only | ID of the group member |
| kTIMGroupTipMemberChangeInfoShutupTime | uint | Read-only | Mute time |

### TIMGroupTipType

Message type of the group system.

| Name | Description |
|-----|-----|
| kTIMGroupTip_None | Invalid group tip |
| kTIMGroupTip_Invite | Invitation tip |
| kTIMGroupTip_Quit | Group exit tip |
| kTIMGroupTip_Kick | Removal tip |
| kTIMGroupTip_SetAdmin | Administrator setting tip |
| kTIMGroupTip_CancelAdmin | Administrator cancelation tip |
| kTIMGroupTip_GroupInfoChange | Group information modification tip |
| kTIMGroupTip_MemberInfoChange | Group member information modification tip |

### GroupTipsElem

Message element of the group system (for all group members).

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupTipsElemTipType | uint [TIMGroupTipType](#timgrouptiptype) | Read-only | Group message type |
| kTIMGroupTipsElemOpUser | string | Read-only | Operator ID |
| kTIMGroupTipsElemGroupName | string | Read-only | Group name |
| kTIMGroupTipsElemGroupId | string | Read-only | Group ID |
| kTIMGroupTipsElemTime | uint | Read-only | Group message time |
| kTIMGroupTipsElemUserArray | array string | Read-only | List of accounts operated on |
| kTIMGroupTipsElemGroupChangeInfoArray | array [GroupTipGroupChangeInfo](#grouptipgroupchangeinfo) | Read-only | Group information change information list. This parameter is valid only when the value of `tips_type` is `kTIMGroupTip_GroupInfoChange`. |
| kTIMGroupTipsElemMemberChangeInfoArray | array [GroupTipMemberChangeInfo](#grouptipmemberchangeinfo) | Read-only | Group membeinformation list. This parameter is valid only when the value of `tips_type` is `kTIMGroupTip_MemberInfoChange`. |
| kTIMGroupTipsElemOpUserInfo | object [UserProfile](#userprofile) | Read-only | Personal profile of the operator |
| kTIMGroupTipsElemOpGroupMemberInfo | object [GroupMemberInfo](#groupmemberinfo) | Read-only | Group member information |
| kTIMGroupTipsElemChangedUserInfoArray | array [UserProfile](#userprofile) | Read-only | List of user profiles operated on |
| kTIMGroupTipsElemChangedGroupMemberInfoArray | array [GroupMemberInfo](#groupmemberinfo) | Read-only | Group member information list |
| kTIMGroupTipsElemMemberNum | uint | Read-only | Number of current group members. This parameter is valid only when the event message type is `kTIMGroupTip_Invite`, `kTIMGroupTip_Quit`, or `kTIMGroupTip_Kick`. |
| kTIMGroupTipsElemPlatform | string | Read-only | Operator platform information |

### TIMGroupReportType

Notification types of the group system.

| Name | Description |
|-----|-----|
| kTIMGroupReport_None | Unknown type |
| kTIMGroupReport_AddRequest | Group join request (only the administrator receives the notification). |
| kTIMGroupReport_AddAccept | A group join request is accepted (only the applicant receives the notification). |
| kTIMGroupReport_AddRefuse | A group join request is rejected (only the applicant receives the notification). |
| kTIMGroupReport_BeKicked | Kicked out of a group by the administrator (only the member who is kicked out of the group receives the notification). |
| kTIMGroupReport_Delete | The group is deleted (all members receive the notification). |
| kTIMGroupReport_Create | A group is created (only the creator receives the notification, which is not displayed). |
| kTIMGroupReport_Invite | Group invitation (invited users receive the notification). |
| kTIMGroupReport_Quit | Quit a group (members who exit the group receive this notification, which is not displayed). |
| kTIMGroupReport_GrantAdmin | An administrator is set (the set administrator receives the notification). |
| kTIMGroupReport_CancelAdmin | An administrator is cancelled (the canceled administrator receives the notification). |
| kTIMGroupReport_RevokeAdmin | A group is revoked (all group members receive the notification, which is not displayed). |
| kTIMGroupReport_InviteReq | Group invitation (only invited users receive the notification). |
| kTIMGroupReport_InviteAccept | Group invitation is accepted (only the user who sends the invitation request receives the notification). |
| kTIMGroupReport_InviteRefuse | Group invitation is refused (only the user who sends an invitation request receives the notification). |
| kTIMGroupReport_ReadReport | The read report is synchronized on multiple terminals (only the user who reports the information receives the notification). |
| kTIMGroupReport_UserDefine | Custom notification (by default, all members receive the notification). |

### GroupReportElem

Notification elements of the group system (for individuals).

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupReportElemReportType | uint [TIMGroupReportType](#timgroupreporttype) | Read-only | Type |
| kTIMGroupReportElemGroupId | string | Read-only | Group ID |
| kTIMGroupReportElemGroupName | string | Read-only | Group name |
| kTIMGroupReportElemOpUser | string | Read-only | Operator ID |
| kTIMGroupReportElemMsg | string | Read-only | Reason for operation |
| kTIMGroupReportElemUserData | string | Read-only | Custom data entered by the operator |
| kTIMGroupReportElemOpUserInfo | object [UserProfile](#userprofile) | Read-only | Personal profile of the operator |
| kTIMGroupReportElemOpGroupMemberInfo | object [GroupMemberInfo](#groupmemberinfo) | Read-only | Group information about the operator |
| kTIMGroupReportElemPlatform | string | Read-only | Operator platform information |

### TIMProfileChangeType

| Name | Description |
|-----|-----|
| kTIMProfileChange_None | Unknown type |
| kTIMProfileChange_Profile | Profile change |

### ProfileChangeElem

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMProfileChangeElemChangeType | uint [TIMProfileChangeType](#timprofilechangetype) | Read-only | Profile change type |
| kTIMProfileChangeElemFromIndentifier | string | Read-only | UserID of the user whose profile is changed |
| kTIMProfileChangeElemUserProfileItem | object [UserProfileItem](#userprofileitem) | Read-only | The specific change information is valid only when the value of `change_type` is `kTIMProfileChange_Profile`. |

### TIMFriendChangeType

| Name | Description |
|-----|-----|
| kTIMFriendChange_None | Unknown type |
| kTIMFriendChange_FriendAdd | Adds a friend. |
| kTIMFriendChange_FriendDel | Deletes a friend. |
| kTIMFriendChange_PendencyAdd | Pending adding |
| kTIMFriendChange_PendencyDel | Pending deletion |
| kTIMFriendChange_BlackListAdd | Adds a blocklist. |
| kTIMFriendChange_BlackListDel | Deletes a blocklist. |
| kTIMFriendChange_PendencyReadedReport | Reports pending message read. |
| kTIMFriendChange_FriendProfileUpdate | Updates friend data. |
| kTIMFriendChange_FriendGroupAdd | Adds a group. |
| kTIMFriendChange_FriendGroupDel | Deletes a group. |
| kTIMFriendChange_FriendGroupModify | Modifies a group. |

### FriendProfileUpdate

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendProfileUpdateIdentifier | string | Write-only | UserID of the friend whose information is updated |
| kTIMFriendProfileUpdateItem | object [FriendProfileItem](#friendprofileitem) | Write-only | Item for which information is updated |

### FriendChangeElem

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendChangeElemChangeType | uint [TIMFriendChangeType](#timfriendchangetype) | Read-only | Information change type |
| kTIMFriendChangeElemFriendAddIdentifierArray | array string | Read-only | List of the UserIDs of new friends. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_FriendAdd`. |
| kTIMFriendChangeElemFriendDelIdentifierArray | array string | Read-only | List of the UserIDs of deleted friends. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_FriendDel`. |
| kTIMFriendChangeElemFriendAddPendencyItemArray | array [FriendAddPendency](#friendaddpendency) | Read-only | List of pending friend add requests. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_PendencyAdd`. |
| kTIMFriendChangeElemPendencyDelIdentifierArray | array string | Read-only | List of friend deletion requests. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_PendencyDel`. |
| kTIMFriendChangeElemPendencyReadedReportTimestamp | uint64 | Read-only | Pending message read report timestamp. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_PendencyReadedReport`. |
| kTIMFriendChangeElemBlackListAddIdentifierArray | array string | Read-only | List of UserIDs added to the blocklist. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_BlackListAdd`. |
| kTIMFriendChangeElemBlackListDelIdentifierArray | array string | Read-only | List of UserIDs removed from the blocklist. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_BlackListDel`. |
| kTIMFriendChangeElemFreindProfileUpdateItemArray | array [FriendProfileUpdate](#friendprofileupdate) | Read-only | Friend profile update list. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_FriendProfileUpdate`. |
| kTIMFriendChangeElemFriendGroupAddIdentifierArray | array string | Read-only | Names list of added friend groups. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_FriendGroupAdd`. |
| kTIMFriendChangeElemFriendGroupDelIdentifierArray | array string | Read-only | Names list of deleted friend groups. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_FriendGroupDel`. |
| kTIMFriendChangeElemFriendGroupModifyIdentifierArray | array string | Read-only | Names list of modified friend groups. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_FriendGroupModify`. |

### MsgBatchSendParam

Parameters of the message group sending API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgBatchSendParamIdentifierArray | array string | Write-only (required) | ID list for group sending |
| kTIMMsgBatchSendParamMsg | object [Message](#message) | Write-only (required) | Message sent in the group |

### MsgBatchSendResult

Result returned by the message group sending API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgBatchSendResultIdentifier | string | Read-only | ID for group sending |
| kTIMMsgBatchSendResultCode | int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Result of sending group message |
| kTIMMsgBatchSendResultDesc | string | Read-only | Description of message sending |
| kTIMMsgBatchSendResultMsg | object [Message](#message) | Read-only | Sent message |

### MsgLocator

Message locator.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgLocatorConvId | bool | Read/Write | Session ID of the message to find |
| kTIMMsgLocatorConvType | bool | Read/Write | Session type of the message to find |
| kTIMMsgLocatorIsRevoked | bool | Read/Write (required) | Whether the message to find is revoked. True: revoked. False: not revoked. The default value is False. |
| kTIMMsgLocatorTime | uint64 | Read/Write (required) | Timestamp of the message to find |
| kTIMMsgLocatorSeq | uint64 | Read/Write (required) | Sequence number of the message to find |
| kTIMMsgLocatorIsSelf | bool | Read/Write (required) | Whether the sender of the message to find is the user himself/herself. True: yes. False: no. The default value is False. |
| kTIMMsgLocatorRand | uint64 | Read/Write (required) | Random code of the message to find |
| kTIMMsgLocatorUniqueId | uint64 | Read/Write (required) | Unique ID of the message to find |

### MsgGetMsgListParam

Parameters of the message acquisition API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgGetMsgListParamLastMsg | object [Message](#message) | Write-only (optional) | The specified message. The value cannot be null. |
| kTIMMsgGetMsgListParamCount | uint | Write-only (optional) | Number of messages following the specified message. |
| kTIMMsgGetMsgListParamIsRamble | bool | Write-only (optional) | Whether the message is a roaming message |
| kTIMMsgGetMsgListParamIsForward | bool | Write-only (optional) | Whether the sorting mode is forward sorting |

### MsgDeleteParam

Parameters of the message deletion API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgDeleteParamMsg | object [Message](#message) | Write-only (optional) | Message to be deleted from the specified session |
| kTIMMsgDeleteParamIsRamble | bool | Write-only (optional) | Whether to delete all local/roaming messages. True: delete roaming messages. False: delete local messages. The default value is False. |

### TIMDownloadType

UUID type.

| Name | Description |
|-----|-----|
| kTIMDownload_VideoThumb | Video thumbnail |
| kTIMDownload_File | File |
| kTIMDownload_Video | Video |
| kTIMDownload_Sound | Sound |

### DownloadElemParam

Parameters of the element download API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgDownloadElemParamFlag | uint | Write-only | The parameter is obtained from message elements and indicates the element download type. |
| kTIMMsgDownloadElemParamType | uint [TIMDownloadType](#timdownloadtype) | Write-only | The parameter is obtained from message elements and indicates the element type. |
| kTIMMsgDownloadElemParamId | string | Write-only | This parameter is obtained from message elements and indicates the element ID. |
| kTIMMsgDownloadElemParamBusinessId | uint | Write-only | This parameter is obtained from message elements and indicates the element BusinessID. |
| kTIMMsgDownloadElemParamUrl | string | Write-only | The parameter is obtained from message elements and indicates the element URL. |

### MsgDownloadElemResult

Result returned by the element download API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgDownloadElemResultCurrentSize | uint | Read-only | Size of files currently downloaded |
| kTIMMsgDownloadElemResultTotalSize | uint | Read-only | Total size of files to be downloaded |

## Session Key Type

Macro definitions related to sessions and definitions of JSON Keys accessed by related structure members.

### Draft

Draft information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMDraftMsg | object [Message](#message) | Read-only | Message in the draft |
| kTIMDraftUserDefine | string | Read-only | Custom data |
| kTIMDraftEditTime | uint | Read-only | Latest edit time of the draft |

### ConvInfo

Session information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMConvId | string | Read-only | Session ID |
| kTIMConvType | uint [TIMConvType](#timconvtype) | Read-only | Session type |
| kTIMConvOwner | string | Read-only | Session owner |
| kTIMConvUnReadNum | uint64 | Read-only | Session unread count |
| kTIMConvActiveTime | uint64 | Read-only | Session activation time |
| kTIMConvIsHasLastMsg | bool | Read-only | Whether the session has a last message |
| kTIMConvLastMsg | object [Message](#message) | Read-only | Last message of session |
| kTIMConvIsHasDraft | bool | Read-only | Whether the session has a draft |
| kTIMConvDraft | object [Draft](#draft) | Read-only (optional) | Session draft |

## Group Key Types

Macro definitions related to groups and definitions of JSON Keys accessed by related structure members.

### TIMGroupAddOption

Option for adding a group.

| Name | Description |
|-----|-----|
| kTIMGroupAddOpt_Forbid | Adding a group is forbidden. |
| kTIMGroupAddOpt_Auth | Administrator approval is required. |
| kTIMGroupAddOpt_Any | Anyone can add a group. |

### TIMGroupType

Group type.

| Name | Description |
|-----|-----|
| kTIMGroup_Public | Public group |
| kTIMGroup_Private | Private group |
| kTIMGroup_ChatRoom | Chat room |
| kTIMGroup_BChatRoom | Online member broadcast group |
| kTIMGroup_AVChatRoom | Interactive live chat room |

### TIMGroupMemberRole

Role types of group members.

| Name | Description |
|-----|-----|
| kTIMMemberRole_None | Undefined |
| kTIMMemberRole_Normal | Group member |
| kTIMMemberRole_Admin | Administrator |
| kTIMMemberRole_Owner | Super administrator (group owner) |

### GroupMemberInfoCustemString

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupMemberInfoCustemStringInfoKey | string | Write-only | Key of a custom field |
| kTIMGroupMemberInfoCustemStringInfoValue | string | Write-only | Value of a custom field |

### GroupMemberInfo

Group member information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupMemberInfoIdentifier | string | Read/Write (required) | ID of a group member |
| kTIMGroupMemberInfoJoinTime | uint | Read-only | Join time of a group member |
| kTIMGroupMemberInfoMemberRole | uint [TIMGroupMemberRole](#timgroupmemberrole) | Read/Write (optional) | Role of a group member |
| kTIMGroupMemberInfoMsgFlag | uint | Read-only | Option for member message receiving |
| kTIMGroupMemberInfoMsgSeq | uint | Read-only | - |
| kTIMGroupMemberInfoShutupTime | uint | Read-only | Member mute time |
| kTIMGroupMemberInfoNameCard | string | Read-only | Group card of a member |
| kTIMGroupMemberInfoCustomInfo | array [GroupMemberInfoCustemString](#groupmemberinfocustemstring) | Read-only | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

### GroupInfoCustemString

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupInfoCustemStringInfoKey | string | Write-only | Key of a custom field |
| kTIMGroupInfoCustemStringInfoValue | string | Write-only | Value of a custom field |

### CreateGroupParam

Parameters of the group creation API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMCreateGroupParamGroupName | string | Write-only (required) | Group name |
| kTIMCreateGroupParamGroupId | string | Write-only (optional) | Group ID. When this parameter is not specified, a group ID allocated by the backend is returned by a callback if the group is created successfully. |
| kTIMCreateGroupParamGroupType | uint [TIMGroupType](#timgrouptype) | Write-only (optional) | Group type. The default value is Public. |
| kTIMCreateGroupParamGroupMemberArray | array [GroupMemberInfo](#groupmemberinfo) | Write-only (optional) | Initial member array of a group |
| kTIMCreateGroupParamNotification | string | Write-only (optional) | Group announcement |
| kTIMCreateGroupParamIntroduction | string | Write-only (optional) | Group introduction |
| kTIMCreateGroupParamFaceUrl | string | Write-only (optional) | URL of a group profile photo |
| kTIMCreateGroupParamAddOption | uint [TIMGroupAddOption](#timgroupaddoption) | Write-only (optional) | Option for adding a group. The default value is Any. |
| kTIMCreateGroupParamMaxMemberCount | uint | Write-only (optional) | Maximum number of group members |
| kTIMCreateGroupParamCustomInfo | array [GroupInfoCustemString](#groupinfocustemstring) | Read-only (optional) | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

### CreateGroupResult

Result returned by the group creation API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMCreateGroupResultGroupId | string | Read-only | ID of a created group |

### GroupInviteMemberParam

Parameters of the member invitation API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupInviteMemberParamGroupId | string | Write-only (required) | Group ID |
| kTIMGroupInviteMemberParamIdentifierArray | array string | Write-only (required) | ID array of the user invited to join a group |
| kTIMGroupInviteMemberParamUserData | string | Write-only (required) | Used for custom data |

### HandleGroupMemberResult

Basic information about a group.

| Name | Description |
|-----|-----|
| kTIMGroupMember_HandledErr | Failure |
| kTIMGroupMember_HandledSuc | Success |
| kTIMGroupMember_Included | Already a group member |
| kTIMGroupMember_Invited | Invitation sent |

### GroupInviteMemberResult

Result returned by the member invitation API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupInviteMemberResultIdentifier | string | Read-only | ID of the user invited to join a group |
| kTIMGroupInviteMemberResultResult | uint [HandleGroupMemberResult](#handlegroupmemberresult) | Read-only | Invitation result |

### GroupDeleteMemberParam

Parameters of the member deletion API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupDeleteMemberParamGroupId | string | Write-only (required) | Group ID |
| kTIMGroupDeleteMemberParamIdentifierArray | array string | Write-only (required) | Array of the deleted group member |
| kTIMGroupDeleteMemberParamUserData | string | Write-only (required) | Used for custom data |

### GroupDeleteMemberResult

Result returned by the member deletion API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupDeleteMemberResultIdentifier | string | Read-only | ID of a deleted member |
| kTIMGroupDeleteMemberResultResult | uint [HandleGroupMemberResult](#handlegroupmemberresult) | Read-only | Deletion result |

### TIMGroupReceiveMessageOpt

Option for receiving a group message.

| Name | Description |
|-----|-----|
| kTIMRecvGroupMsgOpt_ReceiveAndNotify | Group messages are received and users are notified. |
| kTIMRecvGroupMsgOpt_NotReceive | Group messages are not received and the server does not forward group messages. |
| kTIMRecvGroupMsgOpt_ReceiveNotNotify | Group messages are received and users are not notified. |

### GroupSelfInfo

The users own information in a group.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupSelfInfoJoinTime | uint | Read-only | Group join time |
| kTIMGroupSelfInfoRole | uint | Read-only | Role of the user in a group |
| kTIMGroupSelfInfoUnReadNum | uint | Read-only | Unread message count |
| kTIMGroupSelfInfoMsgFlag | uint [TIMGroupReceiveMessageOpt](#timgroupreceivemessageopt) | Read-only | Option for receiving group messages |

### GroupBaseInfo

The result returned by the API used to obtain the list of added groups (basic group information).

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupBaseInfoGroupId | string | Read-only | Group ID |
| kTIMGroupBaseInfoGroupName | string | Read-only | Group name |
| kTIMGroupBaseInfoGroupType | uint [TIMGroupType](#timgrouptype) | Read-only | Group type |
| kTIMGroupBaseInfoFaceUrl | string | Read-only | URL of a group profile photo |
| kTIMGroupBaseInfoInfoSeq | uint | Read-only | Group information Seq value. Each time group information is changed, the value of this field increases. |
| kTIMGroupBaseInfoLastestSeq | uint | Read-only | Seq value of the latest group message. Each message in a group has a unique message Seq and the Seq values start from 1. Each time a message is added to the group, the value of LastestSeq increases by 1. |
| kTIMGroupBaseInfoReadedSeq | uint | Read-only | Seq value of the read message in the user group |
| kTIMGroupBaseInfoMsgFlag | uint | Read-only | Option for receiving messages |
| kTIMGroupBaseInfoIsShutupAll | bool | Read-only | Whether mute is enabled for all members of the current group |
| kTIMGroupBaseInfoSelfInfo | object [GroupSelfInfo](#groupselfinfo) | Read-only | The current user’s personal information in the group |

### GroupDetailInfo

Detailed information about a group.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupDetialInfoGroupId | string | Read-only | Group ID |
| kTIMGroupDetialInfoGroupType | uint [TIMGroupType](#timgrouptype) | Read-only | Group type |
| kTIMGroupDetialInfoGroupName | string | Read-only | Group name |
| kTIMGroupDetialInfoNotification | string | Read-only | Group announcement |
| kTIMGroupDetialInfoIntroduction | string | Read-only | Group introduction |
| kTIMGroupDetialInfoFaceUrl | string | Read-only | URL of the group profile photo |
| kTIMGroupDetialInfoCreateTime | uint | Read-only | Group creation time |
| kTIMGroupDetialInfoInfoSeq | uint | Read-only | Seq value of group information. Each time group information is changed, the value of this field increases. |
| kTIMGroupDetialInfoLastInfoTime | uint | Read-only | Last group information modification time |
| kTIMGroupDetialInfoNextMsgSeq | uint | Read-only | Seq value of the latest group message |
| kTIMGroupDetialInfoLastMsgTime | uint | Read-only | Time of the latest group message |
| kTIMGroupDetialInfoMemberNum | uint | Read-only | Number of current group members |
| kTIMGroupDetialInfoMaxMemberNum | uint | Read-only | Maximum number of group members |
| kTIMGroupDetialInfoAddOption | uint [TIMGroupAddOption](#timgroupaddoption) | Read-only | Option for adding a group |
| kTIMGroupDetialInfoOnlineMemberNum | uint | Read-only | Number of online group members |
| kTIMGroupDetialInfoVisible | uint | Read-only | Whether group members are visible outside |
| kTIMGroupDetialInfoSearchable | uint | Read-only | Whether a group can be searched |
| kTIMGroupDetialInfoIsShutupAll | bool | Read-only | Whether mute is enabled for all members in the group |
| kTIMGroupDetialInfoOwnerIdentifier | string | Read-only | ID of the group owner |
| kTIMGroupDetialInfoCustomInfo | array [GroupInfoCustemString](#groupinfocustemstring) | Read-only | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

### GetGroupInfoResult

Obtain the result returned by the API for the group information list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGetGroupInfoResultCode | int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Result of obtaining detailed information about a group |
| kTIMGetGroupInfoResultDesc | string | Read-only | Description of failure to obtain detailed information about a group |
| kTIMGetGroupInfoResultInfo | Object [GroupDetailInfo](#groupdetailinfo) | Read-only | Detailed information about a group |

### TIMGroupModifyInfoFlag

Set (modify) the type of group information.

| Name | Description |
|-----|-----|
| kTIMGroupModifyInfoFlag_None | - |
| kTIMGroupModifyInfoFlag_Name | Modifies a group name. |
| kTIMGroupModifyInfoFlag_Notification | Modifies a group announcement. |
| kTIMGroupModifyInfoFlag_Introduction | Modifies group introduction. |
| kTIMGroupModifyInfoFlag_FaceUrl | Modifies the URL of a group profile photo. |
| kTIMGroupModifyInfoFlag_AddOption | Modifies the option for adding a group. |
| kTIMGroupModifyInfoFlag_MaxMmeberNum | Modifies the maximum number of group members. |
| kTIMGroupModifyInfoFlag_Visible | Modifies whether the group is visible. |
| kTIMGroupModifyInfoFlag_Searchable | Modifies whether the group can be searched. |
| kTIMGroupModifyInfoFlag_ShutupAll | Modifies whether all members are muted in the group. |
| kTIMGroupModifyInfoFlag_Custom | Modifies custom information about a group. |
| kTIMGroupModifyInfoFlag_Owner | Modifies the group owner. |

### GroupModifyInfoParam

Set parameters of the group information API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupModifyInfoParamGroupId | string | Write-only (required) | Group ID |
| kTIMGroupModifyInfoParamModifyFlag | uint [TIMGroupModifyInfoFlag](#timgroupmodifyinfoflag) | Write-only (required) | Modifies the flag. Multiple values can be set with bitwise OR. |
| kTIMGroupModifyInfoParamGroupName | string | Write-only (required) | Modifies the group name. This parameter must be specified only when `modify_flag` includes `kTIMGroupModifyInfoFlag_Name`. |
| kTIMGroupModifyInfoParamNotification | string | Write-only (required) | Modifies a group announcement. This parameter must be specified only when `modify_flag` includes `kTIMGroupModifyInfoFlag_Notification`. |
| kTIMGroupModifyInfoParamIntroduction | string | Write-only (required) | Modifies group introduction. This parameter must be specified only when `modify_flag` includes `kTIMGroupModifyInfoFlag_Introduction`. |
| kTIMGroupModifyInfoParamFaceUrl | string | Write-only (required) | Modifies the URL of a group profile photo. This parameter must be specified only when `modify_flag` includes `kTIMGroupModifyInfoFlag_FaceUrl`. |
| kTIMGroupModifyInfoParamAddOption | uint | Write-only (optional) | Modifies the option for adding a group. This parameter must be specified only when `modify_flag` includes `kTIMGroupModifyInfoFlag_AddOption`. |
| kTIMGroupModifyInfoParamMaxMemberNum | uint | Write-only (optional) | Modifies the maximum number of group members. This parameter must be specified only when `modify_flag` includes `kTIMGroupModifyInfoFlag_MaxMmeberNum`. |
| kTIMGroupModifyInfoParamVisible | uint | Write-only (optional) | Modifies whether a group is visible. This parameter must be specified only when `modify_flag` includes `kTIMGroupModifyInfoFlag_Visible`. |
| kTIMGroupModifyInfoParamSearchAble | uint | Write-only (optional) | Modifies whether a group can be searched for. This parameter must be specified only when `modify_flag` includes `kTIMGroupModifyInfoFlag_Searchable`. |
| kTIMGroupModifyInfoParamIsShutupAll | bool | Write-only (optional) | Modifies whether all members are muted in a group. This parameter must be specified only when `modify_flag` includes `kTIMGroupModifyInfoFlag_ShutupAll`. |
| kTIMGroupModifyInfoParamOwner | string | Write-only (optional) | Modifies the group owner. This parameter must be specified only when `modify_flag` includes `kTIMGroupModifyInfoFlag_Owner`. In this case, `modify_flag` cannot include other values. When the group owner is modified, there is no reason to modify other information at the same time. |
| kTIMGroupModifyInfoParamCustomInfo | array [GroupInfoCustemString](#groupinfocustemstring) | Write-only (optional) | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

### GroupGetMemberInfoListParam

Obtain parameters of the group member list API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupGetMemberInfoListParamGroupId | string | Write-only (required) | Group ID |
| kTIMGroupGetMemberInfoListParamIdentifierArray | array string | Write-only (optional) | Group member ID list |
| kTIMGroupGetMemberInfoListParamOption | object [GroupMemberGetInfoOption](#groupmembergetinfooption) | Write-only (optional) | Option for obtaining group member information |
| kTIMGroupGetMemberInfoListParamNextSeq | uint64 | Write-only (optional) | Paging pull flag. This parameter is set to 0 when information is pulled for the first time. If callback is successful and the result is not 0, the results must be paginated. When an API is called to transfer information, information is pulled again until the value of this field becomes 0. |

### GroupGetMemberInfoListResult

Obtain the result of the group member list API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupGetMemberInfoListResultNexSeq | uint64 | Read-only | Flag for the next pull. The value 0 returned by the server indicates that no more data is available. Otherwise, this flag must be specified during the next data acquisition. |
| kTIMGroupGetMemberInfoListResultInfoArray | array [GroupMemberInfo](#groupmemberinfo) | Read-only | Member information list |

### TIMGroupMemberModifyInfoFlag

Set (modify) the type of group member information.

| Name | Description |
|-----|-----|
| kTIMGroupMemberModifyFlag_None | - |
| kTIMGroupMemberModifyFlag_MsgFlag | Modifies the option for receiving messages. |
| kTIMGroupMemberModifyFlag_MemberRole | Modifies a member role. |
| kTIMGroupMemberModifyFlag_ShutupTime | Modifies the mute time. |
| kTIMGroupMemberModifyFlag_NameCard | Modifies the group card. |
| kTIMGroupMemberModifyFlag_Custom | Modifies custom information about a group member. |

### GroupModifyMemberInfoParam

Set the parameters of the group member information API.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupModifyMemberInfoParamGroupId | string | Write-only (required) | Group ID |
| kTIMGroupModifyMemberInfoParamIdentifier | string | Write-only (required) | ID of the member whose information is set |
| kTIMGroupModifyMemberInfoParamModifyFlag | uint [TIMGroupMemberModifyInfoFlag](#timgroupmembermodifyinfoflag) | Write-only (required) | Modifies the type. Multiple values can be set by using the bitwise OR operator. |
| kTIMGroupModifyMemberInfoParamMsgFlag | uint | Write-only (optional) | Modifies the option for receiving messages. This parameter must be specified only when `modify_flag` includes `kTIMGroupMemberModifyFlag_MsgFlag`. |
| kTIMGroupModifyMemberInfoParamMemberRole | uint [TIMGroupMemberRole](#timgroupmemberrole) | Write-only (optional) | Modifies a member role. This parameter must be specified only when `modify_flag` includes `kTIMGroupMemberModifyFlag_MemberRole`. |
| kTIMGroupModifyMemberInfoParamShutupTime | uint | Write-only (optional) | Modifies mute time. This parameter must be specified only when `modify_flag` includes `kTIMGroupMemberModifyFlag_ShutupTime`. |
| kTIMGroupModifyMemberInfoParamNameCard | string | Write-only (optional) | Modifies a group card. This parameter must be specified only when `modify_flag` includes `kTIMGroupMemberModifyFlag_NameCard`. |
| kTIMGroupModifyMemberInfoParamCustomInfo | array [GroupMemberInfoCustemString](#groupmemberinfocustemstring) | Write-only (optional) | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

### GroupPendencyOption

Obtain parameters of the group pending information list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupPendencyOptionStartTime | uint64 | Write-only (required) | Sets the pull timestamp. This parameter is set to 0 for the first request. Later the parameter is set based on the timestamp specified by kTIMGroupPendencyResultNextStartTime of the [GroupPendencyResult](#grouppendencyresult) key returned by the server. |
| kTIMGroupPendencyOptionMaxLimited | uint | Write-only (optional) | Recommended amount of pulled information. The server can return information as required. This parameter cannot be used as a flag to indicate whether the operation is complete. |

### TIMGroupPendencyType

Pending request type.

| Name | Description |
|-----|-----|
| kTIMGroupPendency_RequestJoin | Requests to join a group. |
| kTIMGroupPendency_InviteJoin | Invites to join a group. |
| kTIMGroupPendency_ReqAndInvite | Requests and invites to join a group. |

### TIMGroupPendencyHandle

Pending group request handling status.

| Name | Description |
|-----|-----|
| kTIMGroupPendency_NotHandle | Not handled |
| kTIMGroupPendency_OtherHandle | Handled by others |
| kTIMGroupPendency_OperatorHandle | Handled by the operator |

### TIMGroupPendencyHandleResult

Pending group request handling operation type.

| Name | Description |
|-----|-----|
| kTIMGroupPendency_Refuse | Refuse |
| kTIMGroupPendency_Accept | Accept |

### GroupPendency

Pending group request information definition.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupPendencyGroupId | string | Read/Write | Group ID |
| kTIMGroupPendencyFromIdentifier | string | Read/Write | ID of the initiator. For example, for a group join request, the value is the requester. For a group invitation request, the value is the inviter. |
| kTIMGroupPendencyToIdentifier | string | Read/Write | Adjudicator ID. For a group join request, the value is "". For a group invitation request, the value is the invited user. |
| kTIMGroupPendencyAddTime | uint64 | Read-only | Time at which the pending request information was added |
| kTIMGroupPendencyPendencyType | uint [TIMGroupPendencyType](#timgrouppendencytype) | Read-only | Pending request type |
| kTIMGroupPendencyHandled | uint [TIMGroupPendencyHandle](#timgrouppendencyhandle) | Read-only | Pending group request handling status |
| kTIMGroupPendencyHandleResult | uint [TIMGroupPendencyHandleResult](#timgrouppendencyhandleresult) | Read-only | Pending group information handling operation type |
| kTIMGroupPendencyApplyInviteMsg | string | Read-only | Additional information about the request or invitation |
| kTIMGroupPendencyFromUserDefinedData | string | Read-only | Custom field of the request or invitation |
| kTIMGroupPendencyApprovalMsg | string | Read-only | Approval information: accept or refuse. |
| kTIMGroupPendencyToUserDefinedData | string | Read-only | Field defined by the approver |
| kTIMGroupPendencyKey | string | Read-only | Signature information. Customers can ignore the information. |
| kTIMGroupPendencyAuthentication | string | Read-only | Signature information. Customers can ignore the information. |
| kTIMGroupPendencySelfIdentifier | string | Read-only | Self ID |

### GroupPendencyResult

Obtain the returned pending group request information list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupPendencyResultNextStartTime | uint64 | Read-only | Start timestamp of the next pull. The value 0 returned by the server indicates that no more data is available. Otherwise, the timestamp is used as the start timestamp during the next data acquisition. |
| kTIMGroupPendencyResultReadTimeSeq | uint64 | Read-only | Timestamp of read reporting |
| kTIMGroupPendencyResultUnReadNum | uint | Read-only | Number of unread pending requests |
| kTIMGroupPendencyResultPendencyArray | array [GroupPendency](#grouppendency) | Read-only | Pending group request information list |

### GroupHandlePendencyParam

Parameters of the API for handling pending group messages.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupHandlePendencyParamIsAccept | bool | Write-only (optional) | True: accept. False: refuse. The default value is False. |
| kTIMGroupHandlePendencyParamHandleMsg | string | Write-only (optional) | Accept or refuse. The default value is a null string. |
| kTIMGroupHandlePendencyParamPendency | object [GroupPendency](#grouppendency) | Write-only (required) | Pending information details |

## Relationship Chain and Profile Key Types

Macro definitions related to relationship chains and profiles and definitions of JSON Keys accessed by related structure members.

### FriendShipGetProfileListParam

Parameters of the API for handling pending group messages.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendShipGetProfileListParamIdentifierArray | array string | Write-only | UserID list of the target user profiles to obtain |
| kTIMFriendShipGetProfileListParamForceUpdate | bool | Write-only | Whether forced update is enabled. The value false indicates profiles are preferentially obtained from the local cache. If profiles cannot be obtained from the cache, profiles are pulled from the network. The value true indicates profiles are directly pulled from the network. The default value is false. |

### TIMGenderType

User gender type.

| Name | Description |
|-----|-----|
| kTIMGenderType_Unkown | Unknown gender |
| kTIMGenderType_Male | Male |
| kTIMGenderType_Female | Female |

### TIMProfileAddPermission

Option for adding friends.

| Name | Description |
|-----|-----|
| kTIMProfileAddPermission_Unknown | Unknown |
| kTIMProfileAddPermission_AllowAny | Anyone can add friends. |
| kTIMProfileAddPermission_NeedConfirm | Requires verification when a friend is added. |
| kTIMProfileAddPermission_DenyAny | No one can add friends. |

### UserProfileCustemStringInfo

The custom profile field. The value is a string.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMUserProfileCustemStringInfoKey | string | Write-only | Key value of the custom profile field (including the prefix Tag_Profile_Custom_) |
| kTIMUserProfileCustemStringInfoValue | string | Write-only | String value corresponding to the field |

>? The string cannot contain more than 500 bytes.


### UserProfile

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMUserProfileIdentifier | string | Read-only | User ID |
| kTIMUserProfileNickName | string | Read-only | User nickname |
| kTIMUserProfileGender | uint [TIMGenderType](#timgendertype) | Read-only | Gender |
| kTIMUserProfileFaceUrl | string | Read-only | URL of the user’s profile photo |
| kTIMUserProfileSelfSignature | string | Read-only | Personal signature of the user |
| kTIMUserProfileAddPermission | uint [TIMProfileAddPermission](#timprofileaddpermission) | Read-only | Option for adding friends |
| kTIMUserProfileLocation | string | Read-only | User location information |
| kTIMUserProfileLanguage | uint | Read-only | Language |
| kTIMUserProfileBirthDay | uint | Read-only | Birthday |
| kTIMUserProfileLevel | uint | Read-only | Level |
| kTIMUserProfileRole | uint | Read-only | Role |
| kTIMUserProfileCustomStringArray | array [UserProfileCustemStringInfo](#userprofilecustemstringinfo) | Read-only | See [Custom Profile Fields](https://intl.cloud.tencent.com/document/product/1047/33520). |

### UserProfileItem

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMUserProfileItemNickName | string | Write-only | Modifies the nickname of a user. |
| kTIMUserProfileItemGender | uint [TIMGenderType](#timgendertype) | Write-only | Modifies the gender of the user. |
| kTIMUserProfileItemFaceUrl | string | Write-only | Modifies the profile photo of the user. |
| kTIMUserProfileItemSelfSignature | string | Write-only | Modifies the signature of the user. |
| kTIMUserProfileItemAddPermission | uint [TIMProfileAddPermission](#timprofileaddpermission) | Write-only | Modifies the friend adding option for the user. |
| kTIMUserProfileItemLoaction | uint | Write-only | Modifies the location. |
| kTIMUserProfileItemLanguage | uint | Write-only | Modifies the language. |
| kTIMUserProfileItemBirthDay | uint | Write-only | Modifies the birthday. |
| kTIMUserProfileItemLevel | uint | Write-only | Modifies the level. |
| kTIMUserProfileItemRole | uint | Write-only | Modifies the role. |
| kTIMUserProfileItemCustomStringArray | array [UserProfileCustemStringInfo](#userprofilecustemstringinfo) | Write-only | Modifies [Custom Profile Fields](https://intl.cloud.tencent.com/document/product/1047/33520). |

### FriendProfileCustemStringInfo

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendProfileCustemStringInfoKey | string | Write-only | Key of the friend custom profile field |
| kTIMFriendProfileCustemStringInfoValue | string | Write-only | Value of the friend custom profile field |

### FriendProfile

Friend profile.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendProfileIdentifier | string | Write-only | UserID of the friend |
| kTIMFriendProfileGroupNameArray | array string | Write-only | Friend group name list |
| kTIMFriendProfileRemark | string | Read-only | Friend remarks. This value cannot exceed 96 bytes. This field is null if you obtain your own profile. |
| kTIMFriendProfileAddWording | string | Write-only | Reason for adding a friend |
| kTIMFriendProfileAddSource | string | Write-only | Source added during friend request |
| kTIMFriendProfileAddTime | uint64 | Write-only | Time when the friend was added |
| kTIMFriendProfileUserProfile | object [UserProfile](#userprofile) | Read-only | Personal profile of the friend |
| kTIMFriendProfileCustomStringArray | array [FriendProfileCustemStringInfo](#friendprofilecustemstringinfo) | Read-only | [Custom Friend Fields](https://intl.cloud.tencent.com/document/product/1047/33521) |

### FriendProfileItem

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendProfileItemRemark | string | Write-only | Modifies the remarks of a friend. |
| kTIMFriendProfileItemGroupNameArray | array string | Write-only | Modifies the group name list of a friend. |
| kTIMFriendProfileItemCustomStringArray | array [FriendProfileCustemStringInfo](#friendprofilecustemstringinfo) | Write-only | Modifies the [Custom Friend Fields](https://intl.cloud.tencent.com/document/product/1047/33521). |

### TIMFriendType

| Name | Description |
|-----|-----|
| FriendTypeSignle | One-way friend: user B is in the friend list of user A but user A is not in the friend list of user B. |
| FriendTypeBoth | Two-way friend: user B is in the friend list of user A and user A is in the friend list of user B. |

### FriendshipAddFriendParam

Parameters of the API for adding a friend.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipAddFriendParamIdentifier | string | Write-only | UserID corresponding to the friend request |
| kTIMFriendshipAddFriendParamFriendType | uint [TIMFriendType](#timfriendtype) | Write-only | Friend type of the friend request |
| kTIMFriendshipAddFriendParamRemark | string | Write-only | Preliminary remarks |
| kTIMFriendshipAddFriendParamGroupName | string | Write-only | Preliminary group name |
| kTIMFriendshipAddFriendParamAddSource | string | Write-only | Description of the source for adding a friend |
| kTIMFriendshipAddFriendParamAddWording | string | Write-only | Friend request message |

### FriendResult

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendResultIdentifier | string | Read-only | User ID of the relationship chain operation |
| kTIMFriendResultCode | Int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Result of the relationship chain operation |
| kTIMFriendResultDesc | string | Read-only | Detailed description for the failure of a relationship chain operation |

### FriendshipModifyFriendProfileParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipModifyFriendProfileParamIdentifier | string | Write-only | UserID of the modified friend |
| kTIMFriendshipModifyFriendProfileParamItem | object [FriendProfileItem](#friendprofileitem) | Write-only | Options for the modified friend profile |

### FriendAddPendency

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendAddPendencyIdentifier | string | Read-only | UserID of the friend request initiator |
| kTIMFriendAddPendencyNickName | string | Read-only | Nickname of the friend request initiator |
| kTIMFriendAddPendencyAddSource | string | Read-only | Source of the friend request initiator |
| kTIMFriendAddPendencyAddWording | string | Read-only | Friend request message of the friend request initiator |

### TIMFriendPendencyType

| Name | Description |
|-----|-----|
| FriendPendencyTypeComeIn | Sent to the user by someone else |
| FriendPendencyTypeSendOut | Sent by the user to someone else |
| FriendPendencyTypeBoth | Two-way |

### FriendshipGetPendencyListParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipGetPendencyListParamType | uint [TIMFriendPendencyType](#timfriendpendencytype) | Write-only | Obtains the pending type of the friend request. |
| kTIMFriendshipGetPendencyListParamStartSeq | uint64 | Write-only | Obtains the pending request list sequence number of the pending request start sequence. You are advised to save `seq` and the pending list. If a request is received, enter the `seq` value returned by the server. If the `seq` is the latest on the server, no data is returned. |
| kTIMFriendshipGetPendencyListParamStartTime | uint64 | Write-only | Obtains the start timestamp of pending request information. |
| kTIMFriendshipGetPendencyListParamLimitedSize | int | Write-only | The number of items on each page of the obtained pending request information list |

### PendencyPage

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMPendencyPageStartTime | uint64 | Read-only | Start time of the pending request information page |
| kTIMPendencyPageUnReadNum | uint64 | Read-only | Number of unread messages on the pending request information page |
| kTIMPendencyPageCurrentSeq | uint64 | Read-only | Current Seq of the pending request information page |
| kTIMPendencyPagePendencyInfoArray | array [FriendAddPendencyInfo](#friendaddpendencyinfo) | Read-only | Pending request information lists on the pending request information page |

### FriendAddPendencyInfo

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendAddPendencyInfoType | uint [TIMFriendPendencyType](#timfriendpendencytype) | Read-only | Type of the pending friend request |
| kTIMFriendAddPendencyInfoIdentifier | string | Read-only | UserID of the pending friend request |
| kTIMFriendAddPendencyInfoNickName | string | Read-only | Nickname of the pending friend request |
| kTIMFriendAddPendencyInfoAddTime | uint64 | Read-only | Add time of the pending friend request |
| kTIMFriendAddPendencyInfoAddSource | string | Read-only | Source of the pending friend request |
| kTIMFriendAddPendencyInfoAddWording | string | Read-only | Fiend request message of the pending friend request |

### FriendshipDeletePendencyParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipDeletePendencyParamType | uint [TIMFriendPendencyType](#timfriendpendencytype) | Read-only | Type of the pending friend request to delete |
| kTIMFriendshipDeletePendencyParamIdentifierArray | array string | Read-only | UserID list of the pending friend request to delete |

### TIMFriendResponseAction

| Name | Description |
|-----|-----|
| ResponseActionAgree | Agree |
| ResponseActionAgreeAndAdd | Agree and add |
| ResponseActionReject | Reject |

### FriendRespone

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendResponeIdentifier | string | Write-only (required) | UserID of the friend request response |
| kTIMFriendResponeAction | uint [TIMFriendResponseAction](#timfriendresponseaction) | Write-only (required) | Action of the response to the friend request |
| kTIMFriendResponeRemark | string | Write-only (required) | Friend remarks |
| kTIMFriendResponeGroupName | string | Write-only (required) | Friend group list |

### FriendshipDeleteFriendParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipDeleteFriendParamFriendType | uint [TIMFriendType](#timfriendtype) | Write-only | Specifies the type of the friend to be deleted. |
| kTIMFriendshipDeleteFriendParamIdentifierArray | array string | Write-only (optional) | UserID list of friends to be deleted |

### FriendGroupInfo

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipCreateFriendGroupParamNameArray | Array string | Write-only | Name list of the created friend groups |
| kTIMFriendshipCreateFriendGroupParamIdentifierArray | Array string | Write-only | UserID list of friends to be added to the created friend group |

### FriendGroupInfo

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendGroupInfoName | string | Read-only | Group name |
| kTIMFriendGroupInfoCount | uint64 | Read-only | Number of friends in the current group |
| kTIMFriendGroupInfoIdentifierArray | array string | Read-only | UserID list of friends in the current group |

### FriendshipModifyFriendGroupParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipModifyFriendGroupParamName | string | Write-only | Group name to be modified |
| kTIMFriendshipModifyFriendGroupParamNewName | string | Write-only (optional) | New group name |
| kTIMFriendshipModifyFriendGroupParamDeleteIdentifierArray | array string | Write-only (optional) | List of UserIDs of friends to be deleted from the current group |
| kTIMFriendshipModifyFriendGroupParamAddIdentifierArray | Array string | Write-only (optional) | List of UserIDs of friends to be added to the current group |

### FriendshipCheckFriendTypeParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipCheckFriendTypeParamCheckType | uint [TIMFriendType](#timfriendtype) | Write-only | Type of the friend to be checked |
| kTIMFriendshipCheckFriendTypeParamIdentifierArray | array string | Write-only | List of UserIDs of friends to be checked |

### TIMFriendCheckRelation

| Name | Description |
|-----|-----|
| FriendCheckNoRelation | No relation |
| FriendCheckAWithB | B is in A’s friend list |
| FriendCheckBWithA | A is in B’s friend list |
| FriendCheckBothWay | Two-way friendship |

### FriendshipCheckFriendTypeResult

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipCheckFriendTypeResultIdentifier | string | Read-only | UserID of the checked friend |
| kTIMFriendshipCheckFriendTypeResultRelation | uint [TIMFriendCheckRelation](#timfriendcheckrelation) | Read-only | Relation between the two after successful check |
| kTIMFriendshipCheckFriendTypeResultCode | Int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Check result |
| kTIMFriendshipCheckFriendTypeResultDesc | string | Read-only | Description of friend check failure |

