## Version 4.6.54 (Latest Version) @2020.01.03

### SDK

**General changes**

- Mitigated the issue where memory consumption increased when user profiles were frequently pulled
- Improved compatibility with special characters in user profiles
- Fixed known crash issues
- Fixed login failures that occasionally occurred when accounts were frequently switched


## Version 4.6.51 @2019.12.23

### SDK

**General changes**

- Improved network connection quality to quickly detect network quality changes
- Improved the handling of AVChatRoom messages

**For iOS and Mac**

- Modified all IMSDK listeners from strong references to weak references of external objects
- Added the getSenderNickname API for messages, which returns sender nicknames synchronously

**For Android**

- Fixed the issue where offline users were forced offline
- Fixed the issue where the upload progress callback was abnormal on devices running earlier versions of Android
- Fixed the memory leak issue during login
- Added the getSenderNickname API for messages, which returns sender nicknames synchronously

**For Windows**

- Fixed the issue where messages failed to be sent to newly added friends
- Improved the modification and query of custom fields of group information and group member information
- Improved callbacks for all APIs to ensure that callbacks are called and objects are transferred to JSON strings only when the callbacks succeed, and that empty strings are returned when the callbacks fail.

### TUIKit and demo

**For Android**

- Supported setting rounded corners for profile photos displayed in conversation lists
- Fixed the issue where the pinned conversation was abnormal when switching to another account


## Version 4.6.1 @2019.11.13

### SDK

**General changes**

- Supported the roaming of recalled messages
- Fixed the unread count error caused by joining a group by invitation in silent mode through a RESTful API
- Fixed message sending exceptions that occurred occasionally due to poor network connectivity
- Fixed the incorrect logic for role filtering conditions when obtaining group members
- Fixed the issue where the SDK failed to obtain the group name when users sent a message for the first time in a group created through a RESTful API
- Fixed the issue where getUsersProfile failed to obtain user information after caching was disabled
- Fixed the issue where audio files without file extensions could not be downloaded after they were received

**For iOS and Mac**

- Added the OPPOChannelID setting to resolve the issue where OPPO mobile phones with Android 8.0 or later failed to receive iOS push messages
- Optimized annotations to getGrouplist return objects

**For Android**

- Supported setting the channelID of offline push on OPPO mobile phones with Android 8.0 or later in the console
- Deprecated the ext, sound, and desc fields of TIMCustomElem

**For Windows**

- Fixed the abnormal type field of group system messages
- Fixed group type inconsistency between the returned group information and the header file
- Fixed the issue where specifying custom group fields failed during group creation
- Added the sender profile and offline push settings for messages

### TUIKit and demo

**For iOS**

- Added the video call feature
- Supported displaying group profile photos in a 3X3 grid view
- Optimized the conversation list, contacts, and chat UIs

**For Android**

- Added the method for setting whether to display read receipts
- Supported displaying group profile photos in a 3X3 grid view
- Optimized the conversation list, contacts, and chat UIs
- Resolved compatibility issues with the input method, UIs, and file selection for some mobile phones
- Fixed the chaotic display of custom messages
- Resolved the issue where the loading of contacts is slow in the stress test
- Fixed conflict with other library resources
- Fixed the issue where cache directory settings were ineffective

## Version 4.5.111 @2019.10.16

### SDK

**General changes**

- Fixed the pagination issue of the API for obtaining the list of group members of a specified type
- Added the format extension to the URL generated upon sending a file message
- Added the notification callback that is triggered after custom group fields are modified
- Supported obtaining local user and group information before login by calling the initStorage method
- Fixed the memory leak issue
- Fixed the issue where message status codes were incorrect after messages were recalled
- Fixed the issue where getMessage callback error codes were incorrect
- Fixed the issue where the one-to-one chat unread count was incorrect after an app was forcibly killed and restarted

**For iOS and Mac**

  Fixed occasional login failure for sleeping Mac devices

**For Android**

- Fixed stability issues in some scenarios
- Fixed the issue where OPPO mobile phones with Android 8.0 or later could not receive offline push notifications
- Optimized the return types of getElementCount

**For Windows**

- Improved the network reconnection speed for cross-platform libraries
- Fixed the issue where public group settings failed to be managed on Windows
- Added JVM configuration for cross-platform libraries to facilitate passing JVM from the Android environment

### TUIKit and demo

**For iOS**

- Added support for sending and receiving audio messages to and from web applications
- Fixed the swift issue where TUIKit resource files could not be found when loading
- Fixed the issue where the alias could not be seen on the chat UI after a friend’s alias was changed
- Fixed the issue where the conversation list did not refresh promptly after a conversation was pinned to the top

**For Android**

- Added support for sending and receiving audio messages to and from web applications
- Supported setting the input box style
- Supported displaying red dots on unread audio messages
- Fixed the issue where video messages could not be played on x86 devices
- Fixed conflict between FileProvider and the integration side
- Fixed the issue where audio permissions could not be recognized on some models of mobile phones
- Fixed the issue where profile photo loading failed under certain conditions
- Fixed the occasional issue where displayed pop-up messages were incomplete

## Version 4.5.55 @2019.10.10

### SDK

**General changes**

- Fixed the crash problem when switching the network for multiple times
- Improved network connection quality
- Optimized the annotations of some APIs

**For Android**

Improved restrictions on HTTP requests for Android 9.0 or later

**For iOS and Mac**

Optimized pod integration


## Version 4.5.45 @2019.09.18

### SDK

**General changes**

- Improved network connection quality
- Fixed the unread count issue when new messages arrive after a group chat is deleted
- Fixed the issue where deleted conversations could still be obtained through the conversation update callback 
- Optimized logic for pulling the custom fields of groups or group members

**For Android**

Deprecated the setOfflinePushListener API and the TIMOfflinePushNotification class in TIMManager

### TUIKit and demo

**For iOS**

- Fixed NSSting + Common.h class conflict
- Fixed the issue where the display of group tips was incomplete

**For Android**

- Added read receipts
- Made compatible with the typing indicator in earlier versions
- Fixed the issue where resent messages failed to immediately appear at the bottom of the chat window
- Fixed the issue where profile photos failed to appear under certain conditions
- Fixed the issue where multi-element group messages could not be displayed
- Fixed the crash problem caused by specific messages
- Fixed the issue where group admin permissions are incorrect
- Fixed the issue where files sent by web applications could not be properly received

## Version 4.5.15 @2019.08.30

### SDK

**General changes**

- Improved the delivery speed of file messages from overseas users
- Fixed the issue where the message state fetched by getLastMessage was incorrect after a message was recalled and the issue where message recall listening was called back multiple times
- Fixed the issue where the backend failed to obtain the correct muting time after a member is muted, quit the group, and joined the group again
- Fixed the issue where time failed to take effect at savemsg after the msg time was changed
- Fixed the occasional issue where no callback was triggered upon login
- Fixed the issue where the rand and timestamp of a recalled group message were empty
- Fixed the issue where the callback for UserSig expired when the user had logged out and the issue where network reconnection continued when the user had logged out

**For Android**

- Supported FCM push notifications on Android devices by the backend
- Fixed the issue where an error occurred when null was passed in for obtaining a specified friend group
- Fixed checkEquals crashes in specified scenarios

**For Windows**

- Added the unique_id field to MessageLocator
- Supported 64-bit Windows versions
- Added user profile APIs and relationship chain APIs for cross-platform libraries

### TUIKit and demo

**For iOS**

- Supported sending custom messages
- Supported C2C read receipts
- Added red dots for audio messages that have not been played

**For Android**

- Fixed the memory leak issue of the demo in some scenarios
- Fixed crashes in some scenarios
- Fixed the issue where custom message colors were incorrect
- Fixed the issue where the display of pop-up messages was incorrect or incomplete
- Fixed the issue where conversation lists failed to display profile photos
- Fixed the issue where the title bar color could not be changed by using ConversationLayout
- Supported 64-bit ijkplayer
- Supported multi-element messages

## Version 4.4.900 @2019.08.07

### SDK
**General changes**

 - Fixed stability issues in some scenarios
 - Optimized the unread message count
 - Improved the loading speed of recent chats after login
 - Added the log cleaning feature
 - Fixed the issue where messages were lost when synchronizing a large number of unread C2C messages
 - Fixed the issue where system messages about member quitting were not pushed to the current device after the user quit an AVChatroom group
 - Fixed the issue where group system messages occasionally failed to be received
 - Added frequency limit logic to onRefresh and onRefreshConversations
 - Fixed saveMessage sorting errors

**For iOS and Mac**

  - Changed the getGroupInfo callback parameter to TIMGroupInfoResult to obtain the error codes corresponding to each group
  - Optimized the layout of push notifications for 4.x versions to be consistent with 2.x and 3.x versions
  - Fixed the issue where logged-in accounts containing Chinese characters failed to send images, files, and videos

**For Android**

  - Fixed the issue where mobile phones running version 4.2.2 failed to load so
  - Fixed the issue where getGroupInfo returned an incorrect data amount
  - Changed the getGroupInfo callback parameter to TIMGroupDetailInfoResult to obtain the error codes corresponding to each group
  - Unified the use of the com.tencent.imsdk.TIMGroupReceiveMessageOpt class

**For Windows**

  Fixed the issue where the path of the Windows configuration file appeared as gibberish


###  TUIKit and demo

**For iOS**
  - Modified the UI for the iOS demo, including the default profile photo and four feature icons ("Camera", "Video", "Album", and "File") on the input UI
  - Added the profile card to "Me" and placed user information in the profile card
  - Added the feature to view the full image by tapping the profile photo
  - Modified the style of the small gray bar in group chats in the demo so that the member nickname becomes blue and tapping the nickname redirects to the member’s profile page
  - Optimized logic for displaying nicknames in groups in the demo
  - Optimized logic for displaying profile photos on the chat UI
  - Added tap feedback for all UIs, which allows developers to set up and customize feedback in TUIKit

**For Android**

  - Added MotionEvent.ACTION_CANCEL event handling for audio messages in chats
  - Supported displaying profile photos in the conversation list, chat UI, detailed profiles, and contacts
  - Supported modifying profile photos in user profiles
  - Added Intent redirection for the offline push feature
  - Added profile photos for one-to-one chats, group chats, and random chats
  - Added prompts for granting and revoking the group admin role for a group member
  - Added prompts for muting and unmuting group members
  - Fixed the issue where the text "Recalled a message" did not appear in tips after a message was recalled
  - Fixed the issue where the content of the recalled message continued to appear as the last message in the conversation list after a message was recalled
  - Fixed the white screen issue that happened when entering the chat UI after receiving offline messages on MEIZU mobile phones
  - Fixed the issue where the chat pinned to the top did not display the last message when new messages arrived
  - Fixed the Toast notification for the empty username or password
  - Fixed the issue where the display of the GroupTips message for group owner changing was abnormal in TUIKit
  - Fixed the error stating "Didn't find class "android.support.v4.content.FileProvider"" on some mobile phones
  - Optimized logic for pinning a chat to the top and arranged chats in chronological order starting from the most recent
  - Fixed the issue in chats where the soft keyboard and other layouts appeared at the same time
  - Fixed the issue where the contacts UI did not display the "Group Chats", "Blacklist", and "New Contacts" items for newly registered users who have no contacts
  - Fixed the video playing issue where the sound continued after the user tapped the "Back" button on a mobile phone
  - Fixed the issue where, when a user began to record an audio message, the currently playing audio message did not stop and its sound was also recorded
  - Fixed the issue where videos sent by iOS devices cannot be correctly played on some mobile phones


## Version 4.4.716 @2019.07.16


**For iOS and Mac**

- Organized and merged APIs
- Added the API for obtaining the download URLs of file, video, and audio messages
- Added the disableStorage API for disabling local storage
- Fixed the issue where the conversation on the sender’s device could still obtain lastMsg after an online message was sent
- Removed the return value of getSenderProfile and used a callback for fulfilling this purpose
- Changed the modifyReciveMessageOpt group function to modifyReceiveMessageOpt
- Fixed the issue where video screenshots could not be obtained when a device running iOS 2.X or 3.X sent video messages to a device running iOS 4.X
- Fixed crashes that occurred occasionally when reporting data upon logging out
- Optimized the login module (repeated login/frequent login/frequent account switching/auto connection/forced offline of offline users)
- Fixed the issue where the unread count could not be reset after a member quit a group or a group was dismissed
- Fixed the issue where group dismissal notifications could not be received occasionally
- Fixed the issue where message delivery is time-consuming when the app switched to the foreground after staying in the background for a long time
- Optimized the unread count for one-to-one chats
- Changed the TIMLoginParam input parameter of autoLogin to userID
- Changed the TIMLoginParam input parameter of initStorage to userID
- Removed multi-account login APIs, which are newManager, getManager, and deleteManager
- Fixed the occasional crashes of respondsToLocator 
- Fixed occasional crashes caused by TIMGroupInfo > lastMsg calling-related functions
- TUIKit
  - Optimized the update algorithm for recent contact list to reduce the refresh frequency
  - Fixed the blacklist memory leak
  - Added callbacks for pop-up messages and profile photo tapping events
  - Fixed the issue where latest profile photos did not appear in recent contacts and the chat window
  - Optimized document annotations

**For Android**

- Organized and merged APIs
  - Added all APIs in TIMManagerExt to TIMManager
  - Added all APIs in TIMConversationExt to TIMConversation
  - Added all APIs in TIMGroupManagerExt to TIMGroupManager
  - Added all APIs in TIMMessageExt to TIMMessage
  - Added all APIs in TIMUserConfigMsgExt to TIMUserConfig
  - Temporarily retained the APIs in the TIMManagerExt, TIMMessageExt, TIMConversationExt, TIMGroupManagerExt, and TIMUserConfigMsgExt classes for compatibility purposes, but these classes will be deprecated in the future
- Added options for adding friends in one-way and two-way manners 
- Added the disableStorage API for disabling local storage
- Added the API for obtaining the download URLs of file, video, and audio messages
- Fixed the issue where queryUserProfile was null on some Android mobile phones
- Fixed the issue where the conversation on the sender’s device could still obtain lastMsg after an online message was sent
- Removed the return value of getSenderProfile and used a callback to fulfill this purpose instead
- Fixed crashes that occurred occasionally when reporting data upon logging out
- Optimized the login module (repeated login/frequent login/frequent account switching/auto connection/forced offline of offline users)
- Fixed the issue where the unread count could not be reset after a member quit a group or a group was dismissed
- Fixed the issues where group dismissal notifications could not be received occasionally
- Fixed the issue where message delivery was time-consuming when the app switched to the foreground after staying in the background for a long time
- Optimized the unread count for one-to-one chats
- TUIKit
  - Supported playing short videos in chats in landscape or portrait orientation
  - Supported Javadoc documentation
  - Fixed the issue where downloading a video that was being sent could fail the download
  - Fixed the issue where the onSuccess callback of the GroupChatManagerKit.getInstance().sendMessage method was triggered twice
  - Fixed the issue with short audio messages on the chat UI. Specifically, audio message must be longer than 1 second. For messages shorter than 1 second, you will be prompted that the message is too short
  - Fixed the issue in private groups that allowed the same member to be invited repeatedly
  - Fixed the issue where remarks could not be empty
  - Fixed the issue where the time displayed on the chat UI was incorrect when the system time of the device was wrong
  - Fixed the issue where audio messages sent locally could not be downloaded on another mobile phone by roaming
  - Fixed the issue where, after the group owner set the group name to empty, a message appeared stating that the change had took effect while actually the change failed

**For Windows**

- Fixed the issue where image, file, audio, and video messages contained Chinese paths and different devices sent Chinese characters
- Fixed the issue where TIMMsgReportReaded was invalid
- Fixed the issue where the received and recalled messages have different rand and seq values
- Fixed crashes that occurred occasionally when reporting data upon logging out
- Optimized the login module (repeated login/frequent login/frequent account switching/auto connection/forced offline of offline users)
- Fixed the issue where the unread count could not be reset after a member quit a group or a group was dismissed
- Fixed the issue where group dismissal notifications could not be received occasionally
- Fixed the issue where message delivery was time-consuming when the app switched to the foreground after staying in the background for a long time



## Patch for version 4.4.631 @2019.07.03

**For Android**

 Fixed the offline push and crash issues


## Version 4.4.627 @2019.06.27

**For iOS and Mac**

- Fixed the message sending timeout issue when no network connection was available
- Fixed the issue where the message ID value changed after the message was sent
- Fixed the disorderly message issue
- Fixed the issue where message loss occurred when pulling historical chat messages
- Fixed the issue where the system message type was incorrect
- Fixed the issue where the original image size was 0 after an image message was delivered
- Fixed the issue where mobile phones failed to send messages after the system time was changed
- Fixed the issue where reporting conversation reading and obtaining the unread count failed in some cases 
- Fixed the issue where online messages that had been sent could be obtained through getLastMessage for the conversation
- Fixed the issue where obtaining the lastMsg state through the conversation after the last message was recalled was abnormal
- Fixed the issue where the content of a recalled message remained in the conversation list
- Fixed delivery state exceptions for image, audio, and file messages after the network resumed
- Fixed the issue where logged-in accounts containing special characters could not send audio and image files
- Fixed the issue where the V4 version could not obtain the width and height of thumbnails sent by the V2 version
- Fixed the issue where pulling recent conversations failed after creating a conversation saveMessage
- Fixed the issue where getMessage failed to obtain the MemberChangeList content of group Tips messages
- Fixed the issue where getLoginStatus encountered an exception when obtaining the login state
- Fixed the issue where applicants became group members after their group requests were rejected
- Fixed the issue where a log file existed under the root directory of the drive after the log path had been set
- Fixed the issue where the callback for mutual forcible offline was not received
- TUIKit
  - Optimized group management page logic
  - Fixed the compatibility issue with iOS 13
  - Fixed known issues

**For Android**

- Fixed the message sending timeout issue when no network connection is available
- Fixed the issue where the message ID value changed after the message was sent
- Fixed the disorderly message issue
- Fixed the issue where message loss occurred when pulling historical chat messages
- Fixed the issue where the system message type is incorrect
- Fixed the issue where the progress value is abnormal when downloading files
- Fixed the issue where mobile phones failed to send messages after the system time was changed
- Fixed delivery state exceptions for image, audio, and file messages after the network resumed
- Fixed the message sorting issue after a group was dismissed or a user was muted
- Fixed the issue where reporting conversation reading and obtaining unread count failed in some cases 
- Fixed the issue where the content of a recalled message remained in the conversation list
- Fixed the issue where the state obtained through getLastMessage of the conversation was incorrect after the last message was recalled
- Fixed the issue where online messages that had been sent could be obtained through getLastMessage of the conversation
- Fixed the issue where the original image size was 0 after an image message was delivered
- Fixed the issue where the V4 version could not obtain the width and height of thumbnails sent by the V2 version
- Fixed the issue where getLoginUser() could still obtain the logged-in user after forcible offline
- Fixed the issue where getSenderProfile returned blank information
- Fixed the issue where getOpUser of TIMGroupSystemElem was empty
- Fixed the issue where getMessage failed to obtain the MemberChangeList content of group Tips messages
- Fixed the issue where pulling recent conversations failed after creating a conversation saveMessage
- Fixed the issue where a log file existed under the root directory of the drive after a log path had been set
- Fixed known TUIKit issues

**For Windows**

- Fixed the message sending timeout issue when no network connection was available
- Fixed the issue where the message ID value changed after the message was sent
- Fixed the disorderly message issue
- Fixed the issue where message loss occurred when pulling historical chat messages
- Fixed the issue where the system message type was incorrect
- Fixed the issue where the IM SDK module for iOS cross-platform libraries did not include Armv7a architecture
- Fixed the issue where empty messages were not supported by the TIMMsgReportReaded API for cross-platform libraries
- Fixed the issue where multiple IM instances could run on the same cross-platform library device and logged in to the same account without triggering mutual forcible offline
- Added the JSON key for obtaining the unique ID of a message to cross-platform library messages
- Fixed the issue where a log file existed under the root directory of the drive after a log path had been set
- Fixed the issue where getMessage failed to obtain the MemberChangeList content of group Tips messages
- Fixed state exceptions when obtaining lastMsg through the conversation after the last message was recalled
- Fixed the issue where reporting conversation reading and obtaining the unread count failed in some cases

## Version 4.4.479 @2019.06.12

**For iOS**

- Fixed the issue where message loss occurred when pulling offline messages
- Fixed the login failure caused by changing SDKAppID
- Fixed the issue where audio messages failed to be played
- Fixed crashes caused by recalling group messages
- Fixed error 6002 when obtaining the friend list and creating a group
- Improved message sending efficiency
- Optimized the cache to mitigate UI lag
- TUIKit
  - Provided new UI design
  - Provided new architecture design
  - Improved features such as contacts, group management, and relationship chain
  - Fixed known bugs

**For Android**

- Fixed the issue where message loss occurred when pulling offline messages
- Fixed the login failure caused by changing SDKAppID
- Fixed the issue where audio messages failed to be played
- Fixed crashes caused by recalling group messages
- Fixed error 6002 when obtaining the friend list and creating a group
- Fixed Android crashes caused by creating a group with too many members
- Improved message sending efficiency
- Optimized the cache to mitigate UI lag
- TUIKit
  - Provided new UI design
  - Provided new architecture design
  - Improved features such as contacts, group management, and relationship chain
  - Fixed known bugs
  
**For Windows**

- Fixed the issue where message loss occurred when pulling offline messages
- Fixed the login failure caused by changing SDKAppID
- Fixed the issue where audio messages failed to be played
- Fixed crashes caused by recalling group messages
- Fixed error 6002 when obtaining the friend list and creating a group
- Optimized the cache to mitigate UI lag
- Improved message sending efficiency

## Version 4.3.145 @2019.05.31
**For iOS**
- Fixed the issue where the same message was received after switching to another account
- Fixed crashes caused by obtaining C2C roaming messages after the ticket expired
- Fixed the issue where new ChatRoom members could not obtain historical messages
- Fixed FindMsg crashes
- Optimized group message synchronization
- Fixed occasional getReciveMessageOpt exceptions

**For Android**
- Fixed the issue where the same message was received after switching to another account
- Fixed crashes caused by obtaining C2C roaming messages after the ticket expired
- Fixed the issue where new ChatRoom members could not view historical messages
- Fixed the issue where the same message listener was added repeatedly
- Fixed FindMsg crashes
- Optimized group message synchronization


**For Windows**
- Fixed the issue where the same message was received after switching to another account
- Fixed crashes caused by obtaining C2C roaming messages after the ticket expired
- Fixed the issue where new ChatRoom members could not view historical messages
- Optimized group message synchronization

## Version 4.3.135 @2019.05.24

**For iOS**

- Added the checkFriends friend verification API
- Added the queryGroupInfo API for obtaining local data
- Replaced getGroupPublicInfo with getGroupInfo
- Fixed the issue where deleted messages could be found in the message list
- Fixed the issue where local messages could not be obtained before login
- Fixed the issue with the number and sorting of pulled recent contacts
- Fixed group message synchronization after the network resumed
- Fixed the issue where de-duplication failed when a large number of messages were received in a short period
- Fixed the issue where the same message could be delivered again after the app restarted
- Fixed occasional initialization and message synchronization issues
- Fixed occasional errors that occurred when the lastMsg of a conversation was deleted
- Fixed the issue where onRefreshConversation was called back twice with identical data
- Fixed the issue where chatroom could not obtain historical messages that occurred before a user joined the group
- Fixed the issue where copyFrom of TIMMessage did not work
- Fixed the issue where TIMGroupEventListener failed to receive callbacks
- Fixed crash issues reported online
- Optimized connection requests during reconnection
- Optimized the quality of initial connections to different networks and overseas access points
- Improved the network reconnection speed when iOS devices switch to different Wi-Fi networks


**For Android**

- Added the checkFriends API for verifying friends.
- Added the queryGroupInfo API for obtaining local data
- Replaced getGroupDetailInfo and getGroupPublicInfo with getGroupInfo
- Fixed the issue where deleted messages could be found in the message list
- Fixed modifyGroupOwner and getGroupMembersByFilter callback issues
- Fixed the issue where local messages could not be obtained before login
- Fixed the issue with the number and sorting of pulled recent contacts
- Fixed group message synchronization after the network resumed
- Fixed the issue where de-duplication failed when a large amount of messages were received in a short period
- Fixed the issue where the same message could be delivered again after the app restarted
- Fixed occasional initialization and message synchronization errors
- Fixed occasional errors that occurred when the lastMsg of a conversation was deleted
- Fixed the issue where onRefreshConversation was called back twice with identical data
- Fixed the issue where chatroom could not obtain historical messages that occurred before a user joined the group
- Fixed crash issues reported online
- Optimized connection requests during reconnection
- Optimized the quality of initial connections to different networks and overseas access points



**For Windows**

- Supported data reporting for custom fields
- Supported messages that are removed once read
- Added use cases for recalling messages
- Fixed occasional failures in setting upload files
- Fixed the issue where deleted messages could be found in the message list
- Fixed the issue with the number and sorting of pulled recent contacts
- Fixed group message synchronization after the network resumed
- Fixed the issue where de-duplication failed when a large amount of messages were received in a short period
- Fixed the issue where the same message could be delivered again after the app restarted
- Fixed occasional errors that occurred when the lastMsg of a conversation was deleted
- Fixed occasional initialization and message synchronization errors
- Supported returning the JSON string of the delivered message in the successful delivery callback
- Replaced TIMSetRecvNewMsgCallback with TIMAddRecvNewMsgCallback and TIMRemoveRecvNewMsgCallback
- Added socks5 proxy configuration
- Optimized connection requests during reconnection
- Optimized the quality of initial connections to different networks and overseas access points



## Version 4.3.118 @2019.05.10

**For iOS**

- Added querySelfProfile and queryUserProfile (for reading local data) to the TIMFriendshipManager class
- Fixed the issue where getLoginUser encountered an exception when returning the logged-in user
- Fixed the issue where obtaining user profiles that were reported online failed
- Fixed the issue where some local fields became invalid after the app restarted
- Fixed occasional errors that occurred when calling the read report after deleting messages
- Fixed the issue related to IM groups that were reported online
- Fixed the issue with the conversation unread count
- Fixed the issue with online messages
- Fixed the issue where messages occasionally failed to be resent
- Fixed the issue where local ticket expiration led to repeated reconnection
- Fixed crash issues that were reported online
- Optimized the server connection policy
- Optimized the reconnection policy upon disconnection
- Optimized the server overload policy
- Optimized heartbeating to reduce unnecessary outbound packets
- Supported importing CocoaPods in TUIKit
- Added the contacts UI to TUIKit
- Added the friend addition UI to TUIKit
- Added the blacklist UI to TUIKit
- Added the friend search UI to TUIKit
- Added the UI for newly added friends to TUIKit
- Added new features for the friend profile page to TUIKit, including adding remarks, creating a blacklist, and deleting friends
- Optimized the user profile page in TUIKit, including supporting modifying the nickname, personal signature, date of birth, gender, and location
- Improved the feature of pinning a group to top in TUIKit

**For Android**
- Added querySelfProfile and queryUserProfile (for reading local data) to the TIMFriendshipManager class
- Added the addTime field when obtaining a friend’s profile
- Added support for x86 and x86_64 architecture
- Fixed the issue where getLoginUser encountered an exception when returning the logged-in user
- Fixed the issue where obtaining user profiles that were reported online failed
- Fixed the issue where some local fields became invalid after the app restarted
- Fixed occasional errors that occurred when calling the read report after deleting messages
- Fixed the issue related to IM groups that were reported online
- Fixed the issue with the conversation unread count
- Fixed the issue with online messages
- Fixed the issue where messages occasionally failed to be resent
- Fixed the issue where local ticket expiration led to repeated reconnection
- Fixed crash issues reported online
- Optimized the server connection policy
- Optimized the reconnection policy upon network disconnection
- Optimized the server overload policy
- Optimized heartbeating to reduce unnecessary outbound packets
- Added the feature of pinning a chat to top to TUIKit
- Supported changing the nickname and personal signature and displaying the nickname on the profile page in TUIKit
- Fixed the issue in TUIKit where emojis sent by iOS devices failed to be displayed on Android devices
- Fixed the issue with the number of red dots for unread messages on app icons in TUIKit
- Fixed the issue with Meitu M8 mobile phones in TUIKit where, after the plus sign was tapped, a message appeared stating that UI issues occur on the operation UI
- Fixed the issue in TUIKit where profile photos were scaled down after being set and did not fill the entire UI
- Fixed the login and auto login logics in TUIKit
- Fixed the ANR issue caused by exceeding the input content limit in TUIKit 
- Fixed the issue in TUIKit when sending images where images were selected from the photo album, the **OK** button on the preview screen was tapped, but no response was returned
- Fixed the issue in TUIKit where long-pressing image messages on the chat UI did not bring up the action buttons for deleting and recalling messages
- Optimized and fixed crash issues that were reported online in TUIKit

**For Windows**
- Fixed the issue where getLoginUser encountered an exception when returning the logged-in user
- Fixed the issue where obtaining user profiles that were reported online failed
- Fixed the issue where some local fields became invalid after the app restarted
- Fixed occasional errors that occurred when calling the read report after deleting messages
- Fixed the issue related to IM groups that were reported online
- Fixed the issue with the conversation unread count
- Fixed the issue with online messages
- Fixed the issue where messages occasionally failed to be resent
- Fixed the issue where local ticket expiration led to repeated reconnection
- Fixed crash issues reported online
- Optimized the server connection policy
- Optimized the reconnection policy upon network disconnection
- Optimized the server overload policy
- Optimized heartbeating to reduce unnecessary outbound packets



## Version 4.3.81 @2019.04.24

**For iOS**
- Fixed crashes caused by adding message elements to drafts
- Fixed the issue where some accounts failed to pull conversation lists after an app was uninstalled and then reinstalled
- Fixed the issue where usersig expired after the user logged in and then login failure persisted until the app was restarted
- Fixed the issue where usersig expired after the user logged in, messages could not be sent, and the result of the usersig expiration callback could not be received
- Fixed the issue with obtaining the number of group members
- Fixed the request timeout issue (with error code 6012)

**For Android**
- New features:
 - Supplemented earlier versions of SDK with relationship chain features such as the blacklist, friend grouping, and friend request handling
- Bug fixes: 
 - Fixed the issue where an error occurred when the main process of the app was killed
 - Fixed the issue with obtaining the number of group members
 - Fixed the configuration and retrieval issues with custom group fields and custom group member fields
 - Fixed the issue where no onError callback was sent after group profile retrieval timed out
 - Fixed the issue where some accounts failed to pull conversation lists after an app was uninstalled and then reinstalled
 - Fixed the issue where usersig expired after the user logged in and then login failure persisted until the app was restarted
 - Fixed the issue where usersig expired after the user logged in, messages could not be sent, and the result of the usersig expiration callback could not be received
 - Fixed the issue with disorderly messages
 - Fixed the request timeout issue (with error code 6012)
 - Updated error codes for the relationship chain
 - Fixed a critical bug with the DateUtils class (github issue#75) in TUIKit
 - Fixed a crash issue (github issue#86) in TUIKit
 - Fixed issues with using the SDK without permissions in TUIKit
 - Fixed crashes in TUIKit that occurred after deleting a conversation, deleting a message, and long-pressing a message
 - Fixed the issue in TUIKit where popupwindow persisted
 - Fixed the issue with repeated messages in TUIKit
 - Fixed the issue with intercepting empty messages containing whitespaces in TUIKit
 - Fixed the issue in TUIKit where the message unread count did not update after a conversation was deleted
 - Fixed the issue with the maximum number of characters in a message in TUIKit
 - Improved user experience and fixed several "Array Index Is Out of Bound" exceptions

**For Windows**
- Fixed some crash issues
- Fixed the request timeout issue (with error code 6012)
- Fixed the issue where some accounts failed to pull conversation lists after an app was uninstalled and then reinstalled
- Fixed the issue where usersig expired after the user logged in and then login failure persisted until the app was restarted
- Fixed the issue where usersig expired after the user logged in, messages could not be sent, and the result of the usersig expiration callback could not be received



## Version 4.2.52 @2019.04.17

**For iOS**
- New features:
 - Supplemented earlier versions of SDK with relationship chain features such as the blacklist, friend list, and friend request handling
- Bug fixes:
 - Optimized API annotations
 - Fixed the issue with ineffective custom group fields and custom group member fields
 - Fixed the issue where TIMMessage failed to obtain user profiles through senderProfile
 - Fixed issues with the read receipt callback and the state
 - Fixed the issue with the synchronization of unread messages where the last message was not called back
 - Fixed the issue where group messages occasionally failed to be received
 - Fixed the issue where login response packets could not be decrypted
 - Supported the statistical collection and reporting of IP connections and login information
 - Fixed message seq errors

**For Android**
- New features:
 - Supplemented earlier versions of SDK with relationship chain features such as the blacklist, friend list, and friend request handling
- Bug fixes:
 - Fixed the jni leak on Android devices
 - Fixed the issue with incorrect group member roles
 - Fixed the issue where recalling a group message crashed after a member quit the group and joined the group again
 - Fixed the issue where emojis were not displayed in the TUIKit demo
 - Fixed the issue with receiving group conversation messages where the second page often contained repeated messages
 - Fixed some crash issues in the TUIKit demo
 - Fixed the issue where TIMMessage failed to obtain user profiles through senderProfile
 - Fixed issues with the read receipt callback and the state
 - Fixed the issue with unread message synchronization where the last message was not called back
 - Fixed the issue where group messages occasionally failed to be received
 - Fixed the issue where login response packets could not be decrypted
 - Supported the statistical collection and reporting of IP connections and login information
 - Fixed message seq errors

**For Windows**
- New features:
 - Supplemented earlier versions of SDK with relationship chain features such as the blacklist, friend list, and friend request handling
- Bug fixes:
 - Fixed the issue where TIMMessage failed to obtain user profiles through senderProfile
 - Fixed issues with the read receipt callback and the state
 - Fixed the issue with unread message synchronization where the last message was not called back
 - Fixed the issue where group messages occasionally failed to be received
 - Fixed the issue where login response packets could not be decrypted
 - Supported the statistical collection and reporting of IP connections and login information
 - Fixed message seq errors



## Version 4.2.28 @2019.04.08

**For iOS**
- Fixed the issue with the unread count
- Fixed the issue with the message read state
- Fixed the issue with disorderly C2C messages sent through a RESTful API
- Fixed the issue with occasional repeated messages when obtaining roaming messages
- Fixed the issue with the uniqueId empty implementation

**For Android**

- New features:
 Added logic for adding, deleting, and searching for friends
- Bug fixes:
 - Fixed the issue with the unread count
 - Fixed the issue with the message read state
 - Fixed the issue with disorderly C2C messages sent through a RESTful API
 - Fixed the issue with occasional repeated messages when obtaining roaming messages
 - Fixed the issue with the uniqueId empty implementation

**For Windows**
- Fixed the issue with the unread count
- Fixed the issue with the message read state
- Fixed the issue with disorderly C2C messages sent through a RESTful API
- Fixed the issue with occasional repeated messages when obtaining roaming messages

## Version 4.2.10 @2019.03.29

**For iOS**
- New features
 Added logic for adding, deleting, and searching for friends
- Bug fixes:
  - Fixed the timeout issue
  - Optimized auto login logic
  - Fixed crash issues
  - Fixed occasional network connection issues

**For Android**
- Fixed the timeout issue
- Optimized auto login logic
- Fixed the JNI leak
- Fixed crash issues
- Fixed occasional network connection issues

**For Windows**
- Fixed the timeout issue
- Fixed crash issues
- Fixed occasional network connection issues

## Version 4.2.9 @2019.03.27

**For iOS and Mac** 
- Fixed crashes that occurred in the IPv6 environment
- Fixed the issue where setting an integer for the profile failed

**For Android**
Fixed the issue where setting an integer for the profile failed

## Version 4.2.1 @2019.03.15
**For iOS**
- Fixed the issue where the client did not receive relevant instructions after a group was dismissed by the backend
- Fixed the issue where calling deleteConversationAndMessage() failed
- Fixed the issue where no messages were received after the network resumed (requesting message pulling after the network is resumed is now supported on the conversation UI)

**For Android**
- Fixed the issue where incorrect values were returned when groups retrieved pending and processed requests
- Fixed client crashes when the client switched to the background
- Fixed the issue where no messages were received after the network resumed
- Fixed occasional message sorting errors
- Fixed the issue where messages occasionally failed to be sent


**For web**
Supported playing .amr recordings by WEBIM

**For Windows**

- Added the /source-charset:.65001 compilation option
- Fixed crashes when the file system directly ran IMAPP.exe
- Fixed some compilation errors and crash issues
- Removed X64 compilation (currently unsupported)

## Version 4.0.13 @2019.03.13

**For Android**
Fixed crashes caused by login after upgrading from version 3.x to version 4.x

**For iOS**

- Supported directly integrating TUIKit.framework with pods
- Fixed crashes caused by login after upgrading from version 3.x to version 4.x

**For Windows**

- Added the IM demo where the duilib library was used as a UI component
- Added use instructions and integration guidelines


## IM SDK 4.0.12, 2019-3-11
**For iOS**
- Supported bitcode 2 by TUIKit.framework
- Fixed ineffective muting in groups
- Fixed the feature for changing a user’s role in a group

**For Android**
- Fixed ineffective muting in groups
- Fixed the feature for changing a user’s role in a group
- Fixed the issue with modifying group message receiving options
- Fixed the issue with the ineffective offline push toggle


## IM SDK 4.0.10, 2019-3-7
Fixed the message receiving error when an AVChatRoom group had more than 100 members

## IM SDK 4.0.8, 2019-3-6
Optimized audio playback logic in TUIkit

## IM SDK 4.0.7, 2019-3-1
- Fixed the compatibility issue with audio, file, and video messages between newer and earlier versions
- Fixed the login error "-5 tls exchange failed", which previously could only be resolved by uninstalling and then reinstalling the app 

## IM SDK 4.0.4, 2019-2-28
- Fixed the issue where logging in after userSig expired returned an incorrect error code (the correct error code is 6206)
- Optimized mutual forcible offline logic


## IM SDK 4.0.3, 2019-2-25
Fixed the issue with third-party offline push

## IM SDK 4.0.2, 2019-2-20
Fixed the issue where bitcode packaging activation failed

## IM SDK 4.0.1, 2019-2-20
Fixed the issue where login returned -5

## iOS--IM SDK 4.0.0.1, 2019-1-21
Added TUIKIt

## IM SDK 3.3.2, 2018-7-5
- Disabled the automatic read reporting feature that was enabled by default 
- Supported integers by custom information types of the profile relationship chain
- Fixed the issue where the group member count obtained from local storage was incorrect
- Fixed the issue where the friend alias carried in one-to-one chat messages did not refresh in real time

## IM SDK 2.7.2, 2018-7-5
- Disabled automatic read reporting by default
- Supported integers by the custom information types of the profile relationship chain
- Added the message recalling feature
- Fixed the issue where the friend alias carried in one-to-one chat messages did not refresh in real time

## Windows--IM SDK 2.5.8, 2018-7-5
- Fixed the issue where login failed in some cases
- Supported integers for custom information types of the profile relationship chain

## IM SDK 3.3.0, 2018-4-4
**For iOS**
Added the level and role fields to TIMUserProfile

**For Android**
- Supported MEIZU offline push
- Added the level and role standard attributes to user profiles
- Fixed the issue where sending ugc short videos failed when the user logged in again after logging out

## IM SDK 2.7.0, 2018-4-4
**For iOS**
- Added custom data parameters to the API for inviting members to join a group

**For Android**
- Supported MEIZU offline push
- Supported specifying custom data by the API for joining a group by invitation

## Windows--IM SDK 2.5.7, 2018-3-13
- Modified the login module to improve communication security
- Improved the message delivery ability with poor network connectivity
- Fixed occasional crashes when printing logs

## iOS--IM SDK 2.6.0, 2018-3-13
- Provided the API for deleting roaming messages
- Provided the API for serializing and deserializing message objects
- Fixed some historical issues

## iOS--IM SDK 3.2.0, 2018-3-13
- Fixed the issue where an error occurred when getUserProfile contained custom friend fields
- Optimized the update policy of group unread count
- Fixed the logic and policy of storing messages locally
- Fixed some crash issues

## Android--IM SDK 3.2.0, 2018-3-13
- Fixed the issue where sending ugc short videos could fail
- Fixed the issue where no callback occurred after messages were sent without network connection
- Fix the issue where muting all members failed
- Optimized the logic and policy of storing messages locally
- Fixed some crash issues

## Android--IM SDK 2.6.0, 2018-3-13
- Provided the API for deleting roaming messages
- Provided the API for serializing and deserializing message objects
- Fixed some historical issues

## IM SDK 3.1.2, 2017-12-12
- Fixed the network timeout issue on Android devices
- Fixed audio download errors on Android devices
- Fixed several crash issues on Android devices

## IM SDK 2.5.7, 2017-11-08
- Fixed the SDK crash that occurred when the app process was killed
- Fixed the issue where offline messages were repeatedly pushed
- Fixed the issue where internal accounts could be empty when initStorage and login were called at the same time
- Optimized the network detection policy
- Fixed the error in obtaining friend lists
- Fixed some crash issues

## IM SDK 3.1.1, 2017-8-16
- Optimized the regular clearing mechanism for LOG
- Fixed the issue where iOS QALSDK was stuck upon initialization
- Added the feature of muting all members in a group
- Fixed multi-user login failure on iOS devices 
- Fixed crashes that occurred on Android devices when obtaining group lists before login

## IM SDK 2.5.6, 2017-7-14
- Fixed crashes that could occur during login and logout
- Fixed crashes that could occur during push and recording

## IM SDK 3.1.0, 2017-7-3
- Added IMUGCExt.framework and TXRTMPSDK.framework to provide the short video recording and upload features
- Added the message recalling feature


## IM SDK 2.5.5, 2017-6-6
- Optimized logic for internal response packets to reduce time consumption
- Improved the LOG time granularity to the millisecond
- Fixed some crashes and other message synchronization issues

## IM SDKV3 3.0.2, 2017-5-22
- Fixed the issue where an AVChatRoom group could not receive group messages
- Adjusted APIs
    i. Deprecated the setData API from TIMFileElem and TIMSoundElem
    ii. Corrected the spelling of the getConversionList API in TIMManagerExt to getConversationList

## IM SDKV3 3.0.1, 2017-5-15
Fixed the issue where some so libraries were incompatible with devices running systems earlier than Android 5.0

## IM SDKV3 3.0, 2017-5-8
- Rearranged IM SDK and IMCore to IM SDK, IMMessageExt, IMGroupExt, and IMFriendExt
- Optimized the IM SDK initialization method to initSdk: and setUserConfig
- Modified the names of IM SDK APIs and Protocol callback methods to begin with lowercase letters
- Provided IM SDK features: login, receiving and sending messages, profiles, and groups
- Provided IMMessageExt features for existing messages, including message pulling, local storage, and unread count
- Provided IMGroupExt features for existing groups, including group type management and group member management
- Provided IMFriendExt features for existing relationship chains, including the friend list and blacklist

## IM SDK 2.5.4, 2017-4-28
- Fixed the bug in IM SDK’s timer mechanism

## IM SDK 2.5.3, 2017-4-17
**For iOS**
- Supported group messages by sendOnlineMessage where messages are not stored locally, stored offline, or included into the unread count
- Added the findMessages method for obtaining local messages by message IDs
- Provided the silent push option for APNs by TIMIOSOfflinePushConfig
- Fixed the issue with excessive memory consumption when receiving messages frequently

**For Android**
- Added the API for searching for messages (for more information, see findMessages under TIMConversation)
- Supported group messages by sendOnlineMessage where messages will not be stored locally, stored offline, or included into the unread count
- Added the configuration item that allows a device to receive APNs push notifications without playing a sound and vibrating (see TIMMessageOfflinePushSettings.IOSSettings.NO_SOUND_NO_VIBRATION)
- Optimized networking to improve SDK robustness in scenarios with poor network connectivity

**For Windows**
- Fixed issues that could cause crashes

**API changes:**
- Modified how TIMMessageOfflinePushSettings.AndroidSettings and TIMMessageOfflinePushSettings.IOSSettings are constructed
For more information, see [Offline Push](https://cloud.tencent.com/document/product/269/9234)

## IM Android SDK 2.5.2, 2017-3-1
- Fixed the issue where returning outbound packets occasionally timed out (with return code 6205)

## IM SDK 2.5.1, 2017-2-16
- Limited the maximum size of a LOG file to 50 MB
- Fixed the bug where the online user state was returned after a user logged out and the app switched to the background
- Updated the audio and file downloading policy and supported HTTP and HTTPS downloads on iOS devices
- Fixed the state mismatch bug that occurred after messages failed to be sent when the user was not logged in

## IM Web SDK 1.7, 2016-12-20
- Supported cross-instance mutual forcible offline
- Supported multiple concurrently online instances
- Supported the synchronization of group read messages
- Supported the synchronization of C2C read messages
- Optimized the demo directory structure and code
- Added the recent contact list

## IM SDK 2.5, 2016-12-16
- Optimized the TIMOfflinePushInfo object structure
- Fixed audio and file download failures for iOS 9.1
- Optimized network operations
- Fixed some bugs

## IM SDK 2.4.1, 2016-11-24

- Fixed the bug where TIMGroupAssistant unexpectedly pulled the group profile after entering an AVChatRoom group
- Fixed the bug where disabling console printing failed
- Fixed the issue where logging out after initialization and prior to login failed various listeners

## IM SDK 2.4, 2016-11-09
- Supported full compatibility with the ATS mode
- Provided the message forwarding feature where the copyFrom API forwards image and file messages by directly copying them rather than downloading them
- Supported dynamically updating the number of members in AVChatRoom groups where TIMGroupEventListener returns the current number of group members
- Supported customizing message filtering for AVChatRoom groups
- Supported push notification settings of Mi and Huawei mobile phones by TIMOfflinePushInfo attributes
- Optimized the process of pulling group roaming messages
- Optimized the processes of uploading and downloading audio, files, and short videos
- Supported the feature of not throwing onNewMessage when pulling the recent contact list

## IM SDK 2.3, 2016-9-13
- Supported pushing notifications to multiple apps with the same appid
- Added the setOfflinePushToken API with callback to the Android version
- Optimized message deletion logic to automatically exclude messages in the DELETED state when pulling messages
- Moved database files from the subdirectory Library/Caches/ to another subdirectory Document/ to avoid being purged by the system for the iOS version
- Supported adding and deleting multiple TIMMessageListeners for the iOS version
- Named resident threads in the iOS version in a unified manner
- Supported automatically filtering out conversations with message counts of 0 through the API for obtaining conversation lists

## IM Web SDK 1.6, 2016-8-15
- Supported web broadcast messages
- Added friend system notifications
- Added profile system notifications

## IM SDK 2.2, 2016-8-10
- Supported conversation drafts
- Supported marking conversations to store or not to store messages to enable flexible message handling
- Supported traversing messages from old to new by message roaming for message recording scenarios
- Added ext and sounds of push notifications to messages, which allows setting push information for certain messages
- Added stopQALService to the Android SDK, which turns off QALService upon app logout
- Supported network status monitoring and additional error codes for network errors

## IM SDK 2.1, 2016-7-15
- Supported push notification features for Mi and Huawei mobile phones
- Supported the read receipt feature, which is optional depending on product needs
- Supported the typing indicator, which is optional depending on product needs
- Added standard fields such as the gender, date of birth, address, and language to the profile relationship chain
- Added the group member count to joining and quitting group notifications
- Fixed some SDK and demo bugs

## IM Web SDK 1.5, 2016-7-13
- Merged live chat room SDK capabilities
- Fixed issues with uploading images in IE8 and IE9
- Added a new group member count field to tips messages for joining quitting the group
- Fixed some SDK and demo bugs

## IM SDK 2.0, 2016-6-16
- Synchronized read messages across multiple devices to synchronize the unread count when multiple devices are online
- Supported importing historical messages when migrating the app to ensure smooth migration
- Added the message notification state to group message attributes
- Supported setting message attributes flexibly
- Supported filtering push notifications by attributes and tags

## IM Web SDK 1.4, 2016-6-7
- Supported pulling friends’ historical messages
- Supported red packets and like messages
- Supported custom group IDs and live chat rooms by the group creation API
- Optimized SDK APIs by merging the login and initialization APIs
- Optimized the demo directory structure and code

## IM SDK 1.9.3, 2016-5-31
- Fixed resource destruction deadlocks that occurred when the winsdk process quit

## IM SDK 1.9.2, 2016-5-27
- Added ticket expiration callback
- Supported IPv6 (for iOS)

## IM SDK 1.9, 2016-5-4
- Supported groups with more than 10,000 members or infinite members, which is suitable for live streaming scenarios
- Reconstructed the IM demo for better user experience and ease-of-use
- Supported sending messages by priorities
- Added storage and caching for group profiles and relationship chains
- Added APIs for synchronizing group profiles and relationship chains and modifying callbacks
- Supported obtaining friend profiles including remarks and groups
- Supported setting default group profile and relationship chain fields to be pulled
- Supported disabling pulling recent contacts
- Supported synchronizing the last message to the conversation list
- Supported specifying group members whose group information, such as the group name card, is to be pulled
- Supported passing in file paths for audio and file messages (messages can be resent)
- Adapted to dynamic permission management for version 6.0

## IM SDK 1.8.1, 2016-4-13
- Optimized the auto-start process on Android devices (this requires to modify the configuration, see ReadMe.txt for relevant instructions)
- Added the API for sending online messages in one-to-one chats (the messages will be received only when the receiver is online and will not be stored when the receiver is offline)
- Added the API for sending messages in batches
- Improved the performance on Android devices

## IM SDK 1.8, 2016-3-23
- Supported Android offline push
- Added the API for verifying friend relationships
- Added the API for custom relationship chain fields
- Supported customized local storage of messages (for example, identifying audio as read or unread)
- Added the API for compressing images, which meets the need for image compression in non-communication scenarios
- Supported customizing messages’ sound fields to specify APNs sounds
- Improved the callback API for changing the online state


## IM SDK 1.7, 2016-1-25
- Supported limiting the message sending frequency in groups
- Supported transferring group ownership
- Supported customizing the group message notification frequency
- Provided CS channels to remove the need for a persistent connection between the app and backend to reduce power consumption
- Added configuration items, including the roaming toggle for messages and recent contacts, storage duration, and the toggle for concurrent online devices, to improve operational efficiency
- Included group member nicknames and contact cards in downstream messages to improve user experience and ease-of-use
- Simplified the SDK to reduce the installation package size


## IM SDK 1.6, 2015-12-25
- Supported short video messages to meet growing needs for video sharing and social networking
- Supported rule-based sorting of group members
- Supported friend groups of the relationship chain
- Supported filtering sensitive words in group names, announcements, and introductions
- Supported group member contact cards to help users identify group members
- Supported the message notification toggle so that users can toggle on or off message notifications for one-to-one chats and group chats

## IM SDK 1.5, 2015-11-16

- Supported the asynchronous downloading of the message history
- Supported deleting group messages at the server side
- Supported searching for users by nicknames
- Supported searching for groups by group names
- Supported configuring event callbacks in the console
- Supported downloading user credentials of admin accounts
- Optimized some demos and technical logics


## IM SDK 1.4, 2015-10-16
- Supported multi-device login
- Rejected messages from blacklisted users
- Deleted friend recommendations
- Supported pushing nicknames by APNs
- Supported filtering sensitive words in group names
- Supported filtering sensitive words in group announcements
- Supported the guest mode and third-party account login in the demo

## IM SDK 1.3, 2015-09-10
- Supported logging in as guests without usernames and passwords
- Supported message roaming (messages are stored for 7 days by default)
- Supported roaming and deleting recent contacts
- Supported the real-time synchronization of messages through callbacks
- Supported friend recommendation once recommendation logic is defined
- Supported sending original images or thumbnails for improved user experience
- Supported push notifications (for Android devices, this is only available to online users)
- Supported smooth migration
- Supported deleting local messages to protect users’ privacy

## IM SDK 1.2, 2015-08-18
- Supported C2C one-to-one chats on the web platform
- Increased the maximum number of group members to 10,000
- Supported filtering ads and sensitive words in messages
- Added the API for providing message IDs to precisely locate messages
- Added remarks in user profiles
- Supported viewing local messages when offline

## IM SDK 1.1, 2015-07-13
- Supported the Windows C++ platform
- Supported the Public and ChatRoom group types
- Supported adding group introductions and announcements and muting members, blocking messages, and setting group roles
- Added APIs for user profile and relationship chain operations, such as setting nicknames, adding friends, and setting up the blacklist
- Supported file messages
- Optimized image messages where possible image quality values are original image, thumbnail, and large image, changed the upload and download APIs, and passed image URLs
- Added log levels to the log callback API
- Added the logic for executing forcible logout on one device in the event of repeated login attempts
- Supported automatically reporting crashes
- Supported integrating self-owned accounts and third-party accounts in hosting mode
- Added SMS authentication for user registration and login
- Supported ticket verification by using public keys and private keys generated by Tencent
- Added user and group management

## IM SDK 1.0, 2015-05-11
- Supported Android/iOS platforms
- Supported logging in with Tencent accounts and third-party accounts
- Supported the one-to-one chat and group chat (discussion group) conversation types
- Supported text, emoji, image, audio, location, and custom messages
- Supported APNs offline push (for reporting tokens and foreground and background switching events)
- Supported storing messages locally
