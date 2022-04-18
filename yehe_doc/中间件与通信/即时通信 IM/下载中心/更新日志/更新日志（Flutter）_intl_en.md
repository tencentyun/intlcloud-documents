## IM Flutter SDK 3.9.1 @2022.3.24
- Upgraded the underlying library to v6.1.2155.

## IM Flutter SDK 3.9.0 @2022.3.22
- Modified GroupListener.

## IM Flutter SDK 3.8.9 @2022.3.18
- Fixed the registration result listening issue.

## IM Flutter SDK 3.8.4 @2022.3.14
- Updated APIs.

## IM Flutter SDK 3.8.3 @2022.3.1
- Switched the token encoding format based on the environment.

## IM Flutter SDK 3.8.2 @2022.2.21
- Updated group member parameter constraints.

## IM Flutter SDK 3.8.0 @2022.2.17
- Upgraded the underlying API dependencies.

## IM Flutter SDK 3.7.8 @2022.2.15
- Fixed the exception caused by force unwrapping.

## IM Flutter SDK 3.7.7 @2022.2.10
- Fixed the Swift code warning.
- Rewrote Swift's force unwrapping code.
- Added the `id` field to the `message` instance returned by the `sendMessage` API.


## IM Flutter SDK 3.7.5 @2022.01.23
- Upgraded the underlying library to v6.0.1975.
- Supported the TPNS token for offline push configuration.


## IM Flutter SDK 3.7.1 @2022.01.12
- Added the feature of returning the message creation ID for a message sending progress event.
- Optimized the callback by reminding the business side that the callback error is caught in SDK and needs to be modified.

## IM Flutter SDK 3.7.0 @2022.01.10
- Optimized the unpacking of cloudCustomData.


## IM Flutter SDK 3.6.9 @2022.01.06
- Optimized the message reply parameters.


## IM Flutter SDK 3.6.8 @2022.01.06
- Optimized the message reply API.


## IM Flutter SDK 3.6.7 @2022.01.05
- Upgraded the compiling environment for iOS from 8.0 to 9.0.


## IM Flutter SDK 3.6.6 @2021.12.30
- Added the message reply API.
- Fixed the issue for web where the release mode triggered an error.


## IM Flutter SDK 3.6.5 @2021.12.17
- Fixed syntax errors in Java.

## IM Flutter SDK 3.6.4  @2021.12.17
- Fixed the bug for Android where no message was returned for an async registration event.
- Fixed the issue where removing a general listening event triggered an error.
- Added the UUID of a message being sent in its progress event.

## IM Flutter SDK 3.6.3 @2021.12.9
- Optimized the `addFriend` API: Changed `addType` from int to FriendTypeEnum.
- Optimized the `acceptFriendApplication` API: Changed `acceptType` from int to FriendResponseTypeEnum.
- Optimized the `checkFriend` API: Changed `checkType` from int to FriendTypeEnum.
- Optimized the `createGroup` API: Changed `addOpt` from int to GroupAddOptTypeEnum.
- Optimized the `deleteFromFriendList` API: Changed `deleteType` from int to FriendTypeEnum.
- Optimized the `getGroupMemberList` API: Changed `filter` from int to GroupMemberFilterTypeEnum.
- Optimized the `getHistoryMessageList` API: Changed `type` from int to HistoryMsgGetTypeEnum.
- Optimized the `getHistoryMessageListWithoutFormat` API: Changed `type` from int to HistoryMsgGetTypeEnum.
- Optimized the `getGroupMemberList` API: Changed `type` from int to GroupMemberFilterTypeEnum.
- Optimized the `getGroupMemberList` API: Changed `filter` from int to GroupMemberFilterTypeEnum.
- Optimized the `initSDK` API: Changed `loglevel` from int to LogLevelEnum.
- Optimized the `refuseFriendApplication` API: Changed `acceptType` from int to FriendApplicationTypeEnum.
- Optimized the `sendCustomMessage` API: Changed `priority` from int to MessagePriorityEnum.
- Optimized the `sendFaceMessage` API: Changed `priority` from int to MessagePriorityEnum.
- Optimized the `sendFileMessage` API: Changed `priority` from int to MessagePriorityEnum.
- Optimized the `sendForwardMessage` API: Changed `priority` from int to MessagePriorityEnum.
- Optimized the `sendImageMessage` API: Changed `priority` from int to MessagePriorityEnum.
- Optimized the `sendLocationMessage` API: Changed `priority` from int to MessagePriorityEnum.
- Optimized the `sendMergerMessage` API: Changed `priority` from int to MessagePriorityEnum.
- Optimized the `sendSoundMessage` API: Changed `priority` from int to MessagePriorityEnum.
- Optimized the `sendTextAtMessage` API: Changed `priority` from int to MessagePriorityEnum.
- Optimized the `sendTextMessage` API: Changed `priority` from int to MessagePriorityEnum.
- Optimized the `setGroupMemberRole` API: Changed `role` from int to GroupMemberRoleTypeEnum.
- Changed the event callback mode to asynchronous.

## IM Flutter SDK 3.6.2 @2021.12.9
- Fixed the issue where no uuid was passed in for removing an advanced message.


## IM Flutter SDK 3.6.1 @2021.12.8
- Fixed the loss of the file progress event.


## IM Flutter SDK 3.6.0 @2021.12.1
- Added the support for multiple listener registrations and callbacks in modules.
- Added the `markAllMessageAsRead` API for marking all messages as read.
- Added the feature of parsing combined messages.
- Upgraded the Native SDK to v5.8.1668.


## IM Flutter SDK 3.5.6 @2021.11.25
- Fixed the `checkFriend` failure.
- Fixed the issue where `getC2CHistoryMessageList` API failed to get subsequent messages.

## IM Flutter SDK 3.5.5 @2021.11.23
- Adjusted the architecture.


## IM Flutter SDK 3.5.4 @2021.11.22
- Added the `downloadMergeMesasge` API.


## IM Flutter SDK 3.5.3 @2021.11.15
- Added the `onTotalUnreadMessageCountChanged` event.
- Added the `orderkey` field in the `V2TimConversation` API for conversation sorting.


## IM Flutter SDK 3.5.2 @2021.11.12
Added support for web.

## IM Flutter SDK 3.5.1 @2021.11.10
- Added the logic to be compatible with array index out of bounds.


## IM Flutter SDK 3.5.0 @2021.10.1
- Fixed several known issues.
- Added the following APIs:
 - callExperimentalAPI
 - clearC2CHistoryMessage
 - clearGroupHistoryMessage
 - searchLocalMessages
 - findMessages
 - searchGroups
 - searchGroupMembers
 - getSignalingInfo
 - addInvitedSignaling
 - searchFriends

## IM Flutter SDK 1.0.34 @2021.03.22
- Fixed the issue for iOS where getting the message history triggered an error.

## IM Flutter SDK 1.0.33 @2021.03.22
- Changed the `minSdkVersion` value of the SDK to 16.

## IM Flutter SDK 1.0.32 @2021.03.22
- Fixed the crash that occurred when `lastMessage` in the conversation information was empty.

## IM Flutter SDK 1.0.30-1.0.31 @2021.03.18
- Fixed the crash that occurred when the `data` field of a custom message was null.

## IM Flutter SDK 1.0.29 @2021.03.16
- [Important] Fixed the issue where passing in parameters for getting the group member list triggered an error.

## IM Flutter SDK 1.0.28 @2021.03.16
- [Important] Changed the input parameters of the `checkFriends` API.

## IM Flutter SDK 1.0.15-1.0.27 @2021.03.15
- Added the group member custom field.
- Improved iOS signaling.
- Fixed the iOS signaling bug.
- Added the feature of parsing a custom field into `string` before returning it.
- Optimized the settings of custom fields of the profile.
- Updated the `getHistoryMessageList` API for Android.
- Fixed the issue for Android where passing in parameters for the `checkFriend` API triggered an error.

## IM Flutter SDK 1.0.5-1.0.14 @2021.02.26
- Fixed the issue where passing in parameters for the `deleteFriendApplication` API triggered an error.
- Updated the Native SDK to v5.1.132.
- Updated the Native SDK to v5.1.137.
- Fixed the bug that occurred when passing in parameters for the signaling invitation API.
- Fixed the issue where the signaling API did not return an ID.
- Modified the SDK compression configuration.
- Fixed signaling callback bugs.
- Modified the return data of custom messages.
- [Important] Modified the format of content returned for a signaling message. Please upgrade to this version or later to use signaling.


## IM Flutter SDK 1.0.4 @2021.01.14

- Upgraded the SDK for Android to v5.1.129.
- Upgraded the SDK for iOS to v5.1.129.

## IM Flutter SDK 1.0.3 @2021.01.13
- Added support for Android and iOS platforms.
- Added support for one-to-one chat and group chat (discussion and audio-video groups).
- Added support for text, emoji, image, audio, and custom messages.
- Added support for offline push of APNs (reporting of token and foreground/background switch).
- Added the feature of storing messages locally.

## IM Flutter SDK 0.0.1-1.0.2 @2020.12.01
- Launched the Flutter SDK.
- Invited users to join the beta test.
