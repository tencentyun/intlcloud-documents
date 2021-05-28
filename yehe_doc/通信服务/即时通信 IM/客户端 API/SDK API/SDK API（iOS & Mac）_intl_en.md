>!**Do not use APIs of new and old versions at the same time**.

## Initialization and Login APIs
To use Tencent Cloud IM services, you need to perform initialization and log in.

| API | Description |
|---------|---------|
| [initSDK](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a534a3f98ea1447984b5f0932fecfe194) | Initializes the SDK. |
| [unInitSDK](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a286e5358ec4cd0a8f9c66f4d2d7d4544) | Uninitializes the SDK. |
| [login](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a3237ea515b8a78e94a6579447ba282ee) | Logs in. |
| [logout](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#ab4233cb134d5c6125d0a2d2d83ec1afa) | Logs out. |
| [getLoginStatus](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#acfd2f6366780badf80ebf66d95550f89) | Gets the login status. |
| [getLoginUser](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a78ca7f39bca860e46620f8f766508fb0) | Gets the UserID of the current login user. |

## Simple Message APIs
Use the following message APIs if you only need to use text and signaling (a piece of custom buffer) messages.

| API | Description |
|---------|---------|
| [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88) | Sets an event listener for simple messages (text messages and custom messages).<br> Do not use it and [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab) at the same time.|
| [removeSimpleMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#afa3040f676105f3fb78d4835ee3c898b) | Removes the event listener for simple messages (text messages and custom messages). |
| [sendC2CTextMessage](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a8f4eb13fbf039c0216f14f178d9f9f36) | Sends a one-to-one (C2C) text message. |
| [sendC2CCustomMessage](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a20c6ea174904a99fafebb5c1b3475b39) | Sends a one-to-one (C2C) custom (signaling) message. |
| [sendGroupTextMessage](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a74fc1a30a7c1a292e625c5b2cf1e91f0) | Sends a group text message. |
| [sendGroupCustomMessage](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#af8b149e054d532a8fb5ca12a7160c90f) | Sends a group custom (signaling) message. |

## Signaling APIs
| API | Description |
|---------|---------|
| [addSignalingListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a3a7fde0d4d5a342bd93299deaf98e1d1) | Adds a signaling listener. |
| [removeSignalingListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#ae730297ec335735eee3c2f3c464bde33) | Removes a signaling listener. |
| [invite](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a0d75713295f5f19c7d303a0eaeeaaacb) | Invites a user. |
| [inviteInGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#ae7efa9137309a48c93fcd84a6d997506) | Invites certain users in the group. |
| [cancel](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a09bc478d84e053d94004c7ec1bbddf58) | The inviter cancels the invitation. |
| [accept](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a0f486191d6b1755a12de6e2fc42afc14) | The invitee accepts the invitation. |
| [reject](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#aa945a73b34c98e5512ecdd77f2628b53) | The invitee rejects the invitation. |
| [getSignalingInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a0b149836793b8f2d54889b1c3ae40362) | Gets the signaling information. |
| [addInvitedSignaling](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a4332550c567f9f7e6bed5716fd9a1133) | Adds invitation signaling (can be used for invitation signaling triggered by group offline push messages). |

## Advanced Message APIs
If you need to send/receive rich media messages (images, videos, files, etc.) and use advanced features such as recalling messages, marking messages as read, and querying message history, use the following set of advanced message APIs. Do not use simple messages APIs and advanced message APIs at the same time.

| API | Description |
|---------|---------|
| [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab) | Sets an event listener for advanced messages.<br> Do not use it and [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88) at the same time.|
| [removeAdvancedMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a28aeebff4a791c9bb8f91a4f61e020e6) | Removes the listener for advanced messages. |
| [createTextMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a609f4d4c374d9df3abf9974ff8112fc3) | Creates a text message. |
| [createTextAtMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#ad33b6f7cb849054333b18eeb1e9c187d) | Creates an @ text message. |
| [createCustomMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a7a38c42f63a4e0c9e89f6c56dd0da316) | Creates a custom message. |
| [createImageMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a23033a764f0d95ce83c52f3cdeea4137) | Creates an image message. |
| [createSoundMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a254e943133e35b15088769c2159b0d4b) | Creates a voice message. |
| [createVideoMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a959a66944acc6f712710990880259a0b) | Creates a video message. |
| [createFileMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#afbc32249f988afdac127227d9ae000a1) | Creates a file message. |
| [createLocationMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a93b0a2918926e59f56f8fc65dabb8bfd) | Creates a location message. |
| [createFaceMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a5c1199090729348379354eb3402c6d9c) | Creates an emoji message. |
| [createMergerMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a0f56dde34bd350dd6e829e5bff067722) | Creates a combined forward message. |
| [createForwardMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a05d088b7d9883e18af41355cdd3f4562) | Creates a single forward message. |
| [sendMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56) | Sends a message. The message object can be created by the `createXXXMessage` API, where `XXX` is a variable. |
| [setC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#ace29641a1c691bc44705b9bc8b08be37) | Sets the Mute Notifications option for one-to-one messages. |
| [getC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a63d51af9d34e0cd8011da374b7e7a786) | Gets the Mute Notifications status. |
| [setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a40f3e2ada605b73a39b05a3d3144636b) | Sets the Mute Notifications option for group messages. |
| [getC2CHistoryMessageList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a63b5809dea41a83cfff3c63ede7a152b) | Gets one-to-one (C2C) message history. |
| [getGroupHistoryMessageList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#acc79b07f0ac1b4b29b72878850ce4ad1) | Gets group message history. |
| [getHistoryMessageList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#ac1623571db7e6f52484532e2f1630132) | Gets message history. |
| [revokeMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a972ac3fb7744458eb0d6abd96ce35126) | Recalls a message. The message object can be created by the `createXXXMessage` API, where `XXX` is a variable. |
| [markC2CMessageAsRead](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#ad7d239caa69ec7da45f52d6bb02ee19c) | Marks one-to-one (C2C) messages as read. |
| [markGroupMessageAsRead](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a40afaf1f06edd10c90d8d67fa98c2b14) | Marks group messages as read. |
| [deleteMessageFromLocalStorage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a989a11c62ba2001a6a8360d6421d9dd3) | Deletes a message from local storage. |
| [insertGroupMessageToLocalStorage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a941598ae3367267ce6bf8ec3d8dcb2eb) | Adds a message to group message list. |
| [insertC2CMessageToLocalStorage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a220423e265e3916e530814372799cf4f) | Adds a message to the one-to-one message list. |
| [findMessages](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#abacfae1406f7d82241ec4e4a8072fa3e) | Finds local messages by `msgID`. |

## Group APIs
Tencent Cloud IM SDK supports four preset group types, each of which pertains to different scenarios.
- Work group (Work): similar to a regular WeChat group. Users can only join the group by being invited by existing group members.
- Public group (Public): similar to a QQ group. Users can join the group through requests, which need to be approved by the group owner or group admin.
- Meeting group (Meeting): when used with [TRTC](https://intl.cloud.tencent.com/product/trtc), ideal for scenarios such as video conferencing and online education. Users can join and exit the group freely and view the existing message history before they join the group.
- Audio-video group (AVChatRoom): suitable for scenarios such as live streaming and chat rooms with on-screen comments. Users can join and exit the group freely. There is no limit on the number of group members.

| API | Description |
|---------|---------|
| [setGroupListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a74de68e55d787fd1d4ec83b99cd1fcab) | Sets a group listener. |
| [createGroup](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a4bada5d6a06fac04a1424ae2c597e389) | Creates a group (simple). |
| [createGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a10dc812487a4e9071d65a49df277f183) | Creates a group (advanced). Group information and initial group members can be set during group creation. |
| [joinGroup](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a9979ed856657724d317791c723bacef5) | Joins a group. |
| [quitGroup](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#abada02babd5dc4c59f485c6aa1678dcb) | Quits a group. |
| [dismissGroup](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#af6605dd9624849843938573ef05b5463) | Deletes a group. Only the group owner and group admin can delete the group. |
| [getJoinedGroupList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ae12e170ad585eaa8fb9f080bdc3bf8b8) | Gets the list of groups the current user has joined, excluding audio-video groups. |
| [getGroupsInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#aeeffef844fd0948dda227620f0fac895) | Gets the profiles of groups. |
| [setGroupInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a13b25d1f491e18ab0ba953ffc2ca9e82) | Modifies the profile of a group. |
| [ initGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a6d34074aa8ce1e8a6dc41ee53ff5963a) | Initiates group attributes. |
| [ setGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a60bbd75b35c42e823c9538b4be44e3ea) | Sets group attributes. |
| [ deleteGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a60bbd75b35c42e823c9538b4be44e3ea) | Deletes group attributes. |
| [ getGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#af3e1eb1c23996f2beab55670be96fb2d) | Gets group attributes. |
| [getGroupOnlineMemberCount](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ac6236048b0184ee5d35c6071a92b6d1c) | Gets the number of online group members. |
| [getGroupMemberList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a1ba27ad3077804addcfd92c3a45dd092) | Gets the group member list. |
| [getGroupMembersInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ab74754f326c661e94b4511a3b6d91f32) | Gets the profiles of specified group members. |
| [setGroupMemberInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a32caf9bf614778c291194fb5cf3ca3b0) | Modifies the profile of a specified group member. |
| [muteGroupMember](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a0ee1017ecded651208261ac7d1013ad0) | Mutes a group member. |
| [inviteUserToGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#af9d9a04bf3fe5a38346af842f7335f39) | Invites users to a group. |
| [kickGroupMember](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a21d4d4d5b5291d8eda74b3359d857714) | Removes a member from a group. |
| [setGroupMemberRole](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a548aef46b1ef435864678d56f0c0ce54) | Sets the role for a group member. |
| [transferGroupOwner](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a99e8c3488c6bbb553fc662804f7e2f02) | Changes the group owner. |
| [getGroupApplicationList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ae761e7a0c5fd2ad55219bb732edae9cb) | Gets the list of requests to join a group. |
| [acceptGroupApplication](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a72a9fc4dbb99d354121b944e98382e68) | Accepts a request to join a group. |
| [refuseGroupApplication](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ad632874883b7b73e3fba773044bd8c1a) | Rejects a request to join a group. |
| [setGroupApplicationRead](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a141b2b0b02f32039fc3e777599ba2360) | Marks the request list as read. |

## Conversation List APIs
The conversation list is the list a user sees on the first screen after logging in to WeChat or QQ. It includes elements such as conversation node, conversation name, group name, last message, and unread count.

| API | Description |
|---------|---------|
| [setConversationListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a95bac7330779a8a970fc7689e436257f) | Sets a conversation listener. |
| [getConversationList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#afbf2764146025df3c2202058026fda77) | Gets the conversation list. |
| [getConversation](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#ac279fbef674e0de22c038951a9efc779) | Gets a single conversation. |
| [getConversationList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#ac279fbef674e0de22c038951a9efc779) | Gets multiple conversations. |
| [deleteConversation](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a42238db95428faae2da25a093569fda0) | Deletes a conversation. |
| [setConversationDraft](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#ade2830b5c35df27a4b8fea44408a07a0) | Sets draft for a conversation. |
| [pinConversation](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#adc50026943585a0aa37ac8856b6b43bb) | Pins a conversation to the top. |
| [getTotalUnreadMessageCount](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#adc50026943585a0aa37ac8856b6b43bb) | Gets the total unread message count. |

## User Profile APIs
APIs for querying user profiles, modifying one's own user profile, and blocking messages from a specified user (or adding a specified user to the blocklist).

| API | Description |
|---------|---------|
| [getUsersInfo](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a0071a5be9f333698f05fd80aff203560) | Gets users’ profiles. |
| [setSelfInfo](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a2ff0139742c4a0bf6dce1ef7423f3bee) | Modifies one's own user profile. |
| [addToBlackList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#ad1de7b4712309ce4164e4db6574486f0) | Blocks the messages from a user, which means adding the user to the blocklist. |
| [deleteFromBlackList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#afe61664e0afee949f99ec63a288316e2) | Unblocks the messages from a user, which means removing the user from the blocklist. |
| [getBlackList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#aa0e6338aefd556a23507c2798af6e717) | Gets the blocklist. |

## Offline Push APIs
Use the offline push service if you want your app to receive IM messages in real time when it is in the background. For detailed configuration, see [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/34347).

| API | Description |
|---------|---------|
| [setAPNSListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07APNS_08.html#a62e1694cf9e1d65b76f90064cbcbb683) | Sets the APNs listener. |
| [setAPNS](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07APNS_08.html#a6aecbdc0edaa311c3e4e0ed3e71495b1) | Sets the offline push configuration. |

## Friend Management APIs
By default, Tencent Cloud IM does not check your relationship with a user when receiving and sending messages. You can enable the "Check Relationship for One-to-One Messages" on **Feature Configuration** > **Login and Message** > **Relationship Check** in the [IM console](https://console.cloud.tencent.com/im) and use the following APIs to delete/add friends and manage your friend list.

| API | Description |
|---------|---------|
| [setFriendListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#acd403f586f3df84f56b1b757efb2d443) | Sets a relationship chain and a friend profile listener. |
| [getFriendList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a8d03aec2e3efd16b7942944c6cb30d0e) | Gets the friend list. |
| [getFriendsInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a930bb2a8cd664a4037797970ce9fc0d8) | Gets the profiles of specified friends. |
| [setFriendInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a97409aaccf135d60344f002aca06e63e) | Sets the profile of a specified friend. |
| [addFriend](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#ae46b728a77d71e302e10b71ee6b0241e) | Adds a friend. |
| [deleteFromFriendList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a2786c60824ea6ec117429ef2b59630a1) | Deletes friends. |
| [checkFriend](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a2add6bf5b1e2bc8c20bbc2a3f7e0b2f2) | Checks the relationship with a specified user. |
| [getFriendApplicationList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a46147f28e4c974aa29c0e48a1bdc483f) | Gets the list of friend requests. |
| [acceptFriendApplication](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a2546222b4994a5be9f67dfa8eb504e6b) | Accepts a friend request. |
| [refuseFriendApplication](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#acb564676b24c76609acf645c4ad999ad) | Rejects a friend request. |
| [deleteFriendApplication](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a37d87181021d023774a40a79e89e010b) | Deletes a friend request. |
| [setFriendApplicationRead](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#abcdd9faaff90b13d077d10a50373d9df) | Sets a friend request as read. |
| [createFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#acd85704b4a6ad4293d8bbcdb73385f4c) | Creates a friend list. |
| [getFriendGroups](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a44c12380968b1d51c5ea5f90fa627a56) | Gets the information of friend lists. |
| [deleteFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a73a1219065649398d4ba1001f9bd1c9b) | Deletes friend groups. |
| [renameFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a2677f9d9febe8f28f16f3972f7c45638) | Modifies the name of a group list. |
| [addFriendsToFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a24b2297a1d9c2c3fa816839b3108ef72) | Adds friends to a friend group. |
| [deleteFriendsFromFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a65380db025573ac7c6d20f66a8b40ee2) | Deletes friends from a friend group. |


