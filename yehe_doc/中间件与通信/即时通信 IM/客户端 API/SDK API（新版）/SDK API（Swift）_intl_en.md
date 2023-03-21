>!**Do not use APIs of new and old versions at the same time**.

## Initialization and Login APIs

To use the Tencent Cloud Chat service, you need to initialize the SDK and log in.

| API | Description |
|---------|---------|
| [initSDK](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.initsdk(sdkappid:config:)) | Initializes the SDK. |
| [unInitSDK](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.uninitsdk()) | Uninitializes the SDK. |
| [addIMSDKListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.addimsdklistener(listener:)) | Adds a Chat service listener. |
| [removeIMSDKListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.removeimsdklistener(listener:)) | Removes a Chat service listener. |
| [getVersion](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.getversion()) | Gets the version number. |
| [getServerTime](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.getservertime()) | Gets the server time. |
| [login](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.login(userid:usersig:succ:fail:)) | Logs in. |
| [logout](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.logout(succ:fail:)) | Logs out. |
| [getLoginUser](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.getloginuser()) | Gets the currently logged-in user. |
| [getLoginStatus](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.getloginstatus()) | Gets the login status. |
| [getUserStatus](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.getuserstatus(useridlist:succ:fail:)) | Gets user status information. |
| [setSelfStatus](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.setselfstatus(status:succ:fail:)) | Sets user status for yourself. |
| [subscribeUserStatus](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.subscribeuserstatus(useridlist:succ:fail:)) | Subscribes to user status. |
| [unsubscribeUserStatus](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.unsubscribeuserstatus(useridlist:succ:fail:)) | Unsubscribes from user status. |

## Simple Message APIs

Use the following APIs for the sending and receiving of text and signaling (custom buffer) messages.

| API | Description |
|---------|---------|
| [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.addsimplemsglistener(listener:)) | Sets an event listener for simple messages (text messages and custom messages).<br/>Do not use it and [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.addadvancedmsglistener(listener:)) at the same time. |
| [removeSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.removesimplemsglistener(listener:)) | Removes the event listener for simple messages (text messages and custom messages). |
| [sendC2CTextMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.sendc2ctextmessage(text:to:succ:fail:)) | Sends a one-to-one (C2C) text message. |
| [sendC2CCustomMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.sendc2ccustommessage(customdata:to:succ:fail:)) | Sends a one-to-one custom (signaling) message. |
| [sendGroupTextMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.sendgrouptextmessage(text:to:priority:succ:fail:)) | Sends a group text message. |
| [sendGroupCustomMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.sendgroupcustommessage(customdata:to:priority:succ:fail:)) | Sends a group custom (signaling) message. |

## Signaling APIs

| API | Description |
|---------|---------|
| [addSignalingListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Signaling.html#v2timmanager.addsignalinglistener(listener:)) | Adds a signaling listener.                            |
| [removeSignalingListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Signaling.html#v2timmanager.removesignalinglistener(listener:)) | Removes a signaling listener. |
| [invite](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Signaling.html#v2timmanager.invite(invitee:data:onlineuseronly:offlinepushinfo:timeout:succ:fail:)) | Invites a user. |
| [inviteInGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Signaling.html#v2timmanager.inviteingroup(groupid:inviteelist:data:onlineuseronly:timeout:succ:fail:)) | Invites certain users in the group. |
| [cancel](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Signaling.html#v2timmanager.cancel(inviteid:data:succ:fail:)) | Cancels an invitation. |
| [accept](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Signaling.html#v2timmanager.accept(inviteid:data:succ:fail:)) | Accepts an invitation. |
| [reject](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Signaling.html#v2timmanager.reject(inviteid:data:succ:fail:)) | Rejects an invitation. |
| [getSignalingInfo](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Signaling.html#v2timmanager.getsignallinginfo(msg:)) | Gets the signaling information. |
| [addInvitedSignaling](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Signaling.html#v2timmanager.addinvitedsignaling(signalinginfo:succ:fail:)) | Adds invitation signaling (can be used for invitation signaling triggered by offline push messages for group invitations). |
| [modifyInvitation](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Signaling.html#v2timmanager.modifyinvitation(inviteid:data:succ:fail:)) | Modifies invitation signaling. |

## Advanced Message APIs

If you need to send/receive rich media messages (such as image, video, and file messages) and use advanced features such as recalling messages, marking messages as read, and querying message history, use the following set of advanced message APIs. Do not use simple message APIs and advanced message APIs at the same time.

| API | Description |
|---------|---------|
| [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.addadvancedmsglistener(listener:)) | Sets an event listener for advanced messages.<br/>Do not use it and [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.addsimplemsglistener(listener:)) at the same time. |
| [removeAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.removeadvancedmsglistener(listener:)) | Removes the listener for advanced messages. |
| [createTextMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.createtextmessage(text:)) | Creates a text message. |
| [createCustomMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.createcustommessage(data:)) | Creates a custom message. |
| [createImageMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.createimagemessage(imagepath:)) | Creates an image message. |
| [createSoundMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.createsoundmessage(audiofilepath:duration:)) | Creates a voice message. |
| [createVideoMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.createvideomessage(videofilepath:type:duration:snapshotpath:)) | Creates a video message. |
| [createFileMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.createfilemessage(filepath:filename:)) | Creates a file message. |
| [createLocationMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.createlocationmessage(desc:longitude:latitude:)) | Creates a location message. |
| [createFaceMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.createfacemessage(index:data:)) | Creates an emoji message. |
| [createMergerMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.createmergermessage(messagelist:title:abstractlist:compatibletext:)) | Creates a combined forward message. |
| [createForwardMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.createforwardmessage(message:)) | Creates a single forward message. |
| [createTargetedGroupMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.createtargetedgroupmessage(message:receiverlist:)) | Creates a targeted group message |
| [createAtSignedGroupMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.createatsignedgroupmessage(message:atuserlist:)) | Creates an @ group message. |
| [sendMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.sendmessage(message:receiver:groupid:priority:onlineuseronly:offlinepushinfo:progress:succ:fail:)) | Sends a message. The message object can be created using a createXXXMessage API. |
| [setC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.setc2creceivemessageopt(useridlist:opt:succ:fail:)) | Sets the Mute Notifications option for one-to-one messages. |
| [getC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.getc2creceivemessageopt(useridlist:succ:fail:)) | Gets the Mute Notifications status for one-to-one messages. |
| [setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.setgroupreceivemessageopt(groupid:opt:succ:fail:)) | Sets the Mute Notifications option for group messages. |
| [getC2CHistoryMessageList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.getc2chistorymessagelist(userid:count:lastmsg:succ:fail:)) | Gets one-to-one (C2C) message history. |
| [getGroupHistoryMessageList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.getgrouphistorymessagelist(groupid:count:lastmsg:succ:fail:)) | Gets group chat message history. |
| [getHistoryMessageList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.gethistorymessagelist(option:succ:fail:)) | (Advanced API) Gets message history. |
| [revokeMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.revokemessage(msg:succ:fail:)) | Recalls a message. The message object can be created using a createXXXMessage API. |
| [modifyMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.modifymessage(msg:completion:)) | Modifies a message. The message object can be created using a createXXXMessage API. |
| [markC2CMessageAsRead](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.markc2cmessageasread(userid:succ:fail:)) | Marks one-to-one (C2C) messages as read.          |
| [markGroupMessageAsRead](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.markgroupmessageasread(groupid:succ:fail:)) | Marks group messages as read. |
| [markAllMessageAsRead](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.markallmessageasread(succ:fail:)) | Marks all messages as read. |
| [deleteMessageFromLocalStorage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.deletemessagefromlocalstorage(msg:succ:fail:)) | Deletes a message from local storage. |
| [deleteMessages](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.deletemessages(msglist:succ:fail:)) | Deletes messages from local storage and the cloud. |
| [clearC2CHistoryMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.clearc2chistorymessage(userid:succ:fail:)) | Clears chat history with a user from local storage and the cloud. |
| [clearGroupHistoryMessage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.cleargrouphistorymessage(groupid:succ:fail:)) | Clears chat history of a group from local storage and the cloud. |
| [insertGroupMessageToLocalStorage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.insertgroupmessagetolocalstorage(msg:to:sender:succ:fail:)) | Inserts a message in a group chat. |
| [insertC2CMessageToLocalStorage](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.insertc2cmessagetolocalstorage(msg:to:sender:succ:fail:)) | Inserts a message in a one-to-one chat. |
| [findMessages](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.findmessages(messageidlist:succ:fail:)) | Finds local messages by `msgID`. |
| [searchLocalMessages](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.searchlocalmessages(param:succ:fail:)) | Searches for local messages. |
| [sendMessageReadReceipts](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.sendmessagereadreceipts(messagelist:succ:fail:)) | Sends message read receipts. |
| [getMessageReadReceipts](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.getmessagereadreceipts(messagelist:succ:fail:)) | Gets message read receipts. |
| [getGroupMessageReadMemberList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.getgroupmessagereadmemberlist(message:filter:nextseq:count:succ:fail:)) | Gets the list of group members who have read group messages. |
| [setMessageExtensions](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.setmessageextensions(message:extensions:succ:fail:)) | Sets message extensions. |
| [getMessageExtensions](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.getmessageextensions(message:succ:fail:)) | Gets message extensions. |
| [deleteMessageExtensions](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.deletemessageextensions(message:keys:succ:fail:)) | Deletes message extensions. |
| [translateText](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Message.html#v2timmanager.translatetext(sourcetextlist:sourcelanguage:targetlanguage:completion:)) | Translates text messages. |



## Group APIs

Tencent Cloud Chat SDK supports the following predefined group types, each of which pertains to different application scenarios:

- Work group (Work): Users can join the group only after being invited by existing members.
- Public group (Public): Users can join the group through requests, which need to be approved by the group owner or group admin.
- Meeting group (Meeting): used together with [TRTC](https://cloud.tencent.com/product/trtc) to enable scenarios such as video conferencing and online education. Users can join and leave the group freely and view the message history before they join.
- Audio-video group (AVChatRoom): An audio-video group allows users to join and leave freely and is suitable for scenarios such as live streaming and chat rooms with on-screen comments. There is no limit on the number of group members.

| API | Description |
|---------|---------|
| [addGroupListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.addgrouplistener(listener:)) | Adds an event listener for groups. |
| [removeGroupListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.removegrouplistener(listener:)) | Removes an event listener for groups. |
| [createGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.creategroup(grouptype:groupid:groupname:succ:fail:)) | (Simple API) Creates a group. |
| [createGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.creategroup(info:memberlist:succ:fail:)) | (Advanced API) Creates a group. The group information and the initial group members can be set during group creation. |
| [joinGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.joingroup(groupid:msg:succ:fail:)) | Joins a group. |
| [quitGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.quitgroup(groupid:succ:fail:)) | Leaves a group. |
| [dismissGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.dismissgroup(groupid:succ:fail:)) | Disbands a group. Only the group owner and group admin can disband a group. |
| [getJoinedGroupList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.getjoinedgrouplist(succ:fail:)) | Gets the list of groups the current user has joined, excluding audio-video groups. |
| [getGroupsInfo](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.getgroupsinfo(groupidlist:succ:fail:)) | Gets the profiles of groups. |
| [searchGroups](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.searchgroups(searchparam:succ:fail:)) | Searches for groups. |
| [setGroupInfo](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.setgroupinfo(info:succ:fail:)) | Modifies the profile of a group. |
| [ initGroupAttributes](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.initgroupattributes(groupid:attributes:succ:fail:)) | Initializes group attributes. |
| [ setGroupAttributes](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.setgroupattributes(groupid:attributes:succ:fail:)) | Sets group attributes. |
| [ deleteGroupAttributes](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.deletegroupattributes(groupid:keys:succ:fail:)) | Deletes group attributes. |
| [ getGroupAttributes](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.getgroupattributes(groupid:keys:succ:fail:)) | Gets group attributes. |
| [getGroupOnlineMemberCount](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.getgrouponlinemembercount(groupid:succ:fail:)) | Gets the number of online group members. |
| [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.getgroupmemberlist(groupid:filter:nextseq:succ:fail:)) | Gets the group member list. |
| [getGroupMembersInfo](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.getgroupmembersinfo(groupid:memberlist:succ:fail:)) | Gets the profiles of specified group members. |
| [searchGroupMembers](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.searchgroupmembers(searchparam:succ:fail:)) | Searches for the profiles of specified group members. |
| [setGroupMemberInfo](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.setgroupmemberinfo(groupid:info:succ:fail:)) | Modifies the profiles of specified group members. |
| [muteGroupMember](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.mutegroupmember(groupid:memberuserid:mutetimeseconds:succ:fail:)) | Mutes group members. |
| [inviteUserToGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.inviteusertogroup(groupid:userlist:succ:fail:)) | Invites users to a group.                         |
| [kickGroupMember](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.kickgroupmember(groupid:memberlist:reason:succ:fail:)) | Removes a member from a group. |
| [setGroupMemberRole](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.setgroupmemberrole(groupid:memberuserid:newrole:succ:fail:)) | Sets the role for a group member. |
| [markGroupMemberList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.markgroupmemberlist(groupid:memberlist:marktype:enablemark:succ:fail:)) | Marks group members. |
| [transferGroupOwner](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.transfergroupowner(groupid:memberuserid:succ:fail:)) | Transfers the group ownership. |
| [getGroupApplicationList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.getgroupapplicationlist(succ:fail:)) | Gets the list of requests to join a group. |
| [acceptGroupApplication](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.acceptgroupapplication(application:reason:succ:fail:)) | Accepts a request to join a group. |
| [refuseGroupApplication](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.refusegroupapplication(application:reason:succ:fail:)) | Rejects a request to join a group. |
| [setGroupApplicationRead](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.setgroupapplicationread(succ:fail:)) | Marks the request list as read. |
| [getJoinedCommunityList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.getjoinedcommunitylist(succ:fail:)) | Gets the list of community groups the current user has joined. |
| [createTopicInCommunity](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.createtopicincommunity(groupid:topicinfo:succ:fail:)) | Creates a topic. |
| [deleteTopicFromCommunity](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.deletetopicfromcommunity(groupid:topicidlist:succ:fail:)) | Deletes a topic. |
| [setTopicInfo](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.settopicinfo(topicinfo:succ:fail:)) | Modifies topic information. |
| [getTopicInfoList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Group.html#v2timmanager.gettopicinfolist(groupid:topicidlist:succ:fail:)) | Gets the topic list. |

## Conversation List APIs

The conversation list is the list a user sees on the first screen after login. It includes elements such as conversation node, conversation name, group name, last message, and unread count.

| API | Description |
|---------|---------|
| [addConversationListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.addconversationlistener(listener:)) | Adds a conversation listener. |
| [removeConversationListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.removeconversationlistener(listener:)) | Removes a conversation listener. |
| [getConversationList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.getconversationlist(nextseq:count:succ:fail:)) | Gets the conversation list. |
| [getConversation](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.getconversation(conversationid:succ:fail:)) | Gets a specified conversation. |
| [getConversationList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.getconversationlist(conversationidlist:succ:fail:)) | Gets multiple conversations. |
| [getConversationListByFilter](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.getconversationlistbyfilter(filter:succ:fail:)) | (Advanced API) Gets the conversation list. |
| [deleteConversation](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.deleteconversation(conversation:succ:fail:)) | Deletes a conversation. |
| [setConversationDraft](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.setconversationdraft(conversationid:drafttext:succ:fail:)) | Sets a draft for a conversation. |
| [setConversationCustomData](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.setconversationcustomdata(conversationidlist:customdata:succ:fail:)) | Sets custom data for a conversation. |
| [pinConversation](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.pinconversation(conversationid:ispinned:succ:fail:)) | Pins a conversation to the top. |
| [markConversation](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.markconversation(conversationidlist:marktype:enablemark:succ:fail:)) | Marks a conversation. |
| [getTotalUnreadMessageCount](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.gettotalunreadmessagecount(succ:fail:)) | Gets the total unread message count. |
| [createConversationGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.createconversationgroup(groupname:conversationidlist:succ:fail:)) | Creates a conversation group. |
| [getConversationGroupList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.getconversationgrouplist(succ:fail:)) | Gets the conversation group list. |
| [deleteConversationGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.deleteconversationgroup(groupname:succ:fail:)) | Deletes a conversation group. |
| [renameConversationGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.renameconversationgroup(oldname:newname:succ:fail:)) | Renames a conversation group. |
| [addConversationsToGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.addconversationstogroup(groupname:conversationidlist:succ:fail:)) | Adds a conversation to a conversation group. |
| [deleteConversationsFromGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Conversation.html#v2timmanager.deleteconversationsfromgroup(groupname:conversationidlist:succ:fail:)) | Deletes a conversation from a conversation group. |


## User Profile APIs

You can use the following APIs to query user profiles, modify your profile, and block messages from a specified user (that is, adding a specified user to the blocklist).

| API | Description |
|---------|---------|
| [getUsersInfo](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.getusersinfo(useridlist:succ:fail:)) | Gets user profiles. |
| [setSelfInfo](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager.html#v2timmanager.setselfinfo(info:succ:fail:)) | Modifies one's own user profile. |
| [addToBlackList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.addtoblacklist(useridlist:succ:fail:)) | Blocks messages from a specified user, which means adding the user to the blocklist. |
| [deleteFromBlackList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.deletefromblacklist(useridlist:succ:fail:)) | Unblocks messages from a specified user, which means removing the user from the blocklist. |
| [getBlackList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.getblacklist(succ:fail:)) | Gets the blocklist. |

## Offline Push APIs
Use the offline push service if you want your app to receive Chat service messages in real time when it is in the background. For detailed configuration, see [Offline Push (iOS)](https://cloud.tencent.com/document/product/269/9154).

| API | Description |
|---------|---------|
| [setAPNSListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+APNS.html#v2timmanager.setapnslistener(apnslistener:)) | Sets an APNs listener. |
| [setAPNS](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+APNS.html#v2timmanager.setapns(config:succ:fail:)) | Configures APNs Push information. |
| [setVOIP](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+VOIP.html#v2timmanager.setvoip(config:succ:fail:)) | Configures VoIP Push information. |

## Friend Management APIs
By default, Tencent Cloud Chat does not check your relationship with a user when receiving and sending messages. You can enable **Check Relationship for One-to-One Messages** on **Feature Configuration** > **Login and Message** > **Relationship Check** in the [Chat console](https://console.cloud.tencent.com/im) and use the following APIs to delete/add friends and manage your friends.

| API | Description |
|---------|---------|
| [addFriendListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.addfriendlistener(listener:)) | Adds a relationship chain listener to receive contacts and blocklist change events. |
| [removeFriendListener](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.removefriendlistener(listener:)) | Removes a relationship chain listener. |
| [getFriendList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.getfriendlist(succ:fail:)) | Gets the contacts. |
| [getFriendsInfo](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.getfriendsinfo(useridlist:succ:fail:)) | Gets the profiles of specified friends. |
| [setFriendInfo](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.setfriendinfo(info:succ:fail:)) | Sets the profile of a specified friend. |
| [searchFriends](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.searchfriends(searchparam:succ:fail:)) | Searches for friends. |
| [addFriend](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.addfriend(application:succ:fail:)) | Adds a friend. |
| [deleteFromFriendList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.deletefromfriendlist(useridlist:deletetype:succ:fail:)) | Deletes a friend. |
| [checkFriend](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.checkfriend(useridlist:checktype:succ:fail:)) | Checks your relationship with a specified user.           |
| [getFriendApplicationList](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.getfriendapplicationlist(succ:fail:)) | Gets the list of friend requests.                      |
| [acceptFriendApplication](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.acceptfriendapplication(application:accepttype:succ:fail:)) | Accepts a friend request.                                |
| [refuseFriendApplication](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.refusefriendapplication(application:succ:fail:)) | Rejects a friend request.                                |
| [deleteFriendApplication](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.deletefriendapplication(application:succ:fail:)) | Deletes a friend request. |
| [setFriendApplicationRead](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.setfriendapplicationread(succ:fail:)) | Marks a friend request as read. |
| [createFriendGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.createfriendgroup(groupname:useridlist:succ:fail:)) | Creates a friend list. |
| [get​Friend​Group​List](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.getfriendgrouplist(groupnamelist:succ:fail:)) | Gets the list of friend lists. |
| [deleteFriendGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.deletefriendgroup(groupnamelist:succ:fail:)) | Deletes a friend list. |
| [renameFriendGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.renamefriendgroup(oldname:newname:succ:fail:)) | Modifies the name of a friend list. |
| [addFriendsToFriendGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.addfriendstofriendgroup(groupname:useridlist:succ:fail:)) | Adds friends to a friend list. |
| [deleteFriendsFromFriendGroup](https://im.sdk.qcloud.com/doc/en/swift_V2TIMManager+Friendship.html#v2timmanager.deletefriendsfromfriendgroup(groupname:useridlist:succ:fail:)) | Deletes friends from a friend list. |

