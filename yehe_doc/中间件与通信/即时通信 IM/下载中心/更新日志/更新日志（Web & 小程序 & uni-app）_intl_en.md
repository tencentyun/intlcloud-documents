### 2.24.0 @2022.11.3
**New features**

- Supported local profanity by local profanity plugin [tim-profanity-filter-plugin](https://www.npmjs.com/package/tim-profanity-filter-plugin).
- Supported to pull friend custom field and data custom fields to improve product experience,[getFriendProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendProfile) .
- Supported pulling the full list of applications for adding groups,[getGroupApplicationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupApplicationList).
- Supported for sending topic messages is not counted as unread.
- Supported for sending ordinary community messages is not counted as unread.
- Supported voip push when sending messages.

**Bug fixing**
- Fixed friends profile related issues.

### 2.23.1 @2022.9.29
**New features**
- Added the other interfaces support the creation of group-directed messages (that is, sending messages to some group members in the group, other group members will not receive these messages), [createTextMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextMessage) .
- Supported sending videos in mov format.
- Supported push to SDK in REST API,[Updating Friends](https://www.tencentcloud.com/zh/document/product/1047/34904)
- Supported pulling custom friend fields and custom data fields,[getFriendProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendProfile) .
- Added the returned data new features field of the interface isSyncCompleted, which is used to identify whether the synchronization of the conversation list from the cloud is completed,[getConversationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationList) .
- Supported notification to the access side through [MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED) in the community message to which the topic belongs.
- Improve support for uni-app offline push.

**Bug fixing**

- Fixed some group conversations cannot pull roaming messages after the group list exceeds the upper limit of 5000.
- Fixed the customData of the corresponding conversation is '' After calling setConversationCustomData to set the session custom field, log in again.

### 2.23.0 @2022.9.16
**New features**
- Supported to obtain the total number of unread sessions,[getTotalUnreadMessageCount](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getTotalUnreadMessageCount).
- Added the access side listens for the event to get the notification of the change of the total number of unread sessions in the session,[TOTAL_UNREAD_MESSAGE_COUNT_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOTAL_UNREAD_MESSAGE_COUNT_UPDATED).
- Supported tagging of live group members(supported only by the Ultimate edition),[markGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#markGroupMemberList).
- Added the SDK synchronously updates the conversation group where the group conversation is located when a group member is kicked out of the group, or the group is deleted.
- Supported independent subcontracting of uni-apps.
- Supported the SDK automatically restores the message records of the most recent contacts after a network disconnection and reconnection in the web multi-instance login scenario to ensure message reliability.

**Bug fixing**
- Fixed the withdrawal status of the session lastMessage may be out of sync issue in the scenario of web multi-instance login.
- Fixed conversation pinning issue when syncing recent contacts.

### 2.22.0 @2022.8.18
**New features**
- Supported uni-app package to native app for offline push, see [registerPlugin](https://web.sdk.qcloud.com/im/doc/en/SDK.html#registerPlugin)。
- Supported to obtain the list of online members of the live stream room, see[getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList) (supported only by the Ultimate edition).
- Supported live stream room ban members,see [deleteGroupMember](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteGroupMember)(supported only by the Ultimate edition).
- Added set conversation custom data, [setConversationCustomData](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setConversationCustomData).
- Added mark conversation, [markConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#markConversation)(supported only by the Ultimate edition).
- Added get list of conversation group, [getConversationGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationGroupList) (supported only by the Ultimate edition).
- Added create conversation group, [createConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createConversationGroup) (supported only by the Ultimate edition).
- Added delete conversation group, [deleteConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversationGroup) (supported only by the Ultimate edition).
- Added rename conversation group, [renameConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#renameConversationGroup)(supported only by the Ultimate edition).
- Added add conversations to conversation group, [addConversationsToGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addConversationsToGroup)(supported only by the Ultimate edition).
- Added delete conversation from conversation group[deleteConversationsFromGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversationsFromGroup) (supported only by the Ultimate edition).

**Bug fixing**
- Fixed the conversation unread count not updated after being notified that the conversation message has been withdrawn.

### 2.21.2 @2022.8.8
**New features**
- Supported create and send voice messages on the web.
- Added create a merged message and new features ID field of the merged message, [createMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createMergerMessage).

### 2.21.1 @2022.8.3
**Bug fixing**
- Fixed the message duplication problem that resendMessage can cause.

### 2.21.0 @2022.7.28
**New features**
- Added set your own custom status, [setSelfStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setSelfStatus).
- Added get user stauts, [getUserStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getUserStatus).
- Added subscribe user status, [subscribeUserStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#subscribeUserStatus).
- Added unsubscribe user status, [unsubscribeUserStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#unsubscribeUserStatus).
- Supported multi-terminal and multi-instance synchronization of DND settings for group messages and topic messages, [setMessageRemindType](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageRemindType).
- Supported mobile WeChat applet and QQ applet to send file messages, [createFileMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFileMessage).
- Supported modifying cloudCustomData for all types of messages, [modifyMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#modifyMessage).
- Supported live room broadcast messages with the new feature field isBroadcastMessage, [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html).
- Supported multi-terminal and multi-instance synchronization with the option of adding a group.
- Supported general community and topic @all members and topic lastMessage.

**Changes**
- Webworker is enabled by default in the international website and private environment when the browser supports webworker.

**Bug fixing**
- Fixed the issue that lastMessage.payload is set to undefined after receiving a message that does not update the conversation lastMessage.
- Fixed the compensation for group messages caused by online messages did not start.
- Fixed pull roaming messages issue after frequent group withdrawals and additions.
- Fixed The pagination pull group list lag causes the pull group conversation roaming message to be an empty array issue.
- Fixed known issues.

### 2.20.1 @2022.6.27

**Changes**

- Aligned with the native SDK experience, where only group records are deleted and group conversations are not deleted after users leave or are kicked out of a non-audio-video group or the group is deleted.
- Made [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage) unable to delete group system notifications; if a deletion attempt is made, an error message will be reported.
- Supported HTTP for rich media messages of the on-premises deployment.

**Bug fixing**

- Fixed the issue where group conversations were occasionally lost during the switch of the mini program between the foreground and background.
- Fixed the issue where the `lastMessage` of a one-to-one conversation was abnormally updated.

### 2.20.0 @2022.6.9

**New features**

- Added [modifyMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#modifyMessage) to support message modification.
- Added [getMessageListHopping](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageListHopping) to pull the conversation message list by specified sequence or time range.
- Supported read receipts for one or more one-to-one messages (supported only by the Ultimate edition).
- Added the `isPeerRead` field for `lastMessage` of a one-to-one conversation to indicate whether a message was read by the receiver.
- Excluded group tips from the unread count of a conversation.
- Added [TIM.TYPES.KICKED_OUT_REST_API](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.KICKED_OUT_REST_API) to support kickout through the RESTful API.

**Changes**

Optimized [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList) to pull the roaming messages.

**Bug fixing**

- Fixed the issue where the conversation list was not updated due to parameter issues after the [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage) API was called successfully.
- Fixed the issue where `Cannot add property markTimeline, Object is not extensible` occurred during mini program debugging on real devices of some models.


### 2.19.1 @2022.5.7

**New features**
- Supported topic creation in a [community](https://intl.cloud.tencent.com/document/product/1047/33529) for stronger interactions.
- Added [getJoinedCommunityList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getJoinedCommunityList) to get the list of topic-enabled communities.
- Added [createTopicInCommunity](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTopicInCommunity) to create a topic.
- Added [deleteTopicFromCommunity](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteTopicFromCommunity) to delete a topic.
- Added [updateTopicProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateTopicProfile) to set the topic profile.
- Added [getTopicList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getTopicList) to get the topic list.
- Added [Topic](https://web.sdk.qcloud.com/im/doc/en/Topic.html), which indicates the topic object of a community and is used to describe topic attributes such as name, notice, introduction, and unread count.
- Added the [TIM.EVENT.TOPIC_CREATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOPIC_CREATED) event, which will be triggered when a topic is created.
- Added the [TIM.EVENT.TOPIC_DELETED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOPIC_DELETED) event, which will be triggered when a topic is deleted.
- Added the [TIM.EVENT.TOPIC_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOPIC_UPDATED) event, which will be triggered when the topic profile is updated.

### 2.18.2 @2022.4.22

**Changes**

Optimized the audio-video group user experience.

**Bug fixing**

- Fixed the issue where the statistics in certain use cases were inaccurate.
- Fixed the issue where the result returned by the [getGroupMessageReadMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMessageReadMemberList) API was inaccurate.

### 2.18.0 @2022.4.8

**New features**

- Added [sendMessageReadReceipt](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessageReadReceipt) for sending group message read receipts.
- Added [getMessageReadReceiptList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageReadReceiptList) for pulling the list of group message read receipts.
- Added [getGroupMessageReadMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMessageReadMemberList) for pulling the list of members who have (or have not) read a group message.
- Added [findMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#findMessage) for querying local messages in a specified conversation by messageID.
- Aligned the experience of conversation unread count update after messages are recalled with that of NativeIM.

**Changes**

- The concatenation rule of [Message.ID](https://web.sdk.qcloud.com/im/doc/en/Message.html) is `${senderTinyID}-${clientTime}-${random}`, which is consistent with that of a NativeIM message ID.
- When the SDK is in the not ready state, specific reasons are provided for the access side.

**Bug fixing**

After a group member was removed from a group, the `Conversation.groupProfile.memberCount` value that other group members obtained from the [CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) event callback was not updated.

### 2.17.0 @2022.3.2

**New features**

- Supports [Community groups](https://intl.cloud.tencent.com/document/product/1047/33529).
- Supports group notifications for recent contacts' `Conversation.lastMessage`.
- `Message.payload.memberList` supports getting the nickname, profile photo, and other information of group members who joined or left a group.
- Supports WEBP images for image message sending.
- Supports video cover [snapshotUrl](https://web.sdk.qcloud.com/im/doc/en/Message.html#.VideoPayload) for video message sending.
- Improved message transmission efficiency and reduced events such as [CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED).

**Bug fixing**

- After a user sent a message with custom data (cloudCustomData), `cloudCustomData` was empty when the user logged in again.
- When a user logged in again after a [login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login) failure, the SDK reported the error of repeated login.
- After [getGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupProfile) was called, `Conversation.groupProfile` was inconsistent with the latest group profile.

### 2.16.3 @2022.2.11

**Bug fixing**

Fixed login failures that occurred after an Android application was packaged with uni-app (on some devices).

### 2.16.2 @2022.2.10

**New features**

- Supports sending file messages after uni-app packages native apps.
- Supports the international website in India.

**Bug fixing**

- Fixed some emoji rendering issues.

### 2.16.1 @2022.1.14

**New features**

- Added support for Alipay Mini Program to send .image images.
- When [deleteConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversation) is called to delete a conversation, historical messages in the conversation are deleted as well.

**Bug fixing**

- An error occurred when the downstream file message `fileName` was an empty string.
- Fixed the issue caused by the group attribute API call sequence.
- The `__wxConfig is not defined` issue occurred when uni-app packaged apps to Baidu Mini Program and other platforms.


### 2.16.0 @2022.1.5

**New features**

- [setMessageRemindType](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageRemindType) supports setting the **Mute Notifications** mode for C2C conversations.
- [setAllMessageRead](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setAllMessageRead) supports quickly marking unread messages of all conversations as read.
- [sendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessage) supports excluding sent messages from the conversation's unread message count and not updating the conversation's `lastMessage`.
- Allows new members of an audio-video group to view historical messages before joining the group (you must activate the Flagship Edition package to use the feature).
  

**Changes**

- SDK uses the [strict mode](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode).
- The conversations with deleted accounts are filtered out for the conversation list.
- Optimized the update timing of `nick` and `avatar` for roaming messages.
- When receiving peer (friend) profile update information, the SDK updates `conversation.userProfile` accordingly.

**Bug fixing**

- WebSocket persistent connections were disconnected abnormally due to non-UTF-8 characters.
- The runtime error `e.getOnlineOnlyFlag is not a function` occurred when a copied message was passed in to call [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage).
- After [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage) was called, the `lastMessage` of the corresponding conversation was not correctly updated.
- An error occurred when calculating the unread message count of one-to-one conversations.
- Rendering exceptions occurred if `nick` and `avatar` were not carried in real-time messages of one-to-one conversations.
- `lastMessage.payload` was occasionally `null` for conversations.
- Pre-signed image thumbnail upload URLs did not take effect.
- When a user mentioned (@) a group member and logged in again to pull roaming messages, the corresponding `message.atUserList` was an empty array.
- An error occurred when group notifications (group owner changing) are processed.
- Some statistics errors.



### 2.15.0 @2021.10.29

**New features**

- Supports the international website.
- [createLocationMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createLocationMessage) supports sending geographical location messages.
- Supports uploading images, videos, documents for easy download and preview (compatible with uni-app).
- Added the `nick` and `nameCard` parameters to the `lastMessage` data structure of [Conversation](https://web.sdk.qcloud.com/im/doc/en/Conversation.html) to better display the sender's information of the `lastMessage` in a group chat.
  

**Changes**

- [getConversationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationList) supports getting multiple specified conversations at a time.
- Increases the stability of persistent connections.

**Bug fixing**

- The [CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) event was not sent after login when there was no conversation list cache or no pagination for recent contacts.
- In some scenarios, the `isCompleted` parameter was always `false` in the response to the call of the [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList) API.
- The `index` parameter was missing on the recipient side when `index` was set to `0` in the call of the [createFaceMessage](createFaceMessage) API.

### 2.14.0 @2021.9.24

**New features**

- [pinConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#pinConversation) supports pinning a conversation to the top.
- [initGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#initGroupAttributes) and other group attribute related APIs support seat management for audio chat rooms.

**Changes**

- When a group message is sent, the SDK automatically adds the `nameCard` attribute to the message body to facilitate display on the access side.
- Forced logout due to multi-client login or multi-instance login no longer triggers server-side logout callbacks.

**Bug fixing**

- When roaming messages were pulled in one-to-one conversations, messages occasionally got lost.
- Group joining remarks (applyMessage) were missing.

### 2.13.1 @2021.8.27

**Changes**

- When a user consecutively calls the [login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login) API before login, error code `2025` is returned, indicating repeated login.
- After WebSocket reconnection, the SDK logs in the user again and synchronizes unread messages to ensure message reliability.


**Bug fixing**

- When a user consecutively called the [login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login) API before login, the unread message count of the conversation was incorrect.
- If `nameCard` passed in an empty string when the [setGroupMemberNameCard](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberNameCard) API was called, the SDK reported an error.
- When the [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList) API was called, the value of `muteUntil` in the packet returned was incorrect.


### 2.13.0 @2021.8.23

**New features**

Supports friend relationship chain. For more information, see [Usage Guide](https://web.sdk.qcloud.com/im/doc/en/tutorial-03-sns.html).

**Bug fixing**

An error was occasionally reported when WebSocket persistent connections were disconnected.

### 2.12.2 @2021.8.6

**New features**

Video upload progress callback is supported on mini programs.

**Changes**

The unread message count of a conversation no longer includes the group notifications about not saving the modifications on custom group fields to the roaming server.

**Bug fixing**

Users in an audio-video group occasionally failed to receive group notifications on the group joining by themselves.
- When a user used a RESTful API to send C2C messages with `random` being set to `0`, the receiver triggered the [MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED) event twice.


### 2.12.1 @2021.7.20

**New features**

- Supports counting unread messages in meeting groups.
- The [TIM.EVENT.MESSAGE_MODIFIED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_MODIFIED) event is added. When a third-party calls back a modified message, the SDK uses this event to notify the message sender of the message modification.

**Bug fixing**

- Fixed the issue where group roaming messages occasionally get lost when they are pulled.
- Fixed the `xx.toFixed is not a function` issue that may occur during uni-app integration.

### 2.12.0 @2021.7.5

**New features**

- [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage) supports deleting messages.
- During conversation list synchronization, `lastMessage` can be set to a recalled message.
- [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList) supports pulling the group joining time `joinTime`.

**Bug fixing**
The `nick` value is incorrect in the notifications sent when a user is set or canceled as the admin.


### 2.11.2 @2021.6.16

**New features**

- Supports WebSocket. [WebSocket Upgrade Guide](https://web.sdk.qcloud.com/im/doc/en/tutorial-02-upgradeguideline.html)
- Allows uni-app to send image, video, and other file messages.


### 2.10.2 @2021.4.27

**New features**

- The custom field `cloudCustomData` can be set during message creation to meet diverse business needs.
- When [createGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createGroup) or [addGroupMember](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addGroupMember) is called, if a single user exceeds the maximum number of groups a single user can join, use `overLimitUserIDList` to notify the access side.

**Bug fixing**

- After an audio-video group (AVChatRoom) was created in the [console](https://console.cloud.tencent.com/im) and a group owner was specified, messages sent by the RESTful API for [Sending System Messages in a Group](https://intl.cloud.tencent.com/document/product/1047/34958) would be repeated on the group owner side after the group owner joined the group.
- Nickname was missing when [createForwardMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createForwardMessage) was called.
- Occasional errors occurred when [downloadMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#downloadMergerMessage) was called.


### 2.10.1 @2021.3.19

**New features**

- The [createMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createMergerMessage) API for creating combined messages.
- The [createForwardMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createForwardMessage) API for creating forward messages.
- When an account logs in on multiple instances or clients, once conversation read is reported on one instance or client, the unread count of the conversation will be synchronously cleared on the web client.

**Changes**

The MTA statistics feature is deprecated.

**Bug fixing**

- Web: when an account logged in on multiple instances, the profile photo and nickname of the other party in a one-to-one conversation were incorrect.
- When you called back and called the RESTful API to recall messages frequently after sending messages, some of them were not recalled correctly.

### 2.9.3 @2021.2.3

**Changes**

If a user hasn't joined a group (not an audio-video group), calling [quitGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#quitGroup) will return error code 2623, indicating that the user is not in the group.

**Bug fixing**

`avatar` (profile photo) or `nick` (nickname) was inconsistent in the one-to-one conversation message list.

### 2.9.2 @2021.1.26

**New features**

- Supports sending and receiving one-to-one messages with `avatar` (profile photo) and `nick` (nickname) displayed.
- Supported the Tencent Cloud IM upload plugin [tim-upload-plugin](https://www.npmjs.com/package/tim-upload-plugin). This plugin enables more secure and faster file upload, supports web, Baidu, Toutiao, and Alipay mini program platforms, and is merely 26 KB in size. For more information on how to use it, see [registerPlugin](https://web.sdk.qcloud.com/im/doc/en/SDK.html#registerPlugin).

**Bug fixing**

- When a user joined an audio-video group anonymously after logging out, the error code 70402 was returned in the response packet during a long polling.
- The browser environment was misjudged during Taro 3.0+ integration.
- When the image type and size verification failed, there were errors in the returned data structure.



### 2.9.1 @2020.12.23
**Bug fixing**

Fixed the issue where a compilation error occurred when [tim-wx-sdk.js](https://www.npmjs.com/package/tim-wx-sdk) was imported into the basic library v2.14.1 of WeChat Developer Tools.


### 2.9.0 @2020.12.15
**New features**

- The [createTextAtMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextMessage) API allows users to specify @ a specific member or @ all members during a group chat.
- [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html) adds the `namecard` attribute to display group members' group name cards (i.e., their nicknames in a group).


### 2.8.5 @2020.11.23
**Changes**

The [logout](https://web.sdk.qcloud.com/im/doc/en/SDK.html#logout) API can be called when the SDK is not ready.

**Bug fixing**

- Errors occurred in SDK operations when read receipts and read notifications existed at the same time.
- Attempts to anonymously re-join an audio-video group after logout failed.
- The group list was cleared abnormally.

### 2.8.4 @2020.11.4
**New features**

- Baidu, Toutiao, and Alipay mini program platforms are supported (currently, image, video, file messages, or other messages that need to be uploaded to COS cannot be sent).
- The third-party frameworks of MPX and uni-app are supported.

### 2.8.1 @2020.10.29

**New features**

Images in BMP format can be sent.

**Changes**

`unreadCount` and `lastMessage` of the [conversation object](https://web.sdk.qcloud.com/im/doc/en/Conversation.html) are not updated when the sender sends an online message and the recipient receives the online message.

**Bug fixing**

The SDK could not enter the ready state due to problems synchronizing the list of recent contacts.


### 2.8.0 @2020.10.20

**New features**

- [getGroupOnlineMemberCount](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupOnlineMemberCount) supports querying the number of online users in an audio-video group.
- Supports image compression. The access side can choose to display the original image or thumbnail based on business requirements. For more information, see [ImagePayload](https://web.sdk.qcloud.com/im/doc/en/Message.html#.ImagePayload).

**Bug fixing**

Compatibility issues when Taro 3.x integrates WebIM

**Changes**

SDK size reduction. The size of [tim-js-sdk](https://www.npmjs.com/package/tim-js-sdk) is reduced by 8.5%, and that of [tim-wx-sdk](https://www.npmjs.com/package/tim-wx-sdk) is reduced by 15%.


### 2.7.8 @2020.9.24

**New features**

The [TIM.create](https://web.sdk.qcloud.com/im/doc/en/TIM.html#.create) API adds the `oversea` parameter. When this parameter is set to `true`, the SDK uses a domain name outside the Chinese mainland to avoid interference.

**Bug fixing**

- The return value for calling relevant APIs was `undefined` when the SDK was in the `not ready` state.
- Issues related to statistics


### 2.7.7 @2020.8.12

**New features**

The [TIM.EVENT.SDK_RELOAD](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.SDK_RELOAD) event was added.

**Bug fixing**

- Audio-video groups occasionally failed to pull messages in cases where the network was reconnected after a long disconnection or the Mini Program switched to the foreground after running in the background for a long time.
- The type and value of `imageFormat` of an image message were inconsistent with those of the actual image.
- The nicknames displayed in work groups and public groups were incorrect.


### 2.7.6 @2020.7.9

**Bug fixing**

Messages occasionally failed to be pulled if an audio-video group (AVChatRoom) was used for a long time.

### 2.7.5 @2020.7.2

**Bug fixing**

After the RESTful API for [creating a work group](https://intl.cloud.tencent.com/document/product/1047/34895) was called to create a work group successfully and the group members were specified, messages from group members would fail to be sent.


### 2.7.2 @2020.6.30

**Bug fixing**

- Occasionally, when [joinGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#joinGroup) was called, the SDK prompted "Already in the group" but in fact the user was not in the group. Consequently, the user could not send or receive messages.
- The count of messages sent in a temporary meeting group was incorrect.

### 2.7.0 @2020.6.8

**New features**

Supports one-to-one message read receipts (indicating whether the peer has read your messages). For more information, see the event [TIM.EVENT.MESSAGE_READ_BY_PEER](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_READ_BY_PEER). In a [message](https://web.sdk.qcloud.com/im/doc/en/Message.html) that has already been read by the peer, the value of `isPeerRead` is `true`.

**Bug fixing**

- After a user joined a chat room (ChatRoom), the newly created conversation did not display the last message.
- After login, a user who had not joined an audio-video group (AVChatRoom) could still send a message to the audio-video group (AVChatRoom).


### 2.6.6 @2020.5.27

**Bug fixing**

- In audio-video groups (AVChatRoom), messages were occasionally repeatedly displayed on the screen.
- An error was reported when [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList) received an empty message.
- If [login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login) was called again after [logout](https://web.sdk.qcloud.com/im/doc/en/SDK.html#logout), error `70001` occasionally occurred when [joinGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#joinGroup) was called.

### 2.6.4 @2020.5.8

**New features**

The [sendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessage) API added the sending option to support the sending of online messages (no offline or roaming messages; cannot be used for AVChatRoom or BChatRoom) and the configuration of [offline push](https://intl.cloud.tencent.com/document/product/1047/33525).

### 2.6.3 @2020.4.26

**Bug fixing**

- Message content was lost because the input `payload.data payload.extension` type of [createCustomMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createCustomMessage) is incorrect.
- Multiple messages contained in a response to a single request were disordered.
- The unread count could not be cleared occasionally after the read count is reported because the number of unread one-to-one conversions overflows.
- [TIM.EVENT.ERROR](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.ERROR) `event.data.code` and `event.data.undefined` were undefined occasionally.

### 2.6.2 @2020.4.16

**New features**

- [updateGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateGroupProfile) supports muting and unmuting all.
- [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList) supports getting the group member muting deadline timestamp [muteUntil](https://web.sdk.qcloud.com/im/doc/en/GroupMember.html).

**Bug fixing**

The unread count could not be cleared when the latest group message was a group prompt.

### 2.6.1 @2020.4.8

**Bug fixing**

Files could not be uploaded occasionally when the uploaded COS signature was invalid and not updated in a timely manner.


### 2.6.0 @2020.3.30

**New features**
- The web client supports creating and sending video messages of up to 100 MB by calling [createVideoMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createVideoMessage).
- The `nick` and `avatar` attributes are added to [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html) to display the nickname and profile photo address of the message sender in an audio-video group (AVChatRoom). You need to set the nickname and profile photo address in advance by calling [updateMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateMyProfile).
- Web: when an account logs in on multiple instances, the one-to-one message recall notification can be synchronized across these instances.
- After [updateGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateGroupProfile) is called to successfully modify custom group fields, group members can receive group notifications and obtain related content [Message.payload.newGroupProfile.groupCustomField](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupTipPayload).

**Changes**

[TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED) is deprecated and replaced by [MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED).

**Bug fixing**

Errors occurred occasionally when the [getGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupList) API was called.

### 2.5.2 @2020.3.13

**Changes**

When [searchGroupByID](https://web.sdk.qcloud.com/im/doc/en/SDK.html#searchGroupByID) fails, the log level is degraded to warning and the prompt text is modified.

**Bug fixing**

- Anonymous users or visitors failed to join [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM) groups and had statistical problems.
- Other known issues

### 2.5.1 @2020.3.5

**Changes**

When [login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login) is successful, the key-value pair `repeatLogin: true` is added for the `imResponse.data` callback object to identify repeated login of a login account.

**Bug fixing**

The priority of messages received at the receiver side of an audio-video group is different from that set on the sender side.

### 2.5.0 @2020.2.28
**New features**
- The network status change event [TIM.EVENT.NET_STATE_CHANGE](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.NET_STATE_CHANGE) is added, and the access side can make related prompts and guidance based on this event.

**Changes**
[Error codes](https://web.sdk.qcloud.com/im/doc/en/global.html) are reduced and optimized.

**Bug fixing**
- After an audio-video group was created in the [console](https://console.cloud.tencent.com/im) and a group owner was specified, messages sent by other group members will be repeated on the group owner side after the group owner joins the group.
- When groups were created and terminated in the [console](https://console.cloud.tencent.com/im) or using a RESTful API frequently, the SDK did not deliver the [TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED) event.
- [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList) failed to get the group message list occasionally.


### 2.4.2 @2020.2.7

**New features**
[Message priorities](https://intl.cloud.tencent.com/document/product/1047/33526), [enumerated values](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.MSG_PRIORITY_HIGH), and [use cases](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextMessage) can be set for group messages.


### 2.4.1 @2020.1.14

**Changes**
- Anonymous users or visitors can only join [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM) groups.

**Bug fixing**
- Some online messages could not be pulled occasionally.
- After a system notification from an audio-video group was received, the [TIM.EVENT.MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED) event was not delivered.
- In some scenarios, the group message recall result was inaccurate.
- Other known issues

### 2.4.0 @2020.1.3
**New features**
- The [revokeMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#revokeMessage) API is added.
- The `isRevoked` attribute is added to [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html). The attribute value `true` identifies recalled messages.
- The message recall event notification [TIM.EVENT.MESSAGE_REVOKED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_REVOKED) is added.
- [Forced logout due to multi-client login](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.KICKED_OUT_MULT_ACCOUNT) and [forces logout due to UserSig expiration](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.KICKED_OUT_USERSIG_EXPIRED) are added to the forced-logout event notification [TIM.EVENT.KICKED_OUT](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.KICKED_OUT).

**Changes**
- The maximum size of files uploaded through [createFileMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFileMessage) is increased from 20 MB to 100 MB.
- `msgMemberInfo` and `shutupTime` of [group prompts](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupTipPayload) will be deprecated. Use `memberList` and `muteTime` instead.
- The [IM smart customer service entry](https://cloud.tencent.com/act/event/smarty-service?from=im-doc) is added to the console.

**Bug fixing**
- Listening events could not be canceled by calling the [off](https://web.sdk.qcloud.com/im/doc/en/SDK.html#off) API.
- The value and type of the `isRead` attribute in [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html) were incorrect.
- The error code and error message were incorrect when the video file in a sent video message exceeded the maximum size.
- The content of updated custom fields was incorrect occasionally.
- The [JOIN_STATUS_ALREADY_IN_GROUP](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.JOIN_STATUS_ALREADY_IN_GROUP) event occurred occasionally when a user logged in and joined an audio-video group.
- core-js caused potential performance issues.


### 2.3.2 @2019.12.18
**Changes**
[getUserProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getUserProfile) and [updateMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateMyProfile) support [custom profile fields](https://intl.cloud.tencent.com/document/product/1047/33520).

**Bug fixing**
Messages were lost in combined messages obtained using [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList).

### 2.3.1 @2019.12.13
**New features**
- [createImageMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createImageMessage) and [createFileMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFileMessage) support passing in [File](https://developer.mozilla.org/zh-CN/docs/Web/API/File) objects.
- The [createFaceMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFaceMessage) API is added to create emoji messages.
- The message notification efficiency for [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM) groups is optimized to improve the user experience.

**Changes**
- When messages fail to be sent, the SDK returns the actual error codes and error messages.
- When [logout](https://web.sdk.qcloud.com/im/doc/en/SDK.html#logout) is called, only the message channel of the current instance logs out.
- When a callback function passed in by the access side is encapsulated for security purposes and the logic of the callback function is incorrect, errors can be captured and located quickly.
- The SDK provides Chinese error information when [IM server-side error codes](https://intl.cloud.tencent.com/document/product/1047/34348) are received.

**Bug fixing**

- [TIM.EVENT.CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) was triggered several times when a message was sent.
- The SDK reported errors when files, such as images were uploaded if [registerPlugin](https://web.sdk.qcloud.com/im/doc/en/SDK.html#registerPlugin) was not called or incorrect parameters were entered.
- Long polling did not stop after a [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM) group was disbanded.
- When "multi-instance" or "multi-client" login was enabled, other instances or clients failed to receive messages after a web instance was logged out.
- The SDK reported errors occasionally due to the structure of session lists that were pulled.

### 2.2.1 @2019.11.28
**Changes**
The logic for getting group roaming messages is optimized.

**Bug fixing**
- The SDK reported [error code 2901](https://web.sdk.qcloud.com/im/doc/en/global.html) after the group owner of an audio-video group modified the group profile.
- After the group admin processed apps for joining a group, processed apps can be received after refresh.

### 2.2.0 @2019.11.21
**New features**
- Mini Programs support creating and sending video messages via the [createVideoMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createVideoMessage) API. Video messages can be synced across platforms. You need to update to the latest versions of the [TUIKit and SDK](https://intl.cloud.tencent.com/document/product/1047/33996).
- The [getGroupMemberProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberProfile) API is added.
- Compatible with audio and file messages sent by Native IM v3.x.
- Location messages [GeoPayload](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GeoPayload) can be received.

**Changes**
Up to 100 groups can be written to local storage. The SDK does not write the full group list when there are more than 100 groups.

**Bug fixing**
- Long polling of [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM) groups continues after logout.
- The group contact cards in message instances of [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM) groups did not have values.
- Errors were reported when Internet Explorer 10 was used.
- Users could not join groups anonymously.

### 2.1.4 @2019.11.7
**Changes**
- When the `Promise` status returned by an SDK API is `rejected`, the SDK no longer delivers a [TIM.EVENT.ERROR](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.ERROR) event.
- Updates to a user's profile are immediately written to the local cache.

**Bug fixing**
- Code running failed after SDK integration when Angular zone.js modified prototype chains.
- After a group owner created and joined a [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM) group, the group owner could not receive messages.
- Initialization failed when the group list was excessively large.

### 2.1.3 @2019.10.31

**Changes**
Combined messages (multiple message elements in one message) sent via RESTful API calls or the legacy IM version are compatible. For more information, see [Compatibility Guide](https://web.sdk.qcloud.com/im/doc/en/tutorial-01-faq.html).

**Bug fixing**
- The unread count was inaccurate.
- Messages were disordered because read messages were not reported.
- Empty image messages were sent successfully but could not be rendered. The SDK did not support sending empty image messages.
- Empty file messages were sent with incorrect message status. The SDK did not support sending empty file messages.
- SDK code errors were reported occasionally when [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList) was called.

### 2.1.2 @2019.10.25
**New features**
 [getGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupList) supports pulling group profile information, including the group owner ID and group member count.

**Bug fixing**
- SDK code errors were reported when a RESTful API is used to send custom group notifications in an audio-video chat room.
- The SDK did not send a request to pull historical messages when a user re-joined a left group and called the `getMessageList` API.
- SDK code errors were reported when upload failed.

### 2.1.1 @2019.10.18
**New features**
Mini Programs support [sending audio messages](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createAudioMessage). Audio messages can be synced across platforms. You need to update to the latest versions of the [TUIKit and SDK](https://intl.cloud.tencent.com/document/product/1047/33996).

**Bug fixing**
[getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList) could still pull historical messages in a quit group after rejoining.

### 2.1.0 @2019.10.16

**New features**
- Web and Mini Programs support receiving [audio messages](https://web.sdk.qcloud.com/im/doc/en/Message.html#.AudioPayload).
- Web and Mini Programs support receiving [video messages](https://web.sdk.qcloud.com/im/doc/en/Message.html#.VideoPayload).

**Changes**
- The [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList) API can pull up to 15 messages at a time.
- [TIM.TYPES.MSG_SOUND](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.MSG_SOUND) is deprecated and replaced by [TIM.TYPES.MSG_AUDIO](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.MSG_AUDIO).

**Bug fixing**
- [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList) could not pull messages in deleted group chats.
- Group system notifications did not contain group names.
- When a conversation was created after receiving a new message, the conversion did not have the profile of the message sender.

### 2.0.11 @2019.10.12

**Bug fixing**
Image messages failed to be sent under the React framework.

### 2.0.9 @2019.9.19

**New features**
The actual width and height of an image are detected before the image message is sent.

**Changes**
- The HTTPS protocol is used by default.
- [TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED) events are sent when new group system notifications are received.

**Bug fixing**
- Screen splash occurred when mini programs sent image messages.
- JPG or other images failed to be sent.
