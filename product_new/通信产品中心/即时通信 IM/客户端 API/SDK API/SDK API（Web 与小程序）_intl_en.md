## TIM

TIM is the namespace of the IM Web SDK, and provides the static method [create()](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/TIM.html#.create) for creating SDK instances, the event constant [EVENT](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html), and the type constant [TYPES](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html).

**Initialization**

| API | Description |
| --- | --- |
| [create](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/TIM.html#.create) | Creates an SDK instance. |

## SDK instance

| Concept | Description |
| :--- | :---- |
| Message | [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html) indicates the content to be sent and carries multiple attributes which specify whether you are the sender, the sender account, the message generation time, and so on. |
| Conversation | Two types of [Conversation](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Conversation.html) are available:<li>Client to Client (C2C): a one-to-one chat, involving only 2 participants.</li><li>GROUP: a group chat, involving more than 2 participants. |
| Profile | [Profile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Profile.html) describes the basic information of a user, including the nickname, gender, personal signature, and profile photo address. |
| Group | [Group](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html) is a communication system for group chatting. Many types of groups are available: private group, public group, chat room, and audio-and-video chat room. |
| GroupMember (Group member) | [GroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html) indicates the basic information of each group member, such as the ID, nickname, role, and the time of joining the group. |
| Group notification | A group notification is generated when an event such as group member adding or deletion occurs. You can configure whether to display group notifications to group members.<br/>For more information about group notification types, see [Message.GroupTipPayload](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload).|
| Group system message | For example, when a user applies for joining a group, the group admins will receive a system message. After an admin accepts or denies the application, the IM SDK will return the application result to the access terminal, and then the user can view the result displayed on the access terminal.<br/>For more information about types of group system messages, see [Message.GroupSystemNoticePayload](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload).  |
| Message display on Screen | The sent messages, including text segments and images, are displayed on the computer or phone screen. |

### Login
| API | Description |
| --- | --- |
| [login](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#login) | Logs in. |
| [logout](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#logout) | Logs out. |


### Message
| API | Description |
| --- | --- |
| [createTextMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createTextMessage) | Creates a text message. |
| [createImageMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createImageMessage) | Creates an image message. |
| [createAudioMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createAudioMessage) | Creates a voice message. |
| [createVideoMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createVideoMessage) | Creates a video message. |
| [createCustomMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createCustomMessage) | Creates a custom message. |
| [createFaceMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFaceMessage) | Creates a sticker message. |
| [createFileMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFileMessage) | Creates a file message. |
| [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) | Sends a message. |
| [resendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#resendMessage) | Sends a message again. |
| [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) | Obtains the message list.  |
| [setMessageRead](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setMessageRead) | Sets message read receipt.  |

### Conversation
| API | Description |
| --- | --- |
| [getConversationList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getConversationList) | Obtains the conversation list. |
| [getConversationProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getConversationProfile) | Obtains the conversation information. |
| [deleteConversation](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#deleteConversation) | Deletes a conversation. |

### Profile
| API | Description |
| --- | --- |
| [getMyProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMyProfile) | Obtains your personal profile. |
| [getUserProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getUserProfile) | Obtains other user’s profile. |
| [updateMyProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateMyProfile) | Updates your personal profile. |
| [getBlacklist](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getBlacklist) | Obtains your blacklist. |
| [addToBlacklist](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#addToBlacklist) | Adds a user to the blacklist. |
| [removeFromBlacklist](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#removeFromBlacklist) | Deletes a user from the blacklist. |

### Group
| API | Description |
| --- | --- |
| [getGroupList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupList) | Obtains the group list. |
| [getGroupProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupProfile) | Obtains the group information. |
| [createGroup](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createGroup) | Creates a group. |
| [dismissGroup](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#dismissGroup) | Disbands a group. |
| [updateGroupProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateGroupProfile) | Modifies the group information. |
| [joinGroup](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#joinGroup) | Applies for joining a group. |
| [quitGroup](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#quitGroup) | Quits a group. |
| [searchGroupByID](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#searchGroupByID) | Searches for a group. |
| [changeGroupOwner](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#changeGroupOwner) | Transfers the group ownership. |
| [handleGroupApplication](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#handleGroupApplication) | Processes applications for joining the group. |
| [setMessageRemindType](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setMessageRemindType) | Specifies the notification type of group messages. |

### Group member
| API | Description |
| --- | --- |
| [getGroupMemberList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberList) | Obtains the group member list. |
| [getGroupMemberProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberProfile) | Obtains a group member’s profile. |
| [addGroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#addGroupMember) | Adds a group member. |
| [deleteGroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#deleteGroupMember) | Deletes a group member. |
| [setGroupMemberMuteTime](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setGroupMemberMuteTime) |Configures muted period.|
| [setGroupMemberRole](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setGroupMemberRole) | Modifies the group member’s role. |
| [setGroupMemberNameCard](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setGroupMemberNameCard) | Configures the name card for a group member. |
| [setGroupMemberCustomField](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setGroupMemberCustomField) | Configures a custom field for a group member. |

### Others
| API | Description |
| --- | --- |
| [on](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#on) | Enables event listening. |
| [off](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#off) | Disables event listening. |
| [registerPlugin](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#registerPlugin) | Registers a plugin. |
| [setLogLevel](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel) | Configures the log level. |

