## TIM

TIM is the namespace of the IM Web SDK and provides the static method [create()](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/TIM.html#.create) for creating SDK instances, the event constant [EVENT](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html), and the type constant [TYPES](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html).

**Initialization**

| API | Description |
| --- | --- |
| [create](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/TIM.html#.create) | Creates an SDK instance. |

## SDK Instance

| Term| Description |
| :--- | :---- |
| Message | [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html) indicates the content to be sent and carries multiple attributes which specify whether you are the sender, the sender account, the message generation time, and so on. |
| Conversation | Two types of [Conversation](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Conversation.html) are available:<li>Client to Client (C2C): a one-to-one chat, involving only 2 participants.</li><li>GROUP: a group chat, involving more than 2 participants. |
| Profile | [Profile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Profile.html) describes the basic information of a user, including the nickname, gender, personal signature, and profile photo address. |
| Group | [Group](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html) in IM SDK is a  communication system for group chatting, including Work, Public, Meeting, and AVChatRoom.|
|GroupMember (Group member) | [GroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html) indicates the basic information of each group member, such as the ID, nickname, role, and the time of joining the group. |
| Group notification | A group notification is generated when an event such as group member addition or deletion occurs. You can configure whether to display group notifications to group members.<br/>For more information about group notification types, see [Message.GroupTipPayload](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload).|
| Group system message | For example, when a user applies for joining a group, the group admin receives a system message. After the admin accepts or denies the application, the IM SDK returns the application result to the access terminal, and then the user can view the result displayed on the access terminal.<br/>For more information about types of group system messages, see [Message.GroupSystemNoticePayload](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload). |
| Message display on screen | This is the process by which messages, including text and images, are displayed on the computer or phone screen after the user clicks send. |

### Login
| API | Description |
| --- | --- |
| [login](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#login) | Logs in to the IM. |
| [logout](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#logout) | Logs out of the IM console. |


### Message
| API | Description |
| --- | --- |
| [createTextMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createTextMessage) | Creates a text message. |
| [createImageMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createImageMessage) | Creates an image message. |
| [createAudioMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createAudioMessage) | Creates a voice message. |
| [createVideoMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createVideoMessage) | Creates a video message. |
| [createCustomMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createCustomMessage) | Creates a custom message. |
| [createFaceMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFaceMessage) | Creates an emoji message. |
| [createFileMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFileMessage) | Creates a file message. |
| [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) | Sends a message. |
| [revokeMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#revokeMessage) | Recalls a message. |
| [resendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#resendMessage) | Resends a message. |
| [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) | Obtains the message list. |
| [setMessageRead](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setMessageRead) | Sets a message to the read state. |

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
| [getUserProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getUserProfile) | Obtains the profile of a user. |
| [updateMyProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateMyProfile) | Updates your personal profile. |
| [getBlacklist](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getBlacklist) | Obtains your blocklist. |
| [addToBlacklist](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#addToBlacklist) | Adds a user to the blocklist. |
| [removeFromBlacklist](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#removeFromBlacklist) | Deletes a user from the blocklist. |

### Group
| API | Description |
| --- | --- |
| [getGroupList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupList) | Obtains the group list. |
| [getGroupProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupProfile) | Obtains the group profile. |
| [createGroup](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createGroup) | Creates a group. |
| [dismissGroup](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#dismissGroup) | Disbands a group. |
| [updateGroupProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateGroupProfile) | Modifies the group profile. |
| [joinGroup](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#joinGroup) | Applies to join a group. |
| [quitGroup](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#quitGroup) | Quits a group. |
| [searchGroupByID](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#searchGroupByID) | Searches for a group. |
| [changeGroupOwner](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#changeGroupOwner) | Transfers the ownership of a group. |
| [handleGroupApplication](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#handleGroupApplication) | Processes an application for joining a group. |
| [setMessageRemindType](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setMessageRemindType) | Specifies the notification type of group messages. |

### Group member
| API | Description |
| --- | --- |
| [getGroupMemberList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberList) | Obtains the group member list. |
| [getGroupMemberProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberProfile) | Obtains a group member’s profile. |
| [addGroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#addGroupMember) | Adds a group member. |
| [deleteGroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#deleteGroupMember) | Deletes a group member. |
| [setGroupMemberMuteTime](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setGroupMemberMuteTime) | Configures the muting period for a group member. |
| [setGroupMemberRole](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setGroupMemberRole) | Modifies the role of a group member. |
| [setGroupMemberNameCard](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setGroupMemberNameCard) | Configures the name card for a group member. |
| [setGroupMemberCustomField](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setGroupMemberCustomField) | Configures a custom field for a group member. |

### Others
| API | Description |
| --- | --- |
| [on](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#on) | Enables event listening. |
| [off](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#off) | Disables event listening. |
| [registerPlugin](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#registerPlugin) | Registers a plugin. |
| [setLogLevel](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel) | Configures the log level. |
