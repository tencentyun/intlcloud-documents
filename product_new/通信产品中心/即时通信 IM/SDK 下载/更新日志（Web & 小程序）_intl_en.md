### Version 2.4.0 @2020.1.3
**Additions**
- Added the [revokeMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#revokeMessage) API for recalling messages.
- Added the `isRevoked` attribute to [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html). The value `true` identifies the recalled message.
- Added the message recall event notification [TIM.EVENT.MESSAGE_REVOKED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_REVOKED).
- Added forcible logout types of [forcible logout due to multi-client login](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.KICKED_OUT_MULT_ACCOUNT) and [forcible logout due to UserSig expiration](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.KICKED_OUT_USERSIG_EXPIRED) to [TIM.EVENT.KICKED_OUT](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.KICKED_OUT).

**Changes**
- Increased the maximum size of files uploaded through [createFileMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFileMessage) from 20 MB to 100 MB.
- About to deprecate the `msgMemberInfo` and `shutupTime` of [Group Tips](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload) and replace them with `memberList` and `muteTime`, respectively.
- Added the entry to **IM Smart Customer Service** in the console.

**Fixes**
- Fixed the issue where calling the [off](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#off) API failed to cancel listening for events.
- Fixed the incorrect value and type of the `isRead` attribute of [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).
- Fixed the incorrect error code and error message for exceeding the video file size limit when sending a video message.
- Fixed occasional errors in field content after updating custom fields.
- Fixed occasional [JOIN_STATUS_ALREADY_IN_GROUP](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.JOIN_STATUS_ALREADY_IN_GROUP) errors when joining AVChatRoom groups after login.
- Fixed potential performance issues caused by core-js.


### Version 2.3.2 @2019.12.18
**Changes**
Supported [custom profile fields](https://intl.cloud.tencent.com/document/product/1047/33520#.E8.87.AA.E5.AE.9A.E4.B9.89.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5) by [getUserProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getUserProfile) and [updateMyProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateMyProfile).

**Fixes**
Fixed the issue where [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) lost combined messages.

### Version 2.3.1 @2019.12.13
**Additions**
- Supported passing in [file](https://developer.mozilla.org/zh-CN/docs/Web/API/File) objects by [createImageMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createImageMessage) and [createFileMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFileMessage).
- Added the [createFaceMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFaceMessage) API for creating emoji messages.
- Optimized message notification efficiency for [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) groups to dramatically improve the user experience.

**Changes**
- When a message fails to be sent, the SDK returns the actual error code and error message.
- Calling [logout](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#logout) now only logs out from the message channel of the current instance.
- The callback functions passed in by the access side are encapsulated for security purposes. If the logic of callback functions is incorrect, this error can be quickly detected and located.
- The SDK outputs error messages in Chinese when [IM server-side error codes](https://intl.cloud.tencent.com/document/product/1047/34348#.EF.BC.88.E4.BA.8C.EF.BC.89.E6.9C.8D.E5.8A.A1.E7.AB.AF.E7.9A.84.E9.94.99.E8.AF.AF.E7.A0.81) appear.

**Fixes**
- Fixed occasional issues where messages were lost when WeChat Mini Program went to foreground after staying in the background for a long time.
- Fixed the error where [TIM.EVENT.CONVERSATION_LIST_UPDATED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.CONVERSATION_LIST_UPDATED) was triggered several times when a message was sent.
- Fixed the SDK error caused by not calling [registerPlugin](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#registerPlugin) or incorrect input parameters when uploading images.
- Fixed the issue where long polling did not stop after a [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) group was dismissed.
- Fixed the issue where, when "multi-instance" or "multi-client" login was enabled, other instances or clients failed to receive messages after a web instance was logged out.
- Fixed occasional SDK errors due to the structure of the pulled conversation list.

### Version 2.2.1 @2019.11.28
**Changes**
Improved logic for pulling group roaming messages.

**Fixes**
- Fixed the issue where the SDK prompted [error code 2901](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html) after the group owner of an AVChatRoom group modified the group profile.
- Fixed the issue where the group admin received requests that had been processed after refreshing.

### Version 2.2.0 @2019.11.21
**Additions**
- Supported sending video messages by mini programs: [createVideoMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createVideoMessage). Video messages are supported across platforms. To use this feature, update to the latest version of the [TUIKit and SDK](https://cloud.tencent.com/document/product/269/36887).
- Added the [getGroupMemberProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberProfile) API for querying group member profiles.
- Achieved the compatibility with audio and file messages sent by Native IM v3.x.
- Supported [GeoPayload](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GeoPayload) for receiving location messages.

**Changes**
Supported writing up to 100 groups to local storage. The SDK does not write the full group list when more than 100 groups exist.
  
**Fixes**
- Fixed the issue where the long polling of [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) groups continued after logout.
- Fixed the issue where group contact cards in the message instances of [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) groups had no values.
- Fixed the error that was reported when using the IE 10 browser.
- Fixed the inability to join groups anonymously.

### Version 2.1.4 @2019.11.7
**Changes**
- When the `Promise` state returned by an SDK API is `rejected`, the SDK stops delivering [TIM.EVENT.ERROR](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.ERROR) events.
- Updates to the user’s Profile are immediately written to the local cache.

**Fixes**
- Fixed the SDK error caused by modifying prototype chains by zone.js of the Angular framework.
- Fixed the issue where, after the group owner created and joined a [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) group, the owner could not receive messages.
- Fixed the initialization error due to oversize group lists.

### Version 2.1.3 @2019.10.31

**Changes**
Compatible with combined messages (messages that contain multiple message elements in one message) sent by RESTful APIs or earlier IM versions. For more information, see the [Compatibility Guide](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/tutorial-01-faq.html).

**Fixes**
- Fixed the incorrect unread count.
- Fixed disorderly messages caused by not reporting read messages.
- Fixed the issue where empty image messages were sent successfully but could not be rendered. The SDK does not support sending empty image messages.
- Fixed the issue where empty file messages were sent with incorrect message states. The SDK does not support sending empty file messages.
- Fixed occasional SDK code errors that occurred when calling [getGroupMemberList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberList).

### Version 2.1.2 @2019.10.25
**Additions**
 Supported pulling group information including the group owner ID and group member count through the [getGroupList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupList) API.

**Fixes**
- Fixed the SDK code error that occurred when using a RESTful API to send custom group notifications in AVChatRoom groups.
- Fixed the issue where the SDK did not initiate a request to pull historical messages when getMessageList was called upon joining the group again after quitting.
- Fixed the SDK code error caused by upload failures.

### Version 2.1.1 @2019.10.18
**Additions**
Supported [sending audio messages](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createAudioMessage) by mini programs. Audio messages are supported across platforms. To use this feature, update to the latest version of the [TUIKit and SDK](https://intl.cloud.tencent.com/document/product/1047/33996).

**Fixes**
Fixed the issue where, after joining the group again after quitting, [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) could still pull historical messages prior to quitting the group.

### Version 2.1.0 @2019.10.16

**Additions**
- Supported receiving [audio messages](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.AudioPayload) by web and mini programs.
- Supported receiving [video messages](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.VideoPayload) by web and mini programs.

**Changes**
- Supported pulling up to 15 messages at a time by the [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) API.
- Deprecated [TIM.TYPES.MSG_SOUND](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.MSG_SOUND) and replaced it with [TIM.TYPES.MSG_AUDIO](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.MSG_AUDIO).

**Fixes**
- Fixed the issue where [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) failed to pull messages from deleted group chats.
- Fixed the issue where group system notifications did not contain group names.
- Fixed the issue where conversations with newly created messages had no profiles.

### Version 2.0.11 @2019.10.12

**Fixes**
Fixed the React framework bug where image messages could not be sent.

### Version 2.0.9 @2019.9.19

**Additions**
Supported detecting the original width and height of an image before sending the image message.

**Changes**
- Used the HTTPS protocol by default.
- Added the event of receiving new group system notifications whose type is [TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED).

**Fixes**
- Fixed the splash screen issue when sending image messages by mini programs.
- Fixed the error with sending JPG images.
