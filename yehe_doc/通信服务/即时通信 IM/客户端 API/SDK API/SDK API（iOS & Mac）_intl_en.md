>!**Do not use APIs of new and old versions at the same time**.

## Initialization and Login APIs
To use Tencent Cloud IM services, you need to perform initialization and log in.

| API | Description |
|---------|---------|
| [initSDK](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a8035eed3a7c9b3b1c229196ac7bc5da6) | Initializes the SDK. |
| [unInitSDK](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a286e5358ec4cd0a8f9c66f4d2d7d4544) | Uninitializes the SDK. |
| [login](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a38c42943046acdaf615915c9422af07c) | Logs in. |
| [logout](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a20b495d7f7a231ea33507ca4a79f811f) | Logs out. |
| [getLoginStatus](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#acfd2f6366780badf80ebf66d95550f89) | Gets the login status. |
| [getLoginUser](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a78ca7f39bca860e46620f8f766508fb0) | Gets the UserID of the current login user. |

## Simple Message APIs
Use the following message APIs if you only need to use text and signaling (a piece of custom buffer) messages.

| API | Description |
|---------|---------|
| [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a428fe7bf82be1592141d77dfa756ec68) | Sets an event listener for simple messages (text messages and custom messages). <br>Do not use it and [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) at the same time. |
| [removeSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a8f6f9900006bf7ad5bd9bdb8ba0914eb) | Removes the event listener for simple messages (text messages and custom messages). |
| [sendC2CTextMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a50d63810093eccc0491d058d0b883618) | Sends a one-to-one (C2C) text message. |
| [sendC2CCustomMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a5fc3b87e9782e679c08926d07e486b90) | Sends a one-to-one (C2C) custom (signaling) message. |
| [sendGroupTextMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a07788874071937fac6c7093185b145f7) | Sends a group text message. |
| [sendGroupCustomMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a537560a58d49aad36406f6d9db6ded65) | Sends a group custom (signaling) message. |

## Signaling APIs
| API | Description |
|---------|---------|
| [addSignalingListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a3a7fde0d4d5a342bd93299deaf98e1d1) | Adds a signaling listener. |
| [removeSignalingListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#ae730297ec335735eee3c2f3c464bde33) | Removes a signaling listener. |
| [invite](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a0c7b9134995c78f3e2b855acdf65ac12) | Invites a user. |
| [inviteInGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a1ea8dcc4ee2200bf5913a40efd76bf4e) | Invites certain users in the group. |
| [cancel](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#acaac35e5db28db783420b5eb39d53e6f) | The inviter cancels the invitation. |
| [accept](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a1ffb6daba9deed8780f869205daf7771) | The invitee accepts the invitation. |
| [reject](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a39e685924aaa4d22daa88f2ec96aa827) | The invitee rejects the invitation. |
| [getSignalingInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a0b149836793b8f2d54889b1c3ae40362) | Gets the signaling information. |
| [addInvitedSignaling](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#aedfb31fdd3289af36c092b55adeed231) | Adds invitation signaling (can be used for invitation signaling triggered by group offline push messages). |

## Advanced Message APIs
If you need to send/receive rich media messages (images, videos, files, etc.) and use advanced features such as recalling messages, marking messages as read, and querying message history, use the following set of advanced message APIs. Do not use simple messages APIs and advanced message APIs at the same time.

| API | Description |
|---------|---------|
| [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) | Sets an event listener for advanced messages. <br>Do not use it and [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a428fe7bf82be1592141d77dfa756ec68) at the same time. |
| [removeAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a77ec89edbdf500431cbda5ee7aa50920) | Removes the listener for advanced messages. |
| [createTextMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a609f4d4c374d9df3abf9974ff8112fc3) | Creates a text message. |
| [createCustomMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a7a38c42f63a4e0c9e89f6c56dd0da316) | Creates a custom message. |
| [createImageMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a23033a764f0d95ce83c52f3cdeea4137) | Creates an image message. |
| [createSoundMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a9073007806fa186b8999ce656555032a) | Creates a voice message. |
| [createVideoMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a233a9ee5ef2ea371206005d109757f18) | Creates a video message. |
| [createFileMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a9e487ae9541111038ebed900ab639d4c) | Creates a file message. |
| [createLocationMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a2a997472dd62d794cfd4e3a42cfab930) | Creates a location message. |
| [createFaceMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#ab7a593be2cca1c8eddd7e73255f3f34a) | Creates an emoji message. |
| [createMergerMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a2943bb31403aeb22f8582cd9966cf13e) | Creates a combined forward message. |
| [createForwardMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a05d088b7d9883e18af41355cdd3f4562) | Creates a single forward message. |
| [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) | Sends a message. The message object can be created by the `createXXXMessage` API, where `XXX` is a variable. |
| [revokeMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a9e242ba327377fe74b83e8d5572d39a0) | Recalls a message. The message object can be created by the `createXXXMessage` API, where `XXX` is a variable. |
| [getC2CHistoryMessageList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#abca63ad64f69aa4f424cf11849a9b89e) | Gets the one-to-one (C2C) message history. |
| [getGroupHistoryMessageList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a9e242ba327377fe74b83e8d5572d39a0) | Gets the group message history. |
| [markC2CMessageAsRead](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a2ef856a792923811e9d16ed7a101336a) | Marks one-to-one (C2C) messages as read. |
| [markGroupMessageAsRead](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a7fc79e30877b8d77fbdfa24e057376dc) | Marks group messages as read. |
| [deleteMessageFromLocalStorage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a2bb42528f4d166ac826914094655841c) | Deletes a message from the local storage. |
| [insertGroupMessageToLocalStorage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a9b312b67e4da19978b55a7b915815dfe) | Adds a message to the group message list. |

## Group APIs
Tencent Cloud IM SDK supports four preset group types, each of which pertains to different scenarios.
- Work group (Work): similar to a regular WeChat group. Users can only join the group by being invited by existing group members.
- Public group (Public): similar to a QQ group. Users can join the group through requests, which need to be approved by the group owner or group admin.
- Meeting group (Meeting): when used with [TRTC](https://intl.cloud.tencent.com/product/trtc), ideal for scenarios such as video conferencing and online education. Users can join and exit the group freely and view the existing message history before they join the group.
- Audio-video group (AVChatRoom): suitable for scenarios such as live streaming and chat rooms with on-screen comments. Users can join and exit the group freely. There is no limit on the number of group members.

| API | Description |
|---------|---------|
| [setGroupListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a74de68e55d787fd1d4ec83b99cd1fcab) | Sets a group listener. |
| [createGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a3bbcf819c1ec70e520b7f9a42cfbb989) | Creates a (simple) group. |
| [createGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a59824434b6096180b94d8152183dcd2c) | Creates an (advanced) group. The group information and the initial group members can be set during group creation. |
| [joinGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a) | Joins a group. |
| [quitGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#ac2a43b3ada447131df0c5f19e8079be5) | Quits a group. |
| [dismissGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a5bd55cb04867985253949d8cc78f860e) | Deletes a group. Only the group owner and group admin can delete the group. |
| [getJoinedGroupList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a4599e99791c150cc9f3e2492e8b4ce04) | Gets the list of groups the current user has joined, excluding audio-video groups. |
| [getGroupsInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a9bca7e5318cfed44335566a783a6b568) | Pulls the profiles of groups. |
| [setGroupInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144) | Modifies the profile of a group. |
| [setReceiveMessageOpt](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a4974b44d56778b1d5a3df613bee09c87) | Sets the group message receiving option. |
| [getGroupMemberList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a148bb44bf0189a4e61a294a495a43dbe) | Gets the group member list. |
| [getGroupMembersInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a1ab284b80811bcc697d689d7b97edf04) | Gets the profiles of specified group members. |
| [setGroupMemberInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a40b97ee4b138f93e1b2073d1bdff3756) | Modifies the profile of a specified group member. |
| [muteGroupMember](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#aa8a0206f75d75400b517f7e0d80fe9ee) | Mutes a group member. |
| [inviteUserToGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a942d75fdea66e22cdbd8c131cf18e1ea) | Invites users to a group. |
| [kickGroupMember](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a0581f28fddf2ade890aa62e4318d7a97) | Removes a member from a group. |
| [setGroupMemberRole](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#af7ce533e514adfab766b1ee726d9ffce) | Sets the role for a group member. |
| [transferGroupOwner](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a58a2ffae60505a43984fe21bf0bc1101) | Transfers the ownership of a group. |
| [getGroupApplicationList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a29c36ad685159850a30d61a6b9c637e8) | Gets the list of requests to join a group. |
| [acceptGroupApplication](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a51bb9b4f965cb3d01546fef348ac75e4) | Accepts a request to join a group. |
| [refuseGroupApplication](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a46aa78c54986b2c0b7cc0012a3dc94ef) | Rejects a request to join a group. |
| [setGroupApplicationRead](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#ade11e93b96206ef851641c42788132d1) | Marks the request list as read. |

## Conversation List APIs
The conversation list is the list a user sees on the first screen after logging in to WeChat or QQ. It includes elements such as conversation node, conversation name, group name, last message, and unread count.

| API | Description |
|---------|---------|
| [setConversationListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Conversation_08.html#a95bac7330779a8a970fc7689e436257f) | Sets a conversation listener. |
| [getConversationList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Conversation_08.html#af94d9d44e90da448a395e6d92b4e512e) | Gets the conversation list. |
| [deleteConversation](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Conversation_08.html#a142f5289632f29a603937f1d770748c6) | Deletes a conversation. |
| [setConversationDraft](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Conversation_08.html#a462cd163c03cdce230ed3647b414382b) | Sets a draft for a conversation. |


## User Profile APIs
APIs for querying user profiles, modifying one's own user profile, and blocking messages from a specified user (or adding a specified user to the blocklist).

| API | Description |
|---------|---------|
| [getUsersInfo](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#ac638c1dd6ec1e5204637e4b87129cd38) | Gets user profiles. |
| [setSelfInfo](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a328a0d2d07e8d34e12effb73937c3437) | Modifies one's own user profile. |
| [addToBlackList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a67d998da5085b5004bb6aa8d4322022c) | Blocks the messages from a specified user, which means adding the user to the blocklist. |
| [deleteFromBlackList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#aa7e69a67185eaca658ba429cf6309a5f) | Unblocks the messages from a specified user, which means removing the user from the blocklist. |
| [getBlackList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a0d854d64c8ae936014a8424d55508fa3) | Gets the blocklist. |

## Offline Push APIs
Use the offline push service if you want your app to receive IM messages in real time when it is in the background. For detailed configuration, see [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/34347).

| API | Description |
|---------|---------|
| [setAPNSListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07APNS_08.html#a62e1694cf9e1d65b76f90064cbcbb683) | Sets the APNs listener. |
| [setAPNS](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07APNS_08.html#a73bf19c0c019e5e27ec441bc753daa9e) | Sets the offline push configuration. |

## Friend Management APIs
By default, Tencent Cloud IM does not check your relationship with a user when receiving and sending messages. You can enable the "Check Relationship for One-to-One Messages" on **Feature Configuration** > **Login and Message** > **Relationship Check** in the [IM console](https://console.cloud.tencent.com/im) and use the following APIs to delete/add friends and manage your friend list.

| API | Description |
|---------|---------|
| [setFriendListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#acd403f586f3df84f56b1b757efb2d443) | Sets a relationship chain and friend profile listener. |
| [getFriendList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a81131d76924a03ec2b593addd6e4e101) | Gets the friend list. |
| [getFriendsInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a39f6752da11b595e4a5b6dcb0eb6a584) | Gets the profiles of specified friends. |
| [setFriendInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#ac258312c000c1af69fcf51dd6898b74b) | Sets the profile of a specified friend. |
| [addFriend](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#ac1ea1c7de2bfc2b0a25e5f6b3192e304) | Adds a friend. |
| [deleteFromFriendList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#af967134fb177b32d4060fedf3663ace3) | Deletes a friend. |
| [checkFriend](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#ad35446522c481e8fa4260452ec041e15) | Checks your relationship with a specified user. |
| [getFriendApplicationList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#acda7968f1e9adc12261a7e533d709a1c) | Gets the list of friend requests. |
| [acceptFriendApplication](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a51b913927028025e2e450e6e8ce848c0) | Accepts a friend request. |
| [refuseFriendApplication](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a406b964a6513219cfe4803f87f0f00f8) | Rejects a friend request. |
| [deleteFriendApplication](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a363e0622f653694999293c595d552896) | Deletes a friend request. |
| [setFriendApplicationRead](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#ad46c70c18b8f69bf272cbf3466477a85) | Sets a friend request as read. |
| [createFriendGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a231a334fa4a064042d65a67f267ec664) | Creates a friend list. |
| [getFriendGroups](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a63f3eaae567586077d5a8d27c31e2229) | Gets the information of friend lists. |
| [deleteFriendGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a2dc49f2abb1238fc2d47ce6d4f14c1e7) | Deletes friend lists. |
| [renameFriendGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a93f6ba132d9706db7c74daff97a2abd0) | Modifies the name of a friend list. |
| [addFriendsToFriendGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a0265241c39600c390406ca1f8f6ff75d) | Adds friends to a friend list. |
| [deleteFriendsFromFriendGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a4a14a878816c8d6a20981d1903fcf359) | Deletes friends from a friend list. |


