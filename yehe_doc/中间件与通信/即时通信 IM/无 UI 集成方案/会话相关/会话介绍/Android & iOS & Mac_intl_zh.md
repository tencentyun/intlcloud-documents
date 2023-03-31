## Conversation
When a user creates a one-to-one or group chat, and a message is sent or received in it, a conversation will be created.
In the Tencent Cloud Chat SDK, the conversation management class is `V2TIMConversationManager(Android)` or `V2TIMManager(Conversation)(iOS and macOS)`. You can use the conversation management class APIs to display/update the conversation list, update the unread count, pin a conversation to the top, make a conversation draft, and mute message notifications.

## Conversation Class
The conversation class is `V2TIMConversation` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMConversation.html)), which defines the following content:

| Attribute             | Definition                                       | Description                                                  |
| --------------------- | ------------------------------------------------ | ------------------------------------------------------------ |
| type                  | Conversation type                                | See the definition of `V2TIMConversationType`, which can be `C2C` or `Group`. |
| conversationID        | Unique conversation ID                           | It is in the format of `c2c_userID` for a one-to-one chat or `group_groupID` for a group chat. |
| userID                | User ID of the message receiver                  | `userID` stores the user ID of the message receiver if the conversation type is one-to-one chat; otherwise, it is empty. |
| groupID               | Group ID                                         | `groupID` stores the group ID if the conversation type is group chat; otherwise, it is empty. |
| groupType             | Group type                                       | `groupType` is the type of the group if the conversation type is group chat; otherwise, it is empty. |
| showName              | Displayed conversation name                      | The name of a group conversation is displayed in the following order of priority: group name > group ID; <br>The name of a one-to-one conversation is displayed in the following order of priority: friend remarks of the message receiver > nickname of the message receiver > `userID` of the message receiver. |
| faceUrl               | Displayed conversation profile photo             | It is the group profile photo for a group chat or the profile photo of the message receiver for a one-to-one chat. |
| unreadCount           | Unread message count of the conversation         | For detailed directions, see [Conversation Unread Count](https://intl.cloud.tencent.com/document/product/1047/48320). It is invalid and defaults to `0` for an audio-video group (AVChatRoom). |
| recvOpt               | Message receiving option                         | See the definition of `V2TIMReceiveMessageOpt` and the use directions [here](https://intl.cloud.tencent.com/document/product/1047/48032). |
| lastMessage           | Last message in the conversation                 | For detailed directions, see [Conversation List](https://intl.cloud.tencent.com/document/product/1047/48326). |
| groupAtInfolist       | List of @ information in the group conversation  | Generally, it is used to display the notifications of "someone@me" and "@all". |
| draftText             | Draft information                                | The draft information can be set by calling the `setConversationDraft` API. For detailed directions, see [Conversation Draft](https://intl.cloud.tencent.com/document/product/1047/48311). |
| draftTimestamp        | Draft editing time                               | It is automatically generated when a draft is set.           |
| isPinned              | Whether to pin the conversation to the top       | For detailed directions, see [Pinning Conversation to the Top](https://intl.cloud.tencent.com/document/product/1047/48317). |
| orderKey              | Field for sorting conversations                  | For detailed directions, see [Conversation List](https://intl.cloud.tencent.com/document/product/1047/48326). |
| markList              | Conversation mark list                           | For the use directions, see [Conversation Mark](https://intl.cloud.tencent.com/document/product/1047/48853). This attribute is supported from v6.5. |
| customData            | Custom conversation data                         | To set custom data, call the `setConversationCustomData` API. The custom data will be stored on the cloud. Up to 256 bytes are supported. This attribute is supported from v6.5. |
| conversationGroupList | List of groups to which the conversation belongs | For the use directions, see [Conversation Group](https://intl.cloud.tencent.com/document/product/1047/48854). This attribute is supported from v6.5. |

## Conversation Storage Policy
There is no limit on the number of locally stored conversations.
Up to 100 conversations can be stored in the cloud. To increase this limit, upgrade to the Ultimate edition. Then you can set the limit to 500 in the console.

If the information of a conversation has not been updated for a long time, the conversation can be stored in the cloud for up to seven days.

Locally stored conversations may not always be consistent with those stored in the cloud. If you do not call the `deleteConversation` API to delete the local conversations, these conversations will always exist. However, at most 100 conversations can be stored in the cloud. In addition, if the information of a conversation has not been updated for a long time, this conversation can be stored in the cloud for at most seven days. Therefore, local conversations displayed on different mobile phones may be inconsistent with each other.
