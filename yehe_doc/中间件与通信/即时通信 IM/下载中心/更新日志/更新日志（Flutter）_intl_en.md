## IM Flutter TUIKit 0.1.8 @2022.10.21
- Optimized file batch download queue,allowing to select multiple file messages in one click.
- Optimized group list widget which can be updated automatically.
- Optimized camara shooting to support low-performance devices and automatically adjust the resolution.
- Optimized support for customizing the color and text style of the app bar, especially on the TIMUIKitChat component.
- Fixed that friend notes or nicknames could not be displayed in group tips.
- Fixed video play error.
- Fixed several issues.

## IM Flutter SDK 4.1.8 @2022.10.18
- Added support for PC platforms, including macOS and Windows.
- Added message extension.
- Added signaling editor.
- Optimized and upgraded the underlying SDK.
- Fixed the problem of converting high version JDK.
- Fixed several issues.

## IM Flutter TUIKit 0.1.7 @2022.10.18
- Added support for large and RAW images, especially those captured from the latest versions of iOS and the iPhone 14 Pro series, compressed and formatted before automatic sending.
- Optimized performance and stability, especially history message list and initiation.
- Optimized initializing ' TIMUIKitChat ' as an idempotent operation.
- Optimized loading the latest news when scrolling back to the bottom.
- Optimized support for Flutter 2.x and 3.x series.
- Fixed permission support for iOS photo album, only allow some pictures, .
- Fixed several issues.

## IM Flutter TUIKit 0.1.5 @2022.09.22
- Added web support. Now you can implement TUIKit on iOS/Android/Web platforms.
- Added check disk storage after login, controlled in `config` of `init`
- Added `timeDividerConfig`, `notificationAndroidSound` Huawei Google push sound configuration, `isSupportMarkdown` whether the text message supports Markdown parsing, `onTapLink` in`TIMUIKitChatConfig`.
- Removed default Emoji list due to copyright issues. You can provide TUIKit with your own list of emoticons via [tim_ui_kit_sticker_plugin](https://pub.dev/packages/tim_ui_kit_sticker_plugin).
- Optimized disabling the display of @messages in the conversation list
- Optimized the return value of `notificationExt/notificationBody` as `null` in `TIMUIKitChatConfig` and `MessageItemBuilder`, and in specific cases can use default values ​​as needed, which means you can control whether to use automatic Define settings without redefining the same logic in code as TUIKit.
- Optimized to support multi-line text messages.
- Optimized the experience of `TIMUIKitChat`. Also, to use `TIMUIKitChatController`, you need to pass in `controler`, as showed in [tutorial](https://www.tencentcloud.com/en/document/product/1047/50054).

## IM Flutter SDK 4.1.3 @2022.09.21
- Solved some web issues.

## IM Flutter SDK 4.1.1+2 @2022.08.25
- Upgraded the underlying library version to 6.6.x.
- Full support for Flutter Web.

## IM Flutter SDK 4.1.0 @2022.08.09
- Upgraded the underlying library version.

## IM Flutter TUIKit 0.1.3 @2022.08.03
- Added user input status.
- Added the ability to respond to message emojis.
- Added user online status display.

## IM Flutter SDK 4.0.8 @2022.07.25
- Added an advanced interface for obtaining conversation list, which supports grouping and pulling session list by conversation type/tag.
- Added custom tag conversation interface.
- Added conversation grouping capability.
- Reduced Dart version dependency to 2.0.0.
- Supported Flutter multi-engine.
- Supported offline push sound effect configuration on Android.
- Supported custom user online status.
- Upgraded the underlying library version to 6.5.x.

## IM Flutter TUIKit 0.1.2 @2022.07.08
- Fixed the issue that the original referenced third-party underlying recording library `flutter_record_plugin_plus` could not be used.

## IM Flutter TUIKit 0.1.1 @2022.07.07
- Optimized image preview.
- Added LifeCycle hooks for each component.
- Added mute status in group chat page.
- Added ability to clicked and jump to the URL in the text message and the website information preview card.
- Added TUIKit layer global event callbacks, including message language that needs to be prompted / Flutter layer error report / IM API layer error report return, TUIKit no longer pops up information, you can customize the pop-up window according to the callback and prompt language.
- Refactored `TUIKitGroupProfile` group profile component and `TUIKitProfile` user profile component to simplify usage and super fast access.

## IM Flutter SDK 4.0.7 @2022.07.07
- Supported custom corner numbers in iOS.
- Optimized the group application logic.

## IM Flutter SDK 4.0.6 @2022.07.04
- Upgraded the underlying library version to 6.2.x.
- Fixed offline push info field.

## IM Flutter SDK 4.0.5 @2022.07.01
- Added user online status query
- Supported requesting a list of historical messages by message type.
- Supported rich text messages.

## IM Flutter TUIKit 0.1.0 @2022.06.10
- Added the atomic development capability of the `TIMUIKitChat` component, and you can assemble the chat page by yourself through various sub-components.
- Supported ability for message modifying and updating UI.
- Added group application approval page component.
- Added Traditional Chinese characters to international languages.
- Opened more custom component parameters.

## IM Flutter TUIKit 0.0.9 @2022.05.30
- Supported offline push, with the newly released [tim_ui_kit_push_plugin](https://pub.dev/packages/tim_ui_kit_push_plugin) push plugin
- Supported Flutter 3.0
- Optimized local preview of media messages.

## IM Flutter SDK 4.0.2 @2022.05.27
- Fixed local video path.

## IM Flutter SDK 4.0.1 @2022.05.23
- Added topic ability.
- Added message modifying.

## IM Flutter SDK 4.0.0 @2022.04.26
- Upgraded the underlying library version to 6.2.x.
- Fixed offline push info field.

## IM Flutter TUIKit 0.0.8 @2022.04.24
- Added group message read receipt.
- Added a small toolbar in the lower right corner of the chat area to support returning to the bottom/displaying the number of new messages/@message reminder.

## IM Flutter SDK 3.9.3 @2022.4.20
- Fixed the issue where the `boolValue` of a group muting tip was lost.
 - Added the `key(string)-boolValue(bool)` format in addition to the existing `key(string)-value(string)` in the callback for group information modification.
- Fixed the issue where the `nameCard` field of a conversation was not parsed by the instance.
- Added APIs for group message read receipts.
 - Added [sendMessageReadReceptes](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessageReadReceipts.html) to send a read receipt for a group message.
 - Added [getMessageReadReceptes](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/getMessageReadReceipts.html) to get the read receipt for a sent message.
 - Added [getgroupMessageReadMemeberList](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupMessageReadMemberList.html) to get the list of group members who have or have not read a sent group message.
- Improved the Flutter for web.

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
- Supported the Tencent Push Notification Service token for offline push configuration.


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
- Fixed the issue where there was no return for Android async registration events.
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
- [Important] Modified the format of content returned for a signaling message. Upgrade to this version or later to use signaling.


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
