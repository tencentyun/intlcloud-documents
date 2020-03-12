## Common Macros and Basic Configuration Items


### TIMResult

This macro indicates the value that is returned after an API is called.

| Parameter | Value | Description |
|-----|-----|-----|
| TIM_SUCC | 0 | Called the API successfully. |
| TIM_ERR_SDKUNINIT | -1 | Failed to call the API because the IM SDK had not been initialized. |
| TIM_ERR_NOTLOGIN | -2 | Failed to call the API because the user had not logged in. |
| TIM_ERR_JSON | -3 | Failed to call the API because the JSON format or JSON key is incorrect. |
| TIM_ERR_PARAM | -4 | Failed to call the API because a parameter was incorrect. |
| TIM_ERR_CONV | -5 | Failed to call the API because the conversation is invalid. |
| TIM_ERR_GROUP | -6 | Failed to call the API because the group is invalid. |

> If the API parameters contain the callback, the callback is called only when the API returns TIM_SUCC.


### TIMLogLogLevel

This macro indicates the log level.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMLog_Off | 0 | Disabled log output |
| kTIMLog_Verbose | 1 | Details logs during development and commissioning |
| kTIMLog_Debug | 2 | Debugging log |
| kTIMLog_Info | 3 | Information log |
| kTIMLog_Warn | 4 | Warning log |
| kTIMLog_Error | 5 | Error log |
| kTIMLog_Assert | 6 | Assertion log |

### TIMNetworkStatus

This macro indicates the connection event type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMConnected | 0 | Connected |
| kTIMDisconnected | 1 | Disconnected |
| kTIMConnecting | 2 | Connecting |
| kTIMConnectFailed | 3 | Failed to connect |

### TIMConvEvent

This macro indicates the conversation event type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMConvEvent_Add | 0 | Conversation addition. For example, this event is triggered when a new message is received and a new conversation is generated. |
| kTIMConvEvent_Del | 1 | Conversation deletion. For example, this event is triggered when you delete a conversation. |
| kTIMConvEvent_Update | 2 | Conversation update. This event is triggered when the unread message count changes in a conversation and a new message is received. |

### TIMConvType

This macro indicates the conversation type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMConv_Invalid | 0 | Invalid conversation |
| kTIMConv_C2C | 1 | Customer-to-customer (C2C) conversation |
| kTIMConv_Group | 2 | Group conversation |
| kTIMConv_System | 3 | System conversation |

### SdKConfig

This macro is used to initialize the configuration of the IM SDK.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMSdkConfigConfigFilePath | String | Write-only (optional) | Path to the configuration file, which defaults to "/" |
| kTIMSdkConfigLogFilePath | String | Write-only (optional) | Path to the log file, which defaults to "/" |

### TIMGroupMemberInfoFlag

This macro indicates the group member information flag.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupMemberInfoFlag_None | 0x00 | None |
| kTIMGroupMemberInfoFlag_JoinTime | 0x01 | Joining time |
| kTIMGroupMemberInfoFlag_MsgFlag | 0x01 << 1 | Group message receiving option |
| kTIMGroupMemberInfoFlag_MsgSeq | 0x01 << 2 | Sequence number of the message that has been read by the member |
| kTIMGroupMemberInfoFlag_MemberRole | 0x01 << 3 | Member role |
| kTIMGroupMemberInfoFlag_ShutupUntill | 0x01 << 4 | Muting period. 0: mute is disabled. |
| kTIMGroupMemberInfoFlag_NameCard | 0x01 << 5 | Group name card |

### TIMGroupMemberRoleFlag

This macro indicates the group member role flag.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupMemberRoleFlag_All | 0x00 | Obtains all role types. |
| kTIMGroupMemberRoleFlag_Owner | 0x01 | Obtains owners (group owners). |
| kTIMGroupMemberRoleFlag_Admin | 0x01 << 1 | Obtains admins excluding group owners. |
| kTIMGroupMemberRoleFlag_Member | 0x01 << 2 | Obtains common group members excluding group owners and admins. |

### GroupMemberGetInfoOption

This macro provides options for obtaining group member information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupMemberGetInfoOptionInfoFlag | Uint64 [TIMGroupMemberInfoFlag](#timgroupmemberinfoflag) | Read/Write (optional) | Filters by target information. The default value is 0xffffffff, indicating that all information is obtained. |
| kTIMGroupMemberGetInfoOptionRoleFlag | Uint64 [TIMGroupMemberRoleFlag](#timgroupmemberroleflag) | Read/Write (optional) | Filters by member role. The default value is kTIMGroupMemberRoleFlag_All, indicating that all roles are obtained. |
| kTIMGroupMemberGetInfoOptionCustomArray | Array string | Write-only (optional) | For details, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### TIMGroupGetInfoFlag

This macro indicates the group member information flag.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupInfoFlag_None | 0x00 | - |
| kTIMGroupInfoFlag_Name | 0x01 | Group name |
| kTIMGroupInfoFlag_CreateTime | 0x01 << 1 | Group creation time |
| kTIMGroupInfoFlag_OwnerUin | 0x01 << 2 | Group creator account |
| kTIMGroupInfoFlag_Seq | 0x01 << 3 | - |
| kTIMGroupInfoFlag_LastTime | 0x01 << 4 | Last modification time of group information |
| kTIMGroupInfoFlag_NextMsgSeq | 0x01 << 5 | - |
| kTIMGroupInfoFlag_LastMsgTime | 0X01 << 6 | Occurrence time of the last group message |
| kTIMGroupInfoFlag_AppId | 0x01 << 7 | - |
| kTIMGroupInfoFlag_MemberNum | 0x01 << 8 | Number of group members |
| kTIMGroupInfoFlag_MaxMemberNum | 0x01 << 9 | Maximum number of group members |
| kTIMGroupInfoFlag_Notification | 0x01 << 10 | Group announcement content |
| kTIMGroupInfoFlag_Introduction | 0x01 << 11 | Group introduction content |
| kTIMGroupInfoFlag_FaceUrl | 0x01 << 12 | Group profile photo URL |
| kTIMGroupInfoFlag_AddOpton | 0x01 << 13 | Group addition option |
| kTIMGroupInfoFlag_GroupType | 0x01 << 14 | Group type |
| kTIMGroupInfoFlag_LastMsg | 0x01 << 15 | Latest message in the group |
| kTIMGroupInfoFlag_OnlineNum | 0x01 << 16 | Number of online group members |
| kTIMGroupInfoFlag_Visible | 0x01 << 17 | Whether the group is visible |
| kTIMGroupInfoFlag_Searchable | 0x01 << 18 | Whether the group can be searched |
| kTIMGroupInfoFlag_ShutupAll | 0x01 << 19 | Whether all the members of the group are muted |

### GroupGetInfoOption

This macro provides options for obtaining group information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupGetInfoOptionInfoFlag | Uint64 [TIMGroupGetInfoFlag](#timgroupgetinfoflag) | Read/Write (optional) | Filters by target information. The default value is 0xffffffff, indicating that all information is obtained. |
| kTIMGroupGetInfoOptionCustomArray | Array string | Write-only (optional) | For details, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### UserConfig

This macro indicates user configuration.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMUserConfigIsReadReceipt | Bool | Write-only (optional) | true: the read receipt event needs to be received. |
| kTIMUserConfigIsSyncReport | Bool | Write-only (optional) | true: the server deletes messages in the read state. |
| kTIMUserConfigIsIngoreGroupTipsUnRead | Bool | Write-only (optional) | true: group tips are excluded from the read group message count. |
| kTIMUserConfigIsDisableStorage | Bool | Write-only (optional) | Indicates whether to disable local storage. true: yes. false: no. The default value is false. |
| kTIMUserConfigGroupGetInfoOption | Object [GroupGetInfoOption](#groupgetinfooption) | Write-only (optional) | Obtains the default option for group information. |
| kTIMUserConfigGroupMemberGetInfoOption | Object [GroupMemberGetInfoOption](#groupmembergetinfooption) | Write-only (optional) | Obtains the default option for group member information. |

### HttpProxyInfo

This macro indicates HTTP proxy information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMHttpProxyInfoIp | String | Write-only (required) | IP address of the proxy |
| kTIMHttpProxyInfoPort | Int | Write-only (required) | Port of the proxy |

### Socks5ProxyInfo

This macro indicates SOCKS5 proxy information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMSocks5ProxyInfoIp | String | Write-only (required) | IP address of the SOCKS5 proxy |
| kTIMSocks5ProxyInfoPort | Int | Write-only (required) | Port of the SOCKS5 proxy |
| kTIMSocks5ProxyInfoUserName | String | Write-only (optional) | Authenticated username |
| kTIMSocks5ProxyInfoPassword | String | Write-only (optional) | Authenticated password |

### SetConfig

**Update the configuration**

- Custom data
The IM SDK only passes through the data customized by developers to the IM backend. The maximum length of the custom data is 64 bytes. The developer business backend can be notified of the custom data through the third-party [state change callback](https://intl.cloud.tencent.com/document/product/1047/34357).
- HTTP proxy
The HTTP proxy uploads relevant files to the COS when sending text, voice, file, and short-video messages, and downloads relevant files to the local server when receiving text, audio, file, and short-video messages. To enable the HTTP proxy, you cannot set the IP address of the proxy to null or the port to 0. To disable the HTTP proxy, you only need to set the IP address of the proxy to null and the port to 0.
- SOCKS5 proxy
The SOCKS5 proxy must be enabled before initialization. After the SOCKS5 proxy is enabled, all protocols sent by the IM SDK are sent to the IM backend through the SOCKS5 proxy server.


| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMSetConfigLogLevel | Uint [TIMLogLevel](#timloglevel) | Write-only (optional) | Level of logs output to log files |
| kTIMSetConfigCackBackLogLevel | Uint [TIMLogLevel](#timloglevel) | Write-only (optional) | Log level for log callbacks |
| kTIMSetConfigIsLogOutputConsole | Bool | Write-only (optional) | Whether to output logs to the console |
| kTIMSetConfigUserConfig | Object [UserConfig](#userconfig) | Write-only (optional) | User configuration |
| kTIMSetConfigUserDefineData | String | Write-only (optional) | User-defined data, which must be set before initialization if any |
| kTIMSetConfigHttpProxyInfo | Object [HttpProxyInfo](#httpproxyinfo) | Write-only (optional) | Sets the HTTP proxy. The HTTP proxy (if any) must be enabled before image, file, audio, and video messages are sent. |
| kTIMSetConfigSocks5ProxyInfo | Object [Socks5ProxyInfo](#socks5proxyinfo) | Write-only (optional) | Sets the SOCKS5 proxy. The SOCKS5 proxy (if any) must be enabled before image, file, audio, and video messages are sent. |

## Key Message Types

The section describes the definitions of message-related macros and JSON keys for retrieving structure members.

### TIMMsgStatus

This macro indicates the definition of the current message state.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMMsg_Sending | 1 | The message is being sent. |
| kTIMMsg_SendSucc | 2 | The message was successfully sent. |
| kTIMMsg_SendFail | 3 | The message failed to be sent. |
| kTIMMsg_Deleted | 4 | The message was deleted. |
| kTIMMsg_LocalImported | 5 | The message was imported to the local server. |
| kTIMMsg_Revoked | 6 | The message was recalled. |

### TIMMsgPriority

This macro indicates the message priority. A greater number indicates a higher priority.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMMsgPriority_High | 0 | Indicates the highest priority. Generally, this priority is used for red packets or gift messages. |
| kTIMMsgPriority_Normal | 1 | Indicates the normal priority and the second highest. We recommend that you set the priority of common messages to Normal. |
| kTIMMsgPriority_Low | 2 | We recommend that you set the priority of like messages to Low. |
| kTIMMsgPriority_Lowest | 3 | Indicates the lowest priority. Generally, this is the priority for notifications of joining or quitting a group (sent by the backend). |

### Messages

The following describes the JSON keys of messages.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgElemArray | Array [Elem](#elem) | Read/Write (required) | Message element list |
| kTIMMsgConvId | String | Read/Write (optional) | Conversation ID of the message |
| kTIMMsgConvType | Uint [TIMConvType](#timconvtype) | Read/Write (optional) | Conversation type of the message |
| kTIMMsgSender | String | Read/Write (optional) | Message sender |
| kTIMMsgPriority | Uint [TIMMsgPriority](#timmsgpriority) | Read/Write (optional) | Message priority |
| kTIMMsgClientTime | Uint64 | Read/Write (optional) | Client time |
| kTIMMsgServerTime | Uint64 | Read/Write (optional) | Server time |
| kTIMMsgIsFormSelf | Bool | Read/Write (optional) | Whether the message comes from yourself |
| kTIMMsgIsRead | Bool | Read/Write (optional) | Whether the message has been read |
| kTIMMsgIsOnlineMsg | Bool | Read/Write (optional) | Indicates whether the message is an online message. The default value is false. false: the message is a common message. true: the message is a message that will be deleted immediately after being read. |
| kTIMMsgIsPeerRead | Bool | Read-only | Whether the message has been read by the peer of the conversation. |
| kTIMMsgStatus | Uint [TIMMsgStatus](#timmsgstatus) | Read/Write (optional) | Current status of the message |
| kTIMMsgUniqueId | Uint64 | Read-only | Unique ID of the message |
| kTIMMsgRand | Uint64 | Read-only | Random code of the message |
| kTIMMsgSeq | Uint64 | Read-only | Sequence number of the message |
| kTIMMsgCustomInt | Uint32_t | Read/Write (optional) | Custom integer value field |
| kTIMMsgCustomStr | String | Read/Write (optional) | Custom data field |

>
- Corresponding element sequence
Currently, the file and audio elements are not necessarily transferred in the sequence that they are added. Other elements are transferred in the sequence that they are added. However, we recommend that you do not process elements strictly in the Elem sequence. Instead, you should process them by type to prevent the process from crashing when an exception occurs.
- Red packet and like messages in the group
The like and red packet features are supported in the live broadcast scenario. The priority of a like message is lower than that of a red packet message. You can define specific message content by using the custom message [CustomElem](#customelem). When sending a message, you can use `kTIMMsgPriority` to define the message priority.
- Messages that are deleted immediately after being read
When `kTIMMsgIsOnlineMsg` is set to true, a message that is deleted immediately after being read is sent. This message has the following features:
 - For C2C conversations: when this message is sent, the peer can receive the message only when online. If the peer is offline when the message is sent, the peer can no longer receive this message even logging in to IM later.
 - For group conversations: when this message is sent, only online members in the group can receive the message. If a member is offline when the message is sent, the member can no longer receive this message even if logging in to IM later.
 - The server does not store this message.
 - This message is excluded from the unread message count.
 - This message is not stored locally.
- Message custom fields
Developers can add the following custom fields to messages: custom integer fields (specified by `kTIMMsgCustomInt`) and custom binary data fields (specified by `kTIMMsgCustomStr` and must be converted to the String type because JSON does not support binary transfer.) Both types of fields can be used to achieve different effects, for example, indicating whether a voice message has been played. Note that the custom fields are only stored locally and are not synchronized to the server. Therefore, these custom fields cannot be obtained on a different terminal.


### MessageReceipt

This macro indicates the message read receipt.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgReceiptConvId | String | Read-only | Conversation ID |
| kTIMMsgReceiptConvType | Uint [TIMConvType](#timconvtype) | Read-only | Conversation type |
| kTIMMsgReceiptTimeStamp | Uint64 | Read-only | Timestamp |

### TIMElemType

This macro indicates the element type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMElem_Text | 0 | Text element |
| kTIMElem_Image | 1 | Image element |
| kTIMElem_Sound | 2 | Audio element |
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

This macro indicates the element type.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMElemType | Uint [TIMElemType](#timelemtype) | Read/Write (required) | Element type |

### TextElem

This macro indicates the text element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMTextElemContent | String | Read/Write (required) | Text content |

### FaceElem

This macro indicates the emoji element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFaceElemIndex | Int | Read/Write (required) | Emoji index |
| kTIMFaceElemBuf | String | Read/Write (optional) | Extra data, which can be customized by the user. If binary data needs to be transferred, convert it to a string because JSON only supports transferring strings. |

> The IM SDK does not provide any emoji packages. If developers have an emoji package, they can use `kTIMFaceElemIndex` to store the index entry of an emoji in the emoji package. The emoji index entry is customized by the user. Alternatively, you can directly use `kTIMFaceElemBuf` to store the binary data of the emoji, which must be converted into a string because JSON does not support transferring binary data. The binary data of the emoji is customized by the user, and the IM SDK only passes through the binary data.


### LocationElem

This macro indicates the location element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMLocationElemDesc | String | Read/Write (optional) | Location description |
| kTIMLocationElemLongitude | double | Read/Write (required) | Longitude |
| kTIMLocationElemlatitude | double | Read/Write (required) | Latitude |

### TIMImageLevel

This macro indicates the image quality level.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMImageLevel_Orig | 0 | Sends the original image. |
| kTIMImageLevel_Compression | 1 | Sends the compressed image with a smaller size. This is the default value. |
| kTIMImageLevel_HD | 2 | Sends the high-definition (HD) image with a larger size. |

### ImageElem

This macro indicates the image element.

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
- Each image has three specifications, which are Original (original image), Large (large image), and Thumb (thumbnail).
 - Original refers to the original image sent by the user, and its size remains unchanged.
 - Large refers to the resulting image of proportionally compressing the original image. After compression, the height or width (whichever is smaller) is set to 720 pixels.
 - Thumb refers to another resulting image of proportionally compressing the original image. After compression, the height or width (whichever is smaller) is set to 198 pixels.
- If the size of the original image is less than 198 pixels, the original size is used for the three specifications, and no compression is required.
- If the size of the original image ranges between 198 and 720 pixels, the large image is the same as the original image, and no compression is required.
- When an image is displayed on a mobile phone, we recommend that the thumbnail be displayed first. When the user taps the thumbnail, the large image is downloaded. When the user taps the large image, the original image is downloaded. Alternatively, developers can choose to skip the large image so that the original image is directly downloaded when the user taps the thumbnail.
- When an image is displayed on a tablet or PC, due to the high resolution and availability of a Wi-Fi or wired network, we recommend that the large image be displayed directly, and the original image be downloaded when the user taps or clicks the large image.


### SoundElem

This macro indicates the sound element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMSoundElemFilePath | String | Read/Write (required) | This indicates the path of the audio file. Developers must first store the audio file and then specify the path. |
| kTIMSoundElemFileSize | Int | Read/Write (required) | The size (in seconds) of the audio file. |
| kTIMSoundElemFileTime | Int | Read/Write (required) | The duration of the audio file. |
| kTIMSoundElemFileId | String | Read-only | The ID of the audio file during download. |
| kTIMSoundElemBusinessId | Int | Read-only | The BusinessID that is used during download. |
| kTIMSoundElemDownloadFlag | Int | Read-only | Indicates whether it is necessary to apply for a download address. 0: apply from the platform. 1: apply from the COS. 2: directly use the URL for download. |
| kTIMSoundElemUrl | String | Read-only | The download URL. |
| kTIMSoundElemTaskId | Int | Read-only | The task ID. |

>
- A message custom field can be used to indicate whether an audio message file has been played. For example, the value 0 can be defined to indicate that the audio message file has not been played yet, and the value 1 can be defined to indicate that the file has been played. When the user taps Play, the value of the field can be changed to 1.
- Only one sound element can be added to a single message. If multiple sound elements are added to a message, the message may fail to be sent.


### CustomElem

This macro indicates the custom element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMCustomElemData | String | Read/Write | Data of the custom element, which can be binary data |
| kTIMCustomElemDesc | String | Read/Write | Description of the custom element |
| kTIMCustomElemExt | String | Read/Write | Ext field pushed by the backend |
| kTIMCustomElemSound | String | Read/Write | Custom sound |

> When built-in message types cannot meet special requirements, developers can customize message formats. The content of each custom message fully depends on developers, and the IM SDK only passes through the content.


### FileElem

This macro indicates the file element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFileElemFilePath | String | Read/Write (required) | The file path (including the file name). |
| kTIMFileElemFileName | String | Read/Write (optional) | The displayed file name. If this parameter is not specified, kTIMFileElemFileName uses the file name in the file path specified by kTIMFileElemFilePath by default. |
| kTIMFileElemFileSize | Int | Read/Write (required) | The file size. |
| kTIMFileElemFileId | String | Read-only | The UUID during file download. |
| kTIMFileElemBusinessId | Int | Read-only | The BusinessID that is used during download. |
| kTIMFileElemDownloadFlag | Int | Read-only | The file download flag. |
| kTIMFileElemUrl | String | Read-only | The file download URL. |
| kTIMFileElemTaskId | Int | Read-only | The task ID. |

> Only one file element can be added to a single message. If multiple file elements are added to a message, the message may fail to be sent.


### VideoElem

This macro indicates the video element.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMVideoElemVideoType | String | Read/Write (required) | Type of the video file, which is set when a message is sent |
| kTIMVideoElemVideoSize | Uint | Read/Write (required) | Size of the video file |
| kTIMVideoElemVideoDuration | Uint | Read/Write (required) | Duration of the video file, which is set when a message is sent |
| kTIMVideoElemVideoPath | String | Read/Write (required) | Path of the video file |
| kTIMVideoElemVideoId | String | Read-only | UUID when the video file is downloaded |
| kTIMVideoElemBusinessId | Int | Read-only | BusinessID that is used during download |
| kTIMVideoElemVideoDownloadFlag | Int | Read-only | Video file download flag |
| kTIMVideoElemVideoUrl | String | Read-only | URL for downloading the video file |
| kTIMVideoElemImageType | String | Read/Write (required) | Type of the screenshot file, which is set when a message is sent |
| kTIMVideoElemImageSize | Uint | Read/Write (required) | Size of the screenshot file |
| kTIMVideoElemImageWidth | Uint | Read/Write (required) | Width of the screenshot, which is set when a message is sent |
| kTIMVideoElemImageHeight | Uint | Read/Write (required) | Height of the screenshot, which is set when a message is sent |
| kTIMVideoElemImagePath | String | Read/Write (required) | Storage path of the screenshot |
| kTIMVideoElemImageId | String | Read-only | ID that is used when the video screenshot is downloaded |
| kTIMVideoElemImageDownloadFlag | Int | Read-only | Screenshot file download flag |
| kTIMVideoElemImageUrl | String | Read-only | URL that is used to download the screenshot file |
| kTIMVideoElemTaskId | Uint | Read-only | Task ID |

### TIMGroupTipGroupChangeFlag

This macro indicates the group information change type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupTipChangeFlag_Name | 0xa | Change to the group name |
| kTIMGroupTipChangeFlag_Introduction | 11 | Change to the group introduction |
| kTIMGroupTipChangeFlag_Notification | 12 | Change to the group announcement |
| kTIMGroupTipChangeFlag_FaceUrl | 13 | Change to the group profile photo URL |
| kTIMGroupTipChangeFlag_Owner | 14 | Change to the group owner |

### GroupTipGroupChangeInfo

This macro is used to change group information and is valid for group system messages.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupTipGroupChangeInfoFlag | Uint [TIMGroupTipGroupChangeFlag](#timgrouptipgroupchangeflag) | Read-only | Group information change flag for group messages |
| kTIMGroupTipGroupChangeInfoValue | String | Read-only | This indicates the value after the change. Different `info_flag` fields have different meanings. |

### GroupTipMemberChangeInfo

This macro is used to mute group members and is valid for group system messages.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupTipMemberChangeInfoIdentifier | String | Read-only | Group member ID |
| kTIMGroupTipMemberChangeInfoShutupTime | Uint | Read-only | Muting period |

### TIMGroupTipType

This macro indicates the group system message type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupTip_None | 0 | Prompt for an invalid group |
| kTIMGroupTip_Invite | 1 | Prompt for inviting a user to the group |
| kTIMGroupTip_Quit | 2 | Prompt for quitting a group |
| kTIMGroupTip_Kick | 3 | Prompt for removing a member from a group |
| kTIMGroupTip_SetAdmin | 4 | Prompt for setting an admin |
| kTIMGroupTip_CancelAdmin | 5 | Prompt for canceling an admin |
| kTIMGroupTip_GroupInfoChange | 6 | Prompt for modifying group information |
| kTIMGroupTip_MemberInfoChange | 7 | Prompt for modifying group member information |

### GroupTipsElem

This macro indicates the group system message element (for all group members).

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupTipsElemTipType | Uint [TIMGroupTipType](#timgrouptiptype) | Read-only | Group message type |
| kTIMGroupTipsElemOpUser | String | Read-only | Operator ID |
| kTIMGroupTipsElemGroupName | String | Read-only | Group name |
| kTIMGroupTipsElemGroupId | String | Read-only | Group ID |
| kTIMGroupTipsElemTime | Uint | Read-only | Group message time |
| kTIMGroupTipsElemUserArray | Array string | Read-only | List of operated accounts |
| kTIMGroupTipsElemGroupChangeInfoArray | Array [GroupTipGroupChangeInfo](#grouptipgroupchangeinfo) | Read-only | Group profile change information list, which is valid only when `tips_type` is set to `kTIMGroupTip_GroupInfoChange` |
| kTIMGroupTipsElemMemberChangeInfoArray | Array [GroupTipMemberChangeInfo](#grouptipmemberchangeinfo) | Read-only | Group member change information list, which is valid only when `tips_type` is set to `kTIMGroupTip_MemberInfoChange` |
| kTIMGroupTipsElemOpUserInfo | Object [UserProfile](#userprofile) | Read-only | Profile of the operator |
| kTIMGroupTipsElemOpGroupMemberInfo | Object [GroupMemberInfo](#groupmemberinfo) | Read-only | Group member information |
| kTIMGroupTipsElemChangedUserInfoArray | Array [UserProfile](#userprofile) | Read-only | Operated user information list |
| kTIMGroupTipsElemChangedGroupMemberInfoArray | Array [GroupMemberInfo](#groupmemberinfo) | Read-only | Group member information list |
| kTIMGroupTipsElemMemberNum | Uint | Read-only | Current number of group members, which is valid only when `tips_type` is set to `kTIMGroupTip_Invite`, `kTIMGroupTip_Quit`, or `kTIMGroupTip_Kick` |
| kTIMGroupTipsElemPlatform | String | Read-only | Operator platform information |

### TIMGroupReportType

This macro indicates the group system notification type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupReport_None | 0 | Unknown type |
| kTIMGroupReport_AddRequest | 1 | Application to join a group. This notification can only be received by the admin. |
| kTIMGroupReport_AddAccept | 2 | Application to join a group has been approved. This notification can only be received by the applicant. |
| kTIMGroupReport_AddRefuse | 3 | Application to join a group has been rejected. This notification can only be received by the applicant. |
| kTIMGroupReport_BeKicked | 4 | Removed from the group by the admin. This notification can only be received by the member who is removed from the group. |
| kTIMGroupReport_Delete | 5 | The group is dismissed. This notification can be received by all members of the group. |
| kTIMGroupReport_Create | 6 | The group is created. This notification can only be received by the creator and is not displayed. |
| kTIMGroupReport_Invite | 7 | A user is invited to a group. This notification can only be received by the invitee. |
| kTIMGroupReport_Quit | 8 | A user quits a group. This notification can only be received by the member who quits the group and is not displayed. |
| kTIMGroupReport_GrantAdmin | 9 | A user is set as the admin. This notification can only be received by the user who is set as an admin. |
| kTIMGroupReport_CancelAdmin | 10 | A user is canceled to be the admin. This notification can only be received by the user whose admin role is canceled. |
| kTIMGroupReport_RevokeAdmin | 11 | A group is revoked. This notification can be received by all members of the group and is not displayed. |
| kTIMGroupReport_InviteReq | 12 | A user is invited to a group. This notification can only be received by the invitee. |
| kTIMGroupReport_InviteAccept | 13 | The invitation to a group has been approved. This notification can only be received by the inviter. |
| kTIMGroupReport_InviteRefuse | 14 | The invitation to a group has been rejected. This notification can only be received by the inviter. |
| kTIMGroupReport_ReadedSync | 15 | The read report has been synchronized across multiple terminals. This notification can only be received by the reporter. |
| kTIMGroupReport_UserDefine | 16 | A user-defined notification. This notification can be received by all members of the group by default. |

### GroupReportElem

This macro indicates the group system notification element (for individual users).

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupReportElemReportType | Uint [TIMGroupReportType](#timgroupreporttype) | Read-only | Type |
| kTIMGroupReportElemGroupId | String | Read-only | Group ID |
| kTIMGroupReportElemGroupName | String | Read-only | Group name |
| kTIMGroupReportElemOpUser | String | Read-only | Operator ID |
| kTIMGroupReportElemMsg | String | Read-only | Cause of the operation |
| kTIMGroupReportElemUserData | String | Read-only | Custom data entered by the operator |
| kTIMGroupReportElemOpUserInfo | Object [UserProfile](#userprofile) | Read-only | Profile of the operator |
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
| kTIMProfileChangeElemFromIndentifier | String | Read-only | Change to the UserID in the user profile |
| kTIMProfileChangeElemUserProfileItem | Object [UserProfileItem](#userprofileitem) | Read-only | Specific change information, which is valid only when `change_type` is set to `kTIMProfileChange_Profile` |

### TIMFriendChangeType

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMFriendChange_None | 0 | Unknown type |
| kTIMFriendChange_FriendAdd | 1 | Added a friend |
| kTIMFriendChange_FriendDel | 2 | Deleted a friend |
| kTIMFriendChange_PendencyAdd | 3 | Added a pending request |
| kTIMFriendChange_PendencyDel | 4 | Synchronized deleted pending requests across multiple terminals |
| kTIMFriendChange_BlackListAdd | 5 | Added a user to the blacklist |
| kTIMFriendChange_BlackListDel | 6 | Deleted a user from the blacklist |
| kTIMFriendChange_PendencyReadedReport | 7 | Reported read pending requests |
| kTIMFriendChange_FriendProfileUpdate | 8 | Updated a friend’s profile |
| kTIMFriendChange_FriendGroupAdd | 9 | Added a group |
| kTIMFriendChange_FriendGroupDel | 10 | Deleted a group |
| kTIMFriendChange_FriendGroupModify | 11 | Modified a group |

### FriendProfileUpdate

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendProfileUpdateIdentifier | String | Write-only | UserID of a friend whose profile is updated |
| kTIMFriendProfileUpdateItem | Object [FriendProfileItem](#friendprofileitem) | Write-only | Updated profile item |

### FriendChangeElem

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendChangeElemChangeType | Uint [TIMFriendChangeType](#timfriendchangetype) | Read-only | Profile change type |
| kTIMFriendChangeElemFriendAddIdentifierArray | Array string | Read-only | List of added friend UserIDs, which is valid only when `change_type` is set to `kTIMFriendChange_FriendAdd` |
| kTIMFriendChangeElemFriendDelIdentifierArray | Array string | Read-only | List of deleted friend UserIDs, which is valid only when `change_type` is set to `kTIMFriendChange_FriendDel` |
| kTIMFriendChangeElemFriendAddPendencyItemArray | Array [FriendAddPendency](#friendaddpendency) | Read-only | List of pending friend requests, which is valid only when `change_type` is set to `kTIMFriendChange_PendencyAdd` |
| kTIMFriendChangeElemPendencyDelIdentifierArray | Array string | Read-only | List of deleted pending friend requests, which is valid only when `change_type` is set to `kTIMFriendChange_PendencyDel` |
| kTIMFriendChangeElemPendencyReadedReportTimestamp | Uint64 | Read-only | Timestamp for reporting pending requests, which is valid only when `change_type` is set to `kTIMFriendChange_PendencyReadedReport` |
| kTIMFriendChangeElemBlackListAddIdentifierArray | Array string | Read-only | List of UserIDs added to the blacklist, which is valid only when `change_type` is set to `kTIMFriendChange_BlackListAdd` |
| kTIMFriendChangeElemBlackListDelIdentifierArray | Array string | Read-only | List of UserIDs deleted from the blacklist, which is valid only when `change_type` is set to `kTIMFriendChange_BlackListDel` |
| kTIMFriendChangeElemFreindProfileUpdateItemArray | Array [FriendProfileUpdate](#friendprofileupdate) | Read-only | Friend profile update list, which is valid only when `change_type` is set to `kTIMFriendChange_FriendProfileUpdate` |
| kTIMFriendChangeElemFriendGroupAddIdentifierArray | Array string | Read-only | List of added friend groups, which is valid only when `change_type` is set to `kTIMFriendChange_FriendGroupAdd` |
| kTIMFriendChangeElemFriendGroupDelIdentifierArray | Array string | Read-only | List of deleted friend groups, which is valid only when `change_type` is set to `kTIMFriendChange_FriendGroupDel` |
| kTIMFriendChangeElemFriendGroupModifyIdentifierArray | Array string | Read-only | List of modified friend groups, which is valid only when `change_type` is set to `kTIMFriendChange_FriendGroupModify` |

### MsgBatchSendParam

This macro provides the parameters of the API for sending messages in batches.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgBatchSendParamIdentifierArray | Array string | Write-only (required) | List of IDs for batch sending |
| kTIMMsgBatchSendParamMsg | Object [Message](#message) | Write-only (required) | Messages that are sent in batches |

### MsgBatchSendResult

This macro indicates the result returned by the API for sending messages in batches.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgBatchSendResultIdentifier | String | Read-only | Single ID for batch sending |
| kTIMMsgBatchSendResultCode | Int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Result of message batch sending |
| kTIMMsgBatchSendResultDesc | String | Read-only | Description of message sending |
| kTIMMsgBatchSendResultMsg | Object [Message](#message) | Read-only | Sent messages |

### MsgLocator

This macro indicates the message locator.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgLocatorConvId | Bool | Read/Write | Whether the message to be searched for has been recalled. true: yes. false: no. The default value is false. |
| kTIMMsgLocatorConvType | Bool | Read/Write | Whether the message to be searched for has been recalled. true: yes. false: no. The default value is false. |
| kTIMMsgLocatorIsRevoked | bool | Read/write (required) | Whether the message to be searched for has been recalled. true: yes. false: no. The default value is false. |
| kTIMMsgLocatorTime | Uint64 | Read/Write (required) | Timestamp of the message to be searched for |
| kTIMMsgLocatorSeq | Uint64 | Read/Write (required) | Sequence number of the message to be searched for |
| kTIMMsgLocatorIsSelf | Bool | Read/Write (required) | Whether the sender of the message to be searched for is yourself. true: yes. false: no. The default value is false. |
| kTIMMsgLocatorRand | Uint64 | Read/Write (required) | Random code of the message to be searched for |
| kTIMMsgLocatorUniqueId | Uint64 | Read/Write (required) | Unique ID of the message to be searched for |

### MsgGetMsgListParam

This macro provides the parameters of the API for obtaining messages.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgGetMsgListParamLastMsg | Object [Message](#message) | Write-only (optional) | Specified message, which cannot be null |
| kTIMMsgGetMsgListParamCount | Uint | Write-only (optional) | Number of messages that are counted starting from the specified message |
| kTIMMsgGetMsgListParamIsRamble | Bool | Write-only (optional) | Whether the messages are roaming messages |
| kTIMMsgGetMsgListParamIsForward | Bool | Write-only (optional) | Whether the messages are forward sequenced |

### MsgDeleteParam

This macro provides the parameters of the API for deleting messages.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgDeleteParamMsg | Object [Message](#message) | Write-only (optional) | Specified message to be deleted from the conversation |
| kTIMMsgDeleteParamIsRamble | Bool | Write-only (optional) | Whether to delete all local or roaming messages. true: delete roaming messages. false: delete local messages. The default value is false. |

### TIMDownloadType

This macro indicates the UUID type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMDownload_VideoThumb | 0 | Video thumbnail |
| kTIMDownload_File | 1 | File |
| kTIMDownload_Video | 2 | Video |
| kTIMDownload_Sound | 3 | Sound |

### DownloadElemParam

This macro provides the parameters of the API for downloading elements.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgDownloadElemParamFlag | Uint | Write-only | Element download type, which is extracted from the message element |
| kTIMMsgDownloadElemParamType | Uint [TIMDownloadType](#timdownloadtype) | Write-only | Element type, which is extracted from the message element |
| kTIMMsgDownloadElemParamId | String | Write-only | Element ID, which is extracted from the message element |
| kTIMMsgDownloadElemParamBusinessId | Uint | Write-only | Element BusinessID, which is extracted from the message element |
| kTIMMsgDownloadElemParamUrl | String | Write-only | Element URL, which is extracted from the message element |

### MsgDownloadElemResult

This macro indicates the result returned by the API for downloading elements.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMMsgDownloadElemResultCurrentSize | Uint | Read-only | Size of currently downloaded data |
| kTIMMsgDownloadElemResultTotalSize | Uint | Read-only | Total size of the files to be downloaded |

## Conversation Key Types

The following describes the definitions of conversation-related macros and JSON keys for retrieving structure members.

### Drafts

This macro indicates draft information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMDraftMsg | Object [Message](#message) | Read-only | Message in the draft |
| kTIMDraftUserDefine | String | Read-only | User-defined data |
| kTIMDraftEditTime | Uint | Read-only | Last edit time of the draft |

### ConvInfo

This macro indicates conversation information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMConvId | String | Read-only | Conversation ID |
| kTIMConvType | Uint [TIMConvType](#timconvtype) | Read-only | Conversation type |
| kTIMConvOwner | String | Read-only | Conversation owner |
| kTIMConvUnReadNum | Uint64 | Read-only | Unread conversation count |
| kTIMConvActiveTime | Uint64 | Read-only | Conversation activation time |
| kTIMConvIsHasLastMsg | Bool | Read-only | Whether the conversation has the last message |
| kTIMConvLastMsg | Object [Message](#message) | Read-only | Last message of the conversation |
| kTIMConvIsHasDraft | Bool | Read-only | Whether the conversation has a draft |
| kTIMConvDraft | Object [Draft](#draft) | Read-only (optional) | Conversation draft |

## Group Key Types

The following describes the definitions of group-related macros and JSON keys for retrieving structure members.

### TIMGroupAddOption

This macro indicates the group addition option.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupAddOpt_Forbid | 0 | Prohibit adding to the group |
| kTIMGroupAddOpt_Auth | 1 | Require the admin’s approval |
| kTIMGroupAddOpt_Any | 2 | Anyone can be added to the group |

### TIMGroupType

This macro indicates the group type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroup_Public | 0 | Public group |
| kTIMGroup_Private | 1 | Private group |
| kTIMGroup_ChatRoom | 2 | Chatroom |
| kTIMGroup_BChatRoom | 3 | Broadcasting chatroom |
| kTIMGroup_AVChatRoom | 4 | Audio-and-video chatroom |

### TIMGroupMemberRole

This macro indicates the group member role.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMMemberRole_Normal | 0 | Common group member |
| kTIMMemberRole_Admin | 1 | Admin |
| kTIMMemberRole_SuperAdmin | 2 | Super admin |

### GroupMemberInfoCustemString

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupMemberInfoCustemStringInfoKey | String | Write-only | Key of the custom field |
| kTIMGroupMemberInfoCustemStringInfoValue | String | Write-only | Value of the custom field |

### GroupMemberInfo

This macro indicates group member information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupMemberInfoIdentifier | String | Read/wite (required) | ID of the group member |
| kTIMGroupMemberInfoJoinTime | Uint | Read-only | Joining time of the group member |
| kTIMGroupMemberInfoMemberRole | Uint [TIMGroupMemberRole](#timgroupmemberrole) | Read/wite (required) | Role of the group member |
| kTIMGroupMemberInfoMsgFlag | Uint | Read-only | Message receiving option for group members |
| kTIMGroupMemberInfoMsgSeq | Uint | Read-only | - |
| kTIMGroupMemberInfoShutupTime | Uint | Read-only | Muting period of the group member |
| kTIMGroupMemberInfoNameCard | String | Read-only | Group name card of the group member |
| kTIMGroupMemberInfoCustomInfo | Array [GroupMemberInfoCustemString](#groupmemberinfocustemstring) | Read-only | For details, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### GroupInfoCustemString

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupInfoCustemStringInfoKey | String | Write-only | Key of the custom field |
| kTIMGroupInfoCustemStringInfoValue | String | Write-only | Value of the custom field |

### CreateGroupParam

This macro provides the parameters of the API for creating a group.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMCreateGroupParamGroupName | String | Write-only (required) | The group name. |
| kTIMCreateGroupParamGroupId | String | Write-only (optional) | The group ID. If this field is not specified, the callback triggered when the group is successfully created will return a group ID allocated by the backend. |
| kTIMCreateGroupParamGroupType | Uint [TIMGroupType](#timgrouptype) | Write-only (optional) | The group type, which defaults to Public. |
| kTIMCreateGroupParamGroupMemberArray | Array [GroupMemberInfo](#groupmemberinfo) | Write-only (optional) | The array of initial members of the group. |
| kTIMCreateGroupParamNotification | String | Write-only (optional) | The group announcement. |
| kTIMCreateGroupParamIntroduction | String | Write-only (optional) | The group introduction. |
| kTIMCreateGroupParamFaceUrl | String | Write-only (optional) | The group profile photo URL. |
| kTIMCreateGroupParamAddOption | Uint [TIMGroupAddOption](#timgroupaddoption) | Write-only (optional) | The group addition option, which defaults to Any. |
| kTIMCreateGroupParamMaxMemberCount | Uint | Write-only (optional) | The maximum number of members in the group. |
| kTIMCreateGroupParamCustomInfo | Array [GroupInfoCustemString](#groupinfocustemstring) | Read-only (optional) | For details, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### CreateGroupResult

This macro indicates the result returned by the API for creating a group.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMCreateGroupResultGroupId | String | Read-only | ID of the created group |

### GroupInviteMemberParam

This macro provides the parameters of the API for inviting members.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupInviteMemberParamGroupId | String | Write-only (required) | Group ID |
| kTIMGroupInviteMemberParamIdentifierArray | Array string | Write-only (required) | Array of the IDs of users who are invited to the group |
| kTIMGroupInviteMemberParamUserData | String | Write-only (optional) | User-defined data |

### HandleGroupMemberResult

This macro indicates basic group information.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupMember_HandledErr | 0 | Failed |
| kTIMGroupMember_HandledSuc | 1 | Succeeded |
| kTIMGroupMember_Included | 2 | Already a group member |
| kTIMGroupMember_Invited | 3 | Already invited |

### GroupInviteMemberResult

This macro indicates the result returned by the API for inviting members.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupInviteMemberResultIdentifier | String | Read-only | ID of the user who was invited to the group |
| kTIMGroupInviteMemberResultResult | Uint [HandleGroupMemberResult](#handlegroupmemberresult) | Read-only | Invitation result |

### GroupDeleteMemberParam

This macro provides the parameters of the API for deleting members.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupDeleteMemberParamGroupId | String | Write-only (required) | Group ID |
| kTIMGroupDeleteMemberParamIdentifierArray | Array string | Write-only (required) | Array of the IDs of users who are deleted from the group |
| kTIMGroupDeleteMemberParamUserData | String | Write-only (optional) | User-defined data |

### GroupDeleteMemberResult

This macro indicates the result returned by the API for deleting members.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupDeleteMemberResultIdentifier | String | Read-only | ID of the deleted member |
| kTIMGroupDeleteMemberResultResult | Uint [HandleGroupMemberResult](#handlegroupmemberresult) | Read-only | Deletion result |

### TIMGroupReceiveMessageOpt

This macro indicates the group message receiving option.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMRecvGroupMsgOpt_ReceiveAndNotify | 0 | Receive group messages and notify recipients |
| kTIMRecvGroupMsgOpt_NotReceive | 1 | Do not receive group messages, and the server will not forward group messages |
| kTIMRecvGroupMsgOpt_ReceiveNotNotify | 2 | Receive group message but do not notify recipients |

### GroupSelfInfo

This macro indicates personal information in the group.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupSelfInfoJoinTime | Uint | Read-only | Time when the user joins the group |
| kTIMGroupSelfInfoRole | Uint | Read-only | Role of the user in the group |
| kTIMGroupSelfInfoUnReadNum | Uint | Read-only | Unread message count |
| kTIMGroupSelfInfoMsgFlag | Uint [TIMGroupReceiveMessageOpt](#timgroupreceivemessageopt) | Read-only | Group message receiving option |

### GroupBaseInfo

This macro indicates the result (basic group information) returned by the API for obtaining the list of groups that a user has joined.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupBaseInfoGroupId | String | Read-only | Group ID |
| kTIMGroupBaseInfoGroupName | String | Read-only | Group name |
| kTIMGroupBaseInfoGroupType | String [TIMGroupType](#timgrouptype) | Read-only | Group type |
| kTIMGroupBaseInfoFaceUrl | String | Read-only | Group profile photo URL |
| kTIMGroupBaseInfoInfoSeq | Uint | Read-only | Sequence number of the group profile, which increments by one each time the group profile is modified |
| kTIMGroupBaseInfoLastestSeq | Uint | Read-only | Indicates the sequence number of the latest message in the group. Each message in the group has a unique sequence number, which is serial based on the message sending sequence. The value of LastestSeq starts from 1 and increments by 1 each time a message is added to the group. |
| kTIMGroupBaseInfoReadedSeq | Uint | Read-only | Sequence number of the read message in the group |
| kTIMGroupBaseInfoMsgFlag | Uint | Read-only | Message receiving option |
| kTIMGroupBaseInfoIsShutupAll | Bool | Read-only | Whether the mute all feature is enabled for the group |
| kTIMGroupBaseInfoSelfInfo | Object [GroupSelfInfo](#groupselfinfo) | Read-only | Personal information of the user in the group |

### GroupDetailInfo

This macro indicates group details.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupDetialInfoGroupId | String | Read-only | Group ID |
| kTIMGroupDetialInfoGroupType | Uint [TIMGroupType](#timgrouptype) | Read-only | Group type |
| kTIMGroupDetialInfoGroupName | String | Read-only | Group ID |
| kTIMGroupDetialInfoNotification | String | Read-only | Group announcement |
| kTIMGroupDetialInfoIntroduction | String | Read-only | Group introduction |
| kTIMGroupDetialInfoFaceUrl | String | Read-only | Group profile photo URL |
| kTIMGroupDetialInfoCreateTime | Uint | Read-only | Group creation time |
| kTIMGroupDetialInfoInfoSeq | Uint | Read-only | Sequence number of the group profile, which increments by one each time the group profile is modified. |
| kTIMGroupDetialInfoLastInfoTime | Uint | Read-only | Last modification time of group information |
| kTIMGroupDetialInfoNextMsgSeq | Uint | Read-only | Sequence number of the latest message in the group |
| kTIMGroupDetialInfoLastMsgTime | Uint | Read-only | Occurrence time of the latest message in the group |
| kTIMGroupDetialInfoMemberNum | Uint | Read-only | Current number of members in the group |
| kTIMGroupDetialInfoMaxMemberNum | Uint | Read-only | Maximum number of members in the group |
| kTIMGroupDetialInfoAddOption | Uint [TIMGroupAddOption](#timgroupaddoption) | Read-only | Group addition option |
| kTIMGroupDetialInfoOnlineMemberNum | Uint | Read-only | Number of online members in the group |
| kTIMGroupDetialInfoVisible | Uint | Read-only | Whether group members are visible to non-members. |
| kTIMGroupDetialInfoSearchable | Uint | Read-only | Whether the group can be searched for |
| kTIMGroupDetialInfoIsShutupAll | Bool | Read-only | Whether the mute all feature is enabled for the group |
| kTIMGroupDetialInfoOwnerIdentifier | String | Read-only | ID of the group owner |
| kTIMGroupDetialInfoCustomInfo | Array [GroupInfoCustemString](#groupinfocustemstring) | Read-only | For details, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### GetGroupInfoResult

This macro indicates the result returned by the API for obtaining the group information list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGetGroupInfoResultCode | Int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Result of obtaining group details |
| kTIMGetGroupInfoResultDesc | String | Read-only | Description of the failure to obtain group details |
| kTIMGetGroupInfoResultInfo | JSON Object [GroupDetailInfo](#groupdetailinfo) | Read-only | Group details |

### TIMGroupModifyInfoFlag

This macro indicates the group information configuration (modification) type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupModifyInfoFlag_None | 0x00 | - |
| kTIMGroupModifyInfoFlag_Name | 0x01 | Modification of the group name |
| kTIMGroupModifyInfoFlag_Notification | 0x01 << 1 | Modification of the group announcement |
| kTIMGroupModifyInfoFlag_Introduction | 0x01 << 2 | Modification of the group introduction |
| kTIMGroupModifyInfoFlag_FaceUrl | 0x01 << 3 | Modification of the group profile photo URL |
| kTIMGroupModifyInfoFlag_AddOption | 0x01 << 4 | Modification of the group addition option |
| kTIMGroupModifyInfoFlag_MaxMmeberNum | 0x01 << 5 | Modification of the maximum number of members in the group |
| kTIMGroupModifyInfoFlag_Visible | 0x01 << 6 | Modification of whether the group is visible |
| kTIMGroupModifyInfoFlag_Searchable | 0x01 << 7 | Modification of whether the group can be searched for |
| kTIMGroupModifyInfoFlag_ShutupAll | 0x01 << 8 | Modification of whether the mute all feature is enabled for the group |
| kTIMGroupModifyInfoFlag_Owner | 0x01 << 31 | Modification of the group owner |

### GroupModifyInfoParam

This macro provides the parameters of the API for modifying group information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupModifyInfoParamGroupId | String | Write-only (required) | The group ID. |
| kTIMGroupModifyInfoParamModifyFlag | Uint [TIMGroupModifyInfoFlag](#timgroupmodifyinfoflag) | Write-only (required) | Modifies the flag. You can set multiple values, and the bit-wise OR result of these values will be used. |
| kTIMGroupModifyInfoParamGroupName | String | Write-only (optional) | Modifies the group name. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Name`. |
| kTIMGroupModifyInfoParamNotification | String | Write-only (optional) | Modifies the group announcement. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Notification`. |
| kTIMGroupModifyInfoParamIntroduction | String | Write-only (optional) | Modify the group introduction. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Introduction`. |
| kTIMGroupModifyInfoParamFaceUrl | String | Write-only (optional) | Modifies the group profile photo URL. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_FaceUrl`. |
| kTIMGroupModifyInfoParamAddOption | String | Write-only (optional) | Modifies the group addition option. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_AddOption`. |
| kTIMGroupModifyInfoParamMaxMemberNum | Uint | Write-only (optional) | Modifies the maximum number of members in the group. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_MaxMmeberNum`. |
| kTIMGroupModifyInfoParamVisible | Uint | Write-only (optional) | Modifies whether the group is visible. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Visible`. |
| kTIMGroupModifyInfoParamSearchAble | Uint | Write-only (optional) | Modifies whether the group can be searched for. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Searchable`. |
| kTIMGroupModifyInfoParamIsShutupAll | Bool | Write-only (optional) | Modifies whether the mute all feature is enabled for the group. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_ShutupAll`. |
| kTIMGroupModifyInfoParamOwner | String | Write-only (optional) | Modifies the group owner. This field is required only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Owner`. In this case, `modify_flag` cannot contain other values because modifying other information is meaningless when the group owner is modified. |
| kTIMGroupModifyInfoParamCustomInfo | Array [GroupInfoCustemString](#groupinfocustemstring) | Write-only (optional) | For details, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### GroupGetMemberInfoListParam

This macro provides the parameters of the API for obtaining the group member list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupGetMemberInfoListParamGroupId | String | Write-only (required) | Group ID |
| kTIMGroupGetMemberInfoListParamIdentifierArray | Array string | Write-only (optional) | List of group member IDs |
| kTIMGroupGetMemberInfoListParamOption | Object [GroupMemberGetInfoOption](#groupmembergetinfooption) | Write-only (optional) | Option for obtaining group member information |
| kTIMGroupGetMemberInfoListParamNextSeq | Uint64 | Write-only (optional) | Indicates the pagination pulling flag. It is set to 0 for the initial pull attempt. If the callback succeeds and the result is not 0, pagination is required. The value of this field is passed in for the next pulling attempt until the value becomes 0. |

### GroupGetMemberInfoListResult

This macro indicates the result returned by the API for obtaining the group member list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupGetMemberInfoListResultNexSeq | Uint64 | Read-only | The next pulling flag. If the server returns 0, no more data can be pulled. Otherwise, this flag must be included when the API is called again to obtain data. |
| kTIMGroupGetMemberInfoListResultInfoArray | Array [GroupMemberInfo](#groupmemberinfo) | Read-only | The member information list. |

### TIMGroupMemberModifyInfoFlag

This macro indicates the configuration (modification) type of group member information.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupMemberModifyFlag_None | 0x00 | - |
| kTIMGroupMemberModifyFlag_MsgFlag | 0x01 | Modification of the message receiving option |
| kTIMGroupMemberModifyFlag_MemberRole | 0x01 << 1 | Modification of the member role |
| kTIMGroupMemberModifyFlag_ShutupTime | 0x01 << 2 | Modification of the muting period |
| kTIMGroupMemberModifyFlag_NameCard | 0x01 << 3 | Modification of the group name card |

### GroupModifyMemberInfoParam

This macro provides the parameters of the API for setting group member information.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupModifyMemberInfoParamGroupId | String | Write-only (required) | Group ID |
| kTIMGroupModifyMemberInfoParamIdentifier | String | Write-only (required) | ID of the member whose information is set |
| kTIMGroupModifyMemberInfoParamModifyFlag | Uint [TIMGroupMemberModifyInfoFlag](#timgroupmembermodifyinfoflag) | Write-only (required) | Indicates the modification type. You can set multiple values, and the bit-wise OR result of these values will be used. |
| kTIMGroupModifyMemberInfoParamMsgFlag | Uint | Write-only (optional) | Modifies the message receiving option. This field is required only when `modify_flag` contains `kTIMGroupMemberModifyFlag_MsgFlag`. |
| kTIMGroupModifyMemberInfoParamMemberRole | Uint [TIMGroupMemberRole](#timgroupmemberrole) | Write-only (optional) | Modifies the member role. This field is required only when `modify_flag` contains `kTIMGroupMemberModifyFlag_MemberRole`. |
| kTIMGroupModifyMemberInfoParamShutupTime | Uint | Write-only (optional) | Modifies the muting period. This field is required only when `modify_flag` contains `kTIMGroupMemberModifyFlag_ShutupTime`. |
| kTIMGroupModifyMemberInfoParamNameCard | Uint | Write-only (optional) | Modifies the group name card. This field is required only when `modify_flag` contains `kTIMGroupMemberModifyFlag_NameCard`. |
| kTIMGroupModifyMemberInfoParamCustomInfo | Array [GroupMemberInfoCustemString](#groupmemberinfocustemstring) | Write-only (optional) | For details, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### GroupPendencyOption

This macro provides the parameters of the API for obtaining the group pending request list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupPendencyOptionStartTime | Uint64 | Write-only (required) | The pulling timestamp. It is set to 0 for the initial request and then based on the timestamp specified by the kTIMGroupPendencyResultNextStartTime key of [GroupPendencyResult](#grouppendencyresult) returned by the server for subsequent requests. |
| kTIMGroupPendencyOptionMaxLimited | Uint | Write-only (optional) | The recommended number of pending requests to be pulled. The server can return pending requests as required, but this key cannot be used as a flag that indicates whether pulling all pending requests was completed or not. |

### TIMGroupPendencyType

This macro indicates the pending request type.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupPendency_RequestJoin | 0 | Request to join the group |
| kTIMGroupPendency_InviteJoin | 1 | Invitation to a user to join the group |
| kTIMGroupPendency_ReqAndInvite | 2 | Invitation and request to join the group |

### TIMGroupPendencyHandle

This macro indicates the group pending request state.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupPendency_NotHandle | 0 | Not handled |
| kTIMGroupPendency_OtherHandle | 1 | Handled by others |
| kTIMGroupPendency_OperatorHandle | 2 | Handled by the operator |

### TIMGroupPendencyHandleResult

This macro indicates the handling type of group pending requests.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGroupPendency_Refuse | 0 | Reject |
| kTIMGroupPendency_Accept | 1 | Accept |

### GroupPendency

This macro indicates the definition of the group pending request.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupPendencyGroupId | String | Read/Write | Group ID |
| kTIMGroupPendencyFromIdentifier | String | Read/Write | Requester ID, for example, the ID of the requester who requests to join the group or that of the inviter who invites a user to the group |
| kTIMGroupPendencyToIdentifier | String | Read/Write | Decider ID, for example, "" for a request to join the group or the ID of the user who is invited to the group |
| kTIMGroupPendencyAddTime | Uint64 | Read-only | Time when the pending request is added |
| kTIMGroupPendencyPendencyType | Uint [TIMGroupPendencyType](#timgrouppendencytype) | Read-only | Type of the pending request |
| kTIMGroupPendencyHandled | Uint [TIMGroupPendencyHandle](#timgrouppendencyhandle) | Read-only | State of the group pending request |
| kTIMGroupPendencyHandleResult | Uint [TIMGroupPendencyHandleResult](#timgrouppendencyhandleresult) | Read-only | Handling type of the group pending request |
| kTIMGroupPendencyApplyInviteMsg | String | Read-only | Additional information of the application or invitation |
| kTIMGroupPendencyFromUserDefinedData | String | Read-only | Custom field of the applicant or inviter |
| kTIMGroupPendencyApprovalMsg | String | Read-only | Approval information, which is either acceptance or rejection |
| kTIMGroupPendencyToUserDefinedData | String | Read-only | Custom field of the approver |

### GroupPendencyResult

This macro indicates the result returned by the API for obtaining the group pending request list.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupPendencyResultNextStartTime | Uint64 | Read-only | The start timestamp of the next pull. If the server returns 0, no more data can be pulled. Otherwise, this timestamp is used as the start timestamp of the next pull. |
| kTIMGroupPendencyResultReadTimeSeq | Uint64 | Read-only | The timestamp of the read pending request. |
| kTIMGroupPendencyResultUnReadNum | Uint | Read-only | The number of unread pending requests. |
| kTIMGroupPendencyResultPendencyArray | Array [GroupPendency](#grouppendency) | Read-only | The list of group pending requests. |

### GroupHandlePendencyParam

This macro indicates the parameters of the API for handling group pending requests.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMGroupHandlePendencyParamIsAccept | Bool | Write-only (optional) | true: accept. false: reject. The default value is false. |
| kTIMGroupHandlePendencyParamHandleMsg | String | Write-only (optional) | Acceptance or rejection information, which is a null string by default. |
| kTIMGroupHandlePendencyParamPendency | Object [GroupPendency](#grouppendency) | Write-only (required) | The details of the pending request. |

## Key Types of Relationship Chains and Profiles

The following describes the definitions of macros related to the relationship chains and profiles and JSON keys for retrieving structure members.

### FriendShipGetProfileListParam

This macro provides the parameters of the API for handling group pending requests.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendShipGetProfileListParamIdentifierArray | Array string | Write-only | List of the UserIDs of users whose profiles are to be obtained |
| kTIMFriendShipGetProfileListParamForceUpdate | Bool | Write-only | Whether to update the profiles forcibly. false: profiles are preferentially obtained from the local cache, and if this attempt fails, profiles are pulled from the network. true: profiles are directly pulled from the network. The default value is false. |

### TIMGenderType

This macro indicates the user gender.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMGenderType_Unkown | 0 | Unknown |
| kTIMGenderType_Male | 1 | Male |
| kTIMGenderType_Female | 2 | Female |

### TIMProfileAddPermission

This macro indicates the friend addition option.

| Parameter | Value | Description |
|-----|-----|-----|
| kTIMProfileAddPermission_Unknown | 0 | Unknown |
| kTIMProfileAddPermission_AllowAny | 1 | Allow anyone to add friends |
| kTIMProfileAddPermission_NeedConfirm | 2 | Require approval on adding friends |
| kTIMProfileAddPermission_DenyAny | 3 | Prohibit anyone from adding friends |

### UserProfileCustemStringInfo

This macro indicates the custom profile field (string).

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMUserProfileCustemStringInfoKey | String | Write-only | Key value (with the Tag_Profile_Custom_ prefix) of the custom profile field |
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
| kTIMUserProfileAddPermission | Uint [TIMProfileAddPermission](#timprofileaddpermission) | Read-only | Friend addition option of the user |
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
| kTIMUserProfileItemAddPermission | Uint [TIMProfileAddPermission](#timprofileaddpermission) | Write-only | Modify the user’s friend addition option |
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

This macro indicates the friend profile.

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendProfileIdentifier | String | Read-only | UserID of the friend |
| kTIMFriendProfileGroupNameArray | Array string | Read-only | List of friend group names |
| kTIMFriendProfileRemark | String | Read-only | Friend remarks, which is 96 bytes long at the maximum and is empty if the API is called to obtain your own profile |
| kTIMFriendProfileAddWording | String | Read-only | Cause for adding a friend |
| kTIMFriendProfileAddSource | String | Read-only | Source for adding a friend |
| kTIMFriendProfileAddTime | Uint64 | Read-only | Friend addition time |
| kTIMFriendProfileUserProfile | `object` [UserProfile] | Read-only | Personal profile of the friend |
| kTIMFriendProfileCustomStringArray | Array [FriendProfileCustemStringInfo](#friendprofilecustemstringinfo) | Read-only | [Custom friend fields](https://intl.cloud.tencent.com/document/product/1047/33521#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.A5.BD.E5.8F.8B.E5.AD.97.E6.AE.B5) |

### FriendProfileItem

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendProfileItemRemark | String | Write-only | Modify friend remarks |
| kTIMFriendProfileItemGroupNameArray | Array string | Write-only | Modify the friend group name list |
| kTIMFriendProfileItemCustomStringArray | Array [FriendProfileCustemStringInfo](#friendprofilecustemstringinfo) | Write-only | Modify [custom friend fields](https://intl.cloud.tencent.com/document/product/1047/33521#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.A5.BD.E5.8F.8B.E5.AD.97.E6.AE.B5) |

### TIMFriendType

| Parameter | Value | Description |
|-----|-----|-----|
| FriendTypeSignle | 0 | One-way friend: user B is in the friend list of user A, but user A is not in the friend list of user B |
| FriendTypeBoth | 1 | Two-way friend: user B is in the friend list of user A, and user A is also in the friend list of user B |

### FriendshipAddFriendParam

This macro provides the parameters of the API for adding friends.

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
| kTIMFriendResultDesc | String | Read-only | Detailed description of the failed relationship chain operation |

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
| kTIMFriendshipGetPendencyListParamType | Uint [TIMFriendPendencyType](#timfriendpendencytype) | Write-only | The type of the pending friend request. |
| kTIMFriendshipGetPendencyListParamStartSeq | Uint64 | Write-only | The sequence number of the pending request, starting from which the pending request list is obtained. We recommend that the client stores `seq` and the pending request list. When the pending request list needs to be obtained, this field is set to the sequence number returned by `server`. If the `seq` is the latest on the `server`, no data is returned. |
| kTIMFriendshipGetPendencyListParamStartTime | Uint64 | Write-only | The timestamp, starting from which the pending request information is obtained. |
| kTIMFriendshipGetPendencyListParamLimitedSize | Int | Write-only | The number of items on each page of the obtained pending request list. |

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
| kTIMFriendAddPendencyInfoType | Uint [TIMFriendPendencyType](#timfriendpendencytype) | Read-only | Type of the pending friend addition request |
| kTIMFriendAddPendencyInfoIdentifier | String | Read-only | UserID in the pending friend addition request |
| kTIMFriendAddPendencyInfoNickName | String | Read-only | Nickname in the pending friend addition request |
| kTIMFriendAddPendencyInfoAddTime | Uint64 | Read-only | Addition time in the pending friend addition request |
| kTIMFriendAddPendencyInfoAddSource | String | Read-only | Source in the pending friend addition request |
| kTIMFriendAddPendencyInfoAddWording | String | Read-only | Postscript in the pending friend addition request |

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
| kTIMFriendResponeIdentifier | String | Write-only (required) | UserID in the friend addition response |
| kTIMFriendResponeAction | Uint [TIMFriendResponseAction](#timfriendresponseaction) | Write-only (required) | Action in the friend addition response |
| kTIMFriendResponeRemark | String | Write-only (optional) | Friend remarks |
| kTIMFriendResponeGroupName | String | Write-only (optional) | Friend group list |

### FriendshipDeleteFriendParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipDeleteFriendParamFriendType | Uint [TIMFriendType](#timfriendtype) | Write-only | Type of the friend to be deleted |
| kTIMFriendshipDeleteFriendParamIdentifierArray | Array string | Write-only (optional) | List of the UserIDs of friends to be deleted |

### FriendGroupInfo

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipCreateFriendGroupParamNameArray | Array string | Write-only | Name list of created friend groups |
| kTIMFriendshipCreateFriendGroupParamIdentifierArray | Array string | Write-only | List of the UserIDs of friends to be added to the created friend group |

### FriendGroupInfo

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendGroupInfoName | String | Read-only | Friend list name |
| kTIMFriendGroupInfoCount | Uint64 | Read-only | Number of friends in the current friend list |
| kTIMFriendGroupInfoIdentifierArray | Array string | Read-only | List of the UserIDs of friends in the current friend list |

### FriendshipModifyFriendGroupParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipModifyFriendGroupParamName | String | Write-only | Name of the friend list to be modified |
| kTIMFriendshipModifyFriendGroupParamNewName | String | Write-only (optional) | Name of the modified friend list |
| kTIMFriendshipModifyFriendGroupParamDeleteIdentifierArray | Array string | Write-only (optional) | List of the UserIDs of friends to be deleted from the current friend list |
| kTIMFriendshipModifyFriendGroupParamAddIdentifierArray | Array string | Write-only (optional) | List of the UserIDs of friends to be added to the current friend list |

### FriendshipCheckFriendTypeParam

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipCheckFriendTypeParamCheckType | Uint [TIMFriendType](#timfriendtype) | Write-only | Friend type to be checked |
| kTIMFriendshipCheckFriendTypeParamIdentifierArray | Array string | Write-only | List of the UserIDs of friends to be checked |

### TIMFriendCheckRelation

| Parameter | Value | Description |
|-----|-----|-----|
| FriendCheckNoRelation | 0 | No relationship exists between users. |
| FriendCheckAWithB | 1 | User B is in the friend list of user A, but user A is not in the friend list of user B. |
| FriendCheckBWithA | 2 | User A is in the friend list of user B, but user B is not in the friend list of user A. |
| FriendCheckBothWay | 3 | The relationship between users is two-way friendship. |

### FriendshipCheckFriendTypeResult

| JSON Key | Value Type | Attribute | Description |
|-----|-----|-----|-----|
| kTIMFriendshipCheckFriendTypeResultIdentifier | String | Read-only | UserID of the friend to be checked |
| kTIMFriendshipCheckFriendTypeResultRelation | Uint [TIMFriendCheckRelation](#timfriendcheckrelation) | Read-only | Return the relationship between users if the check succeeds |
| kTIMFriendshipCheckFriendTypeResultCode | Int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Check result |
| kTIMFriendshipCheckFriendTypeResultDesc | String | Read-only | Description of the failed friendship check |

