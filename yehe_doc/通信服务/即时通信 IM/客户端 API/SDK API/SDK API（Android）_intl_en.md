>!**Stick on the new API. Do not use it with the older versions.**

## Initialization and Login APIs
To use Tencent Cloud IM services, you need to initialize and log in.

| API | Description |
|---------|---------|
| [initSDK](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ac905c315726b517ba62421471bbecf56) | Initializes the SDK. |
| [unInitSDK](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a8ac73b4f71f9d9a1ca01551c919d3cdd) | Uninitializes the SDK. |
| [login](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a73fc0e14c5f2f5fc06a80081479fb416) | Logs in. |
| [logout](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a0398924fa1b62a8f5cc9b51673273b48) | Logs out. |
| [getLoginStatus](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a1836146275265b2a120412f18961db95) | Obatins the login status. |
| [getLoginUser](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad4b2e5a7df5e786ba369054ac582007f) | Obatins the UserID of the current login user. |

## Simple Message APIs
Use the following message APIs if you only need to use text and signaling (a custom buffer) messages.

| API | Description |
|---------|---------|
| [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b) | Sets an event listener for simple messages (text messages and custom messages).<br>Do not use it with [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823). |
| [removeSimpleMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a86ac462d87f652960d2600a52009849a) | Removes the event listener for simple messages (text messages and custom messages). |
| [sendC2CTextMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a59a8ba6e4a973b4c40a09ae7dfdc6981) | Sends a one-to-one chat (C2C) text message. |
| [sendC2CCustomMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af3e08b936df77210c6cdd0ce5c7fa87f) | Sends a one-to-one chat (C2C) custom (signaling) message. |
| [sendGroupTextMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a56359fd1ce0a96f289dcd4bef522fb52) | Sends a group chat text message. |
| [sendGroupCustomMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afbce8ff97be0a3a42c7dc826d316f2c2) | Sends a group chat custom (signaling) message. |

## Advanced Message APIs
If you need rich-media messages (images, video, files, and others) and advanced features such as receiving and sending messages, recalling messages, marking messages as read, and querying the message history, use the following advanced message APIs. Do not use a mixture of simple message APIs and advanced message APIs.

| API | Description |
|---------|---------|
| [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) | Sets an event listener for advanced messages.<br>Do not use it with [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b). |
| [removeAdvancedMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a44e1e9126bf5b30234330fe19259cd93) | Removes the listener for advanced messages. |
| [createTextMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a3ea254cd12aa0bcfd004f26f759b76a0) | Creates a text message. |
| [createCustomMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5c2495d4b7ecd66e5636aeb865c17efd) | Creates a custom message. |
| [createImageMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#adef5bc7a67b9a69f70f6417fd810d4b1) | Creates an image message. |
| [createSoundMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7e661ce2b4eba1535bd04f3b6539b9dc) | Creates an audio message. |
| [createVideoMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ada17dbc78e9876a8f3a9fd24a73752b5) | Creates a video message. |
| [createFileMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a39e4b6609321fd188a2e156a00bb3135) | Creates a file message. |
| [createLocationMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a67cebe27192392080fc80a86c80a4321) | Creates a location message. |
| [createFaceMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7ad0f3b7eff3978c12d8c912ca164a5d) | Creates an emoji message. |
| [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) | Sends a message. The message object can be created through the createXXXMessage API. |
| [revokeMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad0dfce6be749165cd90a9ff67a1308b1) | Recalls a message. The message object can be created through the createXXXMessage API. |
| [getC2CHistoryMessageList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#afedccbe0e5229ae15e0e07b722ea39df) | Obtains the one-to-one chat (C2C) message history. |
| [getGroupHistoryMessageList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a671e8737fcea0c05dc661c753e5b3597) | Obtains the group message history. |
| [markC2CMessageAsRead](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7c09d0ba4a8018f5f9eec4760c4c7b9b) | Marks one-to-one chat (C2C) messages as read. |
| [markGroupMessageAsRead](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ac0a65f18d361abde8a0ac16132027e69) | Marks group messages as read. |
| [deleteMessageFromLocalStorage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aa31e3b48fb666b970120fc0bc6343534) | Deletes a message from the local storage. |
| [insertGroupMessageToLocalStorage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a04a3f6c250f9d6c0053fd71be74f047f) | Adds a message to the group message list. |


## Group APIs
Tencent Cloud IM SDK supports four predefined group types, each of which pertains to different application scenarios.
- Work group (Work): is similar to a regular WeChat group. Users can only join the group by being invited by existing group members.
- Public group (Public): is similar to a QQ group. Users can join the group through applications, which need to be approved by the group owner or group admin.
- Meeting group (Meeting): when used with [TRTC](https://intl.cloud.tencent.com/product/trtc), it is ideal for scenarios such as video conferencing and online education. Users can join and exit the group freely and view the message history for the periods before they join the group.
- Live-streaming group (AVChatRoom): is suitable for scenarios such as live streaming and chat room with on-screen comments. Users can join and exit the group freely. There is no limit on the number of group members.

| API | Description |
|---------|---------|
| [setGroupListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a092fc428f35eb18c41a80b3655948d40) | Sets an event listener for groups. |
| [createGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af836e4912f668dddf6cc679233cfb0bb) | Creates a group (simple). |
| [createGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a121d53137a38d0fc0bc8a8e0a9c55647) | Creates a group (advanced). Group information and initial group members can be set during group creation. |
| [joinGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564) | Joins a group. |
| [quitGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a6d140dbeb44906de9cb69f69c2ce5919) | Quits a group. |
| [dismissGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd0221c0c842a6dcfa0acc657e50caeb) | Disbands a group. Only the group owner and group admin can disband the group. |
| [getJoinedGroupList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a05bfd8f7df6bfba718abc96fdad49791) | Obtains the list of groups the current user has joined, excluding live-streaming groups. |
| [getGroupsInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ada614335043d548c11f121500e279154) | Pulls profiles of groups. |
| [setGroupInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad87ce42b4dc4d97334fe857e4caa36c4) | Modifies the profile of a group. |
| [setReceiveMessageOpt](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6bf8f3eafb5ffcb1d13bd69231de8bd4) | Sets the group message receiving option. |
| [getGroupMemberList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) | Obtains the list of group members. |
| [getGroupMembersInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#adb08e1c4fa9aff407c7b2678757f66d5) | Obtains the profiles of specified group members. |
| [setGroupMemberInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6f1cf8ede41348b4cd7b63b8e4caa77b) | Modifies the profile of a specified group member. |
| [muteGroupMember](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a450230c4d129611e1b0519827ec0f8b5) | Mutes a group member. |
| [kickGroupMember](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6da6755c6e0c46e96cb02575074a5333) | Removes members from a group. |
| [setGroupMemberRole](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a34ebf60528d02626834f022b4ebabfa8) | Sets the role for a group member. |
| [transferGroupOwner](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ac16d66c8e293c2ee95c7b673e5ad80c4) | Transfers the ownership of a group. |
| [inviteUserToGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#afd219107653b877e446c149531d65e92) | Invites users to a group. |
| [getGroupApplicationList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a240db7bdc023ad6fc63e9ee9b72714c4) | Obtains the list of applications to join a group. |
| [acceptGroupApplication](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad743008d30c909ef0be0f8aa91102e07) | Approves an application to join a group. |
| [refuseGroupApplication](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#aa518c54e77f7c0f6e7dd129d6c433acd) | Rejects an application to join a group. |
| [setGroupApplicationRead](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a498d9d76217cbae0aa235ac928ad02d8) | Marks the application list as read. |

## Conversation List APIs
The conversation list is the list a user sees on the first screen after logging in to WeChat or QQ. It includes elements such as the conversation node, conversation name, group name, last message, and unread count.

| API | Description |
|---------|---------|
| [setConversationListener](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a39228ebb1c5d6855643aa8c1efcc429c) | Sets a conversation listener. |
| [getConversationList](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a1bb5ba2beecb4f68146e7f664124fd8b) | Obtains the list of conversations. |
| [deleteConversation](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a7a6e38c5a7431646bd4c0c4c66279077) | Deletes a conversation. |
| [setConversationDraft](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ae7f2f52bf375dae69368eae42edb28ab) | Sets a draft for a conversation. |

## User Profile APIs
These APIs are used to query user profiles, modify the user profile of oneself, and block messages from a specified user (that is, add a specified user to the blocklist).

| API | Description |
|---------|---------|
| [getUsersInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7ca8c0f71a9875021fc35dfcaff68d1e) | Obtains users’ profiles. |
| [setSelfInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af004ab2f1d1458de354883f1995b678a) | Modifies the user profile of oneself. |
| [addToBlackList](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a8804c7f47000bf1c26aa6ab744a53456) | Blocks messages from a specified user, which means to add the user to the blocklist. |
| [deleteFromBlackList](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a3dcd8f1c70dceafa94ab48796c2f26aa) | Unblocks messages from a specified user, which means to remove the user from the blocklist. |
| [getBlackList](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6269df2d96c910648ab2f0c43e1931c6) | Obtains the blocklist. |

## Offline Push APIs
Use the offline push service if you want your app to receive IM messages in real time when it is running in the background. As there is no unified push service in Mainland China, you need to configure Android offline push for each phone manufacturer.

| API | Description |
|---------|---------|
| [setOfflinePushConfig](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) | Sets the offline push configuration. |

## Friend Management APIs
By default, Tencent Cloud IM does not check for the relationship when receiving and sending messages. You can toggle on "Check Relationship for One-to-One Chat Messages" by navigating to [**Console**](https://console.cloud.tencent.com/im) > **Feature Configuration** > **Login and Message** > **Relationship Check** and use the following APIs to delete or add friends and manage the friend list.

| API | Description |
|---------|---------|
| [setFriendListener](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a17e92c5ca9abad7afe25b654f1fcd75c) | Sets a relationship chain listener to receive friend-list and blocklist change events. |
| [getFriendList](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae478de55db21d42b72a6c5a6a5d16624) | Obtains the list of friends. |
| [getFriendsInfo](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a88732b0f7a5e77a9dd34403fe7bbdd21) | Obtains the profiles of specified friends. |
| [setFriendInfo](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a151b7de6219d966b4194ad7fcc8450fe) | Sets the profile of a specified friend. |
| [addFriend](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a19d0f22aaea285e8cee85a5dd6ed9208) | Adds a friend. |
| [deleteFromFriendList](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#af7ecf8641b58462d038a9c97bfbd4d61) | Deletes a friend. |
| [checkFriend](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#accac9a69c8e4332b0b83755ec54ecfed) | Checks the relationship with a specified user. |
| [getFriendApplicationList](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a2dbf4da19f3b9b170089b8e8cb210166) | Obtains the list of friend requests. |
| [acceptFriendApplication](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ab69ed69330428caff6f468b7df5259fa) | Accepts a friend request. |
| [refuseFriendApplication](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#af1bcbc196015de8e7a94b1575c466f89) | Rejects a friend request. |
| [deleteFriendApplication](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a5c869e3358ca74f9cd2eaebfc7298490) | Deletes a friend request. |
| [setFriendApplicationRead](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a022b4817a31dd25707f14b8184c42675) | Sets a friend request as read. |
| [createFriendGroup](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#afe729e7a74d1e7fd06a5f23c155a08ae) | Creates a friend group. |
| [getFriendGroups](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a0043ca81fdeec5d3e842e85278003d1e) | Obtains the information of friend groups. |
| [deleteFriendGroup](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ac9f06f447ee4452aa12e078b48023cee) | Deletes friend groups. |
| [renameFriendGroup](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a5345957f4d75d8e57ea3b4cff9adee13) | Changes the name of a friend group. |
| [addFriendsToFriendGroup](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6de9168d476ac14e21025ec5c26251df) | Adds friends to a friend group. |
| [deleteFriendsFromFriendGroup](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae367dfec88522e96d96c5ab942e50653) | Deletes friends from a friend group. |
