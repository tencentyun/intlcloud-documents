## Latest Version 4.8.50 @2020.06.22

### SDK

**Common changes**

- Fixed an issue with API 2.0 where the onMemberEnter callback would not be called when a user entered a live streaming group (AVChatRoom).
- Added the groupID parameter to the onGroupInfoChanged and onMemberInfoChanged callbacks of API 2.0.
- Fixed the issue where the update conversation callback would not be called after C2C messages were sent.
- Fixed the issue where messages would not be received after switching accounts to join the same live streaming group (AVChatRoom).
- Fixed an occasional error with incorrect callback sequences when synchronizing unread messages after login.
- Added signaling API.
- Added the group custom property API to live streaming groups (AVChatRoom).
- Fixed known crashes.

**Android platform**

The default log storage location is changed to /sdcard/Android/data/package-name/files/log/tencent/imsdk for compatibility with Android Q version.

**Windows platform**

Fixed issue with group member roles.

### TUIKit and demo

**iOS platform**

- TUIKit now uses API 2.0.
- Audio/Video call feature is now available based on TRTC integration.
- Dark mode is now available.

**Android platform**
- TUIKit now uses API 2.0.
- Audio/Video call feature is now available based on TRTC integration.
- AndroidX is now supported.


## 4.8.10 @2020.05.15

### SDK

**Common changes**

- iOS and Android now support IPv6.
- Live streaming groups (AVChatRoom) now support the dynamic update of the group member list.
- Fixed xlog crash issue.

**iOS and Mac platforms**

- Fixed iOS issue where large files always failed to send.
- Fixed an iOS exception that occurred when messages pulled remarks.

**Android platform**

- The IM SDK now supports AndroidX.
- Fixed Android device crashes caused by network permission issues.

## 4.8.1 @2020.04.30

### SDK

**Common changes**

- API 2.0 is now available for iOS and Android.
- Fixed conversation confusion that occurred when logging in to different accounts in some cases.

## 4.7.10 @2020.04.23

### SDK

**Common changes**

- Fixed login timeout in some network environments.
- Fixed inaccurate unread counts in some scenarios.

## 4.7.2 @2020.04.03

### SDK

**Common changes**

Revised a data error.

## 4.7.1 @2020.03.23

### SDK

**Common changes**

- Optimized the local log size.
- Optimized the login time.
- Fixed the multi-terminal unread count synchronization issue.
- Added the getFriendList API.
- The iOS and Android SDKs enable you to set the message title and content to display on the offline push notifications bar of iOS and Android devices, respectively.</li>

## 4.6.102 @2020.02.28

### SDK

**Common changes**

- Fixed slow message pulling in some scenarios.
- Fixed the compatibility issue with sending 3.x version audio messages to later versions.
- Fixed the issue where the identifiers of some conversions in the obtained conversion list were null.
- Fixed known crashes.
- Fixed Socks5 proxy users' password verification issue.
- Optimized the pending group processing logic.
- Improved the file upload limit to 100 MB.
- Optimized COS upload.
- Fixed the issue where an exception was returned for obtaining the friend list if there was no friend.


## 4.6.56 @2020.01.08

### SDK

**Common changes**

- Mitigated the issue where memory grew when user profiles were frequently pulled.
- Improved compatibility with special characters in user profiles.
- Fixed known crashes.
- Fixed occasional login failures when accounts are switched frequently.
- Fixed reconnection in the pressure test.


## 4.6.51 @2019.12.23

### SDK

**Common changes**

- Improved network connection quality to quickly detect network quality changes.
- Optimized audio-video chat room message handling.

**iOS and Mac platforms**

- Changed all IMSDK listeners from strong references to weak references of external objects.
- Added the getSenderNickname API for messages.

**Android platform**

- Fixed the issue where offline users are kicked off.
- Fixed exceptional upload progress callback on devices running earlier Android versions.
- Fixed memory leak during login.
- Added the getSenderNickname API for messages.

**Windows platform**

- Fixed the issue where messages failed to be sent to newly added friends.
- Improved modification and query of custom fields for group information and group member information.
- Improved callbacks for all APIs to ensure that callbacks will be called and that objects are transferred to JSON strings only when callbacks succeed and empty strings are returned when callbacks fail.

### TUIKit and demo

**Android platform**

- Profile photos displayed in conversation lists can be set with rounded corners.
- Fixed the issue where account switching is exceptional when a conversation is pinned to the top.


## 4.6.1 @2019.11.13

### SDK

**Common changes**

- Roaming messages can be recalled.
- Fixed the unread count error when a user was invited to join a group in silent mode through a RESTful API.
- Fixed occasional message sending exceptions due to poor network connection.
- Fixed incorrect logic for role filtering conditions when group members are obtained.
- Fixed the issue where the SDK failed to get the group name the first time users sent a message in a group created by a RESTful API.
- Fixed the issue where getUsersProfile failed to get user information after caching was disabled.
- Fixed the issue where voice message files without a suffix could not be downloaded after they were received.

**iOS and Mac platforms**

- Added OPPOChannelID settings to fix the issue where OPPO mobile phones running Android 8.0 or later failed to receive iOS push messages.
- Optimized annotations to getGrouplist return objects.

**Android platform**

- Offline pushed channelID on OPPO mobile phones running Android 8.0 or later can be configured in the console.
- The ext, sound, and desc fields of TIMCustomElem have been deprecated.

**Windows platform**

- Fixed the exceptional type field of group system messages.
- Fixed inconsistent group type and header file in the returned group information.
- Fixed the issue where specifying custom group fields failed during group creation.
- Added sender profile and offline push configuration to messages.

### TUIKit and demo

**iOS platform**

- Added the video call feature.
- Added 3X3 grid display of group profile photos.
- Optimized the conversation list, contacts, and chat interface UIs.

**Android platform**

- Added a method to set whether to display read receipts.
- Added 3X3 grid display of group profile photos.
- Optimized the conversation list, contacts, and chat interface UIs.
- Fixed compatibility issues with the input method, UI, and file selection for some mobile phones.
- Fixed messy display of custom messages.
- Fixed slow contact loading in the stress test.
- Fixed the conflicts with other library resources.
- Fixed ineffective cache directory settings.

## 4.5.111 @2019.10.16

### SDK

**Common changes**

- Fixed the paging issue of the API used to get the list of group members of a specified type.
- Added file format extension to the URL generated upon sending a file message.
- Added the notification callback after custom group fields are modified.
- Local user and group information can be obtained before login by calling the initStorage method.
- Fixed the memory leak issue.
- Fixed the issue with incorrect message status codes after sent messages are recalled.
- Fixed the issue with incorrect getMessage callback error codes.
- Fixed incorrect one-to-one chat unread count after an app is killed and restarted.

**iOS and Mac platforms**

  Fixed occasional login failures for sleeping Mac devices.

**Android platform**

- Fixed stability issues in some scenarios.
- Fixed the issue where OPPO mobile phones running Android 8.0 or later could not receive offline push notifications.
- Optimized the return types of the getElementCount API.

**Windows platform**

- Improved the network reconnection speed for cross platform libraries.
- Fixed the Windows public group management setting failure.
- Added JVM configuration to cross-platform libraries to facilitate passing jvm from an Android environment.

### TUIKit and demo

**iOS platform**

- Supported sending and receiving voice messages to and from web applications.
- Fixed the issue where TUIKit resource files could not be found when swift loading.
- Fixed the issue where a friend' alias could not be seen on the chat interface after it was modified.
- Fixed the issue where the conversation list did not refresh promptly after a conversation was pinned to the top.

**Android platform**

- Supported sending and receiving voice messages to and from web applications.
- Supported setting the input box style.
- Displayed a red dot on unread voice messages.
- Fixed the issue where video messages could not be played on x86 devices.
- Fixed conflicts between FileProvider and the integration side.
- Fixed the issue where audio permissions could not be identified on some mobile phone models.
- Fixed the issue where the profile photo cannot be loaded in specific conditions.
- Fixed occasional incomplete display of bubbles.

## 4.5.55 @2019.10.10

### SDK

**Common changes**

- Fixed crashes when networks are switched multiple times.
- Improved network connection quality.
- Optimized annotations of some APIs.

**Android platform**

Optimized HTTP request restrictions on Android 9.0 or later.

**iOS and Mac platforms**

Optimized pod integration.


## 4.5.45 @2019.09.18

### SDK

**Common changes**

- Improved network connection quality.
- Fixed the exceptional unread count when new messages are received after a group chat is deleted.
- Fixed the issue where deleted conversations could still be obtained from the conversation update callback. 
- Optimized the logic for pulling custom group/group member fields.

**Android platform**

Deprecated the setOfflinePushListener API and TIMOfflinePushNotification class in TIMManager.

### TUIKit and demo

**iOS platform**

- Fixed the NSSting + Common.h class conflict issue.
- Fixed the incomplete group tip display issue.

**Android platform**

- Added read receipts.
- Compatible with typing display in earlier versions.
- Fixed the issue where resent messages failed to immediately appear in the bottom of the chat window.
- Fixed the issue where profile photos in a group chat failed to be displayed under specific conditions.
- Fixed the issue where multi-element group messages could not be displayed.
- Fixed crashes caused by specific messages.
- Fixed the group admin permission error.
- Fixed the issue where files sent by web applications could not be received.

## 4.5.15 @2019.08.30

### SDK

**Common changes**

- Improved the speed of sending file messages from users outside China.
- Fixed the issue where the message status fetched by getLastMessage was incorrect after a message was recalled. Fixed the issue where the callback is called multiple times after message listening was recalled.
- Fixed the issue where the backend failed to obtain the muting time after a member is muted, quit the group, and joined the group again.
- Fixed the issue where the msg time was ineffective at savemsg after the msg time was proactively modified.
- Fixed the issue where no callback occurred occasionally upon login.
- Fixed the issue where rand and timestamp of a recalled group message are empty.
- Fixed the issue where UserSig in a callback expires when the user was logged out. Fixed the issue where reconnection continued when the user was logged out.

**Android platform**

- Supported FCM push notifications on Android devices in the backend.
- Fixed the issue where an error was reported when null was passed for getting a specified friend list.
- Fixed checkEquals crashes in specified scenarios.

**Windows platform**

- Added the unique_id field to MessageLocator.
- Supported 64-bit Windows.
- Added user profile APIs and relationship chain APIs to the cross-platform library.

### TUIKit and demo

**iOS platform**

- Supported sending custom messages.
- Added C2C read receipts.
- Added a red dot to audio messages that have not been played.

**Android platform**

- Fixed the demo memory leak issue in some scenarios.
- Fixed crashes in some scenarios.
- Fixed the incorrect custom message color issue.
- Fixed the incorrect or incomplete bubble display issue.
- Fixed the issue where conversation lists failed to display profile photos.
- Fixed the issue where the title bar color could not be changed by ConversationLayout.
- Supported 64-bit ijkplayer.
- Supported multi-element messages.

## 4.4.900 @2019.08.07

### SDK
**Common changes**

 - Fixed stability issues in some scenarios.
 - Optimized the unread message count.
 - Improved the latest conversation list loading speed after login.
 - Added the log cleaning feature.
 - Fixed message loss when synchronizing a large number of unread C2C messages.
 - After a user leaves an audio-video chat room, system messages about members quitting the group will not be pushed to the user's device.
 - Fixed the issue where group system messages occasionally failed to be delivered to users.
 - Added the frequency limit logic to onRefresh/onRefreshConversations.
 - Optimized exceptional saveMessage ordering.

**iOS and Mac platforms**

  - Changed the getGroupInfo callback parameter to TIMGroupInfoResult to fetch the error codes corresponding to each group.
  - Optimized the display style of push notifications for 4.x versions to keep consistency with 2.x and 3.x versions.
  - Fixed the issue where login accounts that contain Chinese characters failed to send images, files, and videos.

**Android platform**

  - Fixed the issue where mobile phones running the 4.2.2 system version failed to load so.
  - Fixed the issue where getGroupInfo returns an incorrect amount of data.
  - Changed the getGroupInfo callback parameter to TIMGroupDetailInfoResult to fetch the error codes corresponding to each group.
  - Used the com.tencent.imsdk.TIMGroupReceiveMessageOpt class in a unified manner.

**Windows platform**

  Fixed the issue where the Windows configuration file path is garbled.


### TUIKit and demo

**iOS platform**
  - Modified the iOS demo UI, including the default profile photo and four feature icons (camera, video, album, and file) on the input interface.
  - Added the profile card to "Me" and put personal information in the profile card.
  - Added the feature to view the large image by tapping the profile photo.
  - Modified the style of the small gray bar in group chats in the demo so that the member nickname becomes blue and tapping the nickname will redirect the member to the member's profile page.
  - Optimized the logic for displaying nicknames in groups in the demo.
  - Optimized the logic for displaying profile photos on the chat interface.
  - Added tap feedback to all interfaces, allowing users to set and customize feedback in TUIKit.

**Android platform**

  - Added MotionEvent.ACTION_CANCEL event handling for audio messages in chats.
  - Added profile photo display in the conversation list, chat interface, detailed profile, and contacts.
  - Added profile photo change in user profiles.
  - Added Intent redirection to offline push functions.
  - Added random profile photos for one-to-one chats and group chats.
  - Added prompts for granting and revoking the group admin role for a group member.
  - Added prompts for muting and unmuting group members.
  - Fixed the issue where the text "You've recalled a message" was not displayed in tips after a message was recalled.
  - Fixed the issue where the content of a recalled message was always displayed as the last message in the conversation list.
  - Fixed the white screen issue on the chat interface after offline messages were received on MEIZU mobile phones.
  - Fixed the issue where the chat conversation pinned to the top did not update to the last message when new messages came in.
  - Fixed Toast notifications when the username or password is empty.
  - Fixed the issue where GroupTips messages transferred from the group owner were displayed abnormally in TUIKit.
  - Fixed the Didn't find class "android.support.v4.content.FileProvider" error reported on some mobile phones.
  - Optimized the logic for pinning a chat to the top to arrange chats in chronological order starting from the most recent.
  - Fixed the issue where the soft keyboard and other layouts appeared in chats at the same time.
  - Fixed the issue where the Group Chats, Blocklist, and New Contacts items were not displayed on the Contacts interface when a user is newly registered with no contacts.
  - Fixed the issue where the video sound continued to play after a user taps the Back button on a mobile phone.
  - Fixed the issue where the playing voice message did not stop and its sound was also recorded during voice message recording.
  - Fixed the issue where videos sent by iOS devices failed to playback on some mobile phones.


## 4.4.716 @2019.07.16


**iOS and Mac platforms**

- Organized and merged APIs.
- Added APIs to get the download URLs of file, video, and voice messages.
- Added the disableStorage API to disable all local storage.
- Fixed the issue where the conversation on the sender's device could still get lastMsg after an online message was sent.
- Removed the return value of getSenderProfile, and used callback instead.
- Changed the group function modifyReciveMessageOpt to modifyReceiveMessageOpt.
- Fixed the issue where video screenshots sent from a device running iOS 2.X or 3.X to a device running iOS 4.X could not be obtained.
- Fixed occasional crashes when data was reported upon exit.
- Optimized the login module (repeated login/frequent login/frequent account switching/automatic connection/offline user being kicked off).
- Fixed the issue where the unread count could not be cleared after a member quit a group or a group was disbanded.
- Fixed the issue where group disband notifications could not be received occasionally.
- Fixed the issue where longer time was required to deliver messages when the app went to foreground after staying in background for a long time.
- Optimized the one-to-one chat unread count.
- Changed the input parameter TIMLoginParam of autoLogin to userID.
- Changed the input parameter TIMLoginParam of initStorage to userID.
- Removed multi-account login APIs: newManager, getManager, and deleteManager.
- Fixed occasional respondsToLocator crashes. 
- Fixed occasional crashes caused by TIMGroupInfo -> lastMsg calling related functions.
- TUIKit
  - Optimized the recent contact list update algorithm to reduce the refresh frequency.
  - Fixed blocklist memory leak.
  - Added message bubble and profile photo click event callbacks.
  - Fixed the issue where the latest profile photo was not displayed in recent contacts or the chat window.
  - Optimized document annotations.

**Android platform**

- Organized and merged APIs.
  - Added all APIs in TIMManagerExt to TIMManager.
  - Added all APIs in TIMConversationExt to TIMConversation.
  - Added all APIs in TIMGroupManagerExt to TIMGroupManager.
  - Added all APIs in TIMMessageExt to TIMMessage.
  - Added all APIs in TIMUserConfigMsgExt to TIMUserConfig.
  - Retained APIs in TIMManagerExt, TIMMessageExt, TIMConversationExt, TIMGroupManagerExt, and TIMUserConfigMsgExt classes provisionally for compatibility purposes, which will be deprecated in the future.
- Added options to add friends in one-way or two-way manner. 
- Added the disableStorage API to disable all local storage.
- Added APIs to get the download URLs of file, video, and voice messages.
- Fixed the issue where queryUserProfile was null on some Android mobile phones.
- Fixed the issue where the conversation on the sender's device could still get lastMsg after an online message was sent.
- Removed the return value of getSenderProfile, and used callback instead.
- Fixed occasional crashes when data was reported upon exit.
- Optimized the login module (repeated login/frequent login/frequent account switching/automatic connection/offline user being kicked off).
- Fixed the issue where the unread count could not be cleared after a member quit a group or a group was disbanded.
- Fixed the issue where group disband notifications could not be received occasionally.
- Fixed the issue where longer time was required to deliver messages when the app went to foreground after staying in background for a long time.
- Optimized the one-to-one chat unread count.
- TUIKit
  - Short video messages in chats can be played in landscape orientation or portrait orientation.
  - Supported Javadoc documentation.
  - Fixed the issue where downloading a video that was being sent failed.
  - Fixed the issue where the onSuccess callback of the GroupChatManagerKit.getInstance().sendMessage method could be triggered twice.
  - Fixed the issue with short audio messages on the chat interface. Audio messages should be at least 1 second long. For messages shorter than 1 second, "Message too short" is displayed.
  - Fixed the issue where a user could be invited to join a private group repeatedly.
  - Fixed the issue where remarks could not be empty.
  - Fixed the issue where the time displayed on the chat interface was incorrect when the system time of the device was incorrect.
  - Fixed the issue where voice messages sent locally could not be downloaded on another mobile phone from roaming messages.
  - Fixed the issue where the group owner failed to set the group name to null but a message stating that the setting was successful was displayed.

**Windows platform**

- Fixed the issues where various platforms sent Chinese characters when image, file, audio, and video messages contained Chinese paths.
- Fixed the issue where TIMMsgReportReaded was invalid.
- Fixed the issue where the received message and recalled message have different rand and seq.
- Fixed occasional crashes when data was reported upon exit.
- Optimized the login module (repeated login/frequent login/frequent account switching/automatic connection/offline user being kicked off).
- Fixed the issue where the unread count could not be cleared after a member quit a group or a group was disbanded.
- Fixed the issue where group disband notifications could not be received occasionally.
- Fixed the issue where longer time was required to deliver messages when the app went to foreground after staying in background for a long time.



## Patch 4.4.631 @2019.07.03

**Android platform**

 Fixed offline push issues and crashes.


## 4.4.627 @2019.06.27

**iOS and Mac platforms**

- Fixed the message sending timeout issue when no network connection was available.
- Fixed the issue where the message ID value was changed after the message was sent.
- Fixed the disordered message issue.
- Fixed the issue where messages were lost when chat room historical messages were pulled.
- Fixed the issue with incorrect system message types.
- Fixed the issue where the obtained original image size of an image message was 0.
- Fixed the issue where mobile phones failed to send messages after the system time was changed.
- Fixed the issue where reporting conversation read and getting the unread count failed in some cases. 
- Fixed the issue where online messages that had been sent could be obtained through getLastMessage of the conversation.
- Fixed the issue where getting lastMsg status through the conversation was exceptional after the last message was recalled.
- Fixed the issue where recalled message content still existed in the conversation list of the peer.
- Fixed the issue where the sending status of image/audio/file messages was exceptional after network reconnection.
- Fixed the issue where login accounts that contained special characters could not send audio and images.
- Fixed the issue where the V4 version could not get the width and height of thumbnails sent by the V2 version.
- Fixed the issue where recent conversations failed to be pulled after saveMessage was created for a conversation.
- Fixed the issue where getMessage failed to get the MemberChangeList content of group tips.
- Fixed the issue when getLoginStatus failed to get the login status.
- Fixed the issue where applicants became group members after their requests to join the group were rejected.
- Fixed the issue where a log file existed under the root directory of the drive letter after a log path has been set.
- Mac: fixed the issue where the callback failed to be received in case of force offline.
- TUIKit
  - Optimized the group management page logic.
  - Fixed the iOS 13 compatibility issue.
  - Fixed known issues.

**Android platform**

- Fixed the message sending timeout issue when no network connection was available.
- Fixed the issue where the message ID value was changed after the message was sent.
- Fixed the disordered message issue.
- Fixed the issue where messages were lost when chat room historical messages were pulled.
- Fixed the issue with incorrect system message types.
- Fixed the issue with exceptional progress value when files were downloaded.
- Fixed the issue where mobile phones failed to send messages after the system time was changed.
- Fixed the issue where the sending status of image/audio/file messages was exceptional after network reconnection.
- Fixed exceptional message sorting after a group was disbanded or a user was muted.
- Fixed the issue where reporting conversation read and getting the unread count failed in some cases. 
- Fixed the issue where recalled message content still existed in the conversation list of the peer.
- Fixed the issue where the status fetched by getLastMessage of the conversation was exceptional after the last message was recalled.
- Fixed the issue where sent online messages could be obtained through getLastMessage of the conversation.
- Fixed the issue where the obtained original image size of an image message was 0.
- Fixed the issue where the V4 version could not get the width and height of thumbnails sent by the V2 version.
- Fixed the issue where getLoginUser() could still get logged in users after force offline.
- Fixed the issue where getSenderProfile returned blank information.
- Fixed the issue where getOpUser of TIMGroupSystemElem was empty.
- Fixed the issue where getMessage failed to get the MemberChangeList content of group tips.
- Fixed the issue where recent conversations failed to be pulled after saveMessage was created for a conversation.
- Fixed the issue where a log file existed under the root directory of the drive letter after a log path has been set.
- Fixed known TUIKit issues.

**Windows platform**

- Fixed the message sending timeout issue when no network connection was available.
- Fixed the issue where the message ID value was changed after the message was sent.
- Fixed the disordered message issue.
- Fixed the issue where messages were lost when chat room historical messages were pulled.
- Fixed the issue with incorrect system message types.
- Fixed the issue where the iOS IM SDK module of the cross-platform library did not include the Armv7a architecture.
- Fixed the issue where empty messages were not supported by the TIMMsgReportReaded API of the cross-platform library.
- Fixed the issue where multiple IM instances could run on one cross-platform library device with the same account and would be kicked off.
- Added the JSON key for getting the unique ID of messages to cross-platform library messages.
- Fixed the issue where a log file existed under the root directory of the drive letter after a log path has been set.
- Fixed the issue where getMessage failed to get the MemberChangeList content of group tips.
- Fixed the issue where getting lastMsg status through the conversation was exceptional after the last message was recalled.
- Fixed the issue where reporting conversation read and getting the unread count failed in some cases.

## 4.4.479 @2019.06.12

**iOS platform**

- Fixed the issue with message loss when offline messages were pulled.
- Fixed the login failure caused by changing SDKAppID.
- Fixed the issue where voice messages failed to play.
- Fixed crashes caused by recalling group messages.
- Fixed the 6002 error when getting friend lists and creating groups.
- Improved the message sending efficiency.
- Optimized the cache to mitigate UI lag.
- TUIKit
  - New UI design
  - New architecture design
  - Improved features such as contacts, group management, and relationship chain.
  - Fixed bugs.

**Android platform**

- Fixed the issue with message loss when offline messages were pulled.
- Fixed the login failure caused by changing SDKAppID.
- Fixed the issue where voice messages failed to play.
- Fixed crashes caused by recalling group messages.
- Fixed the 6002 error when getting friend lists and creating groups.
- Fixed Android devices crashes caused by creating groups with too many members.
- Improved the message sending efficiency.
- Optimized the cache to mitigate UI lag.
- TUIKit
  - New UI design
  - New architecture design
  - Improved features such as contacts, group management, and relationship chain.
  - Fixed bugs.

**Windows platform**

- Fixed the issue with message loss when offline messages were pulled.
- Fixed the login failure caused by changing SDKAppID.
- Fixed the issue where voice messages failed to play.
- Fixed crashes caused by recalling group messages.
- Fixed the 6002 error when getting friend lists and creating groups.
- Optimized the cache to mitigate UI lag.
- Improved the message sending efficiency.

## 4.3.145 @2019.05.31
**iOS platform**
- Fixed the issue where the same message was received after switching to another account.
- Fixed crashes caused by getting C2C roaming messages after the ticket expired.
- Fixed the issue where new chat room members could not see the chat history.
- Fixed FindMsg crashes.
- Optimized group message synchronization.
- Fixed occasional getReciveMessageOpt errors.

**Android platform**
- Fixed the issue where the same message was received after switching to another account.
- Fixed crashes caused by getting C2C roaming messages after the ticket expired.
- Fixed the issue where new chat room members could not see the chat history.
- Fixed the issue where the same message listener was added repeatedly.
- Fixed FindMsg crashes.
- Optimized group message synchronization.


**Windows platform**
- Fixed the issue where the same message was received after switching to another account.
- Fixed crashes caused by getting C2C roaming messages after the ticket expired.
- Fixed the issue where new chat room members could not see the chat history.
- Optimized group message synchronization.

## 4.3.135 @2019.05.24

**iOS platform**

- Added the checkFriends API to verify friends.
- Added the queryGroupInfo API to get local data.
- Deprecated getGroupPublicInfo and replaced it with getGroupInfo.
- Fixed the issue where deleted messages could be seen in the message list.
- Fixed the issue where local messages could not be obtained before login.
- Fixed the pulling quantity and sorting issues of recent contacts.
- Fixed group message synchronization after network reconnection.
- Fixed the issue where identifying duplicates failed when a large number of messages was received in a short time.
- Fixed the issue where the same message might be received again after the app restarted.
- Fixed occasional errors in initialization and message synchronization.
- Fixed occasional errors caused when lastMsg of a conversation was deleted.
- Fixed the issue where onRefreshConversation was called back twice with identical data.
- Fixed the issue where users could not obtain the chat history of a chat room before the time they joined the chat room.
- Fixed the issue where copyFrom of TIMMessage failed to work.
- Fixed the issue where TIMGroupEventListener failed to receive callbacks.
- Fixed crashes reported online.
- Optimized connection requests during reconnection.
- Optimized the quality of first connections to different networks and access points outside China.
- Improved the network reconnection speed when iOS devices switch to Wi-Fi networks.


**Android platform**

- Added the checkFriends API to verify friends.
- Added the queryGroupInfo API to get local data.
- Deprecated the getGroupDetailInfo and getGroupPublicInfo APIs and replaced them with the getGroupInfo API.
- Fixed the issue where deleted messages could be seen in the message list.
- Fixed modifyGroupOwner and getGroupMembersByFilter callback issues.
- Fixed the issue where local messages could not be obtained before login.
- Fixed the pulling quantity and sorting issues of recent contacts.
- Fixed group message synchronization after network reconnection.
- Fixed the issue where identifying duplicates failed when a large number of messages was received in a short time.
- Fixed the issue where the same message might be received again after the app restarted.
- Fixed occasional errors in initialization and message synchronization.
- Fixed occasional errors caused when lastMsg of a conversation was deleted.
- Fixed the issue where onRefreshConversation was called back twice with identical data.
- Fixed the issue where users could not obtain the chat history of a chat room before the time they joined the chat room.
- Fixed crashes reported online.
- Optimized connection requests during reconnection.
- Optimized the quality of first connections to different networks and access points outside China.



**Windows platform**

- Supported custom field data reporting.
- Added messages that disappear after being viewed.
- Added use cases for recalling messages.
- Fixed occasional failures in setting upload files.
- Fixed the issue where deleted messages could be seen in the message list.
- Fixed the pulling quantity and sorting issues of recent contacts.
- Fixed group message synchronization after network reconnection.
- Fixed the issue where identifying duplicates failed when a large number of messages was received in a short time.
- Fixed the issue where the same message might be received again after the app restarted.
- Fixed occasional errors caused when lastMsg of a conversation was deleted.
- Fixed occasional errors in initialization and message synchronization.
- The JSON string of a delivered message is returned in the callback indicating successful delivery.
- Replaced TIMSetRecvNewMsgCallback with TIMAddRecvNewMsgCallback and TIMRemoveRecvNewMsgCallback.
- Added socks5 proxy configuration.
- Optimized connection requests during reconnection.
- Optimized the quality of first connections to different networks and access points outside China.



## 4.3.118 @2019.05.10

**iOS platform**

- Added querySelfProfile and queryUserProfile to the TIMFriendshipManager class (reading local data).
- Fixed the issue where getLoginUser returned a login user exception.
- Fixed the issue where online reported user profiles failed to be obtained.
- Fixed the issue where some local fields became invalid after the app restarted.
- Fixed occasional errors when calling read report after messages were deleted.
- Fixed the online reported IM group issue.
- Fixed the issue with conversation unread counts.
- Fixed the issue with online messages.
- Fixed the issue where messages failed to be re-sent occasionally.
- Fixed the issue where local ticket expiration caused repeated reconnection.
- Fixed crashes reported online.
- Optimized the server connection strategy.
- Optimized the network reconnection strategy.
- Optimized the server overload strategy.
- Optimized heartbeat to reduce unnecessary outbound packets.
- Supported importing through CocoaPods for TUIKit.
- Added the Contacts interface for TUIKit.
- Added the Adding Friends interface for TUIKit.
- Added the Blocklist interface for TUIKit.
- Added the Search Friend interface for TUIKit.
- Added the New Friends interface for TUIKit.
- Added the Remarks, Blocklist, and Delete Friend features to the friend's profile page for TUIKit.
- Supported modification of nicknames, personal signature, date of birth, gender, and location on the user profile page for TUIKit.
- Improve the group pinning feature for TUIKit.

**Android platform**
- Added querySelfProfile and queryUserProfile to the TIMFriendshipManager class (reading local data).
- Added the addTime field to getting a friend's profile.
- Supported the x86 and x86_64 architecture.
- Fixed the issue where getLoginUser returned a login user exception.
- Fixed the issue where online reported user profiles failed to be obtained.
- Fixed the issue where some local fields became invalid after the app restarted.
- Fixed occasional errors when calling read report after messages were deleted.
- Fixed the online reported IM group issue.
- Fixed the issue with conversation unread counts.
- Fixed the issue with online messages.
- Fixed the issue where messages failed to be re-sent occasionally.
- Fixed the issue where local ticket expiration caused repeated reconnection.
- Fixed crashes reported online.
- Optimized the server connection strategy.
- Optimized the network reconnection strategy.
- Optimized the server overload strategy.
- Optimized heartbeat to reduce unnecessary outbound packets.
- Added the "pin chat to top" feature to TUIKit.
- TUIKit: nickname and personal signature can be changed, and the nickname is displayed on profile page.
- TUIKit: fixed the issue where emojis sent by iOS devices failed to be displayed on Android devices.
- TUIKit: fixed the unread message red dot issue.
- TUIKit: fixed the issue where a message appeared stating that UIs were abnormal after the plus sign was tapped on Meitu M8 mobiles phones.
- TUIKit: fixed the issue where profile photos were scaled down after being set and did not fill the entire UI.
- TUIKit: fixed the login and auto login logic.
- TUIKit: fixed the ANR issue when the input content exceeds the maximum limit. 
- TUIKit: fixed the issue where no response was received when images were selected from the photo album and the **OK** button on the preview screen was tapped.
- TUIKit: fixed the issue where the message deleting and recalling buttons were not displayed after image messages were tapped and held on the chat interface.
- TUIKit: optimized and fixed crashes reported online.

**Windows platform**
- Fixed the issue where getLoginUser returned a login user exception.
- Fixed the issue where online reported user profiles failed to be obtained.
- Fixed the issue where some local fields became invalid after the app restarted.
- Fixed occasional errors when calling read report after messages were deleted.
- Fixed the online reported IM group issue.
- Fixed the issue with conversation unread counts.
- Fixed the issue with online messages.
- Fixed the issue where messages failed to be re-sent occasionally.
- Fixed the issue where local ticket expiration caused repeated reconnection.
- Fixed crashes reported online.
- Optimized the server connection strategy.
- Optimized the network reconnection strategy.
- Optimized the server overload strategy.
- Optimized heartbeat to reduce unnecessary outbound packets.



## 4.3.81 @2019.04.24

**iOS platform**
- Fixed crashes caused by adding message elements to drafts.
- Fixed the issue where some accounts failed to pull conversation lists after an app was removed and reinstalled.
- Fixed the issue where login failed when usersig expired in login state and the app was not restarted.
- Fixed the issue where messages could not be sent and the usersig expiration callback was not received when usersig expired in login state.
- Fixed the issue with getting group member counts.
- Fixed the request timeout issue (error code 6012).

**Android platform**
- New features:
 - Supplemented relationship chain features such as blocklist, friend list, and friend request handling of earlier version SDKs.
- Fixed: 
 - Fixed the issue where an error was reported when the main process of the app was killed.
 - Fixed the issue with getting group member counts.
 - Fixed issues with setting and getting custom group fields and custom group member fields.
 - Fixed the issue where no onError callback was sent after getting group profile timed out.
 - Fixed the issue where some accounts failed to pull conversation lists after an app was removed and reinstalled.
 - Fixed the issue where login failed when usersig expired in login state and the app was not restarted.
 - Fixed the issue where messages could not be sent and the usersig expiration callback was not received when usersig expired in login state.
 - Fixed disordered messages.
 - Fixed the request timeout issue (error code 6012).
 - Updated relationship chain error codes.
 - TUIKit: fixed a critical bug with the DateUtils class (github issue#75).
 - TUIKit: fixed a crash (github issue#86).
 - TUIKit: fixed issues with using SDK without permissions.
 - TUIKit: fixed crashes after deleting conversation, deleting message, and long-pressing.
 - TUIKit: fixed the issue where pop-up window would not disappear.
 - TUIKit: fixed the issue with repeated messages.
 - TUIKit: fixed the issue with intercepting empty messages containing whitespace.
 - TUIKit: fixed the issue where unread counts did not update after conversations were deleted.
 - TUIKit: fixed the issue with the maximum number of characters in a message.
 - TUIKit: improved experience and fixed several Array Index Out of Bounds exceptions.

**Windows platform**
- Fixed some crashes.
- Fixed the request timeout issue (error code 6012).
- Fixed the issue where some accounts failed to pull conversation lists after an app was removed and reinstalled.
- Fixed the issue where login failed when usersig expired in login state and the app was not restarted.
- Fixed the issue where messages could not be sent and the usersig expiration callback was not received when usersig expired in login state.



## 4.2.52 @2019.04.17

**iOS platform**
- New features:
 - Supplemented relationship chain features such as blocklist, friend list, and friend request handling of earlier version SDKs.
- Fixed:
 - Optimized API annotations.
 - Fixed the issue with ineffective group custom fields and group member custom fields.
 - Fixed the issue where TIMMessage failed to get user profiles through senderProfile.
 - Fixed the issue with read receipt callback and status.
 - Fixed the issue where the last message did not call back when unread messages were synchronized.
 - Fixed the issue where group messages occasionally could not be received.
 - Fixed the issue where login response packets could not be decrypted.
 - Supported IP connection and login information reporting.
 - Fixed the message seq error.

**Android platform**
- New features:
 - Supplemented relationship chain features such as blocklist, friend list, and friend request handling of earlier version SDKs.
- Fixed:
 - Fixed jni leak on Android.
 - Fixed incorrect group member roles.
 - Fixed recalling group message crashes after a member quit the group and joined the group again.
 - Fixed the issue where emojis were not displayed in the TUIKit demo.
 - Fixed the issue where the second page would often contain repeated messages when group chat messages were received.
 - Fixed some crashes in the TUIKit demo.
 - Fixed the issue where TIMMessage failed to get user profiles through senderProfile.
 - Fixed the issue with read receipt callback and status.
 - Fixed the issue where the last message did not call back when unread messages were synchronized.
 - Fixed the issue where group messages occasionally could not be received.
 - Fixed the issue where login response packets could not be decrypted.
 - Supported IP connection and login information reporting.
 - Fixed the message seq error.

**Windows platform**
- New features:
 - Supplemented relationship chain features such as blocklist, friend list, and friend request handling of earlier version SDKs.
- Fixed:
 - Fixed the issue where TIMMessage failed to get user profiles through senderProfile.
 - Fixed the issue with read receipt callback and status.
 - Fixed the issue where the last message did not call back when unread messages were synchronized.
 - Fixed the issue where group messages occasionally could not be received.
 - Fixed the issue where login response packets could not be decrypted.
 - Supported IP connection and login information reporting.
 - Fixed the message seq error.



## 4.2.28 @2019.04.08

**iOS platform**
- Optimized issues related to unread counts.
- Optimized message read status.
- Fixed disordered C2C messages sent by RESTful APIs.
- Fixed occasional repeated roaming messages fetched.
- Optimized the uniqueId empty implementation issue.

**Android platform**

- New features:
 Added the logic for adding, deleting, and searching friends.
- Fixed:
 - Optimized issues related to unread counts.
 - Optimized message read status.
 - Fixed disordered C2C messages sent by RESTful APIs.
 - Fixed occasional repeated roaming messages fetched.
 - Optimized the uniqueId empty implementation issue.

**Windows platform**
- Optimized issues related to unread counts.
- Optimized message read status.
- Mitigated disordered C2C messages sent by RESTful APIs.
- Fixed occasional repeated roaming messages fetched.

## 4.2.10 @2019.03.29

**iOS platform**
- New features
 Added the logic for adding, deleting, and searching friends.
- Fixed:
  - Mitigated the timeout issue.
  - Optimized the auto login logic.
  - Fixed crashes.
  - Fixed occasional exceptional network connection.

**Android platform**
- Mitigated the timeout issue.
- Optimized the auto login logic.
- Mitigated the JNI leak issue.
- Fixed crashes.
- Fixed occasional exceptional network connection.

**Windows platform**
- Mitigated the timeout issue.
- Fixed crashes.
- Fixed occasional exceptional network connection.

## 4.2.9 @2019.03.27

**iOS and Mac platforms** 
- Fixed crashes in the IPv6 environment.
- Fixed the issue where setting profiles to int failed.

**Android platform**
Fixed the issue where setting profiles to int failed.

## 4.2.1 @2019.03.15
**iOS platform**
- Fixed the issue where clients did not receive relevant instructions after a group was disbanded in the backend.
- Fixed the issue where calling deleteConversationAndMessage() failed.
- Fixed the issue where no messages were received after network reconnection (On the conversion interface, messages can be proactively pulled after network reconnection.)

**Android platform**
- Fixed incorrect group pending and processed requests returned.
- Fixed client crashes when it went to the backend.
- Fixed the issue where no messages were received after network reconnection.
- Fixed occasional message sorting errors.
- Fixed the issue where messages occasionally failed to be sent.


**Web platform**
Web IM can play .amr recordings.

**Windows platform**

- Added the /source-charset:.65001 compilation option.
- Fixed crashes when the file system directly ran IMAPP.exe.
- Fixed various compilation errors and crashes.
- Removed X64 compilation (not supported at present).

## 4.0.13 @2019.03.13

**Android platform**
Fixed crashes caused by login after 3.x is upgraded to 4.x.

**iOS platform**

- pod can directly integrate the TUIKit.framework.
- Fixed crashes caused by login after 3.x is upgraded to 4.x.

**Windows platform**

- Added the IM demo with the duilib library as a UI component.
- Added usage instructions and integration guide.


## IM SDK 4.0.12 2019-3-11
**iOS platform**
- TUIKit.framework supports bitcode 2.
- Fixed ineffective group muting.
- Fixed the feature for modifying a user's role in a group.

**Android platform**
- Fixed ineffective group muting.
- Fixed the feature for modifying a user's role in a group.
- Fixed the issue with modifying group message receiving options.
- Fixed the issue with ineffective offline push toggle.


## IM SDK 4.0.10 2019-3-7
Fixed the message receiving error when an audio-video chat room had more than 100 members.

## IM SDK 4.0.8 2019-3-6
Optimized the audio playback logic for TUIkit.

## IM SDK 4.0.7 2019-3-1
- Fixed the compatibility issue with audio, file, and video messages between earlier and later versions.
- Fixed "-5 tls exchange failed" where login was successful after uninstalling and then reinstalling the app. 

## IM SDK 4.0.4 2019-2-28
- Fixed the issue where an incorrect error code was returned when a user logged in after userSig expired. The correct error code is 6206.
- Optimized the force offline logic.


## IM SDK 4.0.3 2019-2-25
Fixed the issue with third-party offline push.

## IM SDK 4.0.2 2019-2-20
Fixed the issue where bitcode packaging activation failed.

## IM SDK 4.0.1 2019-2-20
Fixed the issue where -5 is returned after login.

## iOS--IM SDK 4.0.0.1 2019-1-21
Added TUIKIt.

## IM SDK 3.3.2 2018-7-5
- Automatic read report is disabled by default. 
- Custom information types of profile relationship chains support integer.
- Fixed the issue where the group member count obtained from local storage was incorrect.
- Fixed the issue where the nickname carried in one-to-one chat messages was not updated in real time.

## IM SDK 2.7.2 2018-7-5
- Automatic read report is disabled by default.
- Custom information types of profile relationship chains support integer.
- Added the Recall Message feature.
- Fixed the issue where the nickname carried in one-to-one chat messages was not updated in real time.

## Windows--IM SDK 2.5.8 2018-7-5
- Fixed login failures in some cases.
- Custom information types of profile relationship chains support integer.

## IM SDK 3.3.0 2018-4-4
**iOS platform**
Added the level and role fields to TIMUserProfile.

**Android platform**
- Supported offline push on MEIZU mobile phones.
- Added standard level and role properties to user profiles.
- Fixed the issue where ugc short video failed to be sent when a user logged in after logging out.

## IM SDK 2.7.0 2018-4-4
**iOS platform**
- Added custom data parameters to the API for inviting users to join a group.

**Android platform**
- Supported offline push on MEIZU mobile phones.
- Supported custom data for the API for inviting users to join a group.

## Windows--IM SDK 2.5.7 2018-3-13
- Modified the login module to improve communication security.
- Improved the message delivery capability with poor network connection.
- Fixed occasional crashes when logs were printed.

## iOS--IM SDK 2.6.0 2018-3-13
- Provided an API for deleting roaming messages.
- Provided an API for serializing and deserializing message objects.
- Fixed some known issues.

## iOS--IM SDK 3.2.0 2018-3-13
- Fixed the issue where an error was reported when getUserProfile contained custom friend fields.
- Optimized the group unread count update strategy.
- Optimized the logic and strategy for local message storage.
- Fixed some crashes.

## Android--IM SDK 3.2.0 2018-3-13
- Fixed the issue where ugc short videos failed to be sent.
- Fixed the issue with no callbacks for sent messages when the network connection is interrupted.
- Fixed the issue where muting all did not take effect.
- Optimized the logic and strategy for local message storage.
- Fixed some crashes.

## Android--IM SDK 2.6.0 2018-3-13
- Provided an API for deleting roaming messages.
- Provided an API for serializing and deserializing message objects.
- Fixed some known issues.

## IM SDK 3.1.2 2017-12-12
- Mitigated the network timeout issue on Android devices.
- Fixed the audio download error on Android devices.
- Fixed various crashes on Android devices.

## IM SDK 2.5.7 2017-11-08
- Fixed SDK crashes when app processes were killed.
- Fixed the issue where offline messages were repeatedly pushed.
- Fixed the issue where internal accounts may be empty when initStorage and login are called at the same time.
- Optimized the network detection strategy.
- Fixed the error in getting friend lists.
- Fixed some crashes.

## IM SDK 3.1.1 2017-8-16
- Optimized the regular log clearing mechanism.
- Fixed the issue where iOS QALSDK crashed upon initialization.
- Added the feature for muting all group members.
- iOS: fixed the multi-user login failure. 
- Android: fixed crashes caused by getting group lists before login.

## IM SDK 2.5.6 2017-7-14
- Fixed crashes during login and logout.
- Fixed crashes during push and recording.

## IM SDK 3.1.0 2017-7-3
- Added IMUGCExt.framework and TXRTMPSDK.framework to provide short video recording and upload.
- Added the Recall Message feature.


## IM SDK 2.5.5 2017-6-6
- Optimized the logic for internal response packets to reduce time consumption.
- Improved the log time granularity to millisecond.
- Fixed some crashes and message synchronization issues.

## IM SDKV3 3.0.2 2017-5-22
- Fixed the issue where users cannot receive group messages in an audio-video chat room.
- Adjusted APIs.
    i. Deprecated TIMFileElem and the setData API in TIMSoundElem.
    ii. Corrected spelling of the getConversionList API in TIMManagerExt to getConversationList.

## IM SDKV3 3.0.1 2017-5-15
Fixed the issue where some so libraries were incompatible with devices running systems earlier than Android 5.0.

## IM SDKV3 3.0 2017-5-8
- Regrouped IM SDK and IMCore into IM SDK, IMMessageExt, IMGroupExt, and IMFriendExt.
- Optimized the IM SDK initialization method to initSdk: and setUserConfig.
- Names of IM SDK APIs and protocol callback methods start with lowercase letters.
- IM SDK features: basic login, receiving and sending messages, profile, and group features
- IMMessageExt features: full message features, including message pulling, local storage, and unread count
- IMGroupExt features: full group features, including group type management and group member management
- IMFriendExt features: full relationship chain features, including friend list and blocklist

## IM SDK 2.5.4 2017-4-28
- Fixed the timer mechanism bug in the IM SDK.

## IM SDK 2.5.3 2017-4-17
**iOS platform**
- sendOnlineMessage supports group messages, which will not be saved to local storage, stored offline, or included in the unread count.
- Added the findMessages method to get local messages by message ID.
- TIMIOSOfflinePushConfig provides the option for setting APNs push muting.
- Fixed the issue with excessive memory consumption when messages were received at high frequency.

**Android platform**
- Added the API for searching messages. (For more information, see findMessages under TIMConversation.)
- sendOnlineMessage supports group messages, which will not be saved to local storage, stored offline, or included in the unread count.
- Added the configuration item that allows a device to receive APNs push notifications without playing a sound or vibration. (For more information, see TIMMessageOfflinePushSettings.IOSSettings.NO_SOUND_NO_VIBRATION.)
- Optimized networking to improve SDK robustness in poor network connection.

**Windows platform**
- Fixed issues that may cause crashes.

**API changes:**
- Changed how TIMMessageOfflinePushSettings.AndroidSettings and TIMMessageOfflinePushSettings.IOSSettings are constructed.
For more information, see [Offline Push]

## IM Android SDK 2.5.2 2017-3-1
- Fixed the issue where the return of outgoing packets occasionally timed out (return code 6205).

## IM SDK 2.5.1 2017-2-16
- Limited the maximum size of log files to 50 MB.
- Fixed the bug where online state was returned after a user logged out and the app went to the backend.
- iOS: updated the audio and file downloading strategy and supported HTTP and HTTPS download.
- Fixed the status mismatch bug after messages failed to be sent when the user was not logged in.

## IM Web SDK 1.7 2016-12-20
- Supported multi-instance force offline.
- Supported simultaneous online of multiple instances.
- Supported synchronization of read group messages.
- Supported synchronization of read C2C messages.
- Optimized the demo directory structure and code.
- Added the recent contacts list.

## IM SDK 2.5 2016-12-16
- Optimized the TIMOfflinePushInfo object structure.
- Fixed audio and file download failures in iOS 9.1.
- Optimized network operations.
- Fixed some bugs.

## IM SDK 2.4.1 2016-11-24

- Fixed the bug where TIMGroupAssistant exceptionally pulls the group profile after entering an audio-video chat room.
- Fixed the bug where disabling console print failed.
- Fixed the issue where various listeners became invalid when logout is called before login after initialization.

## IM SDK 2.4 2016-11-09
- Fully compatible with the ATS mode.
- Message forwarding feature: the copyFrom API forwards image and file messages by copying images and files without downloading them.
- The number of members in an audio-video chat room is dynamically updated. TIMGroupEventListener returns the current number of group members.
- Message filtering can be customized for audio-video chat rooms.
- TIMOfflinePushInfo properties support push notification settings of Mi and Huawei mobile phones.
- Optimized the process of pulling group roaming messages.
- Optimized the processes of uploading and downloading audio, files, and short videos.
- Throwing onNewMessage when pulling the recent contacts list can be disallowed.

## IM SDK 2.3 2016-9-13
- Supported push notifications to multiple apps with one appid.
- Added setOfflinePushToken with callback to the Android version.
- Optimized the message deletion logic to automatically filter messages in the DELETED state when messages were pulled.
- iOS: moved database files from subdirectory Library/Caches/ to subdirectory Document/ to prevent them being cleared by the system.
- Multiple TIMMessageListeners can be added and deleted in iOS versions.
- Resident threads in iOS versions are named in a unified manner.
- The API for getting conversation lists automatically filters conversations with the message count set to 0.

## IM Web SDK 1.6 2016-8-15
- Web broadcast message requirements
- Added friend system notifications.
- Added profile system notifications.

## IM SDK 2.2 2016-8-10
- Supported conversation drafts.
- Conversations can be marked whether to store messages to ensure more flexible message handling.
- Roaming messages can be traversed from old to new, which applies to scenarios where message recording is needed.
- Added ext and sounds of push notifications to messages, allowing setting push information for some messages.
- Added stopQALService to the Android SDK, which turns off QALService when exiting the app.
- Supported network status monitoring and added error codes for network errors.

## IM SDK 2.1 2016-7-15
- Supported notification push to Mi and Huawei mobile phones.
- Supported the read receipts feature, which is optional depending on product needs.
- Supported typing reminder, which is optional depending on product needs.
- Added standard fields such as the gender, date of birth, address, and language to profile relationship chains.
- Notifications for joining and quitting a group contain the group member count.
- Fixed some SDK and demo bugs.

## IM Web SDK 1.5 2016-7-13
- Merged broadcasting chat room SDK capabilities.
- Fixed issues with uploading images in IE8 and 9.
- Added a group member count field to tips for joining and quitting groups.
- Fixed some SDK and demo bugs.

## IM SDK 2.0 2016-6-16
- The unread count can be synchronized between multiple online devices.
- Historical messages can be imported when an app is migrated to ensure smooth migration.
- Added the message notification status to group message properties.
- Supported flexible settings for message priorities.
- Push notifications can be filtered by property and tag.

## IM Web SDK 1.4 2016-6-7
- Friends' message history can be pulled.
- Red packets and like messages can be sent.
- The API for creating groups supports custom group IDs and broadcasting chat rooms.
- Optimized SDK APIs and merged the login and initialization APIs.
- Optimized the demo directory structure and code.

## IM SDK 1.9.3 2016-5-31
- Fixed resource destruction deadlocks when the winsdk process exited.

## IM SDK 1.9.2 2016-5-27
- Added the ticket expiration callback.
- Supported IPv6 (iOS).

## IM SDK 1.9 2016-5-4
- Supported groups with more than 10,000 members (no limit on the number of members, which is suitable for broadcasting scenarios).
- Reconstructed the IM demo for better experience and ease-of-use.
- Messages can be sent based on the priority.
- Added storage and cache for group profiles and relationship chains.
- Added APIs to synchronize group profiles and relationship chains and change callbacks.
- Supported getting friend profiles, including remarks and groups.
- Supported setting default group profile and relationship chain fields to be pulled.
- Supported disabling pulling recent contacts.
- Added synchronizing the last message to the conversation list.
- You can specify the group members whose group information, such as group name cards is to be pulled.
- Supported passing in file paths for voice and file messages (messages can be resent).
- Adapted to Android 6.0 dynamic permission management.

## IM SDK 1.8.1 2016-4-13
- Android: optimized the auto-start process. (To modify configuration, see ReadMe.txt.)
- Added the API for sending online messages in one-to-one chats. (The messages will be received only when the receiver is online and will not be stored when the receiver is offline.)
- Added the API for batch sending messages.
- Optimized Android performance.

## IM SDK 1.8 2016-3-23
- Android offline push
- Added the API to verify friend relationships.
- Added the relationship chain custom field API.
- Messages can be customized for local storage (for example, audio can be identified as read or unread).
- Added the API to compress images, meeting the need for image compression in detached communication scenarios.
- Customized messages' sound fields to specify APNs sounds.
- Optimized callback APIs for online status change.


## IM SDK 1.7 2016-1-25
- Supported limiting the message sending frequency in groups.
- Supported group ownership transfer.
- Group message notification intensity can be customized.
- CS channels are established to remove the need for a persistent connection between the app and backend to reduce battery consumption.
- Added configuration items, including message and recent contacts roaming switch, storage duration, and multi-device online switch to improve the operational efficiency.
- Downstream messages carry group member nicknames and contact cards to improve user experience and ease-of-use.
- Simplified the SDK to reduce the installation package size.


## IM SDK 1.6 2015-12-25
- Short video messages are supported to meet growing needs for video messages and social communication.
- Supported rule-based sorting of group members.
- Supported relationship chain friend grouping.
- Supported filtering of sensitive words in group names, announcements, and introductions.
- Supported group member contact cards to help users identify group members.
- Supported the message notifications switch, allowing users to turn on or off message notifications for one-to-one chats and group chats.

## IM SDK 1.5 2015-11-16

- Supported asynchronous download of message records.
- Group messages can be deleted at the server side.
- Users can be searched by nickname.
- Groups can be searched by group name.
- Event callbacks can be configured in the console.
- User credentials of admin accounts can be downloaded.
- Optimized some demo and technical logic.


## IM SDK 1.4 2015-10-16
- Multi-device login is supported.
- Messages from blocked users cannot be received.
- Deleted friend recommendations.
- APNs pushes nicknames.
- Supported filtering sensitive words in group names.
- Supported filtering sensitive words in group announcements.
- Demo supports the guest mode and third-party account login.

## IM SDK 1.3 2015-09-10
- Users can log in as guests without usernames and passwords.
- Message roaming is supported. (Messages are stored for seven days by default.)
- Recent contacts roaming and deletion are supported.
- Real-time message synchronization through callbacks is supported.
- Friend recommendation is supported after the recommendation logic has been defined.
- Sending original images or thumbnails is supported for better user experience.
- Supported push notifications (available only to online Android users).
- Supported smooth migration.
- Supported deleting local messages to protect users' privacy.

## IM SDK 1.2 2015-08-18
- C2C one-to-one chats on the web platform are supported.
- The maximum number of group members is increased to 10,000.
- Supported filtering ads and sensitive words in messages.
- Added an API that provides message IDs to precisely locate messages.
- Added remarks to user profiles.
- Supported viewing local messages when offline.

## IM SDK 1.1 2015-07-13
- Windows C++ platform is supported.
- Public groups and chat rooms are supported.
- Supported adding group introductions and announcements and added muting, message block, and group role setting.
- Added APIs for user profile and relationship chain operations, such as nicknames, adding friends, and blocklist settings.
- File messages are supported.
- Optimized image messages: image quality includes the original image, thumbnail, and large image. Changed upload and download APIs. Image URLs can be passed.
- Added log levels to the log callback API.
- Added the logic to execute forced logout on one device in the event of repeated logins.
- Added automatic crash reporting.
- Supported self-owned account and third-party account integration in hosting mode.
- Added SMS authentication for user registration and login.
- Supported ticket verification using public keys and private keys generated by Tencent.
- Added user and group management.

## IM SDK 1.0 2015-05-11
- Supported Android/iOS platforms.
- Supported integrating Tencent account and third-party account logins.
- Supported one-to-one chats and group chats (discussion groups).
- Supported text, emoji, image, audio, location, and custom messages.
- APNs push notifications (Token reporting, foreground and background switching event reporting)
- Messages can be stored locally.
