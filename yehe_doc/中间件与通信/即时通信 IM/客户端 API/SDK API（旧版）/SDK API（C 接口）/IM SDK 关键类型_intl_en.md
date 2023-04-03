## Common Macro and Basic Configuration Options


### TIMResult

Values returned after an API is called.

| Name              | Description                                                  |
| ----------------- | ------------------------------------------------------------ |
| TIM_SUCC          | API called successfully.                                     |
| TIM_ERR_SDKUNINIT | Failed to call the API because the Chat SDK is not initialized. |
| TIM_ERR_NOTLOGIN  | Failed to call the API because the user did not log in.      |
| TIM_ERR_JSON      | Failed to call the API because the JSON format or JSON key is incorrect. |
| TIM_ERR_PARAM     | Failed to call the API because parameters are incorrect.     |
| TIM_ERR_CONV      | Failed to call the API because the conversation is invalid.  |
| TIM_ERR_GROUP     | Failed to call the API because the group is invalid.         |

>?If a callback exists in the API parameters, the callback is called only when the API returns a TIM_SUCC message.


### TIMLogLevel

Log level.

| Name            | Description                           |
| --------------- | ------------------------------------- |
| kTIMLog_Off     | Log output disabled                   |
| kTIMLog_Test    | Full log                              |
| kTIMLog_Verbose | Development and debugging details log |
| kTIMLog_Debug   | Debugging log                         |
| kTIMLog_Info    | Information log                       |
| kTIMLog_Warn    | Alarm log                             |
| kTIMLog_Error   | Error log                             |
| kTIMLog_Assert  | Assertion log                         |

### TIMLoginStatus

Login state.

| Name                      | Description   |
| ------------------------- | ------------- |
| kTIMLoginStatus_Logined   | Logged in     |
| kTIMLoginStatus_Logining  | Logging in    |
| kTIMLoginStatus_UnLogined | Not logged in |
| kTIMLoginStatus_Logouting | Logging out   |

### TIMNetworkStatus

Connection event type.

| Name              | Description       |
| ----------------- | ----------------- |
| kTIMConnected     | Connected         |
| kTIMDisconnected  | Disconnected      |
| kTIMConnecting    | Connecting        |
| kTIMConnectFailed | Connection failed |

### TIMConvEvent

Conversation event type.

| Name                 | Description                                                  |
| -------------------- | ------------------------------------------------------------ |
| kTIMConvEvent_Add    | A conversation is added. For example, when a new message is received and a new conversation is generated, this event is triggered. |
| kTIMConvEvent_Del    | A conversation is deleted. For example, if you delete a conversation, this event is triggered. |
| kTIMConvEvent_Update | A conversation is updated. When the number of unread messages in a conversation changes or a new message is received, this event is triggered. |
| kTIMConvEvent_Start  | A conversation is started.                                   |
| kTIMConvEvent_Finish | A conversation is ended.                                     |

### TIMConvType

Conversation type.

| Name             | Description             |
| ---------------- | ----------------------- |
| kTIMConv_Invalid | Invalid conversation    |
| kTIMConv_C2C     | One-to-one conversation |
| kTIMConv_Group   | Group conversation      |
| kTIMConv_System  | System conversation     |

### TIMConversationMarkType

Conversation mark type.

| Name                           | Description                                            |
| ------------------------------ | ------------------------------------------------------ |
| kTIMConversationMarkTypeStar   | Mark a conversation as a favorite                      |
| kTIMConversationMarkTypeUnread | Mark a conversation (important conversation) as unread |
| kTIMConversationMarkTypeFold   | Mark a conversation as collapsed                       |
| kTIMConversationMarkTypeHide   | Mark a conversation as hidden                          |

### TIMPlatform

Platform information.

| Name                   | Description            |
| ---------------------- | ---------------------- |
| kTIMPlatform_Other     | Unknown platform       |
| kTIMPlatform_Windows   | Windows platform       |
| kTIMPlatform_Android   | Android platform       |
| kTIMPlatform_IOS       | iOS platform           |
| kTIMPlatform_Mac       | macOS platform         |
| kTIMPlatform_Simulator | iOS simulator platform |

### SdKConfig

Chat SDK configuration initialization.

| JSON Key                    | Value Type | Attribute             | Description                             |
| --------------------------- | ---------- | --------------------- | --------------------------------------- |
| kTIMSdkConfigConfigFilePath | string     | Write-only (required) | Configuration file path                 |
| kTIMSdkConfigLogFilePath    | string     | Write-only (required) | Log file path                           |
| kTIMSdkConfigJavaVM         | uint64     | Write-only (optional) | Java VM pointer of the Android platform |

### TIMGroupMemberInfoFlag

Group member information identifiers.

| Name                                 | Description                                                  |
| ------------------------------------ | ------------------------------------------------------------ |
| kTIMGroupMemberInfoFlag_None         | None                                                         |
| kTIMGroupMemberInfoFlag_JoinTime     | Group joining time                                           |
| kTIMGroupMemberInfoFlag_MsgFlag      | Group message receiving option                               |
| kTIMGroupMemberInfoFlag_MsgSeq       | Sequence number of the member's read message                 |
| kTIMGroupMemberInfoFlag_MemberRole   | Member role                                                  |
| kTIMGroupMemberInfoFlag_ShutupUntill | Mute period. The value `0` indicates that the member is not muted. |
| kTIMGroupMemberInfoFlag_NameCard     | Group name card                                              |

### TIMGroupMemberRoleFlag

Group member role identifiers.

| Name                           | Description                                             |
| ------------------------------ | ------------------------------------------------------- |
| kTIMGroupMemberRoleFlag_All    | All role types                                          |
| kTIMGroupMemberRoleFlag_Owner  | Owner (group owner)                                     |
| kTIMGroupMemberRoleFlag_Admin  | Admins, excluding group owners                          |
| kTIMGroupMemberRoleFlag_Member | Common group members, excluding group owners and admins |

### GroupMemberGetInfoOption

Option for obtaining group member information.

| JSON Key                                | Value Type                                               | Attribute             | Description                                                  |
| --------------------------------------- | -------------------------------------------------------- | --------------------- | ------------------------------------------------------------ |
| kTIMGroupMemberGetInfoOptionInfoFlag    | uint64 [TIMGroupMemberInfoFlag](#timgroupmemberinfoflag) | Read/Write (optional) | Group member information is filtered based on the information you want to obtain. The default value is `0xffffffff` (obtaining all information). |
| kTIMGroupMemberGetInfoOptionRoleFlag    | uint64 [TIMGroupMemberRoleFlag](#timgroupmemberroleflag) | Read/Write (optional) | Group member information is filtered based on member role. The default value is `kTIMGroupMemberRoleFlag_All` (all roles). |
| kTIMGroupMemberGetInfoOptionCustomArray | Array string                                             | Write-only (optional) | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529) |

### TIMGroupGetInfoFlag

Group member information identifiers.

| Name                           | Description                                       |
| ------------------------------ | ------------------------------------------------- |
| kTIMGroupInfoFlag_None         | -                                                 |
| kTIMGroupInfoFlag_Name         | Group name                                        |
| kTIMGroupInfoFlag_CreateTime   | Group creation time                               |
| kTIMGroupInfoFlag_OwnerUin     | Group creator's account                           |
| kTIMGroupInfoFlag_Seq          | -                                                 |
| kTIMGroupInfoFlag_LastTime     | Last time when the group information was modified |
| kTIMGroupInfoFlag_NextMsgSeq   | -                                                 |
| kTIMGroupInfoFlag_LastMsgTime  | Time of the latest group message                  |
| kTIMGroupInfoFlag_AppId        | -                                                 |
| kTIMGroupInfoFlag_MemberNum    | Number of group members                           |
| kTIMGroupInfoFlag_MaxMemberNum | Maximum number of group members                   |
| kTIMGroupInfoFlag_Notification | Group notice content                              |
| kTIMGroupInfoFlag_Introduction | Group introduction                                |
| kTIMGroupInfoFlag_FaceUrl      | Group profile photo URL                           |
| kTIMGroupInfoFlag_AddOpton     | Group joining option                              |
| kTIMGroupInfoFlag_GroupType    | Group type                                        |
| kTIMGroupInfoFlag_LastMsg      | Last message in the group                         |
| kTIMGroupInfoFlag_OnlineNum    | Number of online members in the group             |
| kTIMGroupInfoFlag_Visible      | Whether the group is visible                      |
| kTIMGroupInfoFlag_Searchable   | Whether the group can be searched                 |
| kTIMGroupInfoFlag_ShutupAll    | Whether the current group has muted all members   |

### GroupGetInfoOption

Option for obtaining group information.

| JSON Key                          | Value Type                                         | Attribute             | Description                                                  |
| --------------------------------- | -------------------------------------------------- | --------------------- | ------------------------------------------------------------ |
| kTIMGroupGetInfoOptionInfoFlag    | uint64 [TIMGroupGetInfoFlag](#timgroupgetinfoflag) | Read/Write (optional) | Group information is filtered based on the information you want to obtain. The default value is `0xffffffff` (obtaining all information). |
| kTIMGroupGetInfoOptionCustomArray | Array string                                       | Write-only (optional) | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529) |

### UserConfig

User configuration.

| JSON Key                               | Value Type                                                   | Attribute             | Description                                                  |
| -------------------------------------- | ------------------------------------------------------------ | --------------------- | ------------------------------------------------------------ |
| kTIMUserConfigIsReadReceipt            | bool                                                         | Write-only (optional) | The value `true` indicates that a read receipt event will be received. |
| kTIMUserConfigIsSyncReport             | bool                                                         | Write-only (optional) | The value `true` indicates that the server will delete the read status. |
| kTIMUserConfigIsIngoreGroupTipsUnRead  | bool                                                         | Write-only (optional) | The value `true` indicates that group tips are not included in the read group message count. |
| kTIMUserConfigIsDisableStorage         | bool                                                         | Write-only (optional) | Whether to disable the local database. `true`: Disable; `false` (default): Enable. |
| kTIMUserConfigGroupGetInfoOption       | object [GroupGetInfoOption](#groupgetinfooption)             | Write-only (optional) | Default option for obtaining group information.              |
| kTIMUserConfigGroupMemberGetInfoOption | object [GroupMemberGetInfoOption](#groupmembergetinfooption) | Write-only (optional) | Default option for obtaining group member information.       |

### HttpProxyInfo

HTTP proxy information.

| JSON Key              | Value Type | Attribute             | Description             |
| --------------------- | ---------- | --------------------- | ----------------------- |
| kTIMHttpProxyInfoIp   | string     | Write-only (required) | IP address of the proxy |
| kTIMHttpProxyInfoPort | int        | Write-only (required) | Port of the proxy       |

### Socks5ProxyInfo

SOCKS5 proxy information.

| JSON Key                    | Value Type | Attribute             | Description                    |
| --------------------------- | ---------- | --------------------- | ------------------------------ |
| kTIMSocks5ProxyInfoIp       | string     | Write-only (required) | IP address of the SOCKS5 proxy |
| kTIMSocks5ProxyInfoPort     | int        | Write-only (required) | Port of the SOCKS5 proxy       |
| kTIMSocks5ProxyInfoUserName | string     | Write-only (optional) | Authentication username        |
| kTIMSocks5ProxyInfoPassword | string     | Write-only (optional) | Authentication password        |

### SetConfig

**Update configuration**

- Custom data
The Chat SDK only passes through data customized by developers to the Chat backend. The maximum length is 64 bytes. The developer service backend can be notified of the custom data through a webhook event [Status Change Webhook](https://intl.cloud.tencent.com/document/product/1047/34357).
- HTTP proxy
When sending messages such as image, voice, file, and video clip messages, the HTTP proxy uploads related files to the COS. When receiving messages such as image, voice, file, and video clip messages, the HTTP proxy downloads related files to the local server. To enable the HTTP proxy, set the IP address of the proxy to a value other than null and the port to a value other than 0 (port 0 is unavailable). To disable the HTTP proxy, set the IP address of the proxy to a null string and the port number to 0.
- SOCKS5 proxy
The SOCKS5 proxy must be enabled before it is initialized. After the SOCKS5 proxy is enabled, all protocols sent by the Chat SDK are sent to the Chat backend through the SOCKS5 proxy server.


| JSON Key                          | Value Type                                 | Attribute             | Description                                                  |
| --------------------------------- | ------------------------------------------ | --------------------- | ------------------------------------------------------------ |
| kTIMSetConfigLogLevel             | uint [TIMLogLevel](#timloglevel)           | Write-only (optional) | Level of the log output to the log file                      |
| kTIMSetConfigCackBackLogLevel     | uint [TIMLogLevel](#timloglevel)           | Write-only (optional) | Log level for log callback                                   |
| kTIMSetConfigIsLogOutputConsole   | bool                                       | Write-only (optional) | Whether to output to the console                             |
| kTIMSetConfigUserConfig           | object [UserConfig](#userconfig)           | Write-only (optional) | User configuration                                           |
| kTIMSetConfigUserDefineData       | string                                     | Write-only (optional) | Custom data. If you need custom data, set it before initialization. |
| kTIMSetConfigHttpProxyInfo        | object [HttpProxyInfo](#httpproxyinfo)     | Write-only (optional) | HTTP proxy information. If you need an HTTP proxy, set it before image, file, voice, and video messages are sent. |
| kTIMSetConfigSocks5ProxyInfo      | Object [Socks5ProxyInfo](#socks5proxyinfo) | Write-only (optional) | SOCKS5 proxy information. If you need a SOCKS5 proxy, set it before initialization. |
| kTIMSetConfigIsOnlyLocalDNSSource | bool                                       | Write-only (optional) | If the value is `true`, the SDK uses only LocalDNS when it selects the optimal IP address. |

## Key Message Types

Definitions of message-related macros and JSON keys accessed by related structure members.

### IOSOfflinePushConfig

Offline push configuration for messages on iOS.

| JSON Key                            | Value Type | Attribute  | Description                                                  |
| ----------------------------------- | ---------- | ---------- | ------------------------------------------------------------ |
| kTIMIOSOfflinePushConfigTitle       | string     | Read/Write | Notification title                                           |
| kTIMIOSOfflinePushConfigSound       | string     | Read/Write | Offline push alert sound URL of the current message on iOS devices. The value `push.no_sound` indicates no alert sound nor vibration. |
| kTIMIOSOfflinePushConfigIgnoreBadge | bool       | Read/Write | Indicates whether to ignore badge count. The value `true` indicates that, on the iOS receiving end, the message will not increase the unread message count on the app icon. |

### TIMAndroidOfflinePushNotifyMode

Android offline push mode.

| Name                                    | Description                                                  |
| --------------------------------------- | ------------------------------------------------------------ |
| kTIMAndroidOfflinePushNotifyMode_Normal | Common notification bar message mode. After an offline message is sent, if you click a message in the notification bar, the app is directly opened and no callback is triggered for the app. |
| kTIMAndroidOfflinePushNotifyMode_Custom | Custom message mode. After an offline message is sent, if you click a message in the notification bar, a callback is triggered for the app. |

### AndroidOfflinePushConfig

Offline push configuration for messages on Android.

| JSON Key                                  | Value Type                                                   | Attribute  | Description                                                  |
| ----------------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| kTIMAndroidOfflinePushConfigTitle         | string                                                       | Read/Write | Notification title                                           |
| kTIMAndroidOfflinePushConfigSound         | string                                                       | Read/Write | Offline push alert sound URL of the current message on Android devices |
| kTIMAndroidOfflinePushConfigNotifyMode    | uint [TIMAndroidOfflinePushNotifyMode](#timandroidofflinepushnotifymode) | Read/Write | Notification mode of the current message                     |
| kTIMAndroidOfflinePushConfigOPPOChannelID | string                                                       | Read/Write | OPPO ChannelID                                               |

>?Description of ChannelID
- In Android 8.0 and later versions, the ChannelID setting is added to messages in the notification bar. At present, this parameter is required for OPPO phones. If this parameter is not specified, OPPO phones running Android 8.0 or later cannot receive offline push messages. In the future, parameters such as `xiaomi_channel_id_` and `huawei_channel_id` might be added.


### TIMOfflinePushFlag

Push rules.

| Name                        | Description                                 |
| --------------------------- | ------------------------------------------- |
| kTIMOfflinePushFlag_Default | Messages are pushed based on default rules. |
| kTIMOfflinePushFlag_NoPush  | Messages are not pushed.                    |

### OfflinePushConfig

Offline message push configuration.

| JSON Key                           | Value Type                                                   | Attribute                                                  | Description                                                  |
| ---------------------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- | ------------------------------------------------------------ |
| kTIMOfflinePushConfigDesc          | string                                                       | Read/Write                                                 | Content displayed for the current message when the peer receives the message pushed offline |
| kTIMOfflinePushConfigExt           | string                                                       | Extension field when the current message is pushed offline |                                                              |
| kTIMOfflinePushConfigFlag          | uint [TIMOfflinePushFlag](#timofflinepushflag)               | Read/Write                                                 | Whether the current message allows push. By default, push is allowed (`kTIMOfflinePushFlag_Default`). |
| kTIMOfflinePushConfigIOSConfig     | object [IOSOfflinePushConfig](#iosofflinepushconfig)         | Read/Write                                                 | iOS offline push configuration                               |
| kTIMOfflinePushConfigAndroidConfig | object [AndroidOfflinePushConfig](#androidofflinepushconfig) | Read/Write                                                 | Android offline push configuration                           |

### TIMMsgStatus

Definition of the current status of a message.

| Name                  | Description                        |
| --------------------- | ---------------------------------- |
| kTIMMsg_Sending       | The message is being sent.         |
| kTIMMsg_SendSucc      | The message was sent successfully. |
| kTIMMsg_SendFail      | Failed to send the message.        |
| kTIMMsg_Deleted       | The message was deleted.           |
| kTIMMsg_LocalImported | The message was imported.          |
| kTIMMsg_Revoked       | The message was recalled.          |

### TIMMsgPriority

Priority of a message. A larger value indicates lower priority.

| Name                   | Description                                                  |
| ---------------------- | ------------------------------------------------------------ |
| kTIMMsgPriority_High   | Highest priority. This priority is generally used for red packet and gift messages. |
| kTIMMsgPriority_Normal | Second highest priority. This priority is recommended for common messages. |
| kTIMMsgPriority_Low    | Low priority. This priority is recommended for like notifications. |
| kTIMMsgPriority_Lowest | Lowest priority. This priority is generally used for group joining/leaving notifications (sent by the backend). |

### Message

Message JSON keys.

| JSON Key                         | Value Type                                     | Attribute             | Description                                                  |
| -------------------------------- | ---------------------------------------------- | --------------------- | ------------------------------------------------------------ |
| kTIMMsgElemArray                 | array [Elem](#elem)                            | Read/Write (required) | List of elements in the message                              |
| kTIMMsgConvId                    | string                                         | Read/Write (optional) | Conversation ID of the message                               |
| kTIMMsgConvType                  | uint [TIMConvType](#timconvtype)               | Read/Write (optional) | Conversation type of the message                             |
| kTIMMsgSender                    | string                                         | Read/Write (optional) | Message sender                                               |
| kTIMMsgPriority                  | uint [TIMMsgPriority](#timmsgpriority)         | Read/Write (optional) | Message priority                                             |
| kTIMMsgClientTime                | uint64                                         | Read/Write (optional) | Client time                                                  |
| kTIMMsgServerTime                | uint64                                         | Read/Write (optional) | Server time                                                  |
| kTIMMsgIsFormSelf                | bool                                           | Read/Write (optional) | Whether the message sender is the current user               |
| kTIMMsgPlatform                  | bool                                           | Read/Write (optional) | Platform that sends the message                              |
| kTIMMsgIsRead                    | bool                                           | Read/Write (optional) | Whether the message is read                                  |
| kTIMMsgIsOnlineMsg               | bool                                           | Read/Write (optional) | Whether the message is an online message. `false` (default): Common message; `true`: Online message. |
| kTIMMsgIsPeerRead                | bool                                           | Read-only             | Whether the message is read by the peer of the conversation  |
| kTIMMsgStatus                    | uint [TIMMsgStatus](#timmsgstatus)             | Read/Write (optional) | Current status of the message                                |
| kTIMMsgUniqueId                  | uint64                                         | Read-only             | Unique ID of the message. `kTIMMsgMsgId` is recommended.     |
| kTIMMsgMsgId                     | string                                         | Read-only             | Unique ID of the message                                     |
| kTIMMsgRand                      | uint64                                         | Read-only             | Random code of the message                                   |
| kTIMMsgSeq                       | uint64                                         | Read-only             | Sequence number of the message                               |
| kTIMMsgCustomInt                 | uint32_t                                       | Read/Write (optional) | Custom integer field (saved locally, will not be sent to the peer end, and will become invalid after the app is uninstalled and reinstalled) |
| kTIMMsgCloudCustomStr            | string                                         | Read/Write (optional) | Custom message data (saved in the cloud, will be sent to the peer end, and can still be pulled after the app is uninstalled and reinstalled) |
| kTIMMsgIsExcludedFromUnreadCount | bool                                           | Read/Write (optional) | Whether to exclude the message from the unread message count of the conversation. `NO` (default): Include; `YES`: Exclude. |
| kTIMMsgGroupAtUserArray          | string                                         | Read/Write (optional) | List of users that need to be mentioned (@). If you need to @all, pass in `kImSDK_MesssageAtALL`. |
| kTIMMsgIsForwardMessage          | bool                                           | Read/Write (optional) | If you need to forward a message, you cannot directly call the `sendMessage` API to send the original message. You need to set `kTIMMsgIsForwardMessage` in the original message to `true` before sending the original message. |
| kTIMMsgSenderProfile             | object [UserProfile](#userprofile)             | Read/Write (optional) | User profile of the message sender                           |
| kTIMMsgSenderGroupMemberInfo     | object [GroupMemberInfo](#groupmemberinfo)     | Read/Write (optional) | Information of the message sender in a group. This parameter is only valid in a group session. Currently, only the `kTIMGroupMemberInfoIdentifier` and `kTIMGroupMemberInfoNameCard` fields can be obtained. For other fields, you are advised to obtain them via the `TIMGroupGetMemberInfoList` API. |
| kTIMMsgOfflinePushConfig         | object [OfflinePushConfig](#offlinepushconfig) | Read/Write (optional) | Offline push settings of the message                         |
| kTIMMsgExcludedFromLastMessage   | string                                         | Read/Write (optional) | Whether to use the current message as the last message (`lastMessage`) of the conversation. `true`: No; `false`: Yes |

>?
- Corresponding element sequence:
Currently, files and voice elements may not be transmitted in the sequence that they are added. Other elements are transmitted in sequence. However, we recommend that you do not overly depend on the element sequence for processing. Processing should be performed based on each element type to prevent process crashes when an exception occurs.
- For group red packet and like notification messages:
In live streaming scenarios, the like and red packet features are provided. The priority of like notifications is low and the priority of red packet notifications is high. You can use [CustomElem](#customelem) to customize message content. When sending a message, you can use `kTIMMsgPriority` to define the message priority.
- Online messages:
If the `kTIMMsgIsOnlineMsg` field is set to `true`, an online message is sent. The message has the following characteristics.
 - One-to-one conversation: When the message is sent, the receiver can receive the message only when the receiver is online. If the receiver is offline, the receiver cannot receive the message even if the peer logs in later.
 - Group conversation: When the message is sent, only online members in the group can receive the message. If a member is offline at the time, the member cannot receive the message even if the member logs in later.
 - The message is not saved on the server.
 - The message is not included in the unread message count.
 - The message is not stored locally.
- Custom fields of the message:
Developers can add custom fields to the message. If integers (specified through `kTIMMsgCustomInt`) and binary data (specified through `kTIMMsgCustomStr`; data must be converted into a string because JSON does not support binary transmission) are customized, different effects can be provided based on the two fields, such as whether voice messages are played. In addition, the values of the two fields are stored locally only and are not synchronized to the server. Therefore, users cannot retrieve these fields when they change devices.


### MessageReceipt

Message read receipt.

| JSON Key                | Value Type                       | Attribute | Description       |
| ----------------------- | -------------------------------- | --------- | ----------------- |
| kTIMMsgReceiptConvId    | string                           | Read-only | Conversation ID   |
| kTIMMsgReceiptConvType  | uint [TIMConvType](#timconvtype) | Read-only | Conversation type |
| kTIMMsgReceiptTimeStamp | uint64                           | Read-only | Timestamp         |

### TIMElemType

Element type.

| Name                   | Description                                      |
| ---------------------- | ------------------------------------------------ |
| kTIMElem_Text          | Text element                                     |
| kTIMElem_Image         | Image element                                    |
| kTIMElem_Sound         | Sound element                                    |
| kTIMElem_Custom        | Custom element                                   |
| kTIMElem_File          | File element                                     |
| kTIMElem_GroupTips     | Group or system message element                  |
| kTIMElem_Face          | Emoji element                                    |
| kTIMElem_Location      | Location element                                 |
| kTIMElem_GroupReport   | Group system message element                     |
| kTIMElem_Video         | Video element                                    |
| kTIMElem_FriendChange  | Element of the relationship chain change message |
| kTIMElem_ProfileChange | Profile change message element                   |
| kTIMElem_Merge         | Combined message element                         |
| kTIMElem_Invalid       | Unknown element type                             |

### Elem

Element type.

| JSON Key     | Value Type                       | Attribute             | Description  |
| ------------ | -------------------------------- | --------------------- | ------------ |
| kTIMElemType | uint [TIMElemType](#timelemtype) | Read/Write (required) | Element type |

### TextElem

Text element.

| JSON Key            | Value Type | Attribute             | Description  |
| ------------------- | ---------- | --------------------- | ------------ |
| kTIMTextElemContent | string     | Read/Write (required) | Text content |

### FaceElem

Emoji element.

| JSON Key          | Value Type | Attribute             | Description                                                  |
| ----------------- | ---------- | --------------------- | ------------------------------------------------------------ |
| kTIMFaceElemIndex | int        | Read/Write (required) | Emoji index                                                  |
| kTIMFaceElemBuf   | string     | Read/Write (optional) | Other additional data that can be customized by the user. To transmit binary data, first convert the binary data into a string. JSON only supports strings. |

>?The Chat SDK does not provide any emoji package. If a developer has emoji packages, the developer may use `kTIMFaceElemIndex` to store emoji indexes in emoji packages or directly use `kTIMFaceElemBuf` to store binary information of emojis (the information must be converted into a string because JSON does not support binary transmission). Emoji packages are customized by users, and the Chat SDK only passes the data through.


### LocationElem

Location element.

| JSON Key                  | Value Type | Attribute             | Description          |
| ------------------------- | ---------- | --------------------- | -------------------- |
| kTIMLocationElemDesc      | string     | Read/Write (optional) | Location description |
| kTIMLocationElemLongitude | double     | Read/Write (required) | Longitude            |
| kTIMLocationElemlatitude  | double     | Read/Write (required) | Latitude             |

### TIMImageLevel

Image quality level.

| Name                       | Description                                                  |
| -------------------------- | ------------------------------------------------------------ |
| kTIMImageLevel_Orig        | The original image is sent.                                  |
| kTIMImageLevel_Compression | A highly compressed image is sent (a small image by default). |
| kTIMImageLevel_HD          | A high definition (HD) image is sent (a large image).        |

### ImageElem

Image element.

| JSON Key                    | Value Type                           | Attribute             | Description                     |
| --------------------------- | ------------------------------------ | --------------------- | ------------------------------- |
| kTIMImageElemOrigPath       | string                               | Read/Write (required) | Path of the sent image          |
| kTIMImageElemLevel          | uint [TIMImageLevel](#timimagelevel) | Read/Write (required) | Quality level of the sent image |
| kTIMImageElemFormat         | int                                  | Read/Write            | Format of the sent image        |
| kTIMImageElemOrigId         | string                               | Read-only             | ID of the original image        |
| kTIMImageElemOrigPicHeight  | int                                  | Read-only             | Height of the original image    |
| kTIMImageElemOrigPicWidth   | int                                  | Read-only             | Width of the original image     |
| kTIMImageElemOrigPicSize    | int                                  | Read-only             | Size of the original image      |
| kTIMImageElemThumbId        | string                               | Read-only             | ID of the thumbnail             |
| kTIMImageElemThumbPicHeight | int                                  | Read-only             | Height of the thumbnail         |
| kTIMImageElemThumbPicWidth  | int                                  | Read-only             | Width of the thumbnail          |
| kTIMImageElemThumbPicSize   | int                                  | Read-only             | Size of the thumbnail           |
| kTIMImageElemLargeId        | string                               | Read-only             | ID of the large image           |
| kTIMImageElemLargePicHeight | int                                  | Read-only             | Height of the large image       |
| kTIMImageElemLargePicWidth  | int                                  | Read-only             | Width of the large image        |
| kTIMImageElemLargePicSize   | int                                  | Read-only             | Size of the large image         |
| kTIMImageElemOrigUrl        | string                               | Read-only             | URL of the original image       |
| kTIMImageElemThumbUrl       | string                               | Read-only             | URL of the thumbnail            |
| kTIMImageElemLargeUrl       | string                               | Read-only             | URL of the large image          |
| kTIMImageElemTaskId         | int                                  | Read-only             | Task ID                         |

>?
- Each image has three specifications:
 - `Original` (original image): An original image refers to an original image sent. The dimensions and size of the original image remain unchanged.
 - `Large` (large image): A large image is an image obtained after the original image is proportionally compressed. After the compression, the height or width (whichever is shorter) is equal to 720 pixels.
 - `Thumb` (thumbnail): A thumbnail is an image obtained after the original image is proportionally compressed. After the compression, the height or width (whichever is shorter) is equal to 198 pixels.
- If the size of the original image is smaller than 198 pixels, the original size is retained for the three specifications and compression is not required.
- If the size of the original image is between 198 pixels and 720 pixels, no compression is required for the large image and original image.
- When an image is displayed on a phone, we recommend that you display the thumbnail first. Then, the user can tap the thumbnail to download the large image and tap the large image to download the original image. Developers may also choose to skip the large image, so the user directly downloads the original image by tapping the thumbnail.
- When images are displayed on a tablet or PC, because the resolution is high and the devices are usually connected to Wi-Fi or a wired network, we recommend that you directly display large images. Then, the user can tap the large image to download the original image.


### SoundElem

Voice element.

| JSON Key                  | Value Type | Attribute             | Description                                                  |
| ------------------------- | ---------- | --------------------- | ------------------------------------------------------------ |
| kTIMSoundElemFilePath     | String     | Read/Write (required) | Path of the voice file. The developer must first store the voice file and then specify the path. |
| kTIMSoundElemFileSize     | int        | Read/Write (required) | Size of the voice message data file (in seconds)             |
| kTIMSoundElemFileTime     | int        | Read/Write (required) | Voice message duration                                       |
| kTIMSoundElemFileId       | string     | Read-only             | Voice ID                                                     |
| kTIMSoundElemBusinessId   | int        | Read-only             | `businessID` used during download                            |
| kTIMSoundElemDownloadFlag | Int        | Read-only             | Whether it is necessary to apply for a download URL. `0`: Yes; `1`: Apply from COS; `2`: Directly use the URL for download |
| kTIMSoundElemUrl          | string     | Read-only             | Download URL                                                 |
| kTIMSoundElemTaskId       | int        | Read-only             | Task ID                                                      |

>?
- You can use a message custom field to specify whether a voice message is played. For example, you can set the valid values of the field to `0` (played) and `1` (not played) and configure the field value to change to `1` when a user taps **Play**.
- Only one voice element can be added to a message. When multiple voice elements are added to a message, sending the message may fail.


### CustomElem

Custom element.

| JSON Key            | Value Type | Attribute  | Description                                   |
| ------------------- | ---------- | ---------- | --------------------------------------------- |
| kTIMCustomElemData  | string     | Read/Write | Data. Binary data is supported.               |
| kTIMCustomElemDesc  | string     | Read/Write | Custom description                            |
| kTIMCustomElemExt   | string     | Read/Write | Field `ext` corresponding to the backend push |
| kTIMCustomElemSound | string     | Read/Write | Custom voice                                  |

>?When the built-in message types cannot meet requirements, developers can customize message formats. The `kTIMCustomElemData` field stores binary information (the information must be converted into a string because JSON does not support binary transmission), and the field value is defined by developers. The Chat SDK is only responsible for passing the messages through.



The following is an example showing how to use `kTIMCustomElemData` to send binary data.

```c++
// Assume that `pBuffer` is a pointer pointing to binary data, and `length` indicates the length of the data.
char * pBuffer;
int length = xxx;

// Use Base16 to encode the binary data into a string
char * pBase16Buf = (char *)malloc(2 * length + 1);
memset(pBase16Buf, 0, 2 * length + 1);
for (int i = 0; i < length; ++i) {
    snprintf(pBase16Buf + 2 * i, 3, "%02X", pBuffer[i]); 
}
std::string strBase16 = std::string(pBase16Buf, strlen(pBase16Buf));
free(pBase16Buf);

// Create a `kTIMCustomElemData` element
json::Object json_element;
json_element[kTIMElemType] = kTIMElem_Custom;
json_element[kTIMCustomElemData] = strBase16.c_str();
json_element[kTIMCustomElemDesc] = "description";
json_element_array.push_back(json_element);
```

 The following is an example showing how to use `kTIMCustomElemData` to receive binary data.

```c++
// Assume that `json_element` is a `kTIMCustomElemData` element. Parse `json_element` to get the `kTIMCustomElemData` field.
std::string strCustomData = json_element[kTIMCustomElemData];

// Use Base16 to decode `strCustomData` to get the original binary data
char * pCustomData = (char*)(strCustomData.c_str());
int customDataLength = (int)(strCustomData.length());

int length = customDataLength / 2;
char * pBuffer = (char *)malloc(length + 1);
memset(pBuffer, 0, length + 1);
for (int i = 0; i < length; ++i) {
    sscanf(pCustomData + 2 * i, "%02X", (char*)(pBuffer + i));
}

// Binary data is used here. `pBuffer` is a pointer pointing to binary data, and `length` indicates the length of the data.
...
// Release `pBuffer`
free(pBuffer);
```


### FileElem

File element.

| JSON Key                 | Value Type | Attribute             | Description                                                  |
| ------------------------ | ---------- | --------------------- | ------------------------------------------------------------ |
| kTIMFileElemFilePath     | string     | Read/Write (required) | File path (including file name)                              |
| kTIMFileElemFileName     | String     | Read/Write (required) | Display file name. If this parameter is not specified, the value of `kTIMFileElemFileName` is the file name in the file path specified by `kTIMFileElemFilePath`. |
| kTIMFileElemFileSize     | int        | Read/Write (required) | File size                                                    |
| kTIMFileElemFileId       | string     | Read-only             | File ID                                                      |
| kTIMFileElemBusinessId   | int        | Read-only             | businessID used during download                              |
| kTIMFileElemDownloadFlag | int        | Read-only             | File download flag                                           |
| kTIMFileElemUrl          | string     | Read-only             | File download URL                                            |
| kTIMFileElemTaskId       | int        | Read-only             | Task ID                                                      |

>?Only one file element can be added to a message. When multiple file elements are added to a message, sending the message may fail.


### VideoElem

Video element.

| JSON Key                       | Value Type | Attribute             | Description                                                  |
| ------------------------------ | ---------- | --------------------- | ------------------------------------------------------------ |
| kTIMVideoElemVideoType         | string     | Read/Write (required) | Video file type. Set this parameter when sending a message.  |
| kTIMVideoElemVideoSize         | uint       | Read/Write (required) | Video file size                                              |
| kTIMVideoElemVideoDuration     | uint       | Read/Write (required) | Video duration. Set this parameter when sending a message.   |
| kTIMVideoElemVideoPath         | string     | Read/Write (required) | Corresponding file path                                      |
| kTIMVideoElemVideoId           | string     | Read-only             | Video ID                                                     |
| kTIMVideoElemBusinessId        | int        | Read-only             | businessID used during download                              |
| kTIMVideoElemVideoDownloadFlag | int        | Read-only             | Flag for video file download                                 |
| kTIMVideoElemVideoUrl          | string     | Read-only             | URL for video file download                                  |
| kTIMVideoElemImageType         | string     | Read/Write (required) | Screenshot file type. Set this parameter when sending a message. |
| kTIMVideoElemImageSize         | uint       | Read/Write (required) | Screenshot file size                                         |
| kTIMVideoElemImageWidth        | uint       | Read/Write (required) | Screenshot height. Set this parameter when sending a message. |
| kTIMVideoElemImageHeight       | uint       | Read/Write (required) | Screenshot width. Set this parameter when sending a message. |
| kTIMVideoElemImagePath         | string     | Read/Write (required) | Path for saving a screenshot                                 |
| kTIMVideoElemImageId           | string     | Read-only             | Screenshot ID                                                |
| kTIMVideoElemImageDownloadFlag | int        | Read-only             | Flag for screenshot file download                            |
| kTIMVideoElemImageUrl          | string     | Read-only             | URL for screenshot file download                             |
| kTIMVideoElemTaskId            | uint       | Read-only             | Task ID                                                      |


### MergerElem

Elements of a combined message.

| JSON Key                      | Value Type | Attribute             | Description                                                  |
| ----------------------------- | ---------- | --------------------- | ------------------------------------------------------------ |
| kTIMMergerElemTitle           | string     | Read/Write (required) | Title of the combined message                                |
| kTIMMergerElemAbstractArray   | uint       | Read/Write (required) | Abstract list of the combined message                        |
| kTIMMergerElemCompatibleText  | uint       | Read/Write (required) | Combined messages are compatible with text. SDKs of early versions do not support combined messages, and they will send a text message with the content `compatibleText` by default. This parameter cannot be empty. |
| kTIMMergerElemMsgArray        | string     | Read/Write (required) | Message list (Up to 300 messages are supported. The message object must be in the `kTIMMsg_SendSucc` status. The message type cannot be `GroupTipsElem` or `GroupReportElem`.) |
| kTIMMergerElemLayersOverLimit | string     | Read-only             | When a combined message also contains combined messages, we call the situation combination nesting. The number of combination nesting levels cannot exceed 100. If the limit is exceeded, `layersOverLimit` will return `YES`, `kTIMMergerElemTitle` and `kTIMMergerElemAbstractArray` will return an empty string, and `DownloadMergerMessage` will return the `ERR_MERGER_MSG_LAYERS_OVER_LIMIT` error code. |
| kTIMMergerElemRelayPbKey      | int        | Read-only             | Key for downloading the message list on the native SDK.      |
| kTIMMergerElemRelayJsonKey    | int        | Read-only             | Key for downloading the message list on the web SDK.         |
| kTIMMergerElemRelayBuffer     | string     | Read-only             | Buffer for message forwarding.                               |

### TIMGroupTipGroupChangeFlag

Group information modification type.

| Name                                | Description                                  |
| ----------------------------------- | -------------------------------------------- |
| kTIMGroupTipChangeFlag_Unknown      | Unknown modification.                        |
| kTIMGroupTipChangeFlag_Name         | Modifies the group name.                     |
| kTIMGroupTipChangeFlag_Introduction | Modifies the group introduction.             |
| kTIMGroupTipChangeFlag_Notification | Modifies the group notice.                   |
| kTIMGroupTipChangeFlag_FaceUrl      | Modifies the URL of the group profile photo. |
| kTIMGroupTipChangeFlag_Owner        | Modifies the group owner.                    |
| kTIMGroupTipChangeFlag_Custom       | Modifies group custom information.           |
| kTIMGroupTipChangeFlag_Attribute    | Modifies group attributes (new)              |

### GroupTipGroupChangeInfo

Group system message - group information modification.

| JSON Key                         | Value Type                                                   | Attribute | Description                                                  |
| -------------------------------- | ------------------------------------------------------------ | --------- | ------------------------------------------------------------ |
| kTIMGroupTipGroupChangeInfoFlag  | uint [TIMGroupTipGroupChangeFlag](#timgrouptipgroupchangeflag) | Read-only | Group information flag for group message modification        |
| kTIMGroupTipGroupChangeInfoValue | string                                                       | Read-only | Modified value. Different values of the `info_flag` field have different meanings. |
| kTIMGroupTipGroupChangeInfoKey   | string                                                       | Read-only | The `key` value corresponding to custom information. The parameter is valid only when the value of `info_flag` is `kTIMGroupTipChangeFlag_Custom`. |

### GroupTipMemberChangeInfo

Group system message - mute for group members.

| JSON Key                               | Value Type | Attribute | Description            |
| -------------------------------------- | ---------- | --------- | ---------------------- |
| kTIMGroupTipMemberChangeInfoIdentifier | string     | Read-only | ID of the group member |
| kTIMGroupTipMemberChangeInfoShutupTime | uint       | Read-only | Mute period            |

### TIMGroupTipType

Group notification type.

| Name                          | Description                                        |
| ----------------------------- | -------------------------------------------------- |
| kTIMGroupTip_None             | Invalid group notification                         |
| kTIMGroupTip_Invite           | Invitation notification                            |
| kTIMGroupTip_Quit             | Group leaving notification                         |
| kTIMGroupTip_Kick             | Notification on member removal from group          |
| kTIMGroupTip_SetAdmin         | Admin setting notification                         |
| kTIMGroupTip_CancelAdmin      | Admin cancellation notification                    |
| kTIMGroupTip_GroupInfoChange  | Group information modification notification        |
| kTIMGroupTip_MemberInfoChange | Group member information modification notification |

### GroupTipsElem

Message element of the group system (for all group members).

| JSON Key                                     | Value Type                                                  | Attribute | Description                                                  |
| -------------------------------------------- | ----------------------------------------------------------- | --------- | ------------------------------------------------------------ |
| kTIMGroupTipsElemTipType                     | uint [TIMGroupTipType](#timgrouptiptype)                    | Read-only | Group message type                                           |
| kTIMGroupTipsElemOpUser                      | string                                                      | Read-only | Operator ID                                                  |
| kTIMGroupTipsElemGroupName                   | string                                                      | Read-only | Group name                                                   |
| kTIMGroupTipsElemGroupId                     | string                                                      | Read-only | Group ID                                                     |
| kTIMGroupTipsElemTime                        | uint                                                        | Read-only | Group message time (disused)                                 |
| kTIMGroupTipsElemUserArray                   | array string                                                | Read-only | List of accounts operated on                                 |
| kTIMGroupTipsElemGroupChangeInfoArray        | array [GroupTipGroupChangeInfo](#grouptipgroupchangeinfo)   | Read-only | Group profile change information list. This parameter is valid only when the value of `tips_type` is `kTIMGroupTip_GroupInfoChange`. |
| kTIMGroupTipsElemMemberChangeInfoArray       | array [GroupTipMemberChangeInfo](#grouptipmemberchangeinfo) | Read-only | Group member change information list. This parameter is valid only when the value of `tips_type` is `kTIMGroupTip_MemberInfoChange`. |
| kTIMGroupTipsElemOpUserInfo                  | object [UserProfile](#userprofile)                          | Read-only | Personal profile of the operator                             |
| kTIMGroupTipsElemOpGroupMemberInfo           | object [GroupMemberInfo](#groupmemberinfo)                  | Read-only | Group member information                                     |
| kTIMGroupTipsElemChangedUserInfoArray        | array [UserProfile](#userprofile)                           | Read-only | List of user profiles operated on                            |
| kTIMGroupTipsElemChangedGroupMemberInfoArray | array [GroupMemberInfo](#groupmemberinfo)                   | Read-only | Group member information list                                |
| kTIMGroupTipsElemMemberNum                   | uint                                                        | Read-only | Number of current group members. This parameter is valid only when the event message type is `kTIMGroupTip_Invite`, `kTIMGroupTip_Quit`, or `kTIMGroupTip_Kick`. |
| kTIMGroupTipsElemPlatform                    | string                                                      | Read-only | Operator platform information                                |

### TIMGroupReportType

Group system message type.

| Name                         | Description                                                  |
| ---------------------------- | ------------------------------------------------------------ |
| kTIMGroupReport_None         | Unknown type                                                 |
| kTIMGroupReport_AddRequest   | Group joining request (received only by the admin)           |
| kTIMGroupReport_AddAccept    | Request to join the group is approved (received only by the applicant) |
| kTIMGroupReport_AddRefuse    | Request to join the group is rejected (received only by the applicant) |
| kTIMGroupReport_BeKicked     | Removed from the group by the admin (received only by the removed user) |
| kTIMGroupReport_Delete       | Group disbanded (received by all members)                    |
| kTIMGroupReport_Create       | Group created (received only by the creator and not displayed) |
| kTIMGroupReport_Invite       | Invited to a group that does not require invitee approval (such as a work group) |
| kTIMGroupReport_Quit         | Group leaving (received only by the user who leaves the group and not displayed) |
| kTIMGroupReport_GrantAdmin   | Admin status set (received only by the set admin)            |
| kTIMGroupReport_CancelAdmin  | Admin status canceled (received only by the canceled admin)  |
| kTIMGroupReport_GroupRecycle | Group repossessed (received by all members and not displayed) |
| kTIMGroupReport_InviteReq    | Invitee received an invitation and needed to accept or reject the invitation |
| kTIMGroupReport_InviteAccept | Group invitation approved (received only by the inviter)     |
| kTIMGroupReport_InviteRefuse | Group invitation rejected (received only by the inviter)     |
| kTIMGroupReport_ReadReport   | Read report synchronized across multiple terminals (received only by the reporter) |
| kTIMGroupReport_UserDefine   | User-defined notification (received by all members by default) |

### GroupReportElem

Group system message element (for individuals).

| JSON Key                             | Value Type                                     | Attribute | Description                          |
| ------------------------------------ | ---------------------------------------------- | --------- | ------------------------------------ |
| kTIMGroupReportElemReportType        | uint [TIMGroupReportType](#timgroupreporttype) | Read-only | Type                                 |
| kTIMGroupReportElemGroupId           | string                                         | Read-only | Group ID                             |
| kTIMGroupReportElemGroupName         | string                                         | Read-only | Group name                           |
| kTIMGroupReportElemOpUser            | string                                         | Read-only | Operator ID                          |
| kTIMGroupReportElemMsg               | string                                         | Read-only | Reason for operation                 |
| kTIMGroupReportElemUserData          | string                                         | Read-only | Custom data entered by the operator  |
| kTIMGroupReportElemOpUserInfo        | object [UserProfile](#userprofile)             | Read-only | Personal profile of the operator     |
| kTIMGroupReportElemOpGroupMemberInfo | object [GroupMemberInfo](#groupmemberinfo)     | Read-only | Group member profile of the operator |
| kTIMGroupReportElemPlatform          | string                                         | Read-only | Operator platform information        |

### TIMProfileChangeType

| Name                      | Description    |
| ------------------------- | -------------- |
| kTIMProfileChange_None    | Unknown type   |
| kTIMProfileChange_Profile | Profile change |

### ProfileChangeElem

| JSON Key                             | Value Type                                         | Attribute | Description                                                  |
| ------------------------------------ | -------------------------------------------------- | --------- | ------------------------------------------------------------ |
| kTIMProfileChangeElemChangeType      | uint [TIMProfileChangeType](#timprofilechangetype) | Read-only | Profile change type                                          |
| kTIMProfileChangeElemFromIndentifier | String                                             | Read-only | UserID of the user whose profile is changed                  |
| kTIMProfileChangeElemUserProfileItem | object [UserProfileItem](#userprofileitem)         | Read-only | Specific change information. This parameter is valid only when `change_type` is `kTIMProfileChange_Profile`. |

### TIMFriendChangeType

| Name                                  | Description                                   |
| ------------------------------------- | --------------------------------------------- |
| kTIMFriendChange_None                 | Unknown type                                  |
| kTIMFriendChange_FriendAdd            | Adds friends                                  |
| kTIMFriendChange_FriendDel            | Deletes friends                               |
| kTIMFriendChange_PendencyAdd          | Adds a pending friend request                 |
| kTIMFriendChange_PendencyDel          | Deletes a pending friend request              |
| kTIMFriendChange_BlackListAdd         | Adds users to the blocklist                   |
| kTIMFriendChange_BlackListDel         | Removes users from the blocklist              |
| kTIMFriendChange_PendencyReadedReport | Reports that a pending friend request is read |
| kTIMFriendChange_FriendProfileUpdate  | Updates friend data                           |
| kTIMFriendChange_FriendGroupAdd       | Adds a friend list                            |
| kTIMFriendChange_FriendGroupDel       | Deletes a friend list                         |
| kTIMFriendChange_FriendGroupModify    | Modifies a friend list                        |

### FriendProfileUpdate

| JSON Key                          | Value Type                                     | Attribute  | Description                                   |
| --------------------------------- | ---------------------------------------------- | ---------- | --------------------------------------------- |
| kTIMFriendProfileUpdateIdentifier | string                                         | Write-only | UserID of the friend whose profile is updated |
| kTIMFriendProfileUpdateItem       | object [FriendProfileItem](#friendprofileitem) | Write-only | Profile update item                           |

### FriendChangeElem

| JSON Key                                             | Value Type                                        | Attribute | Description                                                  |
| ---------------------------------------------------- | ------------------------------------------------- | --------- | ------------------------------------------------------------ |
| kTIMFriendChangeElemChangeType                       | uint [TIMFriendChangeType](#timfriendchangetype)  | Read-only | Profile change type                                          |
| kTIMFriendChangeElemFriendAddIdentifierArray         | array string                                      | Read-only | List of friend UserIDs to be added. This parameter is valid only when `change_type` is `kTIMFriendChange_FriendAdd`. |
| kTIMFriendChangeElemFriendDelIdentifierArray         | array string                                      | Read-only | List of friend UserIDs to be deleted. This parameter is valid only when `change_type` is `kTIMFriendChange_FriendDel`. |
| kTIMFriendChangeElemFriendAddPendencyItemArray       | array [FriendAddPendency](#friendaddpendency)     | Read-only | List of pending friend requests. This parameter is valid only when `change_type` is `kTIMFriendChange_PendencyAdd`. |
| kTIMFriendChangeElemPendencyDelIdentifierArray       | array string                                      | Read-only | List of deleted pending friend requests. This parameter is valid only when `change_type` is `kTIMFriendChange_PendencyDel`. |
| kTIMFriendChangeElemPendencyReadedReportTimestamp    | uint64                                            | Read-only | Timestamp of the report on the reading of a pending friend request. This parameter is valid only when `change_type` is `kTIMFriendChange_PendencyReadedReport`. |
| kTIMFriendChangeElemBlackListAddIdentifierArray      | array string                                      | Read-only | List of UserIDs added to the blocklist. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_BlackListAdd`. |
| kTIMFriendChangeElemBlackListDelIdentifierArray      | array string                                      | Read-only | List of UserIDs deleted from the blocklist. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_BlackListDel`. |
| kTIMFriendChangeElemFreindProfileUpdateItemArray     | array [FriendProfileUpdate](#friendprofileupdate) | Read-only | Friend profile update list. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_FriendProfileUpdate`. |
| kTIMFriendChangeElemFriendGroupAddIdentifierArray    | array string                                      | Read-only | List of the names of the friend lists added. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_FriendGroupAdd`. |
| kTIMFriendChangeElemFriendGroupDelIdentifierArray    | array string                                      | Read-only | List of the names of the friend lists deleted. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_FriendGroupDel`. |
| kTIMFriendChangeElemFriendGroupModifyIdentifierArray | array string                                      | Read-only | List of the names of the friend lists modified. This parameter is valid only when the value of `change_type` is `kTIMFriendChange_FriendGroupModify`. |

### MsgBatchSendParam

Parameters of the batch message sending API.

| JSON Key                             | Value Type                 | Attribute             | Description                                         |
| ------------------------------------ | -------------------------- | --------------------- | --------------------------------------------------- |
| kTIMMsgBatchSendParamIdentifierArray | array string               | Write-only (required) | List of recipient UserIDs for batch message sending |
| kTIMMsgBatchSendParamMsg             | object [Message](#message) | Write-only (required) | Messages sent in batches                            |

### MsgBatchSendResult

Result returned by the batch message sending API.

| JSON Key                         | Value Type                                                   | Attribute | Description                                       |
| -------------------------------- | ------------------------------------------------------------ | --------- | ------------------------------------------------- |
| kTIMMsgBatchSendResultIdentifier | string                                                       | Read-only | Single recipient UserID for batch message sending |
| kTIMMsgBatchSendResultCode       | int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Result of batch message sending                   |
| kTIMMsgBatchSendResultDesc       | string                                                       | Read-only | Description of message sending                    |
| kTIMMsgBatchSendResultMsg        | object [Message](#message)                                   | Read-only | Messages sent                                     |

### MsgLocator

Message locator.

| JSON Key                | Value Type | Attribute             | Description                                                  |
| ----------------------- | ---------- | --------------------- | ------------------------------------------------------------ |
| kTIMMsgLocatorConvId    | bool       | Read/Write            | Conversation ID of the searched message                      |
| kTIMMsgLocatorConvType  | bool       | Read/Write            | Conversation type of the searched message                    |
| kTIMMsgLocatorIsRevoked | bool       | Read/Write (required) | Whether the searched message is recalled. `true`: Yes; `false` (default): No |
| kTIMMsgLocatorTime      | uint64     | Read/Write (required) | Timestamp of the searched message                            |
| kTIMMsgLocatorSeq       | uint64     | Read/Write (required) | Sequence number of the searched message                      |
| kTIMMsgLocatorIsSelf    | bool       | Read/Write (required) | Whether the sender of the searched message is the current user. `true`: Yes; `false` (default): No |
| kTIMMsgLocatorRand      | uint64     | Read/Write (required) | Random code of the searched message                          |
| kTIMMsgLocatorUniqueId  | uint64     | Read/Write (required) | Unique ID of the searched message                            |

### MsgGetMsgListParam

Parameters of the message getting API.

| JSON Key                         | Value Type                 | Attribute             | Description                                        |
| -------------------------------- | -------------------------- | --------------------- | -------------------------------------------------- |
| kTIMMsgGetMsgListParamLastMsg    | object [Message](#message) | Write-only (optional) | Specified message. The value cannot be null.       |
| kTIMMsgGetMsgListParamCount      | uint                       | Write-only (optional) | Number of messages following the specified message |
| kTIMMsgGetMsgListParamIsRamble   | bool                       | Write-only (optional) | Whether the message is a roaming message           |
| kTIMMsgGetMsgListParamIsForward  | bool                       | Write-only (optional) | Whether the sorting mode is forward sorting        |
| kTIMMsgGetMsgListParamLastMsgSeq | bool                       | Write-only (optional) | Sequence number of the message                     |
| kTIMMsgGetMsgListParamTimeBegin  | bool                       | Write-only (optional) | Start time; UTC timestamp, in seconds              |
| kTIMMsgGetMsgListParamTimePeriod | bool                       | Write-only (optional) | Duration, in seconds                               |

### MsgDeleteParam

Parameters of the message deletion API.

| JSON Key                   | Value Type                 | Attribute             | Description                                                  |
| -------------------------- | -------------------------- | --------------------- | ------------------------------------------------------------ |
| kTIMMsgDeleteParamMsg      | object [Message](#message) | Write-only (optional) | Message to be deleted                                        |
| kTIMMsgDeleteParamIsRamble | bool                       | Write-only (optional) | Whether to delete all local or roaming messages. `true`: Delete roaming messages; `false` (default): Delete local messages |

### TIMReceiveMessageOpt

Message receiving options.

| Name                       | Description                                                  |
| -------------------------- | ------------------------------------------------------------ |
| kTIMRecvMsgOpt_Receive     | Messages will be received when the user is online, and APNs push notifications will be received when the user is offline. |
| kTIMRecvMsgOpt_Not_Receive | Messages will not be received when the user is online, and no push notification will be received when the user is offline. |
| kTIMRecvMsgOpt_Not_Notify  | Messages will be received when the user is online, and no push notification will be received when the user is offline. |

### GetC2CRecvMsgOptResult

Query result of the one-to-one message receiving option.

| JSON Key                                | Value Type                                    | Attribute  | Description               |
| --------------------------------------- | --------------------------------------------- | ---------- | ------------------------- |
| kTIMMsgGetC2CRecvMsgOptResultIdentifier | string                                        | Write-only | User ID.                  |
| kTIMMsgDeleteParamIsRamble              | [TIMReceiveMessageOpt](#timreceivemessageopt) | Write-only | Message receiving option. |


### TIMDownloadType

UUID type.

| Name                    | Description     |
| ----------------------- | --------------- |
| kTIMDownload_VideoThumb | Video thumbnail |
| kTIMDownload_File       | File            |
| kTIMDownload_Video      | Video           |
| kTIMDownload_Sound      | Audio           |

### DownloadElemParam

Parameters of the element download API.

| JSON Key                           | Value Type                               | Attribute  | Description                                           |
| ---------------------------------- | ---------------------------------------- | ---------- | ----------------------------------------------------- |
| kTIMMsgDownloadElemParamFlag       | uint                                     | Write-only | Element download type, obtained from message elements |
| kTIMMsgDownloadElemParamType       | uint [TIMDownloadType](#timdownloadtype) | Write-only | Element type, obtained from message elements          |
| kTIMMsgDownloadElemParamId         | string                                   | Write-only | Element ID, obtained from message elements            |
| kTIMMsgDownloadElemParamBusinessId | uint                                     | Write-only | Element BusinessID, obtained from message elements    |
| kTIMMsgDownloadElemParamUrl        | string                                   | Write-only | Element URL, obtained from message elements           |

### MsgDownloadElemResult

Result returned by the element download API.

| JSON Key                             | Value Type | Attribute | Description                             |
| ------------------------------------ | ---------- | --------- | --------------------------------------- |
| kTIMMsgDownloadElemResultCurrentSize | uint       | Read-only | Size of the downloaded part of the file |
| kTIMMsgDownloadElemResultTotalSize   | uint       | Read-only | Total size of the file to be downloaded |

### KeywordListMatchType

Combination types of message search keywords.

| Name                        | Description                  |
| --------------------------- | ---------------------------- |
| TIMKeywordListMatchType_Or  | Contain at least one keyword |
| TIMKeywordListMatchType_And | Contain all keywords         |

### MessageSearchParam

Message search parameters.

| JSON Key                                | Value Type                        | Attribute             | Description                                                  |
| --------------------------------------- | --------------------------------- | --------------------- | ------------------------------------------------------------ |
| kTIMMsgSearchParamKeywordArray          | array string                      | Write-only (required) | Search keyword list. Up to five keywords are supported.      |
| kTIMMsgSearchParamMessageTypeArray      | array [TIMElemType](#timelemtype) | Read-only             | Message types to search. If an empty array is passed in, all message types supported are searched (`FaceElem` and `GroupTipsElem` are not supported). For more information about valid values, see [TIMElemType](#timelemtype). |
| kTIMMsgSearchParamConvId                | string                            | Write-only (required) | Conversation ID.                                             |
| kTIMMsgSearchParamConvType              | uint                              | Write-only (required) | Conversation type. `kTIMConv_Invalid`: Search all conversations; other values: Search specified conversations. |
| kTIMMsgSearchParamSearchTimePosition    | uint                              | Write-only (required) | Start time for search. The default value is `0`, indicating to start searching now. The value can also be the UTC timestamp, in seconds. |
| kTIMMsgSearchParamSearchTimePeriod      | uint                              | Write-only (required) | A time period in the past starting from the start time, in seconds. The default value `0` indicates that the time range is not limited. The value `24x60x60` indicates the past day. |
| kTIMMsgSearchParamPageIndex             | uint                              | Write-only (required) | Page number, used for the paginated display of the search results. Page numbers must start from zero. First call: Call `searchLocalMessage` with `pageSize` set to `10` and `pageIndex` to `0`. Then you can get the total number of results from `totalCount` in the callback. Page quantity calculation: totalPage = (totalCount % loadCount == 0) ? (totalCount / pageIndex) : (totalCount / pageIndex + 1). Second call: You can specify `pageIndex` (`pageIndex` < `totalPage`) to return the subsequent page number. |
| kTIMMsgSearchParamPageSize              | uint                              | Write-only (required) | Number of results per page, used for the paginated display of the search results. If you do not want to paginate the search results, set the parameter to 0. However, a large number of search results without pagination may cause performance issues. |
| kTIMMsgSearchParamKeywordListMatchType  | uint                              | Write-only (required) | Search for messages by keywords combined with OR or AND.     |
| kTIMMsgSearchParamSenderIdentifierArray | uint                              | Write-only (required) | Search for messages by sender UserID.                        |

### MessageSearchResultItem

Message search result items.

| JSON Key                                 | Value Type                | Attribute | Description                                                  |
| ---------------------------------------- | ------------------------- | --------- | ------------------------------------------------------------ |
| kTIMMsgSearchResultItemConvId            | string                    | Read-only | Conversation ID.                                             |
| kTIMMsgSearchResultItemConvType          | uint                      | Read-only | Conversation type. `kTIMConv_Invalid`: Search all conversations; other values: Search specified conversations. |
| kTIMMsgSearchResultItemTotalMessageCount | uint                      | Read-only | Total number of eligible messages found in the current conversation. |
| kTIMMsgSearchResultItemMessageArray      | array [Message](#message) | Read-only | List of eligible messages.                                   |

### MessageSearchResult

Message search results.

| JSON Key                        | Value Type                                                | Attribute | Description                                                  |
| ------------------------------- | --------------------------------------------------------- | --------- | ------------------------------------------------------------ |
| kTIMMsgSearchResultTotalCount   | uint                                                      | Read-only | If you search **a specified conversation**, the total number of eligible messages is returned. If you search **all conversations**, the total number of conversations where the eligible messages reside is returned. |
| kTIMMsgSearchResultItemConvType | uint                                                      | Read-only | Conversation type. `kTIMConv_Invalid`: Search all conversations; other values: Search specified conversations. |
| kTIMMsgSearchResultItemArray    | array [MessageSearchResultItem](#messagesearchresultitem) | Read-only | If you search **a specified conversation**, the result list contains only the results found in the conversation. If you search **all conversations**, eligible messages are grouped by conversation ID and returned on multiple pages. |

### TIMGroupMessageReadMembersFilter

Filter the list of members who have read the group message.

| Name                                         | Description                                         |
| -------------------------------------------- | --------------------------------------------------- |
| TIM_GROUP_MESSAGE_READ_MEMBERS_FILTER_READ   | List of members who have read the group message     |
| TIM_GROUP_MESSAGE_READ_MEMBERS_FILTER_UNREAD | List of members who have not read the group message |

## Key Conversation Types

Definitions of conversation-related macros and JSON keys accessed by related structure members.

### Draft

Draft information.

| JSON Key            | Value Type                 | Attribute | Description                           |
| ------------------- | -------------------------- | --------- | ------------------------------------- |
| kTIMDraftMsg        | object [Message](#message) | Read-only | Draft message                         |
| kTIMDraftUserDefine | string                     | Read-only | User-defined data                     |
| kTIMDraftEditTime   | uint                       | Read-only | Latest edit time of the draft message |

### TIMGroupAtType

Mentioning (@) type.

| Name                   | Description                     |
| ---------------------- | ------------------------------- |
| kTIMGroup_At_Me        | @me                             |
| kTIMGroup_At_All       | @all in the group               |
| kTIMGroup_At_All_At_ME | @all in the group and @me alone |

### GroupAtInfo

Group @ information.

| JSON Key              | Value Type                             | Attribute | Description                                                  |
| --------------------- | -------------------------------------- | --------- | ------------------------------------------------------------ |
| kTIMGroupAtInfoSeq    | uint64                                 | Read-only | Sequence number of an @ message (message with the "@me" or "@all" identifier). |
| kTIMGroupAtInfoAtType | uint [TIMGroupAtType](#timgroupattype) | Read-only | @ notification type: "@me", "@all", or "@all in the group and @me alone". |

### ConvInfo

Conversation information.

| JSON Key                 | Value Type                                         | Attribute            | Description                                                  |
| ------------------------ | -------------------------------------------------- | -------------------- | ------------------------------------------------------------ |
| kTIMConvId               | string                                             | Read-only            | Conversation ID                                              |
| kTIMConvType             | uint [TIMConvType](#timconvtype)                   | Read-only            | Conversation type                                            |
| kTIMConvOwner            | string                                             | Read-only            | Conversation owner                                           |
| kTIMConvUnReadNum        | uint64                                             | Read-only            | Unread message count of the conversation                     |
| kTIMConvActiveTime       | uint64                                             | Read-only            | Conversation activation time                                 |
| kTIMConvIsHasLastMsg     | bool                                               | Read-only            | Whether the conversation has a last message                  |
| kTIMConvLastMsg          | object [Message](#message)                         | Read-only            | Last message of the conversation                             |
| kTIMConvIsHasDraft       | bool                                               | Read-only            | Whether the conversation has a draft                         |
| kTIMConvDraft            | object [Draft](#draft)                             | Read-only (optional) | Draft message in the conversation                            |
| kTIMConvRecvOpt          | uint [TIMReceiveMessageOpt](#timreceivemessageopt) | Read-only (optional) | Message receiving option                                     |
| kTIMConvGroupAtInfoArray | array [GroupAtInfo](#groupatinfo)                  | Read-only (optional) | @ information list of a group conversation, which is used to display "someone@me" or "@all" notifications |
| kTIMConvIsPinned         | object [Draft](#draft)                             | Read-only (optional) | Whether to pin on top                                        |
| kTIMConvShowName         | object [Draft](#draft)                             | Read-only (optional) | Conversation display name. Conversation display name priorities are as follows: 1. group conversation — group name -> group ID; 2. C2C conversation — peer's remarks -> peer's nickname -> peer's userID |

### TIMConversationListFilter

Filter of the advanced API for getting the conversation list.

| JSON Key                                    | Value Type                                               | Attribute  | Description             |
| ------------------------------------------- | -------------------------------------------------------- | ---------- | ----------------------- |
| kTIMConversationListFilterConvType          | uint [TIMConvType](#timconvtype)                         | Write-only | Conversation type       |
| kTIMConversationListFilterConversationGroup | string                                                   | Write-only | Conversation group name |
| kTIMConversationListFilterMarkType          | uint [TIMConversationMarkType](#timconversationmarktype) | Write-only | Mark type               |

### TIMConversationListResult

Result of getting the conversation list.

| JSON Key                            | Value Type                  | Attribute | Description                    |
| ----------------------------------- | --------------------------- | --------- | ------------------------------ |
| TIMConversationListResultConvList   | array [ConvInfo](#convinfo) | Read-only | Conversation list              |
| TIMConversationListResultNextSeq    | uint64                      | Read-only | Cursor for paged pull          |
| TIMConversationListResultIsFinished | bool                        | Read-only | Whether paged pull is finished |

### GetConversationListParam

Parameters for getting the conversation list.

| JSON Key                           | Value Type                       | Attribute  | Description       |
| ---------------------------------- | -------------------------------- | ---------- | ----------------- |
| kTIMGetConversationListParamConvId | string                           | Write-only | Conversation ID   |
| kTIMConvType                       | uint [TIMConvType](#timconvtype) | Write-only | Conversation type |

### GetTotalUnreadNumberResult

Result of getting the unread message count of a conversation.

| JSON Key                                            | Value Type | Attribute | Description                              |
| --------------------------------------------------- | ---------- | --------- | ---------------------------------------- |
| kTIMConvGetTotalUnreadMessageCountResultUnreadCount | int        | Read-only | Unread message count of the conversation |

### TIMConversationOperationResult

Conversation operation result.

| JSON Key                                      | Value Type | Attribute | Description        |
| --------------------------------------------- | ---------- | --------- | ------------------ |
| kTIMConversationOperationResultConversationID | string     | Read-only | Conversation ID    |
| kTIMConversationOperationResultResultCode     | int        | Read-only | Return code        |
| kTIMConversationOperationResultResultInfo     | string     | Read-only | Return information |

## Key Group Types

Definitions of group-related macros and JSON keys accessed by related structure members.

### TIMGroupAddOption

Group joining option.

| Name                   | Description                     |
| ---------------------- | ------------------------------- |
| kTIMGroupAddOpt_Forbid | Forbid anyone to join the group |
| kTIMGroupAddOpt_Auth   | Require admin approval          |
| kTIMGroupAddOpt_Any    | Anyone can join the group       |

### TIMGroupType

Group type.

| Name                 | Description                                                  |
| -------------------- | ------------------------------------------------------------ |
| kTIMGroup_Public     | Public group (Public): Supports up to 2,000 members; allows anyone to apply to join the group, but requires approval by the group owner or admin for group joining; suitable for interest groups managed by group owners |
| kTIMGroup_Private    | Work group (Work): Supports up to 200 members; does not allow proactive group joining and only allows users to be invited to join the group by group members; suitable for work groups randomly created (corresponding to the Private group in the earlier version) |
| kTIMGroup_ChatRoom   | Meeting group (Meeting): Supports up to 6,000 members; allows anyone to join and leave the group freely without approval; suitable for scenarios such as video conference and online training (corresponding to the ChatRoom group in the earlier version) |
| kTIMGroup_BChatRoom  | Broadcasting chat room: An audio-video group (AVChatRoom) is recommended |
| kTIMGroup_AVChatRoom | Audio-video group (AVChatRoom): Supports an unlimited number of members; allows anyone to join and leave the group freely; features high message throughput and is suitable for a chat room with high-concurrency on-screen comments in live streaming scenarios |
| kTIMGroup_Community  | Community group (Community): Supports up to 100,000 members; allows anyone to join and leave the community freely without approval; suitable for group chat scenarios in large communities for purposes such as knowledge sharing and game exchange; supported in v5.8 or later version, and requires the Flagship edition package |

### TIMGroupMemberRole

Group member role type.

| Name                  | Description               |
| --------------------- | ------------------------- |
| kTIMMemberRole_None   | Undefined                 |
| kTIMMemberRole_Normal | Group member              |
| kTIMMemberRole_Admin  | Admin                     |
| kTIMMemberRole_Owner  | Super admin (group owner) |

### GroupMemberInfoCustemString

| JSON Key                                 | Value Type | Attribute  | Description             |
| ---------------------------------------- | ---------- | ---------- | ----------------------- |
| kTIMGroupMemberInfoCustemStringInfoKey   | string     | Write-only | Key of a custom field   |
| kTIMGroupMemberInfoCustemStringInfoValue | string     | Write-only | Value of a custom field |

### GroupMemberInfo

Group member information.

| JSON Key                      | Value Type                                                   | Attribute             | Description                                                  |
| ----------------------------- | ------------------------------------------------------------ | --------------------- | ------------------------------------------------------------ |
| kTIMGroupMemberInfoIdentifier | string                                                       | Read/Write (required) | ID of the group member                                       |
| kTIMGroupMemberInfoGroupId    | string                                                       | Read-only             | Group ID                                                     |
| kTIMGroupMemberInfoJoinTime   | uint                                                         | Read-only             | Group joining time of the group member                       |
| kTIMGroupMemberInfoMemberRole | uint [TIMGroupMemberRole](#timgroupmemberrole)               | Read/Write (optional) | Role of the group member                                     |
| kTIMGroupMemberInfoMsgFlag    | uint                                                         | Read-only             | Message receiving option of the group member                 |
| kTIMGroupMemberInfoMsgSeq     | uint                                                         | Read-only             | -                                                            |
| kTIMGroupMemberInfoShutupTime | uint                                                         | Read-only             | Muting period of the group member                            |
| kTIMGroupMemberInfoNameCard   | string                                                       | Read-only             | Group name card of the group member                          |
| kTIMGroupMemberInfoNickName   | string                                                       | Read-only             | Nickname of the friend                                       |
| kTIMGroupMemberInfoRemark     | string                                                       | Read-only             | Remarks of the friend                                        |
| kTIMGroupMemberInfoFaceUrl    | string                                                       | Read-only             | Profile photo of the friend                                  |
| kTIMGroupMemberInfoCustomInfo | array [GroupMemberInfoCustemString](#groupmemberinfocustemstring) | Read-only             | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

### GroupInfoCustemString

| JSON Key                           | Value Type | Attribute  | Description             |
| ---------------------------------- | ---------- | ---------- | ----------------------- |
| kTIMGroupInfoCustemStringInfoKey   | string     | Write-only | Key of a custom field   |
| kTIMGroupInfoCustemStringInfoValue | string     | Write-only | Value of a custom field |

### CreateGroupParam

Parameters of the group creation API.

| JSON Key                             | Value Type                                            | Attribute             | Description                                                  |
| ------------------------------------ | ----------------------------------------------------- | --------------------- | ------------------------------------------------------------ |
| kTIMCreateGroupParamGroupName        | string                                                | Write-only (required) | Group name                                                   |
| kTIMCreateGroupParamGroupId          | string                                                | Write-only (optional) | Group ID. When this parameter is not specified, a group ID assigned by the backend is returned by a callback if the group is created successfully. If you want to set a custom group ID when creating a community group, the prefix must be "@TGS#_". |
| kTIMCreateGroupParamGroupType        | uint [TIMGroupType](#timgrouptype)                    | Write-only (optional) | Group type. The default value is `Public`.                   |
| kTIMCreateGroupParamGroupMemberArray | array [GroupMemberInfo](#groupmemberinfo)             | Write-only (optional) | Initial member array of the group                            |
| kTIMCreateGroupParamNotification     | string                                                | Write-only (optional) | Group notice                                                 |
| kTIMCreateGroupParamIntroduction     | string                                                | Write-only (optional) | Group introduction                                           |
| kTIMCreateGroupParamFaceUrl          | string                                                | Write-only (optional) | URL of the group profile photo                               |
| kTIMCreateGroupParamAddOption        | uint [TIMGroupAddOption](#timgroupaddoption)          | Write-only (optional) | Group joining option. The default value is `Any`.            |
| kTIMCreateGroupParamMaxMemberCount   | uint                                                  | Write-only (optional) | Maximum number of group members                              |
| kTIMCreateGroupParamCustomInfo       | array [GroupInfoCustemString](#groupinfocustemstring) | Write-only (optional) | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

### CreateGroupResult

Result returned by the group creation API.

| JSON Key                     | Value Type | Attribute | Description             |
| ---------------------------- | ---------- | --------- | ----------------------- |
| kTIMCreateGroupResultGroupId | string     | Read-only | ID of the created group |

### GroupInviteMemberParam

Parameters of the member invitation API.

| JSON Key                                  | Value Type   | Attribute             | Description                                        |
| ----------------------------------------- | ------------ | --------------------- | -------------------------------------------------- |
| kTIMGroupInviteMemberParamGroupId         | string       | Write-only (required) | Group ID                                           |
| kTIMGroupInviteMemberParamIdentifierArray | array string | Write-only (required) | Array of UserIDs of the users invited to the group |
| kTIMGroupInviteMemberParamUserData        | string       | Write-only (optional) | Used for custom data                               |

### HandleGroupMemberResult

Basic information of a group.

| Name                       | Description            |
| -------------------------- | ---------------------- |
| kTIMGroupMember_HandledErr | Failure                |
| kTIMGroupMember_HandledSuc | Success                |
| kTIMGroupMember_Included   | Already a group member |
| kTIMGroupMember_Invited    | Invitation sent        |

### GroupInviteMemberResult

Result returned by the member invitation API.

| JSON Key                              | Value Type                                               | Attribute | Description                         |
| ------------------------------------- | -------------------------------------------------------- | --------- | ----------------------------------- |
| kTIMGroupInviteMemberResultIdentifier | string                                                   | Read-only | ID of the user invited to the group |
| kTIMGroupInviteMemberResultResult     | uint [HandleGroupMemberResult](#handlegroupmemberresult) | Read-only | Invitation result                   |

### GroupDeleteMemberParam

Parameters of the member deletion API.

| JSON Key                                  | Value Type   | Attribute             | Description                        |
| ----------------------------------------- | ------------ | --------------------- | ---------------------------------- |
| kTIMGroupDeleteMemberParamGroupId         | string       | Write-only (required) | Group ID                           |
| kTIMGroupDeleteMemberParamIdentifierArray | array string | Write-only (required) | Array of the deleted group members |
| kTIMGroupDeleteMemberParamUserData        | string       | Write-only (required) | Used for custom data               |

### GroupDeleteMemberResult

Result returned by the member deletion API.

| JSON Key                              | Value Type                                               | Attribute | Description              |
| ------------------------------------- | -------------------------------------------------------- | --------- | ------------------------ |
| kTIMGroupDeleteMemberResultIdentifier | string                                                   | Read-only | ID of the deleted member |
| kTIMGroupDeleteMemberResultResult     | uint [HandleGroupMemberResult](#handlegroupmemberresult) | Read-only | Deletion result          |

### TIMGroupReceiveMessageOpt

Group message receiving option.

| Name                                 | Description                                                  |
| ------------------------------------ | ------------------------------------------------------------ |
| kTIMRecvGroupMsgOpt_ReceiveAndNotify | Receive group messages and notify the access side            |
| kTIMRecvGroupMsgOpt_NotReceive       | Do not receive group messages, and the server will not forward them |
| kTIMRecvGroupMsgOpt_ReceiveNotNotify | Receive group messages but do not notify the access side     |

### GroupSelfInfo

Information of the current user in the group.

| JSON Key                   | Value Type                                                   | Attribute | Description                    |
| -------------------------- | ------------------------------------------------------------ | --------- | ------------------------------ |
| kTIMGroupSelfInfoJoinTime  | uint                                                         | Read-only | Group joining time             |
| kTIMGroupSelfInfoRole      | uint                                                         | Read-only | Role of the user in the group  |
| kTIMGroupSelfInfoUnReadNum | uint                                                         | Read-only | Unread message count           |
| kTIMGroupSelfInfoMsgFlag   | uint [TIMGroupReceiveMessageOpt](#timgroupreceivemessageopt) | Read-only | Group message receiving option |

### GroupBaseInfo

Result returned by the API for obtaining the list of joined groups (basic group information).

| JSON Key                     | Value Type                             | Attribute | Description                                                  |
| ---------------------------- | -------------------------------------- | --------- | ------------------------------------------------------------ |
| kTIMGroupBaseInfoGroupId     | string                                 | Read-only | Group ID                                                     |
| kTIMGroupBaseInfoGroupName   | string                                 | Read-only | Group name                                                   |
| kTIMGroupBaseInfoGroupType   | uint [TIMGroupType](#timgrouptype)     | Read-only | Group type                                                   |
| kTIMGroupBaseInfoFaceUrl     | string                                 | Read-only | URL of the group profile photo                               |
| kTIMGroupBaseInfoInfoSeq     | uint                                   | Read-only | Sequence number of the group information. This value increases every time the group information changes. |
| kTIMGroupBaseInfoLastestSeq  | uint                                   | Read-only | Sequence number of the latest message of the group. Every message in the group has a unique sequence number. Sequence numbers are consecutive numbers based on the sequence of sent messages. The value of `LastestSeq` starts at one and increases by one for each additional message in the group. |
| kTIMGroupBaseInfoReadedSeq   | uint                                   | Read-only | Sequence number of the read message in the user group        |
| kTIMGroupBaseInfoMsgFlag     | uint                                   | Read-only | Message receiving option                                     |
| kTIMGroupBaseInfoIsShutupAll | bool                                   | Read-only | Whether the current group has muted all members              |
| kTIMGroupBaseInfoSelfInfo    | object [GroupSelfInfo](#groupselfinfo) | Read-only | Personal information of the current user in the group        |

### GroupDetailInfo

Detailed information of a group.

| JSON Key                           | Value Type                                            | Attribute | Description                                                  |
| ---------------------------------- | ----------------------------------------------------- | --------- | ------------------------------------------------------------ |
| kTIMGroupDetialInfoGroupId         | string                                                | Read-only | Group ID                                                     |
| kTIMGroupDetialInfoGroupType       | uint [TIMGroupType](#timgrouptype)                    | Read-only | Group type                                                   |
| kTIMGroupDetialInfoGroupName       | String                                                | Read-only | Group name                                                   |
| kTIMGroupDetialInfoNotification    | string                                                | Read-only | Group notice                                                 |
| kTIMGroupDetialInfoIntroduction    | string                                                | Read-only | Group introduction                                           |
| kTIMGroupDetialInfoFaceUrl         | string                                                | Read-only | URL of the group profile photo                               |
| kTIMGroupDetialInfoCreateTime      | uint                                                  | Read-only | Group creation time                                          |
| kTIMGroupDetialInfoInfoSeq         | uint                                                  | Read-only | Sequence number of the group information. This value increases every time the group information changes. |
| kTIMGroupDetialInfoLastInfoTime    | uint                                                  | Read-only | Last time when the group information was modified            |
| kTIMGroupDetialInfoNextMsgSeq      | uint                                                  | Read-only | Sequence number of the latest group message                  |
| kTIMGroupDetialInfoLastMsgTime     | uint                                                  | Read-only | Time of the latest group message                             |
| kTIMGroupDetialInfoMemberNum       | uint                                                  | Read-only | Number of current group members                              |
| kTIMGroupDetialInfoMaxMemberNum    | uint                                                  | Read-only | Maximum number of group members                              |
| kTIMGroupDetialInfoAddOption       | uint [TIMGroupAddOption](#timgroupaddoption)          | Read-only | Group joining option                                         |
| kTIMGroupDetialInfoOnlineMemberNum | uint                                                  | Read-only | Number of online group members                               |
| kTIMGroupDetialInfoVisible         | uint                                                  | Read-only | Whether group members are visible to external users          |
| kTIMGroupDetialInfoSearchable      | uint                                                  | Read-only | Whether the group can be searched                            |
| kTIMGroupDetialInfoIsShutupAll     | bool                                                  | Read-only | Whether the group has muted all members                      |
| kTIMGroupDetialInfoOwnerIdentifier | string                                                | Read-only | ID of the group owner                                        |
| kTIMGroupDetialInfoCustomInfo      | array [GroupInfoCustemString](#groupinfocustemstring) | Read-only | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

### GetGroupInfoResult

Result returned by the API for obtaining the group information list.

| JSON Key                   | Value Type                                                   | Attribute | Description                                                  |
| -------------------------- | ------------------------------------------------------------ | --------- | ------------------------------------------------------------ |
| kTIMGetGroupInfoResultCode | Int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Result of obtaining the detailed group information           |
| kTIMGetGroupInfoResultDesc | string                                                       | Read-only | Information on the failure in obtaining the detailed group information |
| kTIMGetGroupInfoResultInfo | Object [GroupDetailInfo](#groupdetailinfo)                   | Read-only | Detailed group information                                   |

### TIMGroupTopicInfo

Topic information.

| JSON Key                           | Value Type                                             | Attribute                  | Description                                                  |
| ---------------------------------- | ------------------------------------------------------ | -------------------------- | ------------------------------------------------------------ |
| kTIMGroupTopicInfoTopicID          | string                                                 | Read/Write                 | Topic ID                                                     |
| kTIMGroupTopicInfoTopicName        | string                                                 | Read/Write                 | Topic name                                                   |
| kTIMGroupTopicInfoIntroduction     | string                                                 | Read/Write                 | Topic introduction                                           |
| kTIMGroupTopicInfoNotification     | string                                                 | Read/Write                 | Topic notice                                                 |
| kTIMGroupTopicInfoTopicFaceURL     | string                                                 | Read/Write                 | Topic profile photo                                          |
| kTIMGroupTopicInfoIsAllMuted       | bool                                                   | Read/Write                 | Muting all in the topic                                      |
| kTIMGroupTopicInfoSelfMuteTime     | uint32                                                 | Read/Write                 | Muting period of the current user in the topic               |
| kTIMGroupTopicInfoCustomString     | string                                                 | Read/Write                 | Custom topic field                                           |
| kTIMGroupTopicInfoRecvOpt          | uint [TIMReceiveMessageOpt](#timreceivemessageopt)     | Read-only                  | Topic message receiving option. To modify the topic message receiving option, call the [TIMMsgSetGroupReceiveMessageOpt](https://intl.cloud.tencent.com/document/product/1047/34391) API. |
| kTIMGroupTopicInfoDraftText        | string                                                 | Read/Write                 | Topic draft                                                  |
| kTIMGroupTopicInfoUnreadCount      | uint64                                                 | Read-only                  | Number of unread messages in a topic                         |
| kTIMGroupTopicInfoLastMessage      | object [Message](#message)                             | Read-only                  | Last message of the topic                                    |
| kTIMGroupTopicInfoGroupAtInfoArray | array [GroupAtInfo](#groupatinfo)                      | Topic's @ information list |                                                              |
| kTIMGroupTopicInfoModifyFlag       | uint [TIMGroupModifyInfoFlag](#timgroupmodifyinfoflag) | Write-only (required)      | Modifies the flag. Multiple values can be set with "bitwise OR". |

### TIMGroupCounter

Result returned by the API for obtaining the group information list.

| JSON Key              | Value Type | Attribute  | Description                |
| --------------------- | ---------- | ---------- | -------------------------- |
| kTIMGroupCounterKey   | string     | Read/Write | Key of the group counter   |
| kTIMGroupCounterValue | int64      | Read/Write | Value of the group counter |

### TIMGroupModifyInfoFlag

Group information setting (modification) type.

| Name                                 | Description                                         |
| ------------------------------------ | --------------------------------------------------- |
| kTIMGroupModifyInfoFlag_None         | -                                                   |
| kTIMGroupModifyInfoFlag_Name         | Modifies the group name                             |
| kTIMGroupModifyInfoFlag_Notification | Modifies the group notice                           |
| kTIMGroupModifyInfoFlag_Introduction | Modifies the group introduction                     |
| kTIMGroupModifyInfoFlag_FaceUrl      | Modifies the group profile photo URL                |
| kTIMGroupModifyInfoFlag_AddOption    | Modifies the group joining option                   |
| kTIMGroupModifyInfoFlag_MaxMmeberNum | Modifies the maximum number of group members        |
| kTIMGroupModifyInfoFlag_Visible      | Modifies whether the group is visible               |
| kTIMGroupModifyInfoFlag_Searchable   | Modifies whether the group can be searched          |
| kTIMGroupModifyInfoFlag_ShutupAll    | Modifies whether all members are muted in the group |
| kTIMGroupModifyInfoFlag_Custom       | Modifies the custom information of the group        |
| kTIMGroupModifyInfoFlag_Owner        | Modifies the group owner                            |

### GroupModifyInfoParam

Parameters of the group information setting API.

| JSON Key                             | Value Type                                             | Attribute             | Description                                                  |
| ------------------------------------ | ------------------------------------------------------ | --------------------- | ------------------------------------------------------------ |
| kTIMGroupModifyInfoParamGroupId      | string                                                 | Write-only (required) | Group ID                                                     |
| kTIMGroupModifyInfoParamModifyFlag   | uint [TIMGroupModifyInfoFlag](#timgroupmodifyinfoflag) | Write-only (required) | Modifies the flag. Multiple values can be set with "bitwise OR". |
| kTIMGroupModifyInfoParamGroupName    | string                                                 | Write-only (optional) | Modifies the group name. This parameter must be specified only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Name`. |
| kTIMGroupModifyInfoParamNotification | string                                                 | Write-only (optional) | Modifies a group notice. This parameter must be specified only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Notification`. |
| kTIMGroupModifyInfoParamIntroduction | string                                                 | Write-only (optional) | Modifies the group introduction. This parameter must be specified only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Introduction`. |
| kTIMGroupModifyInfoParamFaceUrl      | string                                                 | Write-only (optional) | Modifies the URL of the group profile photo. This parameter must be specified only when `modify_flag` contains `kTIMGroupModifyInfoFlag_FaceUrl`. |
| kTIMGroupModifyInfoParamAddOption    | Uint                                                   | Write-only (optional) | Modifies the group joining option. This parameter must be specified only when `modify_flag` contains `kTIMGroupModifyInfoFlag_AddOption`. |
| kTIMGroupModifyInfoParamMaxMemberNum | uint                                                   | Write-only (optional) | Modifies the maximum number of group members. This parameter must be specified only when `modify_flag` contains `kTIMGroupModifyInfoFlag_MaxMmeberNum`. |
| kTIMGroupModifyInfoParamVisible      | uint                                                   | Write-only (optional) | Modifies whether the group is visible. This parameter must be specified only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Visible`. |
| kTIMGroupModifyInfoParamSearchAble   | uint                                                   | Write-only (optional) | Modifies whether the group can be searched. This parameter must be specified only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Searchable`. |
| kTIMGroupModifyInfoParamIsShutupAll  | bool                                                   | Write-only (optional) | Modifies whether all members are muted in the group. This parameter must be specified only when `modify_flag` contains `kTIMGroupModifyInfoFlag_ShutupAll`. |
| kTIMGroupModifyInfoParamOwner        | string                                                 | Write-only (optional) | Modifies the group owner. This parameter must be specified only when `modify_flag` contains `kTIMGroupModifyInfoFlag_Owner`. The `modify_flag` field containing `kTIMGroupModifyInfoFlag_Owner` cannot contain other values because it is meaningless to modify other information when you modify the group owner. |
| kTIMGroupModifyInfoParamCustomInfo   | array [GroupInfoCustemString](#groupinfocustemstring)  | Write-only (optional) | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

### GroupGetMemberInfoListParam

Parameters of the API for obtaining the group member list.

| JSON Key                                       | Value Type                                                   | Attribute             | Description                                                  |
| ---------------------------------------------- | ------------------------------------------------------------ | --------------------- | ------------------------------------------------------------ |
| kTIMGroupGetMemberInfoListParamGroupId         | string                                                       | Write-only (required) | Group ID                                                     |
| kTIMGroupGetMemberInfoListParamIdentifierArray | array string                                                 | Write-only (optional) | Group member ID list                                         |
| kTIMGroupGetMemberInfoListParamOption          | object [GroupMemberGetInfoOption](#groupmembergetinfooption) | Write-only (optional) | Option for obtaining group member information                |
| kTIMGroupGetMemberInfoListParamNextSeq         | Uint64                                                       | Write-only (optional) | Pulling-by-page flag. This parameter is set to `0` when the information is pulled for the first time. If the callback succeeds and the result is not zero, pagination is needed. The value of this parameter is passed in for the next pull until the value becomes `0`. |

### GroupGetMemberInfoListResult

Result returned by the API for obtaining the group member list.

| JSON Key                                  | Value Type                                | Attribute | Description                                                  |
| ----------------------------------------- | ----------------------------------------- | --------- | ------------------------------------------------------------ |
| kTIMGroupGetMemberInfoListResultNexSeq    | uint64                                    | Read-only | Flag for the next pull. The value 0 returned by the server indicates that no more data is available. Otherwise, this flag must be specified during the next data pull. |
| kTIMGroupGetMemberInfoListResultInfoArray | array [GroupMemberInfo](#groupmemberinfo) | Read-only | Member information list                                      |

### TIMGroupMemberModifyInfoFlag

Group member information setting (modification) type.

| Name                                 | Description                                       |
| ------------------------------------ | ------------------------------------------------- |
| kTIMGroupMemberModifyFlag_None       | -                                                 |
| kTIMGroupMemberModifyFlag_MsgFlag    | Modifies the message receiving option             |
| kTIMGroupMemberModifyFlag_MemberRole | Modifies a member role                            |
| kTIMGroupMemberModifyFlag_ShutupTime | Modifies the mute period                          |
| kTIMGroupMemberModifyFlag_NameCard   | Modifies the group name card                      |
| kTIMGroupMemberModifyFlag_Custom     | Modifies the custom information of a group member |

### GroupModifyMemberInfoParam

Parameters of the group member information setting API.

| JSON Key                                 | Value Type                                                   | Attribute             | Description                                                  |
| ---------------------------------------- | ------------------------------------------------------------ | --------------------- | ------------------------------------------------------------ |
| kTIMGroupModifyMemberInfoParamGroupId    | string                                                       | Write-only (required) | Group ID                                                     |
| kTIMGroupModifyMemberInfoParamIdentifier | string                                                       | Write-only (required) | ID of the member whose information is set                    |
| kTIMGroupModifyMemberInfoParamModifyFlag | uint [TIMGroupMemberModifyInfoFlag](#timgroupmembermodifyinfoflag) | Write-only (required) | Modification type. Multiple values can be set by using "bitwise OR". |
| kTIMGroupModifyMemberInfoParamMsgFlag    | uint                                                         | Write-only (optional) | Modifies the message receiving option. This parameter is valid only when `modify_flag` contains `kTIMGroupMemberModifyFlag_MsgFlag`. |
| kTIMGroupModifyMemberInfoParamMemberRole | uint [TIMGroupMemberRole](#timgroupmemberrole)               | Write-only (optional) | Modifies a member role. This parameter must be specified only when `modify_flag` contains `kTIMGroupMemberModifyFlag_MemberRole`. |
| kTIMGroupModifyMemberInfoParamShutupTime | uint                                                         | Write-only (optional) | Modifies the muting period. This parameter must be specified only when `modify_flag` contains `kTIMGroupMemberModifyFlag_ShutupTime`. |
| kTIMGroupModifyMemberInfoParamNameCard   | string                                                       | Write-only (optional) | Modifies the group name card. This parameter must be specified only when `modify_flag` contains `kTIMGroupMemberModifyFlag_NameCard`. |
| kTIMGroupModifyMemberInfoParamCustomInfo | array [GroupMemberInfoCustemString](#groupmemberinfocustemstring) | Write-only (optional) | See [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

### GroupPendencyOption

Parameters for obtaining the group pending request list.

| JSON Key                          | Value Type | Attribute             | Description                                                  |
| --------------------------------- | ---------- | --------------------- | ------------------------------------------------------------ |
| kTIMGroupPendencyOptionStartTime  | uint64     | Write-only (required) | Sets the pull timestamp. Enter 0 for the first request. Subsequently, enter the corresponding value based on the timestamp specified by `kTIMGroupPendencyResultNextStartTime` in [GroupPendencyResult](#grouppendencyresult) returned by the server. |
| kTIMGroupPendencyOptionMaxLimited | uint       | Write-only (optional) | Recommended amount of pulled data. The server can return data as required. This parameter cannot be used as a flag to indicate whether the operation is completed. |

### TIMGroupPendencyType

Pending request type.

| Name                           | Description                          |
| ------------------------------ | ------------------------------------ |
| kTIMGroupPendency_RequestJoin  | Requests to join a group             |
| kTIMGroupPendency_InviteJoin   | Invites to join a group              |
| kTIMGroupPendency_ReqAndInvite | Requests and invites to join a group |

### TIMGroupPendencyHandle

Processing status of the group pending request.

| Name                             | Description             |
| -------------------------------- | ----------------------- |
| kTIMGroupPendency_NotHandle      | Not handled             |
| kTIMGroupPendency_OtherHandle    | Handled by others       |
| kTIMGroupPendency_OperatorHandle | Handled by the operator |

### TIMGroupPendencyHandleResult

Processing type of the group pending request.

| Name                     | Description |
| ------------------------ | ----------- |
| kTIMGroupPendency_Refuse | Reject      |
| kTIMGroupPendency_Accept | Accept      |

### GroupPendency

Pending group request definition.

| JSON Key                             | Value Type                                                   | Attribute  | Description                                                  |
| ------------------------------------ | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| kTIMGroupPendencyGroupId             | string                                                       | Read/Write | Group ID                                                     |
| kTIMGroupPendencyFromIdentifier      | string                                                       | Read/Write | Requester's ID. For a request to join a group, this key refers to the requester's ID. For a request to invite users to a group, this key refers to the inviter's ID. |
| kTIMGroupPendencyToIdentifier        | string                                                       | Read/Write | Handler's ID, that is, ID of the admin who processes the pending group joining request |
| kTIMGroupPendencyAddTime             | uint64                                                       | Read-only  | Time when the group pending request was added                |
| kTIMGroupPendencyPendencyType        | uint [TIMGroupPendencyType](#timgrouppendencytype)           | Read-only  | Pending request type                                         |
| kTIMGroupPendencyHandled             | uint [TIMGroupPendencyHandle](#timgrouppendencyhandle)       | Read-only  | Processing status of the group pending request               |
| kTIMGroupPendencyHandleResult        | uint [TIMGroupPendencyHandleResult](#timgrouppendencyhandleresult) | Read-only  | Processing type of the group pending request                 |
| kTIMGroupPendencyApplyInviteMsg      | string                                                       | Read-only  | Additional information of the request or invitation          |
| kTIMGroupPendencyFromUserDefinedData | string                                                       | Read-only  | Custom field of the requester or inviter                     |
| kTIMGroupPendencyApprovalMsg         | string                                                       | Read-only  | Approval information: accept or reject                       |
| kTIMGroupPendencyToUserDefinedData   | string                                                       | Read-only  | Custom field of the approver                                 |
| kTIMGroupPendencyKey                 | string                                                       | Read-only  | Signing information, which customers can ignore              |
| kTIMGroupPendencyAuthentication      | string                                                       | Read-only  | Signing information, which customers can ignore              |
| kTIMGroupPendencySelfIdentifier      | string                                                       | Read-only  | Self ID                                                      |

### GroupPendencyResult

Result of obtaining the group pending request list.

| JSON Key                             | Value Type                            | Attribute | Description                                                  |
| ------------------------------------ | ------------------------------------- | --------- | ------------------------------------------------------------ |
| kTIMGroupPendencyResultNextStartTime | uint64                                | Read-only | Start timestamp of the next pull. The value 0 returned by the server indicates that no more data is available. Otherwise, the timestamp is used as the start timestamp of the next data pull. |
| kTIMGroupPendencyResultReadTimeSeq   | uint64                                | Read-only | Report timestamp of the read pending request                 |
| kTIMGroupPendencyResultUnReadNum     | uint                                  | Read-only | Number of unread pending requests                            |
| kTIMGroupPendencyResultPendencyArray | array [GroupPendency](#grouppendency) | Read-only | Group pending request list                                   |

### GroupHandlePendencyParam

Parameters of the API for processing pending group messages.

| JSON Key                              | Value Type                             | Attribute             | Description                                                  |
| ------------------------------------- | -------------------------------------- | --------------------- | ------------------------------------------------------------ |
| kTIMGroupHandlePendencyParamIsAccept  | bool                                   | Write-only (optional) | `true`: Accept; `false` (default): Reject                    |
| kTIMGroupHandlePendencyParamHandleMsg | string                                 | Write-only (optional) | Acceptance or rejection information. The default value is an empty string. |
| kTIMGroupHandlePendencyParamPendency  | object [GroupPendency](#grouppendency) | Write-only (optional) | Pending request details                                      |

### GroupGetOnlineMemberCountResult

Result of getting the number of online members of a group.

| JSON Key                               | Value Type | Attribute | Description                           |
| -------------------------------------- | ---------- | --------- | ------------------------------------- |
| TIMGroupGetOnlineMemberCountResulCount | int        | Read-only | Number of online members of the group |

### TIMGroupSearchFieldKey

Enumeration of group search fields.

| Name                              | Description |
| --------------------------------- | ----------- |
| kTIMGroupSearchFieldKey_GroupId   | Group ID    |
| kTIMGroupSearchFieldKey_GroupName | Group name  |

### GroupSearchParam

Group search parameters.

| JSON Key                       | Value Type                                              | Attribute             | Description                                             |
| ------------------------------ | ------------------------------------------------------- | --------------------- | ------------------------------------------------------- |
| TIMGroupSearchParamKeywordList | array string                                            | Write-only (optional) | Search keyword list. Up to five keywords are supported. |
| TIMGroupSearchParamFieldList   | array [TIMGroupSearchFieldKey](#timgroupsearchfieldkey) | Write-only (optional) | Search domain list.                                     |


### GroupAttributes

Group attribute map objects.

| JSON Key               | Value Type   | Attribute             | Description               |
| ---------------------- | ------------ | --------------------- | ------------------------- |
| TIMGroupAttributeKey   | string       | Write-only (optional) | Group attribute map key   |
| TIMGroupAttributeValue | array string | Write-only (optional) | Group attribute map value |

### TIMGroupMemberSearchFieldKey

Enumeration of group member search fields.

| Name                                     | Description |
| ---------------------------------------- | ----------- |
| kTIMGroupMemberSearchFieldKey_Identifier | User ID     |
| kTIMGroupMemberSearchFieldKey_NikeName   | Nickname    |
| kTIMGroupMemberSearchFieldKey_Remark     | Remarks     |
| kTIMGroupMemberSearchFieldKey_NameCard   | Name card   |

### GroupMemberSearchParam

Group member search parameters.

| JSON Key                             | Value Type                                                   | Attribute             | Description                                                  |
| ------------------------------------ | ------------------------------------------------------------ | --------------------- | ------------------------------------------------------------ |
| TIMGroupMemberSearchParamGroupidList | array string                                                 | Write-only (optional) | Group ID list. If no value is passed in, group members of all groups are searched. |
| TIMGroupMemberSearchParamKeywordList | array string                                                 | Write-only (optional) | Search keyword list. Up to five keywords are supported.      |
| TIMGroupMemberSearchParamFieldList   | array [TIMGroupMemberSearchFieldKey](#timgroupmembersearchfieldkey) | Write-only (optional) | Search domain list.                                          |

## Key Relationship Chain and Profile Types

Definitions of macros related to relationship chains and profiles and definitions of JSON keys accessed by related structure members.

### FriendShipGetProfileListParam

Parameters of the API for processing pending group messages.

| JSON Key                                         | Value Type   | Attribute  | Description                                                  |
| ------------------------------------------------ | ------------ | ---------- | ------------------------------------------------------------ |
| kTIMFriendShipGetProfileListParamIdentifierArray | array string | Write-only | List of UserIDs whose profiles are to be obtained            |
| kTIMFriendShipGetProfileListParamForceUpdate     | bool         | Write-only | Whether to update profiles forcibly. `false` (default): Profiles are preferentially obtained from the local cache, and if such an attempt fails, profiles are pulled from the network; `true`: Profiles are directly pulled from the network. |

### TIMGenderType

User gender type.

| Name                  | Description |
| --------------------- | ----------- |
| kTIMGenderType_Unkown | Unknown     |
| kTIMGenderType_Male   | Male        |
| kTIMGenderType_Female | Female      |

### TIMProfileAddPermission

Friend adding option.

| Name                                 | Description                                  |
| ------------------------------------ | -------------------------------------------- |
| kTIMProfileAddPermission_Unknown     | Unknown                                      |
| kTIMProfileAddPermission_AllowAny    | Automatically accept all new friend requests |
| kTIMProfileAddPermission_NeedConfirm | Friend request verification is required      |
| kTIMProfileAddPermission_DenyAny     | Automatically reject all new friend requests |

### UserProfileCustemStringInfo

Custom profile field, of string type.

| JSON Key                             | Value Type | Attribute  | Description                                                  |
| ------------------------------------ | ---------- | ---------- | ------------------------------------------------------------ |
| kTIMUserProfileCustemStringInfoKey   | string     | Write-only | Value of key of the custom profile field (including the prefix `Tag_Profile_Custom_`) |
| kTIMUserProfileCustemStringInfoValue | string     | Write-only | String value corresponding to the field                      |

>?The string length cannot exceed 500 bytes.


### UserProfile

| JSON Key                         | Value Type                                                   | Attribute | Description                                                  |
| -------------------------------- | ------------------------------------------------------------ | --------- | ------------------------------------------------------------ |
| kTIMUserProfileIdentifier        | string                                                       | Read-only | User ID                                                      |
| kTIMUserProfileNickName          | string                                                       | Read-only | User nickname                                                |
| kTIMUserProfileGender            | uint [TIMGenderType](#timgendertype)                         | Read-only | Gender                                                       |
| kTIMUserProfileFaceUrl           | string                                                       | Read-only | Profile photo URL of the user                                |
| kTIMUserProfileSelfSignature     | string                                                       | Read-only | Personal signature of the user                               |
| kTIMUserProfileAddPermission     | uint [TIMProfileAddPermission](#timprofileaddpermission)     | Read-only | Friend adding option                                         |
| kTIMUserProfileLocation          | string                                                       | Read-only | User location information                                    |
| kTIMUserProfileLanguage          | uint                                                         | Read-only | Language                                                     |
| kTIMUserProfileBirthDay          | uint                                                         | Read-only | Birthday                                                     |
| kTIMUserProfileLevel             | uint                                                         | Read-only | Level                                                        |
| kTIMUserProfileRole              | uint                                                         | Read-only | Role                                                         |
| kTIMUserProfileCustomStringArray | array [UserProfileCustemStringInfo](#userprofilecustemstringinfo) | Read-only | See [Custom Profile Fields](https://intl.cloud.tencent.com/document/product/1047/33520). |

### UserProfileItem

| JSON Key                             | Value Type                                                   | Attribute  | Description                                                  |
| ------------------------------------ | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| kTIMUserProfileItemNickName          | string                                                       | Write-only | Modifies the user nickname                                   |
| kTIMUserProfileItemGender            | uint [TIMGenderType](#timgendertype)                         | Write-only | Modifies the user gender                                     |
| kTIMUserProfileItemFaceUrl           | string                                                       | Write-only | Modifies the user profile photo                              |
| kTIMUserProfileItemSelfSignature     | string                                                       | Write-only | Modifies the user signature                                  |
| kTIMUserProfileItemAddPermission     | uint [TIMProfileAddPermission](#timprofileaddpermission)     | Write-only | Modifies the friend adding option                            |
| kTIMUserProfileItemLoaction          | uint                                                         | Write-only | Modifies the location                                        |
| kTIMUserProfileItemLanguage          | uint                                                         | Write-only | Modifies the language                                        |
| kTIMUserProfileItemBirthDay          | uint                                                         | Write-only | Modifies the birthday                                        |
| kTIMUserProfileItemLevel             | uint                                                         | Write-only | Modifies the level                                           |
| kTIMUserProfileItemRole              | uint                                                         | Write-only | Modifies the role                                            |
| kTIMUserProfileItemCustomStringArray | Array [UserProfileCustemStringInfo](#userprofilecustemstringinfo) | Write-only | Modifies [custom profile fields](https://intl.cloud.tencent.com/document/product/1047/33520) |

### FriendProfileCustemStringInfo

| JSON Key                               | Value Type | Attribute  | Description                              |
| -------------------------------------- | ---------- | ---------- | ---------------------------------------- |
| kTIMFriendProfileCustemStringInfoKey   | string     | Write-only | Key of the custom friend profile field   |
| kTIMFriendProfileCustemStringInfoValue | string     | Write-only | Value of the custom friend profile field |

### FriendProfile

Friend profile.

| JSON Key                           | Value Type                                                   | Attribute | Description                                                  |
| ---------------------------------- | ------------------------------------------------------------ | --------- | ------------------------------------------------------------ |
| kTIMFriendProfileIdentifier        | string                                                       | Read-only | UserID of the friend                                         |
| kTIMFriendProfileGroupNameArray    | array string                                                 | Read-only | List of friend list names                                    |
| kTIMFriendProfileRemark            | String                                                       | Read-only | Friend remarks, which is 96 bytes at most. This parameter is empty if you obtain your own profile. |
| kTIMFriendProfileAddWording        | string                                                       | Read-only | Friend request reason                                        |
| kTIMFriendProfileAddSource         | string                                                       | Read-only | Friend request source                                        |
| kTIMFriendProfileAddTime           | uint64                                                       | Read-only | Time when the friend was added                               |
| kTIMFriendProfileUserProfile       | object [UserProfile](#userprofile)                           | Read-only | Personal profile of the friend                               |
| kTIMFriendProfileCustomStringArray | Array [FriendProfileCustemStringInfo](#friendprofilecustemstringinfo) | Read-only | [Custom friend fields](https://intl.cloud.tencent.com/document/product/1047/33521) |

### FriendProfileItem

| JSON Key                               | Value Type                                                   | Attribute            | Description                                                  |
| -------------------------------------- | ------------------------------------------------------------ | -------------------- | ------------------------------------------------------------ |
| kTIMFriendProfileItemRemark            | string                                                       | Write-only           | Modifies the friend remarks                                  |
| kTIMFriendProfileItemGroupNameArray    | array string                                                 | Modifies the remarks | Modifies the list of friend list names                       |
| kTIMFriendProfileItemCustomStringArray | Array [FriendProfileCustemStringInfo](#friendprofilecustemstringinfo) | Write-only           | Modifies [custom friend fields](https://intl.cloud.tencent.com/document/product/1047/33521) |

### TIMFriendType

| Name             | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| FriendTypeSignle | One-way friend relationship: B is on A's contacts, but A is not on B's contacts |
| FriendTypeBoth   | Two-way friend relationship: A and B are on each other's contacts |

### FriendshipAddFriendParam

Parameters of the friend adding API.

| JSON Key                               | Value Type                           | Attribute  | Description                              |
| -------------------------------------- | ------------------------------------ | ---------- | ---------------------------------------- |
| kTIMFriendshipAddFriendParamIdentifier | string                               | Write-only | UserID that initiates the friend request |
| kTIMFriendshipAddFriendParamFriendType | uint [TIMFriendType](#timfriendtype) | Write-only | Friend type of the friend request        |
| kTIMFriendshipAddFriendParamRemark     | string                               | Write-only | Preliminary remarks                      |
| kTIMFriendshipAddFriendParamGroupName  | string                               | Write-only | Preliminary group name                   |
| kTIMFriendshipAddFriendParamAddSource  | string                               | Write-only | Description of the friend request source |
| kTIMFriendshipAddFriendParamAddWording | string                               | Write-only | Friend request message                   |

### FriendResult

| JSON Key                   | Value Type                                                   | Attribute | Description                                                  |
| -------------------------- | ------------------------------------------------------------ | --------- | ------------------------------------------------------------ |
| kTIMFriendResultIdentifier | string                                                       | Read-only | ID of the user who performs the relationship chain operation |
| kTIMFriendResultCode       | Int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Result of the relationship chain operation                   |
| kTIMFriendResultDesc       | string                                                       | Read-only | Detailed description of the relationship chain operation failure |

### FriendshipModifyFriendProfileParam

| JSON Key                                         | Value Type                                     | Attribute  | Description                     |
| ------------------------------------------------ | ---------------------------------------------- | ---------- | ------------------------------- |
| kTIMFriendshipModifyFriendProfileParamIdentifier | string                                         | Write-only | UserID of the modified friend   |
| kTIMFriendshipModifyFriendProfileParamItem       | object [FriendProfileItem](#friendprofileitem) | Write-only | Modified friend profile options |

### FriendAddPendency

| JSON Key                        | Value Type | Attribute | Description                                            |
| ------------------------------- | ---------- | --------- | ------------------------------------------------------ |
| kTIMFriendAddPendencyIdentifier | string     | Read-only | UserID of the friend request initiator                 |
| kTIMFriendAddPendencyNickName   | string     | Read-only | Nickname of the friend request initiator               |
| kTIMFriendAddPendencyAddSource  | string     | Read-only | Source of the friend request initiator                 |
| kTIMFriendAddPendencyAddWording | string     | Read-only | Friend request message of the friend request initiator |

### TIMFriendPendencyType

| Name                      | Description                             |
| ------------------------- | --------------------------------------- |
| FriendPendencyTypeComeIn  | Friend request received by me           |
| FriendPendencyTypeSendOut | Friend request sent by me               |
| FriendPendencyTypeBoth    | Friend requests received and sent by me |

### FriendshipGetPendencyListParam

| JSON Key                                      | Value Type                                           | Attribute  | Description                                                  |
| --------------------------------------------- | ---------------------------------------------------- | ---------- | ------------------------------------------------------------ |
| kTIMFriendshipGetPendencyListParamType        | uint [TIMFriendPendencyType](#timfriendpendencytype) | Write-only | Type of the pending friend request                           |
| kTIMFriendshipGetPendencyListParamStartSeq    | uint64                                               | Write-only | Start sequence number for getting the list of group pending requests by page. The largest sequence number contained in the returned result for the current page is used as the start sequence number of the next page. |
| kTIMFriendshipGetPendencyListParamStartTime   | uint64                                               | Write-only | Gets the start timestamp of the pending request information  |
| kTIMFriendshipGetPendencyListParamLimitedSize | int                                                  | Write-only | Gets the number of items on each page of the pending request list |

### PendencyPage

| JSON Key                          | Value Type                                            | Attribute | Description                                                  |
| --------------------------------- | ----------------------------------------------------- | --------- | ------------------------------------------------------------ |
| kTIMPendencyPageStartTime         | uint64                                                | Read-only | Start time of the pending request information page           |
| kTIMPendencyPageUnReadNum         | uint64                                                | Read-only | Number of unread requests on the pending request information page |
| kTIMPendencyPageCurrentSeq        | uint64                                                | Read-only | Current sequence number of the pending request information page |
| kTIMPendencyPagePendencyInfoArray | array [FriendAddPendencyInfo](#friendaddpendencyinfo) | Read-only | Pending request information list on the pending request information page |

### FriendAddPendencyInfo

| JSON Key                            | Value Type                                           | Attribute | Description                                             |
| ----------------------------------- | ---------------------------------------------------- | --------- | ------------------------------------------------------- |
| kTIMFriendAddPendencyInfoType       | uint [TIMFriendPendencyType](#timfriendpendencytype) | Read-only | Type of the pending friend request                      |
| kTIMFriendAddPendencyInfoIdentifier | string                                               | Read-only | UserID of the initiator of the pending friend request   |
| kTIMFriendAddPendencyInfoNickName   | string                                               | Read-only | Nickname of the initiator of the pending friend request |
| kTIMFriendAddPendencyInfoAddTime    | uint64                                               | Read-only | Time when the friend request is initiated successfully  |
| kTIMFriendAddPendencyInfoAddSource  | string                                               | Read-only | Source of the initiator of the pending friend request   |
| kTIMFriendAddPendencyInfoAddWording | string                                               | Read-only | Friend request message in the pending friend request    |

### FriendshipDeletePendencyParam

| JSON Key                                         | Value Type                                           | Attribute | Description                                                  |
| ------------------------------------------------ | ---------------------------------------------------- | --------- | ------------------------------------------------------------ |
| kTIMFriendshipDeletePendencyParamType            | uint [TIMFriendPendencyType](#timfriendpendencytype) | Read-only | Type of the pending friend request                           |
| kTIMFriendshipDeletePendencyParamIdentifierArray | array string                                         | Read-only | List of UserIDs corresponding to the pending friend requests to delete |

### TIMFriendResponseAction

| Name                      | Description   |
| ------------------------- | ------------- |
| ResponseActionAgree       | Agree         |
| ResponseActionAgreeAndAdd | Agree and add |
| ResponseActionReject      | Reject        |

### FriendRespone

| JSON Key                    | Value Type                                               | Attribute             | Description                           |
| --------------------------- | -------------------------------------------------------- | --------------------- | ------------------------------------- |
| kTIMFriendResponeIdentifier | string                                                   | Write-only (required) | UserID of the friend request response |
| kTIMFriendResponeAction     | uint [TIMFriendResponseAction](#timfriendresponseaction) | Write-only (required) | Action of the friend request response |
| kTIMFriendResponeRemark     | string                                                   | Write-only (optional) | Friend remarks                        |
| kTIMFriendResponeGroupName  | string                                                   | Write-only (optional) | List of friend lists                  |

### FriendshipDeleteFriendParam

| JSON Key                                       | Value Type                           | Attribute             | Description                      |
| ---------------------------------------------- | ------------------------------------ | --------------------- | -------------------------------- |
| kTIMFriendshipDeleteFriendParamFriendType      | uint [TIMFriendType](#timfriendtype) | Write-only            | Type of the friends to delete    |
| kTIMFriendshipDeleteFriendParamIdentifierArray | array string                         | Write-only (optional) | List of friend UserIDs to delete |

### FriendGroupInfo

| JSON Key                                            | Value Type   | Attribute  | Description                                                  |
| --------------------------------------------------- | ------------ | ---------- | ------------------------------------------------------------ |
| kTIMFriendshipCreateFriendGroupParamNameArray       | Array string | Write-only | List of the names of the created friend lists                |
| kTIMFriendshipCreateFriendGroupParamIdentifierArray | Array string | Write-only | List of the friend UserIDs to be added to the created friend list |

### FriendGroupInfo

| JSON Key                           | Value Type   | Attribute | Description                                           |
| ---------------------------------- | ------------ | --------- | ----------------------------------------------------- |
| kTIMFriendGroupInfoName            | string       | Read-only | Friend list name                                      |
| kTIMFriendGroupInfoCount           | uint64       | Read-only | Number of friends in the current friend list          |
| kTIMFriendGroupInfoIdentifierArray | array string | Read-only | List of the friend UserIDs in the current friend list |

### FriendshipModifyFriendGroupParam

| JSON Key                                                  | Value Type   | Attribute             | Description                                                  |
| --------------------------------------------------------- | ------------ | --------------------- | ------------------------------------------------------------ |
| kTIMFriendshipModifyFriendGroupParamName                  | string       | Write-only            | Original name of the modified friend list                    |
| kTIMFriendshipModifyFriendGroupParamNewName               | string       | Write-only (optional) | New name of the modified friend list                         |
| kTIMFriendshipModifyFriendGroupParamDeleteIdentifierArray | array string | Write-only (optional) | List of friend UserIDs to be deleted from the current friend list |
| kTIMFriendshipModifyFriendGroupParamAddIdentifierArray    | Array string | Write-only (optional) | List of friend UserIDs to be added to the current friend list |

### FriendshipCheckFriendTypeParam

| JSON Key                                          | Value Type                           | Attribute  | Description                     |
| ------------------------------------------------- | ------------------------------------ | ---------- | ------------------------------- |
| kTIMFriendshipCheckFriendTypeParamCheckType       | uint [TIMFriendType](#timfriendtype) | Write-only | Type of the friend to check     |
| kTIMFriendshipCheckFriendTypeParamIdentifierArray | array string                         | Write-only | List of friend UserIDs to check |

### TIMFriendCheckRelation

| Name                  | Description                                       |
| --------------------- | ------------------------------------------------- |
| FriendCheckNoRelation | No relationship                                   |
| FriendCheckAWithB     | B is on A's contacts but A is not on B's contacts |
| FriendCheckBWithA     | A is on B's contacts but B is not on A's contacts |
| FriendCheckBothWay    | Two-way friend relationship                       |

### FriendshipCheckFriendTypeResult

| JSON Key                                      | Value Type                                                   | Attribute | Description                                                 |
| --------------------------------------------- | ------------------------------------------------------------ | --------- | ----------------------------------------------------------- |
| kTIMFriendshipCheckFriendTypeResultIdentifier | string                                                       | Read-only | UserID of the friend checked                                |
| kTIMFriendshipCheckFriendTypeResultRelation   | uint [TIMFriendCheckRelation](#timfriendcheckrelation)       | Read-only | Relationship between the two parties after successful check |
| kTIMFriendshipCheckFriendTypeResultCode       | Int [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) | Read-only | Check result                                                |
| kTIMFriendshipCheckFriendTypeResultDesc       | string                                                       | Read-only | Description of friend check failure                         |

### TIMFriendshipSearchFieldKey

Friend search enumeration.

| Name                                    | Description |
| --------------------------------------- | ----------- |
| kTIMFriendshipSearchFieldKey_Identifier | User ID     |
| kTIMFriendshipSearchFieldKey_NikeName   | Nickname    |
| kTIMFriendshipSearchFieldKey_Remark     | Remarks     |

### FriendSearchParam

| JSON Key                                 | Value Type   | Attribute  | Description                                             |
| ---------------------------------------- | ------------ | ---------- | ------------------------------------------------------- |
| kTIMFriendshipSearchParamKeywordList     | array string | Write-only | Search keyword list. Up to five keywords are supported. |
| kTIMFriendshipSearchParamSearchFieldList | array int    | Write-only | Friend search type.                                     |

### TIMFriendshipRelationType

Relationship between the two parties.

| Name                                         | Description                                                  |
| -------------------------------------------- | ------------------------------------------------------------ |
| kTIMFriendshipRelationType_None              | Unknown relationship.                                        |
| kTIMFriendshipRelationType_InMyFriendList    | One-way friend: The peer is my friend, but I am not the peer's friend. |
| kTIMFriendshipRelationType_InOtherFriendList | One-way friend: The peer is not my friend, but I am the peer's friend. |
| kTIMFriendshipRelationType_BothFriend        | Two-way friend.                                              |

### FriendInfoGetResult

| JSON Key                                      | Value Type                                                   | Attribute | Description           |
| --------------------------------------------- | ------------------------------------------------------------ | --------- | --------------------- |
| kTIMFriendshipFriendInfoGetResultIdentifier   | string                                                       | Read-only | User ID of the friend |
| kTIMFriendshipFriendInfoGetResultRelationType | uint [TIMFriendshipRelationType](#timfriendshiprelationtype) | Read-only | Friend relationship   |
| kTIMFriendshipFriendInfoGetResultErrorCode    | uint                                                         | Read-only | Error code            |
| kTIMFriendshipFriendInfoGetResultErrorMessage | string                                                       | Read-only | Error description     |
| kTIMFriendshipFriendInfoGetResultFriendInfo   | array [FriendProfile](#friendprofile)                        | Read-only | Profile of the friend |
