
## TIM

TIM is the namespace of the IM Web SDK and provides the static method [create()](https://web.sdk.qcloud.com/im/doc/zh-cn//TIM.html#.create) for creating SDK instances, the event constant [EVENT](https://web.sdk.qcloud.com/im/doc/zh-cn//module-EVENT.html), and the type constant [TYPES](https://web.sdk.qcloud.com/im/doc/zh-cn//module-TYPES.html).

**Initialization**

| API | Description |
| --- | --- |
| [create](https://web.sdk.qcloud.com/im/doc/zh-cn//TIM.html#.create) | Creates an SDK instance. |

## SDK Instance

| Term| Description |
| :--- | :---- |
| Message | [Message](https://web.sdk.qcloud.com/im/doc/zh-cn//Message.html) indicates the content to be sent and carries multiple attributes which specify whether you are the sender, the sender account, the message generation time, and so on. |
| Conversation | Two types of [Conversation](https://web.sdk.qcloud.com/im/doc/zh-cn//Conversation.html) are available: <li>Client to Client (C2C): a one-to-one chat, involving only 2 participants.</li><li>GROUP: a group chat, involving more than 2 participants. |
| Profile | [Profile](https://web.sdk.qcloud.com/im/doc/zh-cn//Profile.html) describes the basic information of a user, including the nickname, gender, personal signature, and profile photo address. |
| Group | [Group](https://web.sdk.qcloud.com/im/doc/zh-cn//Group.html) indicates a communication system for group chatting, including Work, Public, Meeting, and AVChatRoom. |
| GroupMember (group member) | [GroupMember](https://web.sdk.qcloud.com/im/doc/zh-cn//GroupMember.html) indicates the basic information of each group member, such as the ID, nickname, role, and the time of joining the group. |
| Group notification | A group notification is generated when an event such as adding or deleting group member occurs. The access side can configure whether to display group notifications to group members. <br/>For more information about group notification types, see [Message.GroupTipPayload](https://web.sdk.qcloud.com/im/doc/zh-cn//Message.html#.GroupTipPayload).|
| Group system message | For example, when a user requests to join a group, the group admin receives a system message. After the admin accepts or rejects the request, the IM SDK returns the result to the access side, which then displays the result to the user. <br/>For more information about group system message types, see [Message.GroupSystemNoticePayload](https://web.sdk.qcloud.com/im/doc/zh-cn//Message.html#.GroupSystemNoticePayload). |
| Message display on screen | The sent messages, including text segments and images, are displayed on the computer or phone screen. |

### Login
| API | Description |
| --- | --- |
| [login](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#login) | Logs in. |
| [logout](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#logout) | Logs out. |


### Message
| API | Description |
| --- | --- |
| [createTextMessage](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#createTextMessage) | Creates a text message. |
| [createImageMessage](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#createImageMessage) | Creates an image message. |
| [createAudioMessage](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#createAudioMessage) | Creates a voice message. |
| [createVideoMessage](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#createVideoMessage) | Creates a video message. |
| [createCustomMessage](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#createCustomMessage) | Creates a custom message. |
| [createFaceMessage](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#createFaceMessage) | Creates an emoji message. |
| [createFileMessage](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#createFileMessage) | Creates a file message. |
| [sendMessage](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#sendMessage) | Sends a message. |
| [revokeMessage](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#revokeMessage) | Recalls a message. |
| [resendMessage](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#resendMessage) | Sends a message again. |
| [getMessageList](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#getMessageList) | Gets the message list.  |
| [setMessageRead](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#setMessageRead) | Sets a message as read.  |

### Conversation
| API | Description |
| --- | --- |
| [getConversationList](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#getConversationList) | Gets the conversation list. |
| [getConversationProfile](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#getConversationProfile) | Gets the conversation information. |
| [deleteConversation](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#deleteConversation) | Deletes a conversation. |

### Profile
| API | Description |
| --- | --- |
| [getMyProfile](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#getMyProfile) | Gets your personal profile. |
| [getUserProfile](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#getUserProfile) | Gets other user’s profile. |
| [updateMyProfile](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#updateMyProfile) | Updates your personal profile. |
| [getBlacklist](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#getBlacklist) | Gets your blocklist. |
| [addToBlacklist](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#addToBlacklist) | Adds a user to the blocklist. |
| [removeFromBlacklist](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#removeFromBlacklist) | Removes a user from the blocklist. |

### Group
| API | Description |
| --- | --- |
| [getGroupList](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#getGroupList) | Gets the group list. |
| [getGroupProfile](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#getGroupProfile) | Gets the group profile. |
| [createGroup](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#createGroup) | Creates a group. |
| [dismissGroup](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#dismissGroup) | Deletes a group. |
| [updateGroupProfile](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#updateGroupProfile) | Modifies the group profile. |
| [joinGroup](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#joinGroup) | Requests to join a group. |
| [quitGroup](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#quitGroup) | Quits a group. |
| [searchGroupByID](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#searchGroupByID) | Searches for a group. |
| [changeGroupOwner](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#changeGroupOwner) | Transfers the group ownership. |
| [handleGroupApplication](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#handleGroupApplication) | Processes requests to join the group. |
| [setMessageRemindType](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#setMessageRemindType) | Specifies the notification type of group messages. |

### Group member
| API | Description |
| --- | --- |
| [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#getGroupMemberList) | Gets the group member list. |
| [getGroupMemberProfile](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#getGroupMemberProfile) | Gets a group member’s profile. |
| [addGroupMember](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#addGroupMember) | Adds a group member. |
| [deleteGroupMember](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#deleteGroupMember) | Deletes a group member. |
| [setGroupMemberMuteTime](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#setGroupMemberMuteTime) |Configures the muting period.|
| [setGroupMemberRole](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#setGroupMemberRole) | Modifies the group member’s role. |
| [setGroupMemberNameCard](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#setGroupMemberNameCard) | Sets the name card for a group member. |
| [setGroupMemberCustomField](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#setGroupMemberCustomField) | Sets a custom field for a group member. |

### Others
| API | Description |
| --- | --- |
| [on](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#on) | Enables event listening. |
| [off](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#off) | Disables event listening. |
| [registerPlugin](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#registerPlugin) | Registers a plugin. |
| [setLogLevel](https://web.sdk.qcloud.com/im/doc/zh-cn//SDK.html#setLogLevel) | Sets the log level. |



