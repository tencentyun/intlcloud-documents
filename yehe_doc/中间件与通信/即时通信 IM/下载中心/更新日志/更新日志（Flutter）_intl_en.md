## Platform Support

We are committed to building a set of Chat SDK and TUIKit for all Flutter platforms, allowing you to run one set of code across all platforms.

| Platform | No-UI SDK ([tencent_cloud_chat_sdk](https://pub.dev/packages/tencent_cloud_chat_sdk)) | TUIKit with UI and Basic Business Logic ([tencent_cloud_chat_uikit](https://pub.dev/packages/tencent_cloud_chat_uikit)) |
|---------|---------|---------|
| iOS | Supported by all versions | Supported by all versions |
| Android | Supported by all versions | Supported by all versions |
| [Web](https://intl.cloud.tencent.com/document/product/1047/45907) | Supported from v4.1.1+2 | Supported from v0.1.5 |
| [macOS](https://intl.cloud.tencent.com/document/product/1047/45907) | Supported from v4.1.8 | Will be supported soon |
| [Windows](https://intl.cloud.tencent.com/document/product/1047/45907) | Supported from v4.1.8 | Will be supported soon |
| [Hybrid development](https://tencentcloud.com/document/product/1047/51456) (Adding Flutter SDK to Existing Native Applications) | Supported from v5.0.0 | Supported from v1.0.0 |

>? For web, macOS, and Windows platforms, you need to perform a few extra steps for integration. For details, see [Support for the Flutter for Web](https://intl.cloud.tencent.com/document/product/1047/45907) and [Support for the Flutter for Desktop](https://intl.cloud.tencent.com/document/product/1047/45907).

## SDK Description

Chat Flutter SDK (Without UI Library) refers to the [tencent_cloud_chat_sdk](https://pub.dev/packages/tencent_cloud_chat_sdk) package, which includes only all Chat client APIs and callbacks.

Chat Flutter TUIKit (Including UI Library) refers to the [tencent_cloud_chat_uikit](https://pub.dev/packages/tencent_cloud_chat_uikit) package, which includes all UI components and business logic in addition to the items included in Chat Flutter SDK (Without UI Library).

>?Chat Flutter SDK (Without UI Library) has been migrated from [tencent_im_sdk_plugin](https://pub.dev/packages/tencent_im_sdk_plugin) to [tencent_cloud_chat_sdk](https://pub.dev/packages/tencent_cloud_chat_sdk), and TUIKit has been migrated from [tim_ui_kit](https://pub.dev/packages/tim_ui_kit) to [tencent_cloud_chat_uikit](https://pub.dev/packages/tencent_cloud_chat_uikit).
> The two original version packages will not be maintained in the future. If you are still using them, please upgrade to the latest versions as soon as possible.

## Update Logs

### Chat Flutter TUIKit (Including UI Library) 1.6.0 @2023.02.08

- Added `scrollToConversation` to `TIMUIKitConversationController`. You can now easily navigate to a specific conversation in the conversation list and move to the next unread conversation by double-clicking the tab bar. For more information, see our [demo source code](https://github.com/TencentCloud/chat-demo-flutter/blob/main/lib/src/conversation.dart).
- Optimized the performance of the historical message list while scrolling over a large distance.

### Chat Flutter TUIKit (Including UI Library) 1.5.0 @2023.02.02

- Added `defaultAvatarAssetPath` to the global configuration `TIMUIKitConfig` to define the default profile photo.
- Added support for Flutter 3.7.0.
- Fixed the `chatBgColor` configuration.

### Chat Flutter TUIKit (Including UI Library) 1.4.0 @2023.01.13

- Added the feature of translating the text in text messages and replied and quoted messages. To use the feature, you only need to long press the text and choose **Translate**. This feature can be enabled or disabled by the `showTranslation` parameter in `ToolTipsConfig`.
- Optimized the position of the window that pops up when text is long pressed.
- Optimized the keyboard pop-up event.

### Chat Flutter SDK (Without UI Library) 5.0.8 @2023.01.13

- Added the group counter capability: Ordinary groups and audio-video groups support meta counters. For details, see groupCounter related APIs.

### Chat Flutter TUIKit (Including UI Library) 1.3.0 @2023.01.11

- Fixed the failure to display the nickname of the new group owner in the group tip message after the group ownership is transferred.
- Removed the confirmation window that pops up before a file is opened.

### Chat Flutter TUIKit (Including UI Library) 1.2.0 @2023.01.06

- Fixed the failure to display the input box when the chat component is switched from recording to keyboard.
- Fixed the issue where, when a combined message is sent to multiple recipients, only the first recipient can receive the message.
- Optimized `MessageItemBuilder` so that it can be used to display the combined message page.

### Chat Flutter TUIKit (Including UI Library) 1.1.0 @2022.12.27

- Embedded the emoji plug-in in TUIKit by default. Now we support three types of emojis: Unicode emoji, small image emoji, and big image emoji. The emoji use methods have been optimized. For more information, see [here](https://www.tencentcloud.com/document/product/1047/52227).
- Optimized the topic feature to support more custom capabilities.
- Optimized the animation for the input area, keyboard, sticker panel, and "More" panel.
- Optimized: Emojis, including Unicode and small images, can be inserted to any position in text messages.
- Optimized: The profile photo in a profile can be previewed with a large image.
- Optimized: The user ID in a user profile can be copied.
- Optimized: Several UI details are added, including `TIMUIKitAddFriend`, `TIMUIKitAddGroup`, `TIMUIKitGroupProfile`, and `TIMUIKitProfile`.
- Optimized: `TIMUIKitGroupProfile` and `TIMUIKitProfile` support modifying content by modifying IDs.
- Optimized `TIMUIKitGroupChat` to display the loading animation when a user clicks the image/video download button.
- Fixed some errors.


### Chat Flutter SDK (Without UI Library) 5.0.6 @2022.11.29

- Fixed the iOS bundle version loss issue.
- Improvement: The underlying native SDK has been upgraded to 6.9.3557.

### Chat Flutter TUIKit (Including UI Library) 1.0.1 @2022.11.28

- Removed `groupTRTCTipsItemBuilder` from `MessageItemBuilder`. Please use `customMessageItemBuilder` instead.

### Chat Flutter TUIKit (Including UI Library) 1.0.0 @2022.11.23

- Supported adding the Flutter module to your existing applications, that is, hybrid development. For more information, see [here](https://www.tencentcloud.com/document/product/1047/51456).
- Supported customizing stickers and emojis. **The use methods have changed greatly. For more information, see [here](https://www.tencentcloud.com/document/product/1047/52227#.E8.A1.A8.E6.83.85.E6.8F.92.E4.BB.B6.E5.8D.87.E7.BA.A7.E6.8C.87.E5.8D.97).**
- Supported adding the Flutter module to your existing applications, that is, hybrid development. For more information, see [here](https://www.tencentcloud.com/document/product/1047/51456).
- Supported customizing stickers and emojis. **The use methods have changed greatly. For more information, see [here](https://www.tencentcloud.com/document/product/1047/52227#.E8.A1.A8.E6.83.85.E6.8F.92.E4.BB.B6.E5.8D.87.E7.BA.A7.E6.8C.87.E5.8D.97).**
- Optimized the loading time of the historical message list, especially when there are a large number of media and file messages.
- Supported scrolling in more panel areas.
- Optimized the feature of loading the latest messages when scrolling back to the bottom for smoother loading.
- Fixed the Android album image quantity issue.
- Fixed the border crossing issue of long text in the group profile card.
- Fixed some errors.

>?If you upgrade your TUIKit to this version, pay special attention to the changes of the emoji part (the second update item) and audio/video call part (the last but one update item). Otherwise, related capabilities will not work properly.
> If you have any questions in the process of modification, feel free to contact us.

### Chat Flutter SDK (Without UI Library) 5.0.4 @2022.11.23

- Multimedia message online URLs will no longer be returned by default. They need to be obtained by calling the `getMessageOnlineUrl` API.
- Multimedia message local URLs (`localurl`) will no longer be returned by default. They will be returned only after you download messages successfully by calling the `downloadMessage` API.
- The `onMessageDownloadProgressCallback` callback is added for `advanceMessageListener` and will be triggered when the multimedia message download progress is updated.
- Added the `disableBadgeNumber` method to iOS clients. After the method is called, the application badge is not set by default when the application is switched to the background.
- Supported adding the Flutter module to your existing applications, that is, hybrid development. For more information, see [here](https://www.tencentcloud.com/document/product/1047/51456).
- Optimized the underlying dynamic library download logic for PC clients.
- Upgraded the underlying SDK version to 6.8.
- Reconstructed the web client underlying SDK. You need to import the corresponding JS via npm as instructed [here](https://intl.cloud.tencent.com/document/product/1047/45907).
- Reconstructed the macOS client underlying SDK. You need to import the SDK as instructed [here](https://intl.cloud.tencent.com/document/product/1047/45907).

>?Major changes have been made to multimedia messages and file messages. Please modify your existing logic for obtaining and rendering such messages according to the first four updates. Otherwise, the messages will not be displayed.
> If you have any questions in the process of modification, feel free to contact us.

### Chat Flutter TUIKit (Including UI Library) 0.1.8 @2022.10.21

- Optimized the file batch download queue to allow a user to select multiple file messages at a time.
- Optimized the group list widget to support automatic update.
- Optimized camera shooting to support low-performance devices and automatically adjust the resolution for the devices.
- Optimized the support for customizing the color and text styles of the app bar, especially on the `TIMUIKitChat` component.
- Fixed the issue where friend notes or nicknames could not be displayed in group tips.
- Fixed video playback errors.
- Fixed several issues.

### Chat Flutter SDK (Without UI Library) 4.1.8 @2022.10.18

- Added support for PC platforms, including macOS and Windows.
- Added message extensions.
- Added signaling editing.
- Upgraded the underlying SDK.
- Fixed the later-version JDK conversion issue.
- Fixed several issues.

### Chat Flutter TUIKit (Including UI Library) 0.1.7 @2022.10.18

- Added support for large and RAW images, especially those captured from the latest versions of iOS and the iPhone 14 Pro series, compressed and formatted before automatic sending.
- Optimized performance and stability, especially the historical message list and startup.
- Optimized the initialization of `TIMUIKitChat` as an idempotent operation.
- Supported loading the latest messages when scrolling back to the bottom.
- Optimized support for Flutter 2.x and 3.x series.
- Permission support for iOS album: allowing only certain images.
- Fixed several issues.

### Chat Flutter TUIKit (Including UI Library) 0.1.5 @2022.09.22

- Added web support. Now you can implement TUIKit on iOS/Android/Web platforms.
- Added the feature of checking disk storage after login, which can be configured in `config` in `init`.
- Added the following attributes to `TIMUIKitChatConfig`: `timeDividerConfig`, `notificationAndroidSound` (Huawei and Google push sound configuration), `isSupportMarkdown` (whether text messages support Markdown parsing), and `onTapLink`.
- Removed the default emoji list due to copyright issues. You can provide TUIKit with your own emoji list via [tim_ui_kit_sticker_plugin](https://pub.dev/packages/tim_ui_kit_sticker_plugin).
- Optimized: Now you can disable the display of @ messages in the conversation list
- Optimized: Now you can set the return values of `notificationExt` and `notificationBody` in `TIMUIKitChatConfig` and `MessageItemBuilder` as `null`, and, in specific cases, you can use the default values ​​as needed. This means you can control whether to use custom settings without redefining the same logic as TUIKit in code.
- Optimized: Supported multi-line text messages.
- Optimized the experience of `TIMUIKitChat`. In addition, to use `TIMUIKitChatController`, you need to pass in `controler`, as described [here](https://intl.cloud.tencent.com/document/product/1047/50054).

### Chat Flutter SDK (Without UI Library) 4.1.3 @2022.09.21

- Fixed some web issues.

### Chat Flutter SDK (Without UI Library) 4.1.1+2 @2022.08.25

- Upgraded the underlying library version to 6.6.x.
- Full support for Chat Flutter SDK for web.

### Chat Flutter SDK (Without UI Library) 4.1.0 @2022.08.09

- Upgraded the underlying library version.

### Chat Flutter TUIKit (Including UI Library) 0.1.3 @2022.08.03

- Added user input status.
- Added the capability to respond to message emojis.
- Added the display of user online status.

### Chat Flutter SDK (Without UI Library) 4.0.8 @2022.07.25

- Added an advanced API for getting the conversation list, which supports pulling the conversation list by conversation type/tag.
- Added an API for customizing conversation marks.
- Added the conversation grouping capability.
- Decreased the dependent Dart version to 2.0.0.
- Supported multi-engine Flutter.
- Supported offline push sound effect configuration on Android.
- Supported custom user online status.
- Upgraded the underlying library version to 6.5.x.

### Chat Flutter TUIKit (Including UI Library) 0.1.2 @2022.07.08

- Fixed the issue where the original referenced third-party underlying recording library `flutter_record_plugin_plus` could not be used.

### Chat Flutter TUIKit (Including UI Library) 0.1.1 @2022.07.07

- Optimized the image preview logic.
- Added lifecycle hooks for each component.
- Added the mute status to group chat page.
- Supported redirection upon clicking URLs in text messages and added the website information preview card.
- Added TUIKit layer global event callbacks, including callbacks for messages that need to be prompted, Flutter layer errors, and Chat API layer errors. TUIKit no longer provides message pop-ups. You can customize pop-up windows based on callbacks and prompts.
- Reconstructed the group profile component `TUIKitGroupProfile` and user profile component `TUIKitProfile`, simplifying usage and enabling super-fast access.

### Chat Flutter SDK (Without UI Library) 4.0.7 @2022.07.07

- Supported custom badge numbers in iOS.
- Optimized the group joining request logic.

### Chat Flutter SDK (Without UI Library) 4.0.6 @2022.07.04

- Upgraded the underlying library version to 6.2.x.
- Fixed offline push information fields.

### Chat Flutter SDK (Without UI Library) 4.0.5 @2022.07.01

- Added user online status query.
- Supported requesting historical messages by message type.
- Supported sending rich text messages.

### Chat Flutter TUIKit (Including UI Library) 0.1.0 @2022.06.10

- Added the atomic development capability of the `TIMUIKitChat` component, and you can assemble the chat page by yourself through various sub-components.
- Supported the capability to edit messages and update UIs.
- Added group joining request approval page components.
- Added Traditional Chinese as a language option.
- Opened up more custom component parameters.

### Chat Flutter TUIKit (Including UI Library) 0.0.9 @2022.05.30

- Supported offline push, with the newly released [tim_ui_kit_push_plugin](https://pub.dev/packages/tim_ui_kit_push_plugin) push plugin.
- Supported Flutter 3.0.
- Optimized the local preview of media messages.

### Chat Flutter SDK (Without UI Library) 4.0.2 @2022.05.27

- Fixed the local video path issue.

### Chat Flutter SDK (Without UI Library) 4.0.1 @2022.05.23

- Added the topic capability.
- Added the message editing capability.

### Chat Flutter SDK (Without UI Library) 4.0.0 @2022.04.26

- Upgraded the underlying library version to 6.2.x.
- Fixed offline push information fields.

### Chat Flutter TUIKit (Including UI Library) 0.0.8 @2022.04.24

- Added the group message read receipt capability.
- Added a small toolbar in the lower right corner of the chat area to support returning to the bottom/displaying the number of new messages/@message reminder.

### Chat Flutter SDK (Without UI Library) 3.9.3 @2022.04.20

- Fixed the issue where the `boolValue` of a group muting tip was lost.
- Added the `key(string)-boolValue(bool)` format in addition to the existing `key(string)-value(string)` in the callback for group information modification.
- Fixed the issue where the `nameCard` field of a conversation was not parsed by the instance.
- Added APIs for group message read receipts.
- [sendMessageReadReceptes](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessageReadReceipts.html): Sends group message read receipts.
- [getMessageReadReceptes](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getMessageReadReceipts.html): Gets read receipts for messages sent by yourself.
- [getgroupMessageReadMemeberList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupMessageReadMemberList.html): Gets the list of members who have (or have not) read a message sent by yourself.
- Improved the Flutter for web.

### Chat Flutter TUIKit (Including UI Library) 0.0.7 @2022.04.13

- Optimized experience.

### Chat Flutter TUIKit (Including UI Library) 0.0.6 @2022.04.08

- Opened up the API for automatically displaying sent messages on the screen and provided more custom capability parameters.
- Optimized user login authentication.
- Optimized privacy policies to better align with personal information protection laws.

### Chat Flutter TUIKit (Including UI Library) 0.0.5 @2022.03.24

- Opened up more custom capabilities of the chat area component `TIMUIKitChat`.

### Chat Flutter SDK (Without UI Library) 3.9.1 @2022.03.24

- Upgraded the underlying library to v6.1.2155.

### Chat Flutter SDK (Without UI Library) 3.9.0 @2022.03.22

- Modified GroupListener.

### Chat Flutter SDK (Without UI Library) 3.8.9 @2022.03.18

- Fixed the registration result listening issue.

### Chat Flutter TUIKit (Including UI Library) 0.0.4 @2022.03.17

- Added support for sending images and videos.
- Optimized topic styles.
- Optimized the search component.

### Chat Flutter TUIKit (Including UI Library) 0.0.3 @2022.03.14

- Optimized component details.
- Improved the automatic internationalization capability.
- Added the global search component `TIMUIKitSearch`.
- Added the in-conversation search component `TIMUIKitSearchMsgDetail`.
- Added the friend adding component `TIMUIKitAddFriend`.
- Added the group joining component `TIMUIKitAddGroup`.
- Added topic styles.

### Chat Flutter SDK (Without UI Library) 3.8.4 @2022.03.14

- Updated APIs.

### Chat Flutter TUIKit (Including UI Library) 0.0.2 @2022.03.02

- Optimized the `TIMUIKitChat` component.
- Supported automatic and manual switching between Simplified Chinese and English.

### Chat Flutter TUIKit (Including UI Library) 0.0.1 @2022.03.01

- Launched Tencent Cloud Chat for Flutter (including the UI library and business logic).
- Released the first seven main components, including the chat area, conversation list, contact and group profiles, contacts list, blocklist, and friend request list.

### Chat Flutter SDK (Without UI Library) 3.8.3 @2022.03.01

- Switched the token encoding format based on the environment.

### Chat Flutter SDK (Without UI Library) 3.8.2 @2022.02.21

- Updated group member parameter constraints.

### Chat Flutter SDK (Without UI Library) 3.8.0 @2022.02.17

- Upgraded the underlying API dependencies.

### Chat Flutter SDK (Without UI Library) 3.7.8 @2022.02.15

- Fixed the exception caused by force unwrapping.

### Chat Flutter SDK (Without UI Library) 3.7.7 @2022.02.10

- Fixed the Swift code warning.
- Rewrote Swift's force unwrapping code.
- Added the `id` field to the `message` instance returned by the `sendMessage` API.

### Chat Flutter SDK (Without UI Library) 3.7.5 @2022.01.23

- Upgraded the underlying library to v6.0.1975.
- Supported the TPNS token for offline push configuration.

### Chat Flutter SDK (Without UI Library) 3.7.1 @2022.01.12

- Added the feature of returning the message creation ID for a message sending progress event.
- Optimized the callback by reminding the business side that the callback error is caught in SDK and needs to be modified.

### Chat Flutter SDK (Without UI Library) 3.7.0 @2022.01.10

- Optimized the unpacking of cloudCustomData.

### Chat Flutter SDK (Without UI Library) 3.6.9 @2022.01.06

- Optimized the message reply parameters.

### Chat Flutter SDK (Without UI Library) 3.6.8 @2022.01.06

- Optimized the message reply API.

### Chat Flutter SDK (Without UI Library) 3.6.7 @2022.01.05

- Upgraded the compiling environment for iOS from 8.0 to 9.0.

### Chat Flutter SDK (Without UI Library) 3.6.6 @2021.12.30

- Added the message reply API.
- Fixed the issue for web where the release mode triggered an error.

### Chat Flutter SDK (Without UI Library) 3.6.5 @2021.12.17

- Fixed syntax errors in Java.

### Chat Flutter SDK (Without UI Library) 3.6.4 @2021.12.17

- Fixed the issue where there was no return for Android async registration events.
- Fixed the issue where removing a general listening event triggered an error.
- Added the UUID of a message being sent in its progress event.

### Chat Flutter SDK (Without UI Library) 3.6.3 @2021.12.9

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

### Chat Flutter SDK (Without UI Library) 3.6.2 @2021.12.9

- Fixed the issue where no uuid was passed in for removing an advanced message.

### Chat Flutter SDK (Without UI Library) 3.6.1 @2021.12.8

- Fixed the loss of the file progress event.

### Chat Flutter SDK (Without UI Library) 3.6.0 @2021.12.1

- Added the support for multiple listener registrations and callbacks in modules.
- Added the `markAllMessageAsRead` API for marking all messages as read.
- Added the feature of parsing combined messages.
- Upgraded the Native SDK to v5.8.1668.

### Chat Flutter SDK (Without UI Library) 3.5.6 @2021.11.25

- Fixed the `checkFriend` failure.
- Fixed the issue where `getC2CHistoryMessageList` API failed to get subsequent messages.

### Chat Flutter SDK (Without UI Library) 3.5.5 @2021.11.23

- Adjusted the architecture.

### Chat Flutter SDK (Without UI Library) 3.5.4 @2021.11.22

- Added the `downloadMergeMesasge` API.

### Chat Flutter SDK (Without UI Library) 3.5.3 @2021.11.15

- Added the `onTotalUnreadMessageCountChanged` event.
- Added the `orderkey` field in the `V2TimConversation` API for conversation sorting.

### Chat Flutter SDK (Without UI Library) 3.5.2 @2021.11.12

Added support for web.

### Chat Flutter SDK (Without UI Library) 3.5.1 @2021.11.10

- Added the logic to be compatible with array index out of bounds.

### Chat Flutter SDK (Without UI Library) 3.5.0 @2021.10.1

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

### Chat Flutter SDK (Without UI Library) 1.0.34 @2021.03.22

- Fixed the issue for iOS where getting the message history triggered an error.

### Chat Flutter SDK (Without UI Library) 1.0.33 @2021.03.22

- Changed the `minSdkVersion` value of the SDK to 16.

### Chat Flutter SDK (Without UI Library) 1.0.32 @2021.03.22

- Fixed the crash that occurred when `lastMessage` in the conversation information was empty.

### Chat Flutter SDK (Without UI Library) 1.0.30-1.0.31 @2021.03.18

- Fixed the crash that occurred when the `data` field of a custom message was null.

### Chat Flutter SDK (Without UI Library) 1.0.29 @2021.03.16

- [Important] Fixed the issue where passing in parameters for getting the group member list triggered an error.

### Chat Flutter SDK (Without UI Library) 1.0.28 @2021.03.16

- [Important] Changed the input parameters of the `checkFriends` API.

### Chat Flutter SDK (Without UI Library) 1.0.15-1.0.27 @2021.03.15

- Added the group member custom field.
- Improved iOS signaling.
- Fixed the iOS signaling bug.
- Added the feature of parsing a custom field into `string` before returning it.
- Optimized the settings of custom fields of the profile.
- Updated the `getHistoryMessageList` API for Android.
- Fixed the issue for Android where passing in parameters for the `checkFriend` API triggered an error.

### Chat Flutter SDK (Without UI Library) 1.0.5-1.0.14 @2021.02.26

- Fixed the issue where passing in parameters for the `deleteFriendApplication` API triggered an error.
- Updated the Native SDK to v5.1.132.
- Updated the Native SDK to v5.1.137.
- Fixed the bug that occurred when passing in parameters for the signaling invitation API.
- Fixed the issue where the signaling API did not return an ID.
- Modified the SDK compression configuration.
- Fixed signaling callback bugs.
- Modified the return data of custom messages.
- [Important] Modified the format of content returned for a signaling message. Please upgrade to this version or later to use signaling.

### Chat Flutter SDK (Without UI Library) 1.0.4 @2021.01.14

- Upgraded the SDK for Android to v5.1.129.
- Upgraded the SDK for iOS to v5.1.129.

### Chat Flutter SDK (Without UI Library) 1.0.3 @2021.01.13

- Added support for Android and iOS platforms.
- Added support for one-to-one chat and group chat (discussion and audio-video groups).
- Added support for text, emoji, image, audio, and custom messages.
- Added support for offline push of APNs (reporting of token and foreground/background switch).
- Added the feature of storing messages locally.

### Chat Flutter SDK (Without UI Library) 0.0.1-1.0.2 @2020.12.01

- Launched the Flutter SDK.
- Invited users to join the beta test.
