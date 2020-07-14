### 2.6.6 @2020.5.27

**Fixed**

- Messages in an audio-video chat room are occasionally repeated on the screen.
- [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) reports an error when an empty message is received.
- The 70001 error occurs occasionally during [joinGroup](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#joinGroup) when a user [logs out](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#logout) and then [logs in](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#login).

### 2.6.4 @2020.5.8

**Added**

Added a sending option for [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) to send online messages. In this case, offline and roaming messages are not stored. This feature is not supported by audio-video chat rooms or broadcasting chat rooms. Added configurations for [offline push](https://intl.cloud.tencent.com/document/product/1047/33525).

### 2.6.3 @2020.4.26

**Fixed**

- Message content was lost because the input `payload.data payload.extension` type of [createCustomMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createCustomMessage) is incorrect.
- Multiple messages contained in a response to a single request were disordered.
- The unread count could not be cleared occasionally after the read count is reported because the number of unread C2C conversions overflows.
- [TIM.EVENT.ERROR](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.ERROR) `event.data.code` and `event.data.undefined` were undefined occasionally.

### 2.6.2 @2020.4.16

**Added**

- [updateGroupProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateGroupProfile) supports muting and unmuting all.
- [getGroupMemberList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberList) can get the group member muting deadline timestamp [muteUntil](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html).

**Fixed**

The unread count could not be cleared when the latest group message was a group prompt.

### 2.6.1 @2020.4.8

**Fixed**

Files could not be uploaded occasionally when the uploaded COS signature was invalid and not updated in a timely manner.


### 2.6.0 @2020.3.30

**Added**
- The web client can create and send video messages [createVideoMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createVideoMessage) of up to 100 MB in size.
- The `nick` and `avatar` properties are added in [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html) to display the nickname and profile photo address of the message sender in an audio-video chat room. The nickname and profile photo address need to be set in advance by calling [updateMyProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateMyProfile).
- When an account logs in on multiple instances, namely, multiple webpages or web browsers, the C2C message cancellation notification can be synchronized between these webpages or web browsers.
- After [updateGroupProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateGroupProfile) is called to successfully modify custom group fields, group members can receive group prompts and obtain related content [Message.payload.newGroupProfile.groupCustomField](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload).

**Changed**

[TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED) is deprecated and replaced by [MESSAGE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED).

**Fixed**

Errors occurred occasionally when the [getGroupList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupList) API was called.

### 2.5.2 @2020.3.13

**Changed**

When [searchGroupByID](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#searchGroupByID) fails, the log level is degraded to warning and the prompt text is modified.

**Fixed**

- Anonymous users or visitors failed to join [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) groups and had statistical problems.
- Other known issues

### 2.5.1 @2020.3.5

**Changed**

When [login](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#login) is successful, the key value pair `repeatLogin: true` is added for the `imResponse.data` callback object to identify repeated login for a login account.

**Fixed**

The priority of messages received at the receiver side of an audio-video chat room is different from that set on the sender side.

### 2.5.0 @2020.2.28
**Added**
- The network status change event [TIM.EVENT.NET_STATE_CHANGE](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.NET_STATE_CHANGE) is added, and the access side can display related prompts and guidance based on this event.
- Running in WeChat Mini Program plug-in environments is supported.

**Changed**
[Error codes](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html) are reduced and optimized.

**Fixed**
- After an audio-video chat room was created in the [console](https://console.cloud.tencent.com/im) and a group owner was specified, messages sent by other group members would be repeated on the group owner side after the group owner joined the group.
- When groups were frequently created and terminated in the [console](https://console.cloud.tencent.com/im) or using a RESTful API, the SDK did not deliver the [TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED) event.
- [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) occasionally failed to get the group message list.


### 2.4.2 @2020.2.7

**Added**
[Message priorities](https://intl.cloud.tencent.com/document/product/1047/33526), [enumerated values](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.MSG_PRIORITY_HIGH), and [use cases](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createTextMessage) can be set for group messages.


### 2.4.1 @2020.1.14

**Changed**
- Anonymous users or visitors can only join [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) groups.

**Fixed**
- Some online messages occasionally cannot be pulled.
- After a system notification from an audio-video chat room is received, the [TIM.EVENT.MESSAGE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED) event is not delivered.
- In some scenarios, the group message recall result is inaccurate.
- Other known issues

### 2.4.0 @2020.1.3
**Added**
- The [revokeMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#revokeMessage) API is added.
- The `isRevoked` property is added for [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html). The property value `true` identifies recalled messages.
- The message recall event notification [TIM.EVENT.MESSAGE_REVOKED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_REVOKED) is added.
- [Force offline due to multi-client login](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.KICKED_OUT_MULT_ACCOUNT) and [force offline due to UserSig expiration](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.KICKED_OUT_USERSIG_EXPIRED) are added to [TIM.EVENT.KICKED_OUT](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.KICKED_OUT).

**Changed**
- The maximum size of files uploaded through [createFileMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFileMessage) is increased from 20 MB to 100 MB.
- `msgMemberInfo` and `shutupTime` of [Group Prompts](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload) will be deprecated. Use `memberList` and `muteTime` instead.

**Fixed**
- Listening events could not be canceled by calling the [off](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#off) API.
- The value and type of the `isRead` property in [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html) were incorrect.
- The error code and error message were incorrect when a sent video message exceeded the maximum size.
- The content of updated custom fields was occasionally incorrect.
- The [JOIN_STATUS_ALREADY_IN_GROUP](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.JOIN_STATUS_ALREADY_IN_GROUP) event occasionally occurred when a user logged in and joined an audio-video chat room.
- Potential performance issues caused by core-js.


### 2.3.2 @2019.12.18
**Changed**
[getUserProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getUserProfile) and [updateMyProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateMyProfile) supports [custom profile fields](https://intl.cloud.tencent.com/document/product/1047/33520#.E8.87.AA.E5.AE.9A.E4.B9.89.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5).

**Fixed**
Messages were lost in combined messages obtained using [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList).

### 2.3.1 @2019.12.13
**Added**
- [createImageMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createImageMessage) and [createFileMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFileMessage) support passing in [File](https://developer.mozilla.org/zh-CN/docs/Web/API/File) objects.
- The [createFaceMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFaceMessage) API is added.
- The message notification efficiency for [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) groups is optimized to improve the user experience.

**Changed**
- When messages fail to be sent, the SDK returns the actual error codes and error messages.
- When [logout](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#logout) is called, only the message channel of the current instance logs out.
- When a callback function passed in by the access side is encapsulated for security purposes and the logic of the callback function is incorrect, errors can be captured and located quickly.
- The SDK outputs error messages in Chinese when [IM server side error codes](https://intl.cloud.tencent.com/document/product/1047/34348#.EF.BC.88.E4.BA.8C.EF.BC.89.E6.9C.8D.E5.8A.A1.E7.AB.AF.E7.9A.84.E9.94.99.E8.AF.AF.E7.A0.81) appear.

**Fixed**
- Messages were occasionally lost when the WeChat Mini Program went to the foreground after staying in the background for a long time.
- [TIM.EVENT.CONVERSATION_LIST_UPDATED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.CONVERSATION_LIST_UPDATED) was triggered several times when a message was sent.
- The SDK reported errors when files, such as images, were uploaded if [registerPlugin](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#registerPlugin) was not called or incorrect parameters were entered.
- Long polling did not stop after a [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) group was disbanded.
- When "multi-instance" or "multi-client" login was enabled, other instances or clients failed to receive messages after a web instance logged out.
- The SDK occasionally reported errors due to the structure of pulled conversion lists.

### 2.2.1 @2019.11.28
**Changed**
The logic for getting group roaming messages is optimized.

**Fixed**
- The SDK reported the [2901 error code](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html) after the group owner of an audio-video chat room modified the group profile.
- After the group admin processed applications for joining a group, the processed applications could still be received after refresh.

### 2.2.0 @2019.11.21
**Added**
- WeChat Mini Programs support creating and sending video messages [createVideoMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createVideoMessage). Video messages can be synced across platforms. Upgrade to the latest versions of the [TUIKit and SDK](https://intl.cloud.tencent.com/document/product/1047/33996).
- The [getGroupMemberProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberProfile) API is added.
- Audio and file messages sent by Native IM v3.x are compatible.
- Location messages [GeoPayload](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GeoPayload) can be received.

**Changed**
Up to 100 groups can be written to local storage. The SDK does not write the full group list when there are more than 100 groups.

**Fixed**
- Long polling of [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) groups continues after logout.
- The group contact cards in message instances of [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) groups did not have values.
- Errors were reported when Internet Explorer 10 was used.
- Users could not join groups anonymously.

### 2.1.4 @2019.11.7
**Changed**
- When the `Promise` status returned by an SDK API is `rejected`, the SDK no longer delivers a [TIM.EVENT.ERROR](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.ERROR) event.
- Updates to a user's profile are immediately written to the local cache.

**Fixed**
- Code running failed after SDK integration when Angular zone.js modified prototype chains.
- After a group owner created and joined a [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) group, the group owner could not receive messages.
- Initialization failed when the group list was large.

### 2.1.3 @2019.10.31

**Changed**
Combined messages (multiple message elements in one message) sent by RESTful APIs or the legacy IM are compatible. For more information, see [Compatibility Guide](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/tutorial-01-faq.html).

**Fixed**
- The unread count was inaccurate.
- Messages were disordered because read messages were not reported.
- Empty image messages were sent successfully but could not be rendered. The SDK did not support sending empty image messages.
- Empty file messages were sent with incorrect message status. The SDK did not support sending empty file messages.
- SDK code errors were reported occasionally when [getGroupMemberList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberList) was called.

### 2.1.2 @2019.10.25
**Added**
 [getGroupList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupList) is added, which supports pulling group profile information, including the group owner ID and group member count.

**Fixed**
- SDK code errors were reported when a RESTful API was used to send custom group notifications in an audio-video chat room.
- The SDK did not send a request to get historical messages when a user re-joined a previously quit group and called the getMessageList API.
- SDK code errors were reported when upload failed.

### 2.1.1 @2019.10.18
**Added**
WeChat Mini Programs support [sending audio messages](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createAudioMessage). Audio messages can be synced across platforms. Upgrade to the latest versions of the [TUIKit and SDK](https://intl.cloud.tencent.com/document/product/1047/33996).

**Fixed**
[getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) could still pull historical messages in a previously quit group after rejoining.

### 2.1.0 @2019.10.16

**Added**
- Web and WeChat Mini Programs support receiving [audio messages](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.AudioPayload).
- Web and WeChat Mini Programs support receiving [video messages](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.VideoPayload).

**Changed**
- The [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) API can pull up to 15 messages at a time.
- [TIM.TYPES.MSG_SOUND](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.MSG_SOUND) is deprecated and replaced by [TIM.TYPES.MSG_AUDIO](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.MSG_AUDIO).

**Fixed**
- [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) could not get messages in deleted group chats.
- Group notifications did not contain group names.
- When a conversation is created after receiving a new message, the conversion did not have the profile of the message sender.

### 2.0.11 @2019.10.12

**Fixed**
Image messages failed to be sent under the React framework.

### 2.0.9 @2019.9.19

**Added**
The actual width and height of an image are detected before the image message is sent.

**Changed**
- The HTTPS protocol is used by default.
- [TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED) events are sent when new group notifications are received.

**Fixed**
- Screen splash occurred when WeChat Mini Programs sent image messages.
- JPG or other images failed to be sent.
