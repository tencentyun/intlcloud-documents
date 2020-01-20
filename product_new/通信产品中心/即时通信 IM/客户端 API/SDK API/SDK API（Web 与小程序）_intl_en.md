## TIM

TIM is the namespace of the IM Web SDK, and provides the static method **create()** for creating SDK instances, the event constant **EVENT**, and the type constant **TYPES**.

**Initialization**

| API | Description |
| --- | --- |
| **create** | Creates an SDK instance. |

## SDK instance

| Concept | Description |
| :--- | :---- |
| Message | **Message** indicates the content to be sent and carries multiple attributes which specify whether you are the sender, the sender account, the message generation time, and so on. |
| Conversation | Two types of **Conversation** are available:<li>Client to Client (C2C): a one-to-one chat, involving only 2 participants.</li><li>GROUP: a group chat, involving more than 2 participants. |
| Profile | **Profile** describes the basic information of a user, including the nickname, gender, personal signature, and profile photo address. |
| Group | **Group** is a communication system for group chatting. Many types of groups are available: private group, public group, chat room, and audio-and-video chat room. |
| GroupMember (Group member) | **GroupMember** indicates the basic information of each group member, such as the ID, nickname, role, and the time of joining the group. |
| Group notification | A group notification is generated when an event such as group member adding or deletion occurs. You can configure whether to display group notifications to group members.<br/>For more information about group notification types, see **Message.GroupTipPayload**.|
| Group system message | For example, when a user applies for joining a group, the group admins will receive a system message. After an admin accepts or denies the application, the IM SDK will return the application result to the access terminal, and then the user can view the result displayed on the access terminal.<br/>For more information about types of group system messages, see **Message.GroupSystemNoticePayload**.  |
| Message display on Screen | The sent messages, including text segments and images, are displayed on the computer or phone screen. |

### Login
| API | Description |
| --- | --- |
| **login** | Logs in. |
| **logout** | Logs out. |


### Message
| API | Description |
| --- | --- |
| **createTextMessage** | Creates a text message. |
| **createImageMessage** | Creates an image message. |
| **createAudioMessage** | Creates a voice message. |
| **createVideoMessage** | Creates a video message. |
| **createCustomMessage** | Creates a custom message. |
| **createFaceMessage** | Creates a sticker message. |
| **createFileMessage** | Creates a file message. |
| **sendMessage** | Sends a message. |
| **resendMessage** | Sends a message again. |
| **getMessageList** | Obtains the message list.  |
| **setMessageRead** | Sets message read receipt.  |

### Conversation
| API | Description |
| --- | --- |
| **getConversationList** | Obtains the conversation list. |
| **getConversationProfile** | Obtains the conversation information. |
| **deleteConversation** | Deletes a conversation. |

### Profile
| API | Description |
| --- | --- |
| **getMyProfile** | Obtains your personal profile. |
| **getUserProfile** | Obtains other user’s profile. |
| **updateMyProfile** | Updates your personal profile. |
| **getBlacklist** | Obtains your blacklist. |
| **addToBlacklist** | Adds a user to the blacklist. |
| **removeFromBlacklist** | Deletes a user from the blacklist. |

### Group
| API | Description |
| --- | --- |
| **getGroupList** | Obtains the group list. |
| **getGroupProfile** | Obtains the group information. |
| **createGroup** | Creates a group. |
| **dismissGroup** | Disbands a group. |
| **updateGroupProfile** | Modifies the group information. |
| **joinGroup** | Applies for joining a group. |
| **quitGroup** | Quits a group. |
| **searchGroupByID** | Searches for a group. |
| **changeGroupOwner** | Transfers the group ownership. |
| **handleGroupApplication** | Processes applications for joining the group. |
| **setMessageRemindType** | Specifies the notification type of group messages. |

### Group member
| API | Description |
| --- | --- |
| **getGroupMemberList** | Obtains the group member list. |
| **getGroupMemberProfile** | Obtains a group member’s profile. |
| **addGroupMember** | Adds a group member. |
| **deleteGroupMember** | Deletes a group member. |
| **setGroupMemberMuteTime** |Configures muted period.|
| **setGroupMemberRole** | Modifies the group member’s role. |
| **setGroupMemberNameCard** | Configures the name card for a group member. |
| **setGroupMemberCustomField** | Configures a custom field for a group member. |

### Others
| API | Description |
| --- | --- |
| **on** | Enables event listening. |
| **off** | Disables event listening. |
| **registerPlugin** | Registers a plugin. |
| **setLogLevel** | Configures the log level. |

