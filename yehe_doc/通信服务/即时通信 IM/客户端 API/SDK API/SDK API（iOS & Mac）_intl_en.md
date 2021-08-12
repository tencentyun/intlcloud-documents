>!**Do not use APIs of new and old versions at the same time**.

## Initialization and Login APIs
To use Tencent Cloud IM services, you need to initialize the SDK and log in.

| API                                             | Description                                                         |
|---------|---------|
| [initSDK](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a8035eed3a7c9b3b1c229196ac7bc5da6) | Initializes the SDK. |
| [unInitSDK](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a286e5358ec4cd0a8f9c66f4d2d7d4544) | Uninitializes the SDK. |
| [getVersion](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#ae8281def98e669d701171ede7aa3c176) |Gets the version number. |
| [getServerTime](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a4adcf2642bcb706cd6cfe7e5c5f85f06) |Gets the server time. |
| [login](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a38c42943046acdaf615915c9422af07c) | Logs in. |
| [logout](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a20b495d7f7a231ea33507ca4a79f811f) | Logs out. |
| [getLoginUser](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a78ca7f39bca860e46620f8f766508fb0) | Gets the currently logged-in user. |
| [getLoginStatus](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#acfd2f6366780badf80ebf66d95550f89) | Gets the login status. |


## Simple Message APIs
Use the following APIs for the sending and receiving of text and signaling (custom buffer) messages.

| API                                             | Description                                                         |
|---------|---------|
| [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88) | Sets an event listener for simple messages (text messages and custom messages).<br> Do not use it and [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab) at the same time.|
| [removeSimpleMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#afa3040f676105f3fb78d4835ee3c898b) | Removes the event listener for simple messages (text messages and custom messages). |
| [sendC2CTextMessage](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a50d63810093eccc0491d058d0b883618) | Sends a one-to-one (C2C) text message. |
| [sendC2CCustomMessage](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a5fc3b87e9782e679c08926d07e486b90) | Sends a one-to-one (C2C) custom (signaling) message. |
| [sendGroupTextMessage](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a07788874071937fac6c7093185b145f7) | Sends a group text message. |
| [sendGroupCustomMessage](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a537560a58d49aad36406f6d9db6ded65) | Sends a group custom (signaling) message. |

## Signaling APIs
| API                                             | Description                                                         |
|---------|---------|
| [addSignalingListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a3a7fde0d4d5a342bd93299deaf98e1d1) | Adds a signaling listener. |
| [removeSignalingListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#ae730297ec335735eee3c2f3c464bde33) | Removes a signaling listener. |
| [invite](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a594071fa1a70373582ed6082c581b332) | Invites a user. |
| [inviteInGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#ac01a4e703c925aaf5f78df67faca15be) | Invites certain users in the group. |
| [cancel](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#acaac35e5db28db783420b5eb39d53e6f) | Cancels an invitation. |
| [accept](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a1ffb6daba9deed8780f869205daf7771) | Accepts an invitation. |
| [reject](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a39e685924aaa4d22daa88f2ec96aa827) | Rejects an invitation. |
| [getSignalingInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a0b149836793b8f2d54889b1c3ae40362) | Gets the signaling information. |
| [addInvitedSignaling](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#aedfb31fdd3289af36c092b55adeed231) | Adds invitation signaling (can be used for invitation signaling triggered by offline push messages for group invitations). |

## Advanced Message APIs
If you need to send/receive rich media messages (images, videos, files, etc.) and use advanced features such as recalling messages, marking messages as read, and querying message history, use the following advanced message APIs. Do not use simple messages APIs and advanced message APIs at the same time.

| API                                             | Description                                                         |
|---------|---------|
| [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab) | Sets an event listener for advanced messages.<br> Do not use it and [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88) at the same time.|
| [removeAdvancedMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a28aeebff4a791c9bb8f91a4f61e020e6) | Removes the listener for advanced messages. |
| [createTextMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a609f4d4c374d9df3abf9974ff8112fc3) | Creates a text message. |
| [createTextAtMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#aaebbd8ed9b9766d01f996ec722744346) | Creates an @ text message. |
| [createCustomMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a7a38c42f63a4e0c9e89f6c56dd0da316) | Creates a custom message. |
| [createImageMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a23033a764f0d95ce83c52f3cdeea4137) | Creates an image message. |
| [createSoundMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a9073007806fa186b8999ce656555032a) | Creates a voice message. |
| [createVideoMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a233a9ee5ef2ea371206005d109757f18) | Creates a video message. |
| [createFileMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a9e487ae9541111038ebed900ab639d4c) | Creates a file message. |
| [createLocationMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a2a997472dd62d794cfd4e3a42cfab930) | Creates a location message. |
| [createFaceMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#ab7a593be2cca1c8eddd7e73255f3f34a) | Creates an emoji message. |
| [createMergerMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a2943bb31403aeb22f8582cd9966cf13e) | Creates a combined forward message. |
| [createForwardMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a05d088b7d9883e18af41355cdd3f4562) | Creates a single forward message. |
| [sendMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) | Sends a message. The message object can be created using a `createXXXMessage` API. |
| [setC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#ae628f19d856921d27081c3f40005e9d9) | Sets the Mute Notifications option for one-to-one messages. |
| [getC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a1c743a6fe1d17a21dc80e584fd1de2d1) | Gets the Mute Notifications status for one-to-one messages. |
| [setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a379eeef926e41ec5d48287e7fb55b80a) | Sets the Mute Notifications option for group messages. |
| [getC2CHistoryMessageList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a1c743a6fe1d17a21dc80e584fd1de2d1) | Gets one-to-one (C2C) message history. |
| [getGroupHistoryMessageList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a9e242ba327377fe74b83e8d5572d39a0) | Gets group chat message history. |
| [getHistoryMessageList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a99e8f00ee60df12e346548b743523218) | Gets message history. |
| [revokeMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a2ef856a792923811e9d16ed7a101336a) | Recalls a message. The message object can be created using a `createXXXMessage` API. |
| [markC2CMessageAsRead](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#acb3a67bd2fa131b50c611a48fa78f34d) | Marks one-to-one (C2C) messages as read. |
| [markGroupMessageAsRead](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a7fc79e30877b8d77fbdfa24e057376dc) | Marks group messages as read. |
| [deleteMessageFromLocalStorage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a2bb42528f4d166ac826914094655841c) | Deletes a message from local storage. |
| [deleteMessages](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a9e394ea720ecdc10d497b63b6f2b22c4) | Deletes messages from local storage and the cloud. |
| [clearC2CHistoryMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a005c7767172d9a3980974b68c780c33b) | Clears chat history with a user from local storage and the cloud. |
| [clearGroupHistoryMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a16c01c19a285e2bd11443c868c8256e6) | Clears chat history of a group from local storage and the cloud. |
| [insertGroupMessageToLocalStorage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a9b312b67e4da19978b55a7b915815dfe) | Inserts a message in a group chat. |
| [insertC2CMessageToLocalStorage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#acc1dccd310d1965248cff0d4fd5ca45f) | Inserts a message in a one-to-one chat. |
| [findMessages](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a4a0c47d706d8784656225c1e9065f6f1) | Finds local messages by `msgID`. |
| [searchLocalMessages](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a10878d0bd326b07ec6a605c5695c7de1) | Searches for local messages. |

## Group APIs
Tencent Cloud IM SDK supports four preset group types, each of which pertains to different scenarios.
- Work group (Work): similar to a WeChat group. Users can join the group only after being invited by existing members.
- Public group (Public): similar to a QQ group. Users can join the group through requests, which need to be approved by the group owner or group admin.
- Meeting group (Meeting): used together with [TRTC](https://intl.cloud.tencent.com/product/trtc) to enable scenarios such as video conferencing and online education. Users can join and leave the group freely and view the message history before they join.
- Audio-video group (AVChatRoom): suitable for scenarios such as live streaming and chat rooms with on-screen comments. Users can join and leave the group freely. There is no limit on the number of group members.

| API                                             | Description                                                         |
|---------|---------|
| [setGroupListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a74de68e55d787fd1d4ec83b99cd1fcab) | Sets an event listener for groups. |
| [createGroup](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a3bbcf819c1ec70e520b7f9a42cfbb989) | Creates a (simple) group. |
| [createGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a59824434b6096180b94d8152183dcd2c) | Creates an (advanced) group. The group information and the initial group members can be set during group creation. |
| [joinGroup](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a) | Joins a group. |
| [quitGroup](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#ac2a43b3ada447131df0c5f19e8079be5) | Quits a group. |
| [dismissGroup](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a5bd55cb04867985253949d8cc78f860e) | Deletes a group. Only the group owner and group admin can delete a group. |
| [getJoinedGroupList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a4599e99791c150cc9f3e2492e8b4ce04) | Gets the list of groups the current user has joined, excluding audio-video groups. |
| [getGroupsInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a9bca7e5318cfed44335566a783a6b568) | Gets the profiles of groups. |
| [searchGroups](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ac9a960921e512621340159d82a4b5259) | Searches for groups. |
| [setGroupInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144) | Modifies the profile of a group. |
| [ initGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a1b3a56dfc345f1ef2a575cb36156e745) | Initializes group attributes. |
| [ setGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a134342ddb51d1ee83f3981ed91d26885) | Sets group attributes. |
| [ deleteGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#aa504ffca9492580ca27a45f78a87e2cb) | Deletes group attributes. |
| [ getGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ac8a74db230669d1b49da47bb0895cbf9) | Gets group attributes. |
| [getGroupOnlineMemberCount](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ada2eadb44f6865e9848df94fb5bae4ae) | Gets online group members. |
| [getGroupMemberList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a148bb44bf0189a4e61a294a495a43dbe) | Gets group member list. |
| [getGroupMembersInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a1ab284b80811bcc697d689d7b97edf04) | Gets the profiles of specified group members. |
| [searchGroupMembers](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a35ceb734976c833047cceb8b31055b18) | Searches for group members by profile. |
| [setGroupMemberInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a40b97ee4b138f93e1b2073d1bdff3756) | Modifies the profile of a specified group member. |
| [muteGroupMember](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#aa8a0206f75d75400b517f7e0d80fe9ee) | Mutes a group member. |
| [inviteUserToGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a942d75fdea66e22cdbd8c131cf18e1ea) | Invites users to a group. |
| [kickGroupMember](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a0581f28fddf2ade890aa62e4318d7a97) | Removes a member from a group. |
| [setGroupMemberRole](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#af7ce533e514adfab766b1ee726d9ffce) | Sets the role for a group member. |
| [transferGroupOwner](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a58a2ffae60505a43984fe21bf0bc1101) | Changes the group owner. |
| [getGroupApplicationList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a29c36ad685159850a30d61a6b9c637e8) | Gets the list of requests to join a group. |
| [acceptGroupApplication](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a51bb9b4f965cb3d01546fef348ac75e4) | Accepts a request to join a group. |
| [refuseGroupApplication](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a46aa78c54986b2c0b7cc0012a3dc94ef) | Rejects a request to join a group. |
| [setGroupApplicationRead](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ade11e93b96206ef851641c42788132d1) | Marks the request list as read. |

## Conversation List APIs
The conversation list is the list a user sees on the first screen after logging in to WeChat or QQ. It includes elements such as conversation node, conversation name, group name, last message, and unread count.

| API                                             | Description                                                         |
|---------|---------|
| [setConversationListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a95bac7330779a8a970fc7689e436257f) | Sets a conversation listener. |
| [getConversationList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#af94d9d44e90da448a395e6d92b4e512e) | Gets the conversation list. |
| [getConversation](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#ad4b7b80fbe0cff25027371b416ede9f9) | Gets a conversation. |
| [getConversationList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#ab1f5e86e270b122cb725266d234d9dd5) | Gets multiple conversations. |
| [deleteConversation](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a142f5289632f29a603937f1d770748c6) | Deletes a conversation. |
| [setConversationDraft](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a462cd163c03cdce230ed3647b414382b) | Sets draft for a conversation. |
| [pinConversation](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a06cefb398f5a327dff4cefe6fb18c5b8) | Pins a conversation to the top. |
| [getTotalUnreadMessageCount](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#abe76208f616713a09df582a6c1665d38) | Gets the total unread message count. |

## User Profile APIs
You can use the following APIs to query user profiles, modify your profile, and block messages from a specified user (i.e., adding a specified user to the blocklist).

| API                                             | Description                                                         |
|---------|---------|
| [getUsersInfo](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#ac638c1dd6ec1e5204637e4b87129cd38) | Gets users’ profiles. |
| [setSelfInfo](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a328a0d2d07e8d34e12effb73937c3437) | Modifies one's own user profile. |
| [addToBlackList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a67d998da5085b5004bb6aa8d4322022c) | Blocks messages from a specified user, which means adding the user to the blocklist. |
| [deleteFromBlackList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#aa7e69a67185eaca658ba429cf6309a5f) | Unblocks messages from a specified user, which means removing the user from the blocklist. |
| [getBlackList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a0d854d64c8ae936014a8424d55508fa3) | Gets the blocklist. |

## Offline Push APIs
Use the offline push service if you want your app to receive IM messages in real time when it is in the background. For detailed configuration, see [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/34347).

| API                                             | Description                                                         |
|---------|---------|
| [setAPNSListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07APNS_08.html#a62e1694cf9e1d65b76f90064cbcbb683) | Sets an APNs listener. |
| [setAPNS](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07APNS_08.html#a73bf19c0c019e5e27ec441bc753daa9e) | Configures offline push. |

## Friend Management APIs
By default, Tencent Cloud IM does not check your relationship with a user when receiving and sending messages. You can enable "Check Relationship for One-to-One Messages" on **Feature Configuration** > **Login and Message** > **Relationship Check** in the [IM console](https://console.cloud.tencent.com/im) and use the following APIs to delete/add friends and manage your friend list.

| API                                             | Description                                                         |
|---------|---------|
| [setFriendListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#acd403f586f3df84f56b1b757efb2d443) | Sets a relationship chain and friend profile listener. |
| [getFriendList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a81131d76924a03ec2b593addd6e4e101) | Gets the friend list. |
| [getFriendsInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a39f6752da11b595e4a5b6dcb0eb6a584) | Gets the profiles of specified friends. |
| [setFriendInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#ac258312c000c1af69fcf51dd6898b74b) | Sets the profile of a specified friend. |
| [searchFriends](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a0c18db2119464cc087ed0657e6962257) | Searches for friends. |
| [addFriend](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#ac1ea1c7de2bfc2b0a25e5f6b3192e304) | Adds a friend. |
| [deleteFromFriendList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#af967134fb177b32d4060fedf3663ace3) | Deletes friends. |
| [checkFriend](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#aad1b09fab6523d9a36147b4ed4efac67) | Checks relationship with specified users. |
| [getFriendApplicationList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#aad1b09fab6523d9a36147b4ed4efac67) | Gets the list of friend requests. |
| [acceptFriendApplication](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a51b913927028025e2e450e6e8ce848c0) | Accepts a friend request. |
| [refuseFriendApplication](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a406b964a6513219cfe4803f87f0f00f8) | Rejects a friend request. |
| [deleteFriendApplication](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a363e0622f653694999293c595d552896) | Deletes a friend request. |
| [setFriendApplicationRead](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#ad46c70c18b8f69bf272cbf3466477a85) | Marks a friend request as read. |
| [createFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a8b33edab15ae7d179e4e2d885e7d2b7d) | Creates a friend list. |
| [getFriendGroups](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a63f3eaae567586077d5a8d27c31e2229) | Gets the information of friend lists. |
| [deleteFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a2dc49f2abb1238fc2d47ce6d4f14c1e7) | Deletes friend lists. |
| [renameFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a93f6ba132d9706db7c74daff97a2abd0) | Modifies the name of a friend list. |
| [addFriendsToFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a0265241c39600c390406ca1f8f6ff75d) | Adds friends to a friend list. |
| [deleteFriendsFromFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a4a14a878816c8d6a20981d1903fcf359) | Deletes friends from a friend list. |

