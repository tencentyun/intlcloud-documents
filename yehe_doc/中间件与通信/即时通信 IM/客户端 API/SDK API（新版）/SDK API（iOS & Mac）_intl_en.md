>!**Do not use APIs of new and old versions at the same time**.

## Initialization and Login APIs
To use the Tencent Cloud Chat service, you need to initialize the SDK and log in.

| API                                                          | Description                        |
| ------------------------------------------------------------ | ---------------------------------- |
| [initSDK](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a8035eed3a7c9b3b1c229196ac7bc5da6) | Initializes the SDK.               |
| [unInitSDK](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a286e5358ec4cd0a8f9c66f4d2d7d4544) | Uninitializes the SDK              |
| [addIMSDKListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ac569656a58908afba491710a8cb3c8d9) | Adds the Chat listener.            |
| [removeIMSDKListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a2e2a7e64bf51888c98636e5974a8aca7) | Removes the Chat listener.         |
| [getVersion](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ae8281def98e669d701171ede7aa3c176) | Gets the version number.           |
| [getServerTime](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a4adcf2642bcb706cd6cfe7e5c5f85f06) | Gets the server time.              |
| [login](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a38c42943046acdaf615915c9422af07c) | Logs in.                           |
| [logout](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a20b495d7f7a231ea33507ca4a79f811f) | Logs a user out                    |
| [getLoginUser](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a78ca7f39bca860e46620f8f766508fb0) | Gets the currently logged-in user. |
| [getLoginStatus](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#acfd2f6366780badf80ebf66d95550f89) | Gets the login status              |


## Simple Message APIs
Use the following APIs for the sending and receiving of text and signaling (custom buffer) messages.

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88) | Sets an event listener for simple messages (text messages and custom messages).<br>Do not use this API and [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab) at the same time. |
| [removeSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#afa3040f676105f3fb78d4835ee3c898b) | Removes the event listener for simple messages (text messages and custom messages) |
| [sendC2CTextMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a50d63810093eccc0491d058d0b883618) | Sends a one-to-one chat (C2C) text message                   |
| [sendC2CCustomMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a5fc3b87e9782e679c08926d07e486b90) | Sends a one-to-one chat (C2C) custom (signaling) message     |
| [sendGroupTextMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a07788874071937fac6c7093185b145f7) | Sends a group chat text message                              |
| [sendGroupCustomMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a537560a58d49aad36406f6d9db6ded65) | Sends a group chat custom (signaling) message                |

## Signaling APIs
| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [addSignalingListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a3a7fde0d4d5a342bd93299deaf98e1d1) | Adds a signaling listener.                                   |
| [removeSignalingListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#ae730297ec335735eee3c2f3c464bde33) | Removes a signaling listener.                                |
| [invite](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a594071fa1a70373582ed6082c581b332) | Invites a user.                                              |
| [inviteInGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#ac01a4e703c925aaf5f78df67faca15be) | Invites certain users in a group.                            |
| [cancel](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#acaac35e5db28db783420b5eb39d53e6f) | Cancels an invitation.                                       |
| [accept](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a1ffb6daba9deed8780f869205daf7771) | Accepts an invitation.                                       |
| [reject](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a39e685924aaa4d22daa88f2ec96aa827) | Rejects an invitation.                                       |
| [getSignalingInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a0b149836793b8f2d54889b1c3ae40362) | Gets the signaling information.                              |
| [addInvitedSignaling](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#aedfb31fdd3289af36c092b55adeed231) | Adds invitation signaling (can be used for invitation signaling triggered by offline push messages for group invitations). |
| [modifyInvitation](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a1f1d6f5053c07996a611e284ac15cbb5) | Modifies the invitation signaling.                           |

## Advanced Message APIs
If you need to send/receive rich media messages (such as image, video, and file messages) and use advanced features such as recalling messages, marking messages as read, and querying message history, use the following set of advanced message APIs. Do not use simple message APIs and advanced message APIs at the same time.

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab) | Sets an event listener for advanced messages. <br>Do not use this API and [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88) at the same time. |
| [removeAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a28aeebff4a791c9bb8f91a4f61e020e6) | Removes the listener for advanced messages                   |
| [createTextMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a609f4d4c374d9df3abf9974ff8112fc3) | Creates a text message                                       |
| [createTextAtMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#aaebbd8ed9b9766d01f996ec722744346) | Creates an @ text message.                                   |
| [createCustomMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7a38c42f63a4e0c9e89f6c56dd0da316) | Creates a custom message                                     |
| [createImageMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a23033a764f0d95ce83c52f3cdeea4137) | Creates an image message                                     |
| [createSoundMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9073007806fa186b8999ce656555032a) | Creates a voice message.                                     |
| [createVideoMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a233a9ee5ef2ea371206005d109757f18) | Creates a video message                                      |
| [createFileMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9e487ae9541111038ebed900ab639d4c) | Creates a file message.                                      |
| [createLocationMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2a997472dd62d794cfd4e3a42cfab930) | Creates a location message                                   |
| [createFaceMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#ab7a593be2cca1c8eddd7e73255f3f34a) | Creates an emoji message                                     |
| [createMergerMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2943bb31403aeb22f8582cd9966cf13e) | Creates a combined forward message.                          |
| [createForwardMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a05d088b7d9883e18af41355cdd3f4562) | Creates a single forward message.                            |
| [createTargetedGroupMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a8bddd2f566a53362b4da5448fdd18fbc) | Creates a targeted group message.                            |
| [createAtSignedGroupMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#adfb065794694a2061af2642f18c4aeb7) | Creates a group @ message.                                   |
| [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) | Sends a message. The message object can be created using a `createXXXMessage` API. |
| [setC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#ae628f19d856921d27081c3f40005e9d9) | Sets the Mute Notifications option for one-to-one messages.  |
| [getC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a1c743a6fe1d17a21dc80e584fd1de2d1) | Gets the Mute Notifications status for one-to-one messages.  |
| [setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a379eeef926e41ec5d48287e7fb55b80a) | Sets the Mute Notifications option for group messages.       |
| [getC2CHistoryMessageList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#abca63ad64f69aa4f424cf11849a9b89e) | Gets the one-to-one chat (C2C) message history               |
| [getGroupHistoryMessageList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9e242ba327377fe74b83e8d5572d39a0) | Gets the group chat message history                          |
| [getHistoryMessageList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a99e8f00ee60df12e346548b743523218) | Gets the message history.                                    |
| [revokeMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2ef856a792923811e9d16ed7a101336a) | Recalls a message. The message object can be created using a `createXXXMessage` API. |
| [modifyMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7609c2dd8550e43b23d24069200d37cb) | Modifies a message.                                          |
| [markC2CMessageAsRead](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acb3a67bd2fa131b50c611a48fa78f34d) | Marks one-to-one chat (C2C) messages as read                 |
| [markGroupMessageAsRead](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7fc79e30877b8d77fbdfa24e057376dc) | Marks group messages as read                                 |
| [markAllMessageAsRead](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a53d889a6242b5551aa3655e40967a62f) | Marks all conversations as read.                             |
| [deleteMessageFromLocalStorage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2bb42528f4d166ac826914094655841c) | Deletes a message from the local storage                     |
| [deleteMessages](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9e394ea720ecdc10d497b63b6f2b22c4) | Deletes messages from local storage and the cloud.           |
| [clearC2CHistoryMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a005c7767172d9a3980974b68c780c33b) | Clears chat history with a user from local storage and the cloud. |
| [clearGroupHistoryMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a16c01c19a285e2bd11443c868c8256e6) | Clears chat history of a group from local storage and the cloud. |
| [insertGroupMessageToLocalStorage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9b312b67e4da19978b55a7b915815dfe) | Inserts a message in a group chat.                           |
| [insertC2CMessageToLocalStorage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acc1dccd310d1965248cff0d4fd5ca45f) | Inserts a message in a one-to-one chat.                      |
| [findMessages](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a4a0c47d706d8784656225c1e9065f6f1) | Finds local messages by `msgID`.                             |
| [searchLocalMessages](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a10878d0bd326b07ec6a605c5695c7de1) | Searches for local messages.                                 |
| [sendMessageReadReceipts](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a375af7e0f3e0f0b3135ccd517de9fdd8) | Sends message read receipts.                                 |
| [getMessageReadReceipts](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a69192bc43e551f34f5d483dae5e70410) | Gets message read receipts.                                  |
| [getGroupMessageReadMemberList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#aa345a87cfa4da2983f878bb5385d0b82) | Gets the list of group members who have read group messages. |
| [setMessageExtensions](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2e8b8f7ef94d02823cfab0cf5b1e1fea) | Sets message extensions.                                     |
| [getMessageExtensions](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3ae68d2d8aeff6abd21981914836dc1a) | Gets message extensions.                                     |
| [deleteMessageExtensions](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#af3fad5575625e7597a482375d7a65fa6) | Deletes message extensions.                                  |
| [translateText](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#aee0c1e26b0401576ee82967698da35f6) | Translates a text message.                                   |

## Group APIs
Tencent Cloud Chat SDK supports five preset group types, each of which pertains to different scenarios.
- Work group (Work): Users can join the group only after being invited by group members. This group type is the same as private groups (Private) in earlier versions.
- Public group (Public): Users can join the group through requests, which need to be approved by the group owner or group admin.
- Meeting group (Meeting): used together with [TRTC](https://www.tencentcloud.com/products/trtc) to enable scenarios such as video conferencing and online education. Users can join and leave the group freely and view the message history before they join. Same as chat room (ChatRoom) in earlier versions.
- Community: A user can join and leave a community freely. It is suitable for chat scenarios with a super large number of community members, such as knowledge sharing and game discussion. This feature is supported by a client with the SDK enhanced edition v5.8.1668 or later and the web SDK v2.17.0 or later. To use it, you need to purchase the [Ultimate edition](https://buy.cloud.tencent.com/avc?from=17182), and then enable it via **[console](https://console.cloud.tencent.com/im)** > **Feature Configuration** > **Group configuration** > **Group feature configuration** > **Community**.
- Audio-video group (AVChatRoom): An audio-video group allows users to join and leave freely and is suitable for scenarios such as live streaming and chat rooms with on-screen comments. There is no limit on the number of group members.

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setGroupListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a74de68e55d787fd1d4ec83b99cd1fcab) | Sets an event listener for groups. (This API is to be disused. Please use the `addGroupListener` and `removeGroupListener` APIs.) |
| [addGroupListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#af583b113cdec570b08ae80d682fba52c) | Adds an event listener for groups.                           |
| [removeGroupListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a2b2093489bf869f70c03be39f4ed08a1) | Removes an event listener for groups.                        |
| [createGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a3bbcf819c1ec70e520b7f9a42cfbb989) | (Simple API) Creates a group.                                |
| [createGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a59824434b6096180b94d8152183dcd2c) | (Advanced API) Creates a group. The group information and the initial group members can be set during group creation. |
| [joinGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a) | Joins a group                                                |
| [quitGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ac2a43b3ada447131df0c5f19e8079be5) | Leaves a group.                                              |
| [dismissGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a5bd55cb04867985253949d8cc78f860e) | Disbands a group. Only the group owner and group admin can disband a group. |
| [getJoinedGroupList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a4599e99791c150cc9f3e2492e8b4ce04) | Gets the list of groups the current user has joined, excluding audio-video groups. |
| [getGroupsInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a9bca7e5318cfed44335566a783a6b568) | Pulls the profiles of groups                                 |
| [searchGroups](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ac9a960921e512621340159d82a4b5259) | Searches for groups.                                         |
| [setGroupInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144) | Modifies the profile of a group                              |
| [initGroupAttributes](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1b3a56dfc345f1ef2a575cb36156e745) | Initializes group attributes.                                |
| [setGroupAttributes](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a134342ddb51d1ee83f3981ed91d26885) | Sets group attributes.                                       |
| [deleteGroupAttributes](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa504ffca9492580ca27a45f78a87e2cb) | Deletes group attributes.                                    |
| [getGroupAttributes](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ac8a74db230669d1b49da47bb0895cbf9) | Gets group attributes.                                       |
| [getGroupOnlineMemberCount](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ada2eadb44f6865e9848df94fb5bae4ae) | Gets the number of online group members.                     |
| [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a98681b9036e73acbe8f84737b5291326) | Gets the group member list                                   |
| [getGroupMembersInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1ab284b80811bcc697d689d7b97edf04) | Gets the profiles of specified group members                 |
| [searchGroupMembers](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a35ceb734976c833047cceb8b31055b18) | Searches for group members by profile.                       |
| [setGroupMemberInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a40b97ee4b138f93e1b2073d1bdff3756) | Modifies the profile of a specified group member             |
| [muteGroupMember](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa8a0206f75d75400b517f7e0d80fe9ee) | Mutes a group member.                                        |
| [inviteUserToGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a942d75fdea66e22cdbd8c131cf18e1ea) | Invites users to a group                                     |
| [kickGroupMember](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a0581f28fddf2ade890aa62e4318d7a97) | Removes a member from a group.                               |
| [setGroupMemberRole](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a0f1c341a3dc53d6a6557a438b0c64b65) | Sets a role for a group member.                              |
| [markGroupMemberList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a21238536e7cb2c3fd086797e7dc1b970) | Marks group members.                                         |
| [transferGroupOwner](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a58a2ffae60505a43984fe21bf0bc1101) | Transfers the ownership of a group                           |
| [getGroupApplicationList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a29c36ad685159850a30d61a6b9c637e8) | Gets the list of applications to join a group                |
| [acceptGroupApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a51bb9b4f965cb3d01546fef348ac75e4) | Accepts an application to join a group                       |
| [refuseGroupApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a46aa78c54986b2c0b7cc0012a3dc94ef) | Rejects a request to join a group.                           |
| [setGroupApplicationRead](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ade11e93b96206ef851641c42788132d1) | Marks the application list as read                           |
| [getJoinedCommunityList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a17350dec83b7cd32d308a1f2b2827fdd) | Gets the list of community groups the current user has joined. |
| [createTopicInCommunity](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a8cc04d04254867787060cf1cae0fc5b8) | Creates a topic.                                             |
| [deleteTopicFromCommunity](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a31b726136637a58b5bb246eaac41187c) | Deletes a topic.                                             |
| [setTopicInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a237e2fa6e16e55143c516c5428a23936) | Modifies topic information.                                  |
| [getTopicInfoList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#af93ad10e0e2b21d6ae3c8ec45021b159) | Gets the message list.                                       |

## Conversation List APIs
The conversation list is the list a user sees on the first screen after login. It includes elements such as conversation node, conversation name, group name, last message, and unread count.

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setConversationListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a95bac7330779a8a970fc7689e436257f) | Sets a conversation listener. (This API is to be disused. Please use the `addConversationListener` and `removeConversationListener` APIs.) |
| [addConversationListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a39b4f352f1740171fb56143149201cd9) | Adds a conversation listener.                                |
| [removeConversationListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#ab9e1627559fb4259228b4e547b192c83) | Removes a conversation listener.                             |
| [getConversationList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#ab1f5e86e270b122cb725266d234d9dd5) | Gets the conversation list                                   |
| [getConversation](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#ad4b7b80fbe0cff25027371b416ede9f9) | Gets a specified conversation.                               |
| [getConversationList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#af94d9d44e90da448a395e6d92b4e512e) | Gets multiple conversations.                                 |
| [ getConversationListByFilter](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#ac1b77eedff7f2f8742a873cf766daec9) | Gets the advanced conversation API to specify the conversation type, mark type, and group name. |
| [deleteConversation](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a142f5289632f29a603937f1d770748c6) | Deletes a conversation                                       |
| [setConversationDraft](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a462cd163c03cdce230ed3647b414382b) | Sets a draft for a conversation                              |
| [setConversationCustomData](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#af82623b98c07f36767a47c59f5a23927) | Sets custom conversation data.                               |
| [pinConversation](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a06cefb398f5a327dff4cefe6fb18c5b8) | Pins a conversation to the top.                              |
| [markConversation](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a77c02a146f774979e1e04d7334cd2d06) | Marks a conversation.                                        |
| [getTotalUnreadMessageCount](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#abe76208f616713a09df582a6c1665d38) | Gets the total unread message count.                         |
| [ createConversationGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a2f5f4587c881aa26fbdce3b4d469aa0a) | Creates a conversation group.                                |
| [ getConversationGroupList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a037b0973be9feef207a64f2e043792ab) | Gets the list of conversation groups.                        |
| [ deleteConversationGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#aa7b91ded9e451335bc931525839ce736) | Deletes a conversation group.                                |
| [ renameConversationGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a1a9492196c94450b2992079cffab96a6) | Renames a conversation group.                                |
| [ addConversationsToGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a37c78d27216882504d2710a066478db5) | Adds a conversation to a conversation group.                 |
| [ deleteConversationsFromGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a16ee46fa4b7278a0386be9ff633fa552) | Deletes a conversation from a conversation group.            |

## User Profile APIs
You can use the following APIs to query user profiles, modify your profile, and block messages from a specified user (that is, adding a specified user to the blocklist).

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getUsersInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ac638c1dd6ec1e5204637e4b87129cd38) | Gets users’ profiles                                         |
| [setSelfInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a328a0d2d07e8d34e12effb73937c3437) | Modifies one’s own user profile                              |
| [ getUserStatus](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#abe44a4c51c686248d483674d77d71053) | Queries a user's status.                                     |
| [ setSelfStatus](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a7d771431a61635888bdc4def438c4328) | Sets one's own status.                                       |
| [ subscribeUserStatus](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a20e6cbe409549e0d2ff62be76914e0b3) | Subscribes to a user's status.                               |
| [ unsubscribeUserStatus](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a3780734bb50398ebe65155c3223542f0) | Unsubscribes from a user's status.                           |
| [addToBlackList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a67d998da5085b5004bb6aa8d4322022c) | Blocks messages from a specified user, which means adding the user to the blocklist. |
| [deleteFromBlackList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#aa7e69a67185eaca658ba429cf6309a5f) | Unblocks messages from a specified user, which means removing the user from the blocklist. |
| [getBlackList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a0d854d64c8ae936014a8424d55508fa3) | Gets the blocklist                                           |

## Offline Push APIs
Use the offline push service if you want your app to receive Chat service messages in real time when it is in the background.

| API                                                          | Description                |
| ------------------------------------------------------------ | -------------------------- |
| [setAPNSListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07APNS_08.html#a62e1694cf9e1d65b76f90064cbcbb683) | Sets an APNs listener.     |
| [setAPNS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07APNS_08.html#a73bf19c0c019e5e27ec441bc753daa9e) | Configures APNs Push info. |
| [setVOIP](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07VOIP_08.html#a0bd652eed597771ca1381d0d6ea67704) | Configures VoIP Push info. |

## Friend Management APIs
By default, Tencent Cloud Chat does not check your relationship with a user when receiving and sending messages. You can enable **Check Relationship for One-to-One Messages** on **Feature Configuration** > **Login and Message** > **Relationship Check** in the [Chat console](https://console.cloud.tencent.com/im) and use the following APIs to delete/add friends and manage your friends.

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setFriendListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#acd403f586f3df84f56b1b757efb2d443) | Sets a relationship chain and friend profile listener. (This API is to be disused. Please use the `addFriendListener` and `removeFriendListener` APIs.) |
| [addFriendListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a1de011b63b3c20b1be519dc7ba124704) | Adds a relationship chain listener.                          |
| [removeFriendListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#aed40ccbbc4e15be79154077a6d3ec085) | Removes a relationship chain listener.                       |
| [getFriendList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a81131d76924a03ec2b593addd6e4e101) | Gets the contacts.                                           |
| [getFriendsInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a39f6752da11b595e4a5b6dcb0eb6a584) | Gets the profiles of specified friends                       |
| [setFriendInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ac258312c000c1af69fcf51dd6898b74b) | Sets the profile of a specified friend                       |
| [searchFriends](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a9a036dcc1bd65474a3d2e90f2bb6b9c6) | Searches for friends.                                        |
| [addFriend](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ac1ea1c7de2bfc2b0a25e5f6b3192e304) | Adds a friend                                                |
| [deleteFromFriendList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#af967134fb177b32d4060fedf3663ace3) | Deletes a friend                                             |
| [checkFriend](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#aad1b09fab6523d9a36147b4ed4efac67) | Checks relationship with specified users.                    |
| [getFriendApplicationList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#acda7968f1e9adc12261a7e533d709a1c) | Gets the list of friend requests                             |
| [acceptFriendApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a51b913927028025e2e450e6e8ce848c0) | Accepts a friend request                                     |
| [refuseFriendApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a406b964a6513219cfe4803f87f0f00f8) | Rejects a friend request                                     |
| [deleteFriendApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a363e0622f653694999293c595d552896) | Deletes a friend request                                     |
| [setFriendApplicationRead](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ad46c70c18b8f69bf272cbf3466477a85) | Marks a friend request as read.                              |
| [createFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a8b33edab15ae7d179e4e2d885e7d2b7d) | Creates a friend list                                        |
| [getFriendGroups](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a63f3eaae567586077d5a8d27c31e2229) | Gets the information of friend lists                         |
| [deleteFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a2dc49f2abb1238fc2d47ce6d4f14c1e7) | Deletes friend lists                                         |
| [renameFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a93f6ba132d9706db7c74daff97a2abd0) | Modifies the name of a friend list                           |
| [addFriendsToFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a0265241c39600c390406ca1f8f6ff75d) | Adds friends to a friend list                                |
| [deleteFriendsFromFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a4a14a878816c8d6a20981d1903fcf359) | Removes friends from a friend list.                          |
